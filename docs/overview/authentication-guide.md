---
layout: page
title: Authentication Guide
permalink: /docs/overview/authentication-guide/
---

# Authentication guide

## Overview

The PawFinder Service API uses a token-based authentication system.
Read-only operations, `GET` requests, don't require authentication.
Operations that change data, such as `POST`, `PUT`, `PATCH`, and
`DELETE` require an API token passed in the request header.

## Authentication requirements

| HTTP Method | Purpose | Authentication Required |
|-------------|---------|------------------------|
| `GET` | Retrieve pet or shelter profiles | No |
| `POST` | Add a new pet or shelter profile | Yes |
| `PUT` | Replace an entire pet or shelter profile | Yes |
| `PATCH` | Partially update a pet or shelter profile | Yes |
| `DELETE` | Remove pet or shelter profiles from the PawFinder System | Yes |

## Authenticating requests

For any write operation, include the API token in the `Authorization` header:

```shell
Authorization: Bearer API_TOKEN
```

### Authenticated example request

```bash
curl -X POST {base_url}/shelters \
  -H "Authorization: Bearer token_here" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Dallas Animal Rescue",
    "city": "Dallas",
    "state": "TX"
  }'
```

### Read-only example request

```bash
curl {base_url}/pets
```

## Create an API token

For development and testing purposes, assign any string as the token.
In a production environment, PawFinder issues tokens through a proper
authentication system.

**For local development:**

1. As described in the [Tutorial Requirements](tutorial-requirements.md),
start the PawFinder json-server instance: `json-server -w pawfinder-db-source.json`.
2. Use any string as the token, such as `test-token`, `dev-key`, etc.
3. Pass it in the `Authorization: Bearer` header to perform write operations.

## Security best practices

- **Never commit tokens to version control.** Use environment variables
or create an `.env` file and add it to the `.gitignore` file.
- **Rotate tokens regularly** in production environments.
- **Use different tokens for different environments** such as development,
stage, QA, and production.
- **Store tokens securely** and treat them like passwords.
- **Limit token permissions**. In a production environment with a robust backend
system, use tokens with write-only or read-only scopes as needed.

### Environment variable example

```bash
# Store the token in an .env file and don't commit it to git
API_TOKEN=secret_token

# Use the token in the request
curl -X POST {base_url}/pets \
  -H "Authorization: Bearer $API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "Buddy", "species": "dog"}'
```

## Error responses

### Missing authentication

A write operation attempt without an authentication header returns
a `401 Unauthorized` response:

```json
{
  "error": "Unauthorized",
  "message": "Authentication token is required for this operation."
}
```

### Invalid authentication

An invalid or malformed token returns a `403 Forbidden` response:

```json
{
  "error": "Forbidden",
  "message": "Invalid or expired authentication token."
}
```

### Reaching the rate limit

Reaching the rate limit returns the `429 Too Many Requests` response:

```json
{
  "error": "Too Many Requests",
  "message": "Rate limit exceeded. Try again in 60 seconds.",
  "status": 429,
  "retry_after": 60
}
```

## Rate limiting

For development and testing, there are currently no strict rate limits,
as json-server isn't designed for high-volume traffic. In production,
use rate limiting to:

- Prevent abuse
- Ensure fair access across users
- Protect backend resources

A typical approach would limit requests per IP or API key over a time window.
In a production environment, responses might include rate limit headers:

```shell
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 45
X-RateLimit-Reset: 1638360000
```

An example breakdown of client request limits:

| Tier | Requests per minute | Daily limit |
|------|---------------------|-------------|
| Free | 60 | 1,000 |
| Standard | 300 | 10,000 |
| Premium | 1,000 | 100,000 |
| Enterprise | Custom | Custom |

## Implementation note

The PawFinder Service API is a project for shared documentation practice
and educational purposes only. PawFinder uses json-server and an intentionally
minimal authentication system. In a production system, consider the following:

- Audit logging of all authenticated requests
- Cryptographic key management
- [OAuth 2.0](https://oauth.net/2/) or similar industry-standard authentication
- Abuse prevention systems with robust rate limiting methods
- Token TTLs, time to live policies, and refresh mechanisms
