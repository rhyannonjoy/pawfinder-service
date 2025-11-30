---
layout: page
title: Replace a pet profile
permalink: /docs/api-reference/put-pets-by-id/
---

## Replace a pet profile

This operation edits all fields of an existing pet record in the PawFinder System.

### PUT vs PATCH

`PUT` replaces an entire profile and `PATCH` only updates
the fields provided in the request body. In a `PUT` request,
missing fields set to `null` or default values. In a `PATCH`
request, fields not present in the request remain unchanged.

### Endpoint structure

```bash
PUT /pets/{id}
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
| `name` | string | Pet's name |
| `species` | string | Pet's species |
| `breed` | string | Pet's breed |
| `age_months` | number | Pet's age in months |
| `gender` | string | Pet's gender |
| `size` | string | Pet's size category |
| `temperament` | string | Pet's personality traits and behavioral characteristics |
| `medical` | object | Pet's medical information |
| `medical.spayed_neutered` | boolean | Pet's spayed/neutered status|
| `medical.vaccinations` | array | List of vaccinations the pet has received |
| `description` | string | Pet's personality, needs, and background |
| `shelter_id` | number | ID of the pet's current shelter |
| `status` | string | Pet's adoption status |
| `intake_date` | string | Date the pet entered the shelter in Year-Month-Day format |

### Field requirements

| Field | Validation Rule |
|---|---|
| `species` | Must be either `cat` or `dog` |
| `gender` | Must be `male` or `female` |
| `size` | Must be `small`, `medium`, or `large` |
| `medical.spayed_neutered` | Must be boolean |
| `medical.vaccinations` | Must be array of strings |
| `status` | Must be `available`, `pending`, or `adopted` |
| `intake_date` | Must be valid ISO 8601 date in YYYY-MM-DD format |

### `id` generation

PawFinder auto-generates pet unique identifiers, `id`. The system
ignores `id` fields in `PUT` request bodies or returns a `400` error.

### cURL request

```bash
# Recommended base_url = http://localhost:3000
curl -X PUT {base_url}/pets/4 \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
        "name": "Bella", 
        "species": "dog", 
        "breed": "Labrador Retriever", 
        "age_months": 12, 
        "gender": "female", 
        "size": "large", 
        "temperament": "friendly, energetic", 
        "medical": { 
          "spayed_neutered": true, 
          "vaccinations": ["rabies", "dhpp", "leptospirosis"] 
        }, 
       "description": "Bella is a young lab who loves
                      to play fetch and swim.", 
       "shelter_id": 4, 
       "status": "adopted", 
       "intake_date": "2025-10-01" 
} 
```

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `200` | Success | `{ "name": "Bella", "species": "dog", ...}` |
| `400` | Missing values | `{ "error": "Bad Request", "message": "Missing required field: name", ... }`|
| `400` | Invalid values | `{ "error": "Bad Request", "message": "Invalid value for 'species'. Must be one of: cat, dog.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Pet with ID 4 not found.", ... }`|

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
