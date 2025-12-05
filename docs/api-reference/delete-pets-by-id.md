---
layout: page
title: Delete a pet profile
permalink: /docs/api-reference/delete-pets-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Delete a pet profile

This operation permanently removes a pet record from the PawFinder
database. Use this operation when someone adopts a pet and the
record is no longer needed, or to clean up outdated or incorrect
profiles from the platform.

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
# Delete the pet profile with `id`= 6
# Recommended base_url = http://localhost:3000
curl -X DELETE {base_url}/pets/6 \
  -H "Authorization: Bearer API_TOKEN"
```

### Success response `200`

In production REST APIs, `DELETE` operations
typically return either `204 No Content` for empty responses
or `200 OK` with a confirmation message. The PawFinder
API returns the deleted pet profile object for reference:

```json
{
  "name": "Luna",
  "species": "cat",
  "breed": "Domestic Shorthair",
  "age_months": 18,
  "gender": "female",
  "size": "small",
  "temperament": "playful, affectionate",
  "medical": {
    "spayed_neutered": true,
    "vaccinations": ["fvrcp", "rabies"]
  },
  "description": "Luna is a playful tabby who loves
                 interactive toys and sunny windows.",
  "shelter_id": 1,
  "status": "available",
  "intake_date": "2025-09-01",
  "id": 6
}
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `401` | Missing API token | `{ "error": "Unauthorized", "message": "Authentication token is required for this operation.", ... }` |
| `403` | Invalid API token | `{ "error": "Forbidden", "message": "Invalid or expired authentication token.", ...}` |
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Pet with 'id' 6 not found.", ... }` |

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
