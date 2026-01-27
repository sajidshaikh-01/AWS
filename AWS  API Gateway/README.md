# AWS API Gateway – Complete Deep Dive README

This README provides an in-depth explanation of **API Gateway**, including API types, integrations, authorizations, transformations, deployments, and real-time interview questions.

---

# 📘 1. What is AWS API Gateway?

AWS API Gateway is a fully managed service to create, publish, secure, monitor, and maintain APIs at scale. It supports:

* REST APIs
* HTTP APIs
* WebSocket APIs

It acts as a **front door** for serverless & microservice applications.

---

# 🧩 2. API Gateway Types & Their Features

## **1. REST API (Legacy – Feature Rich)**

* Full features (validators, auth, transformations, models)
* Supports complex API workflows
* Higher cost
* **Best for production enterprise workloads**

## **2. HTTP API (Modern – Lightweight & Cheaper)**
g
* Lower latency
* Simple routing
* JWT authorizers
* Cheaper than REST
* **Best for simple HTTP backends & Lambda**

## **3. WebSocket API**

* Real-time communication (chat apps, notifications)
* Bi-directional

---

# 🔗 3. API Gateway with HTTP Integrations

API Gateway can forward requests to HTTP/HTTPS servers:

* EC2 instances
* On-prem servers (via VPC Link)
* Third-party endpoints

### Integration Types:

* **HTTP Proxy** → API Gateway passes request directly
* **HTTP Custom Integration** → You can transform request/response

---

# 🌐 4. REST API – Resources and Methods

REST APIs use:

* **Resources** → `/users`, `/orders/{id}`
* **Methods** → GET, POST, PUT, DELETE

### Example:

```
/users           → GET: list users
/users/{id}      → GET: get user
/users           → POST: create user
```

---

# ⚡ 5. API Gateway + AWS Lambda (Most Common Integration)

API Gateway triggers Lambda with event payload:

```json
{
  "resource": "/users",
  "httpMethod": "POST",
  "body": "{\"name\": \"John\"}"
}
```

Lambda returns:

```json
{
  "statusCode": 200,
  "body": "{ \"message\": \"Success\" }"
}
```

---

# 🧪 6. API Gateway Mock Integration (No Backend Needed)

Used to:

* Create dummy APIs
* Test API Gateway config
* API prototyping

Mock returns static responses without backend.

---

# 🛢 7. API Gateway + DynamoDB Direct Integration

API Gateway can perform CRUD operations directly on DynamoDB **without Lambda**.

Example mapping template:

```json
{
  "TableName": "Users",
  "Key": {"userId": {"S": "$input.params('id')"}}
}
```

---

# 📌 8. Path & Query String Parameters

### Path Params:

```
/users/{id}
```

Access inside integration:

```json
$input.params('id')
```

### Query Params:

```
/users?status=active
```

Access:

```json
$input.params('status')
```

---

# 📩 9. Headers in API Gateway

Read header:

```json
$input.params().header.X-Custom-Header
```

---

# 🔍 10. Input Validation at API Gateway Level

You can enforce validation using:

* Request Validator
* Models (JSON Schema)
* Required headers, query params

Reduces load on backend.

---

# 🔄 11. Modify Requests Before Backend (Mapping Templates)

Mapping Templates let you:

* Add new fields
* Rename fields
* Validate data
* Convert formats (XML → JSON)

Example transformation:

```json
{
  "username": "$input.json('$.name')",
  "createdAt": "$context.requestTime"
}
```

---

# ✏ 12. Modify Request Body Before Backend (VTL Templates)

Example:

```json
#set($inputRoot = $input.path('$'))
{
  "id": "$context.requestId",
  "data": $input.json('$')
}
```

---

# 🧠 13. Integration Request with Lambda

Customize what Lambda receives:

```json
{
  "method": "$context.httpMethod",
  "path": "$context.resourcePath",
  "body": $input.json('$')
}
```

---

# 🔁 14. Transform Lambda Responses

Lambda response transformation example:

```json
#set($output = $input.json('$'))
{
  "status": "ok",
  "payload": $output
}
```

---

# 🔐 15. Authenticate API Gateway Using IAM Roles

You can restrict access using IAM:

* `AWS_IAM` auth type
* Clients sign requests using SigV4 signature

Best for internal APIs.

---

# 🔑 16. Protect API Gateway Using API Keys

Steps:

1. Create API Key
2. Create Usage Plan
3. Attach to API Stage
4. Require API Key in method request

---

# 🔒 17. AWS Custom Authorizer (Lambda Authorizer)

Custom logic for authentication.

Used for:

* JWT validation
* OAuth / SSO
* Role-based access

Authorizer returns an **IAM policy**:

```json
{
  "principalId": "user123",
  "policyDocument": { ... }
}
```

---

# 👤 18. Pass User Info from Custom Authorizer to Lambda

Use:

* `context` object

Example:

```json
$context.authorizer.userId
```

---

# ♻ 19. Zero Downtime API Updates (Lambda Alias + Stage Variables)

Approach:

1. Use Lambda Versioning
2. Create Aliases (`prod`, `v1`, `v2`)
3. Map alias via Stage Variable:

```
lambdaAlias = prod
```

4. Update alias → No downtime

---

# 🟡 20. Canary Deployment in API Gateway

Enable gradual rollout:

* 95% → old version
* 5% → new version

Roll back instantly if needed.

---

# 🌐 21. Map Custom Domain to API Gateway

Steps:

1. Buy domain (Route 53)
2. Create ACM certificate
3. Associate custom domain with API
4. Create base path mapping

Example domain:

```
https://api.mycompany.com/v1/users
```


