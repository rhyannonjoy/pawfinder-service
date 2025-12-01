---
layout: page
title: Partially update a shelter profile
permalink: /docs/api-reference/patch-shelters-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Partially update a shelter profile

This operation edits specific fields of an existing shelter record
in the PawFinder System.

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

Only include fields that need updating. Omitted fields remain unchanged.

| Property | Type | Description |
|---|---|---|
| `name` | string | Shelter's name |
| `address` | string | Shelter's address information |
| `phone` | string | Shelter's phone number, E.164 format |
| `email` | string | Shelter's email address |
| `hours` | string | Shelter's hours of operation |
| `available_pet_count` | integer | Shelter's available pets |
| `adoption_fee_range` | string | Shelter's fee range in United States Dollar |

### Field requirements

| Field | Validation Rule |
|---|---|
| `phone` | Must be E.164 format: +1-XXX-XXX-XXXX |
| `id` | Auto-generated, can't be manually changed |

### cURL request

```bash
# Recommended base_url = http://localhost:3000
curl -X PATCH {base_url}/shelters/1 \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
          "available_pet_count": 20 
      } 
```

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `200` | `id` match | `{ "name": "Dallas Animal Services", "address": ...}` |
| `400` | Invalid field values | `{ "error": "Bad Request", "message": "Invalid value for 'adoption_fee_range'. Must be in USD.", ... }` |
| `404` | No matching `id` | `{ "error": "Not Found", "message": "Shelter with ID 1 not found.", ...}` |

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
