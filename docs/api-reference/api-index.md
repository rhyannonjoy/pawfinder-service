---
layout: page
title: API Index
permalink: /docs/api-reference/api-index/
---

## API Index

- Run PawFinder locally or in a compatible server environment.
- All requests and responses are in the JSON data format.
- Recommended base_url: `http://localhost:3000`

### Reference topics

#### Resources

- [`/pets` resource](pets.md)
- [`/shelters` resource](shelters.md)

#### `/pets` operations

- [GET all pet profiles](get-all-pets.md)
- [GET pet profiles by `id`](get-pets-by-id.md)
- [GET pet profiles from a specific shelter](get-pets-from-shelter.md)
- [GET pet profiles using filters](get-pets-with-filters.md)
- [POST pet profiles](post-pets.md)
- [PUT pet profiles by `id`](put-pets-by-id.md)
- [PATCH pet profiles by `id`](patch-pets-by-id.md)
- [DELETE pet profiles by `id`](delete-pets-by-id.md)

#### `/shelters` operations

- [GET all shelter profiles](get-all-shelters.md)
- [GET shelter profiles by `id`](get-shelters-by-id.md)
- [POST shelter profiles](post-shelters.md)
- [PUT shelter profiles by `id`](put-shelters-by-id.md)
- [PATCH shelter profiles by `id`](patch-shelters-by-id.md)
- [DELETE shelter profiles by `id`](delete-shelters-by-id.md)

### Common error responses for all endpoints

`429 Too Many Requests` - exceeding rate limit

```json
{
  "error": "Too Many Requests",
  "message": "Rate limit exceeded. Try again in 60 seconds.",
  "status": 429,
  "retry_after": 60
}
```

`500 Internal Server Error` - something is wrong with the server

```json
{
  "error": "Internal Server Error",
  "message": "An unexpected error occurred. Please try again later.",
  "status": 500
}
```

`503 Service Unavailable` - during PawFinder Maintenance

```json
{
  "error": "Service Unavailable",
  "message": "API is temporarily unavailable for maintenance.",
  "status": 503
}
```

### Troubleshooting

If encountering connection errors like `Connection refused` or
`ENOBUFS` while testing with high request volumes, this typically
indicates the local port is reaching its connection limit.
This is normal during stress testing and doesn't reflect production
API performance. To continue testing locally, either increase OS
connection limits, run many instances on different ports such as 3001, 3002, or test against a staging environment if available.

**OS-specific guidance**:

- **Linux**: Use `ulimit -n` to check current file descriptor
limits and change `/etc/security/limits.conf` to increase them
- **macOS**: Use `launchctl maxfiles` to adjust file limits,
or change `/etc/launchd.conf` for persistent changes
- **Windows**: Change the registry key `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters` and adjust `MaxUserPort` to increase ephemeral port range

### Versioning

The PawFinder API currently doesn't use URI versioning, but plans to.

_Future version support policy_:

- PawFinder supports all major versions for 24 months after
a new version releases.
- Deprecated endpoints include a `Sunset` header indicating
end-of-life date.
- PawFinder introduces breaking changes in major version increments.
- Minor updates and bug fixes won't require version changes.
