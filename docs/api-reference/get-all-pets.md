---
layout: page
title: Get all pet profiles
permalink: /docs/api-reference/get-all-pets/
---

![PawFinder paws image](../images/paws.svg)

## Get all pet profiles

This operation retrieves all pets in the PawFinder system.

### Endpoint structure

```bash
GET /pets
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
curl -X GET {base_url}/pets
```

### Example responses

| Code | Scenario | Response |
|---|---|---|
| `200` | Success | `[{ "name": "Luna", "species": "cat", ...}, ...]` |
| `429` | Rate limit exceeded | `{ "error": "Too Many Requests", "message": "Rate limit exceeded. Try again in 60 seconds.", ... }`|

**Successful responses includes a list of pets with the following**:

- `name`: Pet's name
- `species`: Pet's species
- `breed`: Pet's breed if known
- `age_months`: Pet's age in months
- `gender`: Pet's gender if known
- `size`: Pet's size category
- `temperament`: Pet's personality traits and behavioral characteristics
- `medical`: Pet's medical information
- `description`: Pet's personality, needs, background
- `shelter_id`: Unique identifier of the pet's current shelter
- `status`: Pet's current adoption stage
- `intake_date`: Pet's shelter entry date
- `id`: Pet's unique identifier

### Related topics

- [`/pets` resource](pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
