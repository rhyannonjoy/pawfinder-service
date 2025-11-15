# API Reference

## Running PawFinder

- Run PawFinder locally or in a compatible server environment.
- All requests and responses are in the JSON data format.
- Suggested base URL:

```shell
http://localhost:3000
```

## Versioning

The PawFinder API currently doesn't use URI versioning.
Available resources include:

```shell
{base_url}/pets
{base_url}/shelters
```

**Future version support policy**:

- PawFinder will support all major versions for 24 months after a new version releases.
- Deprecated endpoints will include a `Sunset` header indicating end-of-life date.
- Breaking changes will only be introduced in major version increments.
- Minor updates and bug fixes won't require version changes.
