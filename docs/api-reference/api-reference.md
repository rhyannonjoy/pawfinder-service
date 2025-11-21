---
layout: page
title: API Reference
permalink: /docs/api-reference/
---

# API reference

- Run PawFinder locally or in a compatible server environment.
- All requests and responses are in the JSON data format.
- _Recommended_ base URL:

```bash
http://localhost:3000
```

## Reference topics

### Resources

- [`/pets` resource](pets.md)
- [`/shelters` resource](shelters.md)

### `/pets` operations

- [GET all pet profiles](get-all-pets.md)
- [GET pet profiles by ID](get-pets-by-id.md)
- [GET pet profiles with filters](get-pets-with-filters.md)
- [POST pet profiles](post-pets.md)
- [PUT pet profiles by ID](put-pets-by-id.md)
- [PATCH pet profiles by ID](patch-pets-by-id.md)
- [DELETE pet profiles by ID](delete-pets-by-id.md)

### `/shelters` operations

- [GET all shelter profiles](get-all-shelters.md)
- [GET shelter profiles by ID](get-shelters-by-id.md)
- [GET pet profiles from a specific shelter](get-pets-from-shelter.md)
- [POST shelter profiles](post-shelters.md)
- [PUT shelter profiles by ID](put-shelters-by-id.md)
- [PATCH shelter profiles by ID](patch-shelters-by-id.md)
- [DELETE shelter profiles by ID](delete-shelters-by-id.md)

## Common error responses for all endpoints

`429 Too Many Requests` - reaching rate limit

```json
{
  "error": "Too Many Requests",
  "message": "Rate limit exceeded. Try again in 60 seconds",
  "status": 429,
  "retry_after": 60
}
```

`500 Internal Server Error` - something is wrong with the server

```json
{
  "error": "Internal Server Error",
  "message": "An unexpected error occurred. Please try again later",
  "status": 500
}
```

`503 Service Unavailable` - during PawFinder Maintenance

```json
{
  "error": "Service Unavailable",
  "message": "API is temporarily unavailable for maintenance",
  "status": 503
}
```

## Versioning

The PawFinder API currently doesn't use URI versioning, but plans to.

_Future version support policy_:

- PawFinder supports all major versions for 24 months after a new version releases.
- Deprecated endpoints include a `Sunset` header indicating end-of-life date.
- PawFinder introduces breaking changes in major version increments.
- Minor updates and bug fixes won't require version changes.
