---
layout: page
title: Add a new shelter profile
permalink: /docs/api-reference/post-shelters/
---

![PawFinder paws image](../images/paws.svg)

## Add a new shelter profile

This operation creates a new shelter profile in the PawFinder system.

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

All fields required.

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

### `id` generation

PawFinder auto-generates shelter unique identifiers, `id`. The system
ignores `id` fields in `POST` request bodies or returns a `400` error.

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

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `201` | Created | `{ "name": "Plano Animal Services", "address": ...}` |
| `400` | Missing values | `{ "error": "Bad Request", "message": "Missing required field: name", ... }`|
| `400` | Invalid values | `{ "error": "Bad Request", "message": "Invalid value for 'adoption_fee_range'. Must be in USD.", ... }`|

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
