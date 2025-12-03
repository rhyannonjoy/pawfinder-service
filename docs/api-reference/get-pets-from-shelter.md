---
layout: page
title: Get pet profiles from a specific shelter
permalink: /docs/api-reference/get-pets-from-shelter/
---

![PawFinder paws image](../images/paws.svg)

## Get pet profiles from a specific shelter

This operation retrieves all pets associated with a specific shelter.

### Endpoint structure

```bash
GET /pets?shelter_id={id}
```

### Path parameters

This operation doesn't use path parameters.

### Query parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `shelter_id` | integer | Shelter's unique identifier |

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
curl -X GET {base_url}/pets?shelter_id=1
```

### Example responses

| Code | Scenario | Response |
|---|---|---|
| `200` | Success | `[{ "name": "Luna", "species": "cat", ...}, ...]` |
| `200` | Success, no matches | `[]` |
| `400` | Malformed `id` | `{ "error": "Bad Request", "message": "Invalid shelter 'id'. Must be a positive integer.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 1 not found.", ... }`|

**Successful responses include a list of pets with the following**:

- `name`: Pet's name
- `species`: Pet's species
- `breed`: Pet's breed
- `age_months`: Pet's age in months
- `gender`: Pet's gender
- `size`: Pet's size category
- `temperament`: Pet's personality traits and behavioral characteristics
- `medical`: Pet's medical information
- `description`: Pet's personality, needs, and background
- `shelter_id`: Unique identifier of pet's current shelter
- `status`: Pet's current adoption stage
- `intake_date`: Pet's shelter entry date
- `id`: Pet's unique identifier

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
