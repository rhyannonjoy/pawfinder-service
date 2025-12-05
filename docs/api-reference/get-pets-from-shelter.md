---
layout: page
title: Get pet profiles from a specific shelter
permalink: /docs/api-reference/get-pets-from-shelter/
---

![PawFinder paws image](../images/paws.svg)

## Get pet profiles from a specific shelter

This operation retrieves all pet profiles associated with a specific
shelter. Use this operation to populate shelter-specific adoption
pages, allow users to browse pets by location, or generate reports
comparing pet inventory and outcomes across facilities.

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
# Retrieve all pet profiles with `shelter_id`= 1
# -X GET is optional, as GET is the default operation
# Recommended base_url = http://localhost:3000
curl -X GET {base_url}/pets?shelter_id=1
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

Either returns an empty array `[]` for no results or
an array of pet profile objects:

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
| `400` | Malformed `id` | `{ "error": "Bad Request", "message": "Invalid shelter 'id'. Must be a positive integer.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 1 not found.", ... }`|

### Related topics

- [`/shelters` resource](shelters.md)
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
