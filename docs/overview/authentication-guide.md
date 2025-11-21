---
layout: page
title: Authentication Guide
permalink: /docs/overview/authentication-guide/
---

# Authentication guide

All API requests require authentication using API keys passed in the request header:

```shell
Authorization: Bearer YOUR_API_KEY
```

**Get an API key**:

1. Create a free account at developers.pawfinder.com
2. Generate an API key from your dashboard
3. Store your key securely, it grants access to your account

**Security best practices**:

- Never commit API keys to version control
- Rotate keys every 90 days
- Use environment variables to store keys in production
- Use key-specific permissions for team access

**Rate Limits**:

API usage is subject to rate limits based on your account tier:

| Tier | Requests per minute | Daily limit |
|------|---------------------|-------------|
| Free | 60 | 1,000 |
| Standard | 300 | 10,000 |
| Premium | 1,000 | 100,000 |
| Enterprise | Custom | Custom |

Every response includes rate limit headers:

```shell
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 45
X-RateLimit-Reset: 1638360000
```

When you exceed your rate limit, the API returns the `429 Too Many Requests` HTTP status code.
Try exponential backoff in your retry logic to handle rate limiting gracefully.
