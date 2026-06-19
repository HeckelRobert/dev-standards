# API Design Standard

## Purpose

This document defines conventions for HTTP APIs in Heckel Platform projects.

Default API style is REST. See `standards/technology-selection.md` for GraphQL and gRPC selection.

---

# General Principles

APIs are contracts. Breaking changes require versioning and communication.

Business logic remains in Application handlers, not in controllers or minimal API delegates.

APIs return explicit error responses. See `standards/coding-standard.md` error handling section.

---

# URL Design

Use plural nouns for resource collections.

```
GET    /api/v1/customers
GET    /api/v1/customers/{id}
POST   /api/v1/customers
PUT    /api/v1/customers/{id}
PATCH  /api/v1/customers/{id}
DELETE /api/v1/customers/{id}
```

Use kebab-case for multi-word path segments.

```
/api/v1/quality-inspections
```

Nest resources only when the child cannot exist without meaningful parent context.

```
GET /api/v1/customers/{customerId}/orders
```

Avoid deep nesting beyond two levels.

---

# Versioning

Include major version in the URL path.

```
/api/v1/...
```

Increment major version only for breaking changes.

Non-breaking additions (new optional fields, new endpoints) do not require a version bump.

Document deprecation policy in `docs/architecture.md`.

---

# Request and Response Format

Default format: JSON (`application/json`).

Use ISO 8601 for date and time values in UTC unless requirements specify otherwise.

Use consistent property naming: camelCase in JSON payloads.

Avoid exposing internal identifiers or implementation details in property names.

---

# Pagination

Collection endpoints that may return large result sets shall support pagination.

Preferred pattern: cursor or offset with explicit limits.

```
GET /api/v1/customers?page=1&pageSize=25
```

Response should include pagination metadata:

```json
{
  "items": [],
  "page": 1,
  "pageSize": 25,
  "totalCount": 120
}
```

Default page size: 25. Maximum page size: 100 unless requirements specify otherwise.

---

# Error Responses

Use RFC 7807 Problem Details (`application/problem+json`).

```json
{
  "type": "https://api.example.com/errors/validation",
  "title": "Validation failed",
  "status": 400,
  "detail": "One or more fields are invalid.",
  "errors": {
    "name": ["Name is required."]
  }
}
```

Do not leak stack traces, internal paths, or secrets in API responses.

| Situation | Status |
|-----------|--------|
| Validation failure | 400 |
| Missing or invalid authentication | 401 |
| Authenticated but not permitted | 403 |
| Resource not found | 404 |
| Conflict (duplicate, state conflict) | 409 |
| Unexpected server error | 500 |

---

# Authentication and Authorization

Protected endpoints require authentication per ADR-004.

Authorization is enforced in Application layer handlers or pipeline behaviors, not only at the HTTP boundary.

Document required roles or policies in OpenAPI descriptions and `docs/security.md`.

---

# OpenAPI

Every HTTP API shall publish an OpenAPI document.

Generate from code (Swashbuckle, NSwag, or native .NET OpenAPI) where practical.

The OpenAPI document is a deliverable: keep it accurate and review it in pull requests.

Include:

* Endpoint descriptions
* Request and response schemas
* Authentication requirements
* Error response schemas

Do not modify a copy-pasted `swagger.yaml` that is generated from the backend. Regenerate from source.

---

# Idempotency

`GET`, `PUT`, and `DELETE` shall be idempotent.

`POST` operations that create resources should return `201 Created` with a `Location` header when applicable.

For critical non-idempotent `POST` operations (payments, orders), consider idempotency keys when requirements demand it.

---

# Filtering and Sorting

Use query parameters for optional filtering and sorting.

```
GET /api/v1/customers?status=active&sort=name
```

Document supported filters in OpenAPI. Reject unsupported filters with `400`, not silent ignore.

---

# Related Documents

* standards/coding-standard.md
* standards/security-standard.md
* adrs/ADR-004-Authentication-Strategy.md
* adrs/ADR-011-Layering-and-Dependency-Rules.md
