---
layout: page
title: Replace a pet profile
permalink: /docs/api-reference/put-pets-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Replace a pet profile

This operation edits all fields of an existing pet record
in the PawFinder System.

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

All fields required except `id`, which is auto-generated.

| Property name | Type | Description | Value Format |
| ------------- | ----------- | ----------- |----------- |
| `name` | string | Pet's name | Any text |
| `species` | string | Pet's animal type | `cat`, `dog` |
| `breed` | string | Pet's breed or breed mix | Any text |
| `age_months` | integer | Pet's age in months | Numeric value |
| `gender` | string | Pet's gender | `male`, `female` |
| `size` | string | Pet's size category | `small`, `medium`, `large` |
| `temperament` | string | Pet's personality traits, behavioral characteristics | Any text |
| `medical` | object | Pet's medical information | See nested fields below |
| `medical.spayed_neutered` | boolean | Pet's spay/neuter state | `true` or `false` |
| `medical.vaccinations` | array | List of pet's current vaccinations | Any text |
| `description` | string | Pet's personality, needs, background | Any text |
| `shelter_id` | integer | Unique identifier of pet's current shelter| Numeric value |
| `status` | string | Pet's current adoption stage | `available`, `pending`, or `adopted`|
| `intake_date` | string | Pet's shelter entry date | ISO 8601 Format, "YYYY-MM-DD" |
| `id` | integer | Pet's unique identifier | Auto-generated, read-only |

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

| Code | Scenario | Response |
|---|---|---|
| `200` | Success | `{ "name": "Bella", "species": "dog", ...}` |
| `400` | Missing values | `{ "error": "Bad Request", "message": "Missing required field: name", ... }`|
| `400` | Invalid values | `{ "error": "Bad Request", "message": "Invalid value for 'species'. Must be one of: 'cat', 'dog'.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Pet with 'id' 4 not found.", ... }`|

### Related topics

- [`/pets` resource](pets.md)
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
