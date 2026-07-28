# API Design

> How to design clear, consistent, and evolvable APIs that your consumers will love.

> **Related:** [Architecture Styles](architecture-styles.md) | [What Is Software Architecture?](what-is-software-architecture.md)

---

## What Is It?

API design is the practice of defining **contracts** between services or between a service and its clients. A good API is:
- **Consistent** — same patterns everywhere
- **Predictable** — consumers can guess how it works
- **Evolvable** — you can add features without breaking existing clients

---

## REST

The dominant style for HTTP APIs.

### Resource Naming

Use plural nouns for resources, not verbs.

| Good | Bad |
|------|-----|
| `GET /users` | `GET /getUsers` |
| `GET /users/123` | `GET /user?id=123` |
| `POST /users` | `POST /createUser` |
| `PATCH /users/123` | `POST /updateUser` |

### HTTP Methods

| Method | Action | Idempotent | Safe |
|--------|--------|------------|------|
| `GET` | Read a resource | Yes | Yes |
| `POST` | Create (or trigger an action) | No | No |
| `PUT` | Full replace | Yes | No |
| `PATCH` | Partial update | No | No |
| `DELETE` | Remove a resource | Yes | No |

```bash
# Collection
GET    /users           # List users
POST   /users           # Create a user

# Single resource
GET    /users/123       # Get user 123
PUT    /users/123       # Replace user 123 entirely
PATCH  /users/123       # Update specific fields of user 123
DELETE /users/123       # Delete user 123

# Sub-resources
GET    /users/123/orders      # Orders for user 123
POST   /users/123/orders      # Create order for user 123
```

### Actions That Don't Fit CRUD

If an action doesn't map to create/read/update/delete, use a **verb in the URL** with POST:

```
POST /orders/123/cancel
POST /users/123/activate
POST /articles/456/publish
```

### Status Codes

| Code | Meaning | When |
|------|---------|------|
| `200 OK` | Success | GET, PUT, PATCH |
| `201 Created` | Created | POST |
| `204 No Content` | Success, no body | DELETE, sometimes PUT |
| `400 Bad Request` | Client error | Invalid input |
| `401 Unauthorized` | Not authenticated | Missing/invalid token |
| `403 Forbidden` | Not authorized | Valid token but not allowed |
| `404 Not Found` | Resource doesn't exist | Wrong ID |
| `409 Conflict` | State conflict | Duplicate, version conflict |
| `422 Unprocessable Entity` | Validation failed | Invalid field values |
| `429 Too Many Requests` | Rate limited | Back off |
| `500 Internal Server Error` | Server error | Something broke |
| `503 Service Unavailable` | Temporarily down | Maintenance, overload |

> **Tip:** Never return `200 OK` with an error body. Use the right status code. Clients check the status code, not the body.

### Error Responses

Always return a consistent error format:

```json
{
    "error": {
        "code": "INVALID_FIELD",
        "message": "Email must be a valid email address",
        "details": {
            "field": "email",
            "value": "not-an-email"
        },
        "request_id": "req_abc123"
    }
}
```

### Pagination

```bash
GET /users?page=1&per_page=20&sort=name&order=asc

# Response
{
    "data": [...],
    "pagination": {
        "page": 1,
        "per_page": 20,
        "total": 143,
        "total_pages": 8,
        "next": "/users?page=2&per_page=20",
        "prev": null
    }
}
```

### Versioning

Three common strategies:

| Strategy | Example | Pros | Cons |
|----------|---------|------|------|
| URL prefix | `/api/v1/users` | Simple, obvious | Clutters URLs |
| Header | `Accept: application/vnd.api+json;version=2` | Clean URLs | Harder to discover |
| Query param | `/api/users?version=2` | Simple | Easy to forget |

> **Recommendation:** Use URL prefix (`/v1/`) for public APIs. It's the most explicit and least surprising.

---

## GraphQL

An alternative to REST where clients specify exactly what data they need.

```graphql
# Query
query {
    user(id: "123") {
        name
        email
        posts {
            title
        }
    }
}

# Response
{
    "data": {
        "user": {
            "name": "Alice",
            "email": "alice@example.com",
            "posts": [
                { "title": "Hello World" }
            ]
        }
    }
}
```

| Pros | Cons |
|------|------|
| Clients fetch exactly what they need | Complex query validation |
| Strongly typed schema | Caching is harder than REST |
| Single endpoint, no versioning | N+1 query problem (must use DataLoader) |
| Great for rapidly evolving frontends | Over-fetching prevention can cause under-fetching |

**When to use GraphQL:** Complex data graphs, multiple clients with different data needs, rapidly evolving frontends.

**When to stick with REST:** Simple CRUD, public APIs with unknown consumers, cache-heavy systems.

---

## API Design Checklist

| Rule | How |
|------|-----|
| Consistent naming | All plural nouns, same case |
| Proper status codes | Don't return 200 for errors |
| Error body | Always return a structured error |
| Pagination | Every list endpoint |
| Rate limiting | Return `429` with `Retry-After` header |
| Idempotency keys | `POST` endpoints that shouldn't duplicate |
| Logging | Log request IDs, trace spans |
| Documentation | OpenAPI/Swagger spec generated from code |

## Common Mistakes

| Mistake | Problem | Solution |
|---------|---------|----------|
| Returning 200 for everything | Client can't distinguish success from error | Use proper status codes |
| No pagination | Client can't handle large datasets | Always paginate list endpoints |
| Breaking changes without warning | Clients fail unexpectedly | Version your API |
| Inconsistent naming | `/getUser`, `/users`, `/api/v1/User` | Enforce a naming convention |
| Exposing internal IDs | Security risk, tight coupling | Use UUIDs or public IDs |
| No rate limiting | One client can DDoS your API | Always rate limit |

## Related Topics

- [Architecture Styles](architecture-styles.md) — How APIs connect services
- [Scalability Patterns](scalability-patterns.md) — Caching, rate limiting, load balancing

## Further Learning

- *REST API Design Rulebook* — Mark Masse
- [Microsoft REST API Guidelines](https://github.com/microsoft/api-guidelines)
- [JSON:API](https://jsonapi.org/) — A specification for building APIs

---

> **Next:** [Dependency Injection](dependency-injection.md) | **Previous:** [Domain-Driven Design](domain-driven-design.md)
