---
layout: page
title: Delete a shelter profile
permalink: /docs/api-reference/delete-shelters-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Delete a shelter profile

This operation permanently removes a shelter record from the
PawFinder database. Use this operation when a shelter record
is no longer needed, or to clean up outdated or incorrect
profiles from the platform.

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
# Delete the shelter profile with `id`= 5
# Recommended base_url = http://localhost:3000
curl -X DELETE {base_url}/shelters/5 \
  -H "Authorization: Bearer pawfinder-secret-2025"
```

### Success response `200`

In production REST APIs, `DELETE` operations typically
return either `204 No Content` for empty responses
or `200 OK` with a confirmation message. The PawFinder
API returns the deleted shelter profile object for reference:

```json
{
  "name": "Dallas Animal Services",
  "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
  "phone": "+1-214-671-0249",
  "email": "info@dallasanimalservices.org",
  "hours": "Mon-Sat 11:00-18:00",
  "available_pet_count": 22,
  "adoption_fee_range": "75-200",
  "id": 5
}
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `401` | Missing API token | `{ "error": "Unauthorized", "message": "Authentication token is required for this operation.", ... }` |
| `403` | Invalid API token | `{ "error": "Forbidden", "message": "Invalid or expired authentication token.", ...}` |
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 5 not found.", ... }` |

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
