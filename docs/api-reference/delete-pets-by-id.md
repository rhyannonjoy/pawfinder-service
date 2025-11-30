---
layout: page
title: Delete a pet profile
permalink: /docs/api-reference/delete-pets-by-id/
---

## Delete a pet profile

This operation removes a pet record from the PawFinder database.
Use this endpoint to ensure that users can access fresh
data.

### Endpoint structure

```bash
DELETE /pets/{id}
```

### Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Pet's unique identifier |

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
curl -X DELETE {base_url}/pets/6 \
  -H "Authorization: Bearer API_TOKEN"
```

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `200` | Success | `{ "message": "Pet with ID 6 successfully deleted.", ... }` |
| `204` | `NO CONTENT` | No response body |
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Pet with ID 6 not found.", ... }` |

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
