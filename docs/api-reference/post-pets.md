---
layout: page
title: Add a new pet profile
permalink: /docs/api-reference/post-pets/
---

![PawFinder paws image](../images/paws.svg)

## Add a new pet profile

This operation creates a new pet profile in the PawFinder system.
Use this operation to add newly intake animals to shelter inventory,
list pets for adoption after medical clearance and evaluation, or
register animals transferred from other facilities.

### Endpoint structure

```bash
POST /pets
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

All fields required except for `id`, which is auto-generated.

| Property | Type | Description | Value Format |
|---|---|---|---|
| `name` | string | Pet's name | Any text |
| `species` | string | Pet's species | `cat` or `dog` |
| `breed` | string | Pet's breed | Any text |
| `age_months` | number | Pet's age in months | Numeric value |
| `gender` | string | Pet's gender | `male` or `female` |
| `size` | string | Pet's size category | `small`, `medium`, or `large` |
| `temperament` | string | Pet's personality traits and behavioral characteristics | Any text |
| `medical` | object | Pet's medical information | See nested fields below |
| `medical.spayed_neutered` | boolean | Pet's spayed/neutered state| `true` or `false` |
| `medical.vaccinations` | array | List of vaccinations the pet has received | Any text |
| `description` | string | Pet's personality, needs, and background | Any text |
| `shelter_id` | number | Unique identifier of pet's current shelter | Numeric value |
| `status` | string | Pet's current adoption stage | `available`, `pending`, or `adopted` |
| `intake_date` | string | Pet's shelter entry date | ISO 8601 format, "YYYY-MM-DD" |
| `id` | integer| Pet's unique identifier | Auto-generated, read-only |

### cURL request

```bash
# Recommended base_url = http://localhost:3000
curl -X POST {base_url}/pets \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
          "name": "Charlie", 
          "species": "dog", 
          "breed": "Beagle", 
          "age_months": 24, 
          "gender": "male", 
          "size": "medium", 
          "temperament": "curious, friendly", 
          "medical": { 
            "spayed_neutered": true, 
            "vaccinations": ["rabies", "dhpp"] 
          }, 
         "description": "Charlie is a friendly beagle who loves exploring.", 
         "shelter_id": 1, 
         "status": "available", 
         "intake_date": "2025-12-04" 
} 
```

### Success response `201 Created`

Returns the created pet profile with the assigned `id`:

```json
{ 
  "name": "Charlie", 
  "species": "dog", 
  "breed": "Beagle", 
  "age_months": 24, 
  "gender": "male", 
  "size": "medium", 
  "temperament": "curious, friendly", 
  "medical": { 
    "spayed_neutered": true, 
    "vaccinations": ["rabies", "dhpp"] 
  }, 
  "description": "Charlie is a friendly beagle who loves exploring.", 
  "shelter_id": 1, 
  "status": "available", 
  "intake_date": "2025-11-12",
  "id": 42
} 
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `400` | Missing values | `{ "error": "Bad Request", "message": "Missing required field: name", ... }`|
| `400` | Invalid values | `{ "error": "Bad Request", "message": "Invalid value for 'species'. Must be one of 'cat', 'dog'.", ... }`|
| `401` | Missing API token | `{ "error": "Unauthorized", "message": "Authentication token is required for this operation.", ... }` |
| `403` | Invalid API token | `{ "error": "Forbidden", "message": "Invalid or expired authentication token.", ...}` |

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
