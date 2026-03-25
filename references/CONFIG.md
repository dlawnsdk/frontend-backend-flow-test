# Configuration Reference

Configuration guide for `frontend-backend-flow-test`.

## Table of Contents

- [Service Configuration](#service-configuration)
- [Authentication](#authentication)
- [Test Account](#test-account)
- [Features](#features)
- [Operation Options](#operation-options)
- [Modes](#modes)
- [Examples](#examples)

---

## Service Configuration

```json
{
  "service": {
    "name": "My Service",
    "api_base": "https://api.example.com",
    "timeout": 30,
    "retry": 3,
    "environment": "staging"
  }
}
```

**Fields:**
- `name` (string, required): Service display name
- `api_base` (string, required): Base URL for all API calls
- `timeout` (integer, optional): Reserved for future request timeout handling
- `retry` (integer, optional): Reserved for future retry handling
- `environment` (string, optional): Helpful label for safety messaging (`local`, `dev`, `staging`, etc.)

---

## Authentication

### Header-Based (Default)

```json
{
  "auth": {
    "method": "header",
    "token_key": "Authorization",
    "token_prefix": "Bearer"
  }
}
```

### Cookie-Based

```json
{
  "auth": {
    "method": "cookie",
    "cookie_name": "session"
  }
}
```

### Custom Headers

```json
{
  "auth": {
    "method": "custom",
    "headers": {
      "x-access-token": "{token}",
      "x-access-id": "{user_id}"
    }
  }
}
```

Use `{token}` and `{user_id}` placeholders.

### No Authentication

```json
{
  "auth": {
    "method": "none"
  }
}
```

---

## Test Account

```json
{
  "test_account": {
    "email": "test@example.com",
    "password": "password123",
    "login_endpoint": "/auth/login",
    "request_encoding": "json",
    "token_path": "data.accessToken",
    "user_id_path": "data.user.id"
  }
}
```

**Fields:**
- `email` (string, required)
- `password` (string, required)
- `login_endpoint` (string, optional, default: `/login`)
- `request_encoding` (string, optional): `json`, `data`, or `params`
- `token_path` (string, optional): JSON path to extract token
- `user_id_path` (string, optional): JSON path to extract user ID

---

## Features

Each feature represents one frontend-backend flow surface.

```json
{
  "features": {
    "faq": {
      "name": "Admin FAQ",
      "create": { ... },
      "read": { ... },
      "update": { ... },
      "delete": { ... }
    }
  }
}
```

### CREATE

```json
{
  "create": {
    "endpoint": "/admin/faqs",
    "method": "POST",
    "request_encoding": "json",
    "include_user_id": false,
    "id_field": "data.seq",
    "test_data": {
      "question": "[AutoTest] FAQ question",
      "answer": "Auto-generated answer"
    }
  }
}
```

### READ

```json
{
  "read": {
    "endpoint": "/admin/faqs",
    "detail_endpoint": "/admin/faqs/{id}",
    "list_path": "data.items"
  }
}
```

### UPDATE

```json
{
  "update": {
    "endpoint": "/admin/faqs/{id}",
    "method": "PUT",
    "request_encoding": "json",
    "include_user_id": false,
    "include_resource_id": false,
    "resource_id_field": "faqSeq",
    "test_data": {
      "question": "[AutoTest] Updated FAQ question",
      "answer": "Updated answer"
    }
  }
}
```

### DELETE

```json
{
  "delete": {
    "endpoint": "/admin/faqs/{id}",
    "method": "DELETE",
    "request_encoding": "data",
    "include_user_id": false,
    "include_resource_id": false,
    "resource_id_field": "faqSeq"
  }
}
```

---

## Operation Options

Supported per operation where relevant:

- `endpoint`: request path
- `method`: HTTP method
- `request_encoding`: `json`, `data`, or `params`
- `include_user_id`: whether to inject authenticated user id into payload
- `user_id_field`: field name used when `include_user_id` is true
- `include_resource_id`: whether to inject current resource id into payload
- `resource_id_field`: field name used when `include_resource_id` is true
- `id_field`: JSON path to extract created resource id
- `test_data`: payload body for that operation

---

## Modes

### Default generation
Generates live flow-oriented test files for configured create/read/update/delete operations.

### `--read-only`
Generates read-focused tests without update/delete write flow.
Use for safer smoke validation when mutation is not desired.

### `--dry-run`
Currently means generation-only at generator time. It does **not** automatically add runtime network blocking to generated scripts.

---

## Examples

See [EXAMPLES.md](EXAMPLES.md) for sample configurations.
