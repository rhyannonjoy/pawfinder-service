---
layout: page
title: Get a pet profile by ID
permalink: /docs/api-reference/get-pets-by-id/
---

# Get pet profiles by id

This operation retrieves a pet's profile by their ID.

## Endpoint structure

```bash
GET /pets/{id}
```

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Pet's unique identifier |

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

## Request body

This operation doesn't require a request body.

## cURL request

```bash
curl -X GET {base_url}/pets/1
```

## Example responses

**Response**: `200 OK`

```json
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
```

**Response**: `400 Bad Request` - invalid `id`, either non-numeric or negative integer

```json
{
  "error": "Bad Request",
  "message": "Invalid pet ID. Must be a positive integer",
  "status": 400
}
```

**Response**: `404 Not Found` - no matching `id`

```json
{
  "error": "Not Found",
  "message": "Pet with ID 999 not found",
  "status": 404
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

## Related topics

- [`/pets` resource](pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
