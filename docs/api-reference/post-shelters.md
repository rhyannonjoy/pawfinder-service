---
layout: page
title: Add a new shelter profile
permalink: /docs/api-reference/post-shelters/
---

![PawFinder paws image](../images/paws.svg)

## Add a new shelter profile

This operation creates a new shelter profile in the PawFinder system.
Use this operation to onboard new animal shelters and rescue groups,
register more facility locations for existing organizations, or
add foster networks that manage pet adoption listings.

### Endpoint structure

```bash
POST /shelters
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

All fields required except for `id`, which is auto-generated.

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
# Recommended base_url = http://localhost:3000
curl -X POST {base_url}/shelters \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
        "name": "Plano Animal Services", 
        "address": "4028 W Plano Pkwy, Plano, TX 75093", 
        "phone": "+1-972-769-4360", 
        "email": "contact@planoanimalservices.org", 
        "hours": "Mon-Fri 10:00-17:00, Sat 10:00-16:00", 
        "available_pet_count": 12, 
        "adoption_fee_range": "80-150" 
} 
```

### Success response `201 Created`

Returns the created shelter profile with the assigned `id`:

```json
{ 
  "name": "Plano Animal Services", 
  "address": "4028 W Plano Pkwy, Plano, TX 75093", 
  "phone": "+1-972-769-4360", 
  "email": "contact@planoanimalservices.org",       
  "hours": "Mon-Fri 10:00-17:00, Sat 10:00-16:00", 
  "available_pet_count": 12, 
  "adoption_fee_range": "80-150",
  "id": 12
} 
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `400` | Missing values | `{ "error": "Bad Request", "message": "Missing required field: name", ... }`|
| `400` | Invalid values | `{ "error": "Bad Request", "message": "Invalid value for 'adoption_fee_range'. Must be in USD.", ... }`|
| `401` | Missing API token | `{ "error": "Unauthorized", "message": "Authentication token is required for this operation.", ... }` |
| `403` | Invalid API token | `{ "error": "Forbidden", "message": "Invalid or expired authentication token.", ...}` |

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
