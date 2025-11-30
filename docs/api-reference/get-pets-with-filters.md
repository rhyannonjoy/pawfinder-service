---
layout: page
title: Get pet profiles using filters
permalink: /docs/api-reference/get-pets-with-filters/
---

## Get pet profiles using filters

This operation retrieves pets profiles that match the specified filter criteria.

### Endpoint structure

```bash
GET /pets?{query_parameters}
```

### Path parameters

This operation doesn't require path parameters.

### Query parameters

This operation accepts the following optional query parameters
to filter results:

| Parameter | Type | Description |
|-----------|------|-------------|
| `species` | string | Filter pets by species, `cat`|
| `status` | string | Filter pets by adoption status, `available`|
| `breed` | string | Filter pets by breed |
| `size` | string | Filter pets by size category, `small`|
| `gender` | string | Filter pets by gender |
| `shelter_id` | integer | Filter pets by shelter ID |

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
curl -X GET {base_url}/pets?species=cat&status=available
```

### Example responses

**Response**: `200 OK` - with a match

```json
[
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
    "description": "Luna is a playful tabby who loves interactive
                   toys and sunny windows.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-09-01",
    "id": 1
  }
]
```

**Response**: `200 OK` - without any matches

```json
{
  []
}
```

**Response**: `400 Bad Request` - malformed query parameters

```json
{
  "error": "Bad Request",
  "message": "Invalid query parameter format",
  "status": 400
}
```

**Successful responses includes a list of pets with the following**:

- `name` : Pet's name
- `species` : Pet's species
- `breed` : Pet's breed if known
- `age_months` : Pet's age in months
- `gender` : Pet's gender if known
- `size` : Pet's size category
- `temperament` : Pet's personality traits and behavioral characteristics
- `medical` : Pet's medical information
- `description` : Pet's personality, needs, background
- `shelter_id` : ID of pet's current shelter
- `status` : Pet's adoption status
- `intake_date` : When the pet entered the shelter
- `id` : Pet's unique record ID

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
