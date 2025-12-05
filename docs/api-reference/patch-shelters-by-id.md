---
layout: page
title: Partially update a shelter profile
permalink: /docs/api-reference/patch-shelters-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Partially update a shelter profile

This operation updates specific fields of an existing shelter
record without affecting other data. Use this operation to
change shelter operating hours or contact details, pet
availability numbers, or edit administrative information
without resubmitting the entire shelter profile.

### PUT vs PATCH

`PUT` replaces an entire profile and `PATCH` only updates
the fields provided in the request body. In a `PUT` request,
missing fields set to `null` or default values. In a `PATCH`
request, fields not present in the request remain unchanged.

### Endpoint structure

```bash
PATCH /shelters/{id}
```

### Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | Yes |

### Authentication

**Required** - include an API token in the Authorization header:

```bash
Authorization: Bearer API_TOKEN
```

### Request body

Only include fields that need updating.
Omitted fields remain unchanged.

| Property | Type | Description | Value Format |
|---|---|---|---|
| `name` | string | Shelter's name | Any text |
| `address` | string | Shelter's location information | Any text |
| `phone` | string | Shelter's phone number | E.164 format: "+1-XXX-XXX-XXXX" |
| `email` | string | Shelter's email address | Any text |
| `hours` | string | Shelter's hours of operation | Any text |
| `available_pet_count` | integer | Shelter's available pets | Numeric value |
| `adoption_fee_range` | string | Shelter's fee range | United States Dollars |
| `id` | integer | Shelter's unique identifier | Auto-generated, read-only |

### cURL request

```bash
# Update values in the shelter profile with `id`= 1
# Recommended base_url = http://localhost:3000
curl -X PATCH {base_url}/shelters/1 \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
          "available_pet_count": 20 
      } 
```

### Success response `200`

Returns the entire shelter profile object:

```json
{
  "name": "Dallas Animal Services",
  "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
  "phone": "+1-214-671-0249",
  "email": "info@dallasanimalservices.org",
  "hours": "Mon-Sat 11:00-18:00",
  "available_pet_count": 20,
  "adoption_fee_range": "75-200",
  "id": 1
}
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `400` | Invalid field values | `{ "error": "Bad Request", "message": "Invalid value for 'adoption_fee_range'. Must be in USD.", ... }` |
| `401` | Missing API token | `{ "error": "Unauthorized", "message": "Authentication token is required for this operation.", ... }` |
| `403` | Invalid API token | `{ "error": "Forbidden", "message": "Invalid or expired authentication token.", ...}` |
| `404` | No matching `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 1 not found.", ...}` |

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
