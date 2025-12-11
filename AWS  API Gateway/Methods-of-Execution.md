# AWS API Gateway – Method Request, Integration Request, Integration Response, Method Response
---

## Overview — request/response pipeline

API Gateway processes requests in four stages:

1. **Method Request** — client → API Gateway (validate what clients can send)
2. **Integration Request** — API Gateway → backend (transform and forward)
3. **Integration Response** — backend → API Gateway (transform backend reply)
4. **Method Response** — API Gateway → client (what client receives)

Flow:

```
Client → Method Request → Integration Request → Backend
Backend → Integration Response → Method Response → Client
```

---

## 1) Method Request

**Purpose:** Define and validate what the client is allowed to send before the request reaches your backend.

**You can configure:**

* HTTP method (GET, POST, PUT, DELETE, etc.)
* Path parameters (`/users/{id}`) and whether they're required
* Query parameters (`?q=search`)
* Headers and whether they are required
* Request body (model/schema) and validation (JSON schema)
* Authorization (IAM, Cognito, Lambda authorizer, API key)
* Request Validation (enable strict schema validation to reject bad payloads)

**DevOps notes / use cases:**

* Reject malformed requests early to reduce backend load and cost.
* Enforce API keys or authorizers to protect environments (dev/stage/prod).

**Example (concept):**

* `GET /users/{id}` — require path param `id` and API key.

---

## 2) Integration Request

**Purpose:** Map and transform the client request into the format expected by the backend (Lambda, HTTP backend, AWS service).

**Integration types:**

* `AWS_PROXY` / Lambda Proxy Integration (most common for Lambda + SAM/Serverless)
* Lambda non-proxy (custom mapping)
* HTTP/HTTP_PROXY
* AWS (integration with native AWS services like SQS, SNS, DynamoDB)
* MOCK

**Key features:**

* **Mapping templates (VTL)** — transform client payload, add headers, compute fields (e.g., timestamp), remove sensitive fields.
* **Headers & query string mappings** — forward or rename headers and query params.
* **Pass-through behavior** — control whether to apply template or forward as-is.

**When to use non-proxy integration:**

* When backend expects a different shape than the client JSON.
* When integrating with legacy HTTP servers, third-party APIs, or AWS services that require specific parameter names.

**VTL example (transform client to backend payload):**

```vtl
#set($inputRoot = $input.path('$'))
{
  "action": "create_user",
  "request_id": "$context.requestId",
  "client_ip": "$context.identity.sourceIp",
  "body": $input.json('$')
}
```

**DevOps notes / use cases:**

* Add tracing or correlation IDs before invoking backend.
* Mask or drop sensitive client fields.
* Convert form-encoded data into JSON for backend.

---

## 3) Integration Response

**Purpose:** Translate raw backend responses (payloads and status codes) into API Gateway response selections so clients receive standardized responses.

**What it does:**

* Uses response status/success patterns or regex to match backend outputs.
* Maps backend status or error messages to HTTP status codes.
* Applies mapping templates to rewrite the response body and headers.

**Example:** Lambda returns `{ "status": "error", "message": "Not found" }` — map to HTTP 404 and an error model.

**VTL example (map backend error → client-friendly JSON):**

```vtl
#if($input.path('$.errorMessage'))
  {
    "error": true,
    "message": "$input.path('$.errorMessage')"
  }
#else
  $input.body
#end
```

**DevOps notes / use cases:**

* Normalize all backend errors into a single schema for clients and for downstream monitoring.
* Map different backend status codes to consistent HTTP statuses (e.g., DB constraint → 409 Conflict).
* Add CORS headers or security headers at response time.

---

## 4) Method Response

**Purpose:** Define the final response shape, headers, and status codes presented to the client.

**You configure:**

* HTTP status codes the method can return (200, 201, 400, 401, 404, 500)
* Response models (JSON schema) per status code
* Response headers (CORS, custom headers)

**DevOps notes / use cases:**

* Validate outgoing responses (model enforcement) for documentation and client contracts.
* Ensure CORS headers are present for browser-based frontends.

---

## Practical example — FastAPI on Lambda + API Gateway (Production checklist)

**Goals:** Validate input, add metadata, standardize errors, enable CORS, integrate with DynamoDB.

**Method Request**

