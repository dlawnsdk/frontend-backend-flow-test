# Examples

Example configurations for `frontend-backend-flow-test`.

## Table of Contents

- [Admin FAQ Flow](#admin-faq-flow)
- [Generic E-commerce Flow](#generic-e-commerce-flow)
- [Read-Only Smoke Flow](#read-only-smoke-flow)

---

## Admin FAQ Flow

Good starter target for admin frontend ↔ backend validation.

```json
{
  "service": {
    "name": "Dangori Admin Backend",
    "api_base": "http://localhost:8090/api",
    "environment": "local"
  },
  "auth": {
    "method": "header",
    "token_key": "Authorization",
    "token_prefix": "Bearer"
  },
  "test_account": {
    "email": "admin-test@example.com",
    "password": "change-me",
    "login_endpoint": "/admin/auth/login",
    "request_encoding": "json",
    "token_path": "data.accessToken"
  },
  "features": {
    "faq": {
      "name": "Admin FAQ",
      "create": {
        "endpoint": "/admin/faqs",
        "method": "POST",
        "request_encoding": "json",
        "id_field": "data.seq",
        "test_data": {
          "question": "[AutoTest] FAQ question",
          "category": "GENERAL",
          "answer": "Auto-generated answer",
          "displayOrder": 9999,
          "active": false
        }
      },
      "read": {
        "endpoint": "/admin/faqs"
      },
      "update": {
        "endpoint": "/admin/faqs/{id}",
        "method": "PUT",
        "request_encoding": "json",
        "include_resource_id": false,
        "test_data": {
          "question": "[AutoTest] Updated FAQ question",
          "category": "GENERAL",
          "answer": "Updated answer",
          "displayOrder": 9998,
          "active": false
        }
      },
      "delete": {
        "endpoint": "/admin/faqs/{id}",
        "method": "DELETE",
        "request_encoding": "data",
        "include_resource_id": false
      }
    }
  }
}
```

---

## Generic E-commerce Flow

```json
{
  "service": {
    "name": "MyShop API",
    "api_base": "https://api.myshop.com/v1",
    "environment": "staging"
  },
  "auth": {
    "method": "header",
    "token_key": "Authorization",
    "token_prefix": "Bearer"
  },
  "test_account": {
    "email": "test@myshop.com",
    "password": "testpass123",
    "login_endpoint": "/auth/login",
    "request_encoding": "json",
    "token_path": "data.token"
  },
  "features": {
    "products": {
      "name": "Products",
      "create": {
        "endpoint": "/products",
        "method": "POST",
        "request_encoding": "json",
        "id_field": "id",
        "test_data": {
          "name": "[TEST] Sample Product",
          "price": 29.99,
          "stock": 100
        }
      },
      "read": {
        "endpoint": "/products",
        "detail_endpoint": "/products/{id}"
      },
      "update": {
        "endpoint": "/products/{id}",
        "method": "PATCH",
        "request_encoding": "json",
        "test_data": {
          "name": "[TEST] Updated Product",
          "price": 31.99,
          "stock": 95
        }
      },
      "delete": {
        "endpoint": "/products/{id}",
        "method": "DELETE",
        "request_encoding": "data"
      }
    }
  }
}
```

---

## Read-Only Smoke Flow

Use generator with `--read-only` when you want safer live validation.

```json
{
  "service": {
    "name": "Public API",
    "api_base": "https://api.example.com",
    "environment": "staging"
  },
  "auth": {
    "method": "none"
  },
  "test_account": {
    "email": "unused@example.com",
    "password": "unused"
  },
  "features": {
    "catalog": {
      "name": "Catalog",
      "read": {
        "endpoint": "/catalog",
        "detail_endpoint": "/catalog/{id}"
      }
    }
  }
}
```

Usage:

```bash
python3 scripts/generate_tests.py --config config.json --read-only
```
