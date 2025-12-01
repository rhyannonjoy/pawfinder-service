---
layout: page
title: Delete a shelter profile
permalink: /docs/api-reference/delete-shelters-by-id/
---

## Delete a shelter profile

This operation removes a shelter record from the PawFinder database.
Use this endpoint to ensure that users can access fresh data.

### Endpoint structure

```bash
DELETE /shelters/{id}
```

### Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Shelter's unique identifier |

### Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

### Authentication

**Required** - include an API token in the Authorization header:

```bash
Authorization: Bearer API_TOKEN
```

### Request body

This operation doesn't require a request body.

### cURL request

```bash
# Recommended base_url = http://localhost:3000
curl -X DELETE {base_url}/shelters/5 \
  -H "Authorization: Bearer pawfinder-secret-2025"
```

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `200` | Success | `{ "message": "Shelter with ID 5 successfully deleted.", ... }` |
| `204` | `NO CONTENT` | No response body |
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with ID 5 not found.", ... }` |

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
