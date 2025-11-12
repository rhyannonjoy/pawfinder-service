# API Reference

## Base URL and versioning

Make all API requests to:

```shell
https://api.pawfinder.com
```

**Versioning**

The PawFinder API uses URI versioning.
The current stable version is `v1`:

```shell
https://api.pawfinder.com/v1/pets
https://api.pawfinder.com/v1/shelters
```

**Version support policy**:

- PawFinder supports all major versions for 24 months after a new version releases
- Deprecated endpoints include a `Sunset` header indicating end-of-life date
- Breaking changes are only introduced in major version increments
- Minor updates and bug fixes don't require version changes
