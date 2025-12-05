---
layout: page
title: Get all pet profiles
permalink: /docs/api-reference/get-all-pets/
---

![PawFinder paws image](../images/paws.svg)

## Get all pet profiles

This operation retrieves all pet profiles in the PawFinder system.
Use this operation to populate adoption listings, enable browse
and discovery features, or sync pet data with external platforms.

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
# -X GET is optional, as GET is the default operation
# Recommended base_url = http://localhost:3000
curl -X GET {base_url}/pets
```

### Response fields

Each pet profile object contains the following properties:

| Property | Type | Value Format |
|---|---|---|
| `name` | string | Any text |
| `species` | string | `cat` or `dog` |
| `breed` | string | Any text |
| `age_months` | integer | Numeric value |
| `gender` | string | `male` or `female` |
| `size` | string | `small`, `medium`, or `large` |
| `temperament` | string | Any text |
| `medical` | object | See nested fields below |
| `medical.spayed_neutered` | boolean | `true` or `false` |
| `medical.vaccinations` | array | Array of strings |
| `description` | string | Any text |
| `shelter_id` | integer | Numeric value |
| `status` | string | `available`, `pending`, or `adopted` |
| `intake_date` | string | ISO 8601 Format, "YYYY-MM-DD" |
| `id` | integer | Auto-generated, read-only |

### Success response `200`

Returns an array of pet profile objects:

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
    "description": "Luna is a playful tabby who loves
                  interactive toys and sunny windows.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-09-01",
    "id": 1,
  },
  ...
]
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `404` | Incorrect endpoint | `{ "error": "Not Found", "message": "The requested endpoint does not exist.", ... }`|
| `429` | Rate limit exceeded | `{ "error": "Too Many Requests", "message": "Rate limit exceeded. Try again in 60 seconds.", ... }`|

### Related topics

- [`/pets` resource](pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
