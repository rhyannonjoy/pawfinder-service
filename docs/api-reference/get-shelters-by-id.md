---
layout: page
title: Get a shelter profile by ID
permalink: /docs/api-reference/get-shelters-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Get shelter profiles by `id`

This operation retrieves a shelter's profile by their `id`.

### Endpoint structure

```bash
GET /shelter/{id}
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

This operation doesn't require authentication.

### Request body

This operation doesn't require a request body.

### cURL request

```bash
# Recommended base_url = http://localhost:3000
# -X GET is optional, as GET is the default operation
curl -X GET {base_url}/shelters/1
```

### Example responses

| Code | Scenario | Response |
|---|---|---|
| `200` | Success | `{ "name": "Dallas Animal Services", "address": ...}` |
| `400` | Malformed `id` | `{ "error": "Bad Request", "message": "Invalid shelter 'id'. Must be a positive integer.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 1 not found.", ... }`|

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
