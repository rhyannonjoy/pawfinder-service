---
layout: page
title: Get all shelter profiles
permalink: /docs/api-reference/get-all-shelters/
---

![PawFinder paws image](../images/paws.svg)

## Get all shelter profiles

This operation retrieves all shelter profiles in the PawFinder system.

### Endpoint structure

```bash
GET /shelters
```

### Path parameters

This operation doesn't require parameters.

### Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

### Authentication

This operation doesn't require authentication.

### Request body

This operation doesn't require a request body.

### cURL request

```bash
# Recommended base_url = http://localhost:3000
# -X GET is optional, as GET is the default operation
curl -X GET {base_url}/shelters
```

### Example responses

| Code | Scenario | Response |
|---|---|---|
| `200` | Success | `[{ "name": "Dallas Animal Services", "address": ...}, ...]` |
| `429` | Rate limit exceeded | `{ "error": "Too Many Requests", "message": "Rate limit exceeded. Try again in 60 seconds.", ... }`|

**Successful responses includes a list of shelters with the following**:

- `name`: Shelter's name
- `address`: Shelter's location information
- `phone`: Shelter's phone number
- `email`: Shelter's email address
- `hours`: Shelter's hours of operation
- `available_pet_count`: Amount of shelter's available pets
- `adoption_fee_range`: Shelter's fee range in United States Dollars
- `id`: Shelter's unique identifier

### Related topics

- [`/shelters` resource](shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