* Configure path `/users` POST
* Require `Content-Type: application/json`
* Attach a request model (JSON schema) for user creation
* Require API key or Cognito authorizer

**Integration Request**

* Use **Lambda Proxy** for simple cases. For transformation or legacy backends use **Lambda non-proxy** and VTL to add `request_id` and `timestamp`.

**Integration Response**

* Map Lambda success object to HTTP 201 with a `Location` header.
* Map Lambda errors (validation, not found, DB errors) to 4xx/5xx with a standardized error format.

**Method Response**

* Define 201 model for success and 4xx/5xx models for errors.
* Add `Access-Control-Allow-Origin: *` (or specific origin) and `Access-Control-Allow-Headers`.

**Monitoring & Observability**

* Enable CloudWatch logs for API Gateway (execution logs and access logs).
* Add X-Ray tracing: propagate trace IDs in Integration Request to Lambda.
* Export metrics to CloudWatch and set alarms for 4xx/5xx spikes.

---

## Example VTL mapping templates (useful snippets)

**1. Add request metadata to payload (Integration Request):**

```vtl
#set($inputRoot = $input.path('$'))
{
  "requestId": "$context.requestId",
  "sourceIp": "$context.identity.sourceIp",
  "stage": "$context.stage",
  "body": $input.json('$')
}
```

**2. Convert backend error into client-friendly payload (Integration Response):**

```vtl
#set($body = $input.path('$'))
{
  "status": "error",
  "message": $util.escapeJavaScript($input.path('$.message'))
}
```

**3. Pass headers from method to backend (mapping example):**

```
"headers": {
  "Authorization": "$input.params('Authorization')",
  "X-Request-Id": "$context.requestId"
}
```

---

## Terraform snippet (API Gateway REST + Lambda non-proxy example)

```hcl
resource "aws_api_gateway_rest_api" "api" {
  name = "users-api"
}

resource "aws_api_gateway_resource" "users" {
  rest_api_id = aws_api_gateway_rest_api.api.id
  parent_id   = aws_api_gateway_rest_api.api.root_resource_id
  path_part   = "users"
}

resource "aws_api_gateway_method" "users_post" {
  rest_api_id   = aws_api_gateway_rest_api.api.id
  resource_id   = aws_api_gateway_resource.users.id
  http_method   = "POST"
  authorization = "NONE"
  request_models = {
    "application/json" = "UserCreateModel"
  }
}

resource "aws_api_gateway_integration" "users_post_integration" {
  rest_api_id = aws_api_gateway_rest_api.api.id
  resource_id = aws_api_gateway_resource.users.id
  http_method = aws_api_gateway_method.users_post.http_method

  integration_http_method = "POST"
  type                    = "AWS_PROXY" # or "AWS" for non-proxy
  uri                     = aws_lambda_function.user_create.invoke_arn
}
```

> Note: For non-proxy integrations you will need `aws_api_gateway_integration_response` and `aws_api_gateway_method_response` resources to map responses.

---

## Suggested GitHub folder structure for this project

```
api-gateway-project/
├─ terraform/
│  ├─ main.tf
│  ├─ lambda.tf
│  └─ api_gateway.tf
├─ lambda/
│  ├─ user_service/
│  │  ├─ app.py (FastAPI)
│  │  ├─ requirements.txt
│  │  └─ handler.py (wrap for Lambda)
│  └─ deploy.sh
├─ docs/
│  ├─ openapi.yaml
│  └─ README.md
└─ ci/
   ├─ github-actions.yml
   └─ tests/
```

---

## Quick tips & gotchas (DevOps)

* **CORS surprises:** If you forget to map `OPTIONS` method and proper headers, browser clients will fail.
* **Binary payloads:** Configure `binary_media_types` if returning non-text content.
* **Lambda size/time:** Use proxy integration for simplicity but ensure your Lambda returns proper API Gateway compatible response when using proxy.
* **Mapping errors:** Always test integration response mapping with different error shapes from your backend.
* **Local testing:** Use `sam local start-api` or `serverless offline` for quicker iteration.

---

## Next steps I can add to this canvas (tell me which you want):

* Full terraform + SAM/Serverless project files ready to push to GitHub
* Example VTL mapping templates for common error types
* OpenAPI (Swagger) file that matches the Method/Model definitions
* CI pipeline (GitHub Actions) to deploy API + Lambda

---

*End of document.*
