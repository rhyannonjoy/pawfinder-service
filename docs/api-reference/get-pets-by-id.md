---
layout: page
title: Get a pet profile by ID
permalink: /docs/api-reference/get-pets-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Get pet profiles by `id`

This operation retrieves a pet's profile by their `id`.
Use this endpoint to retrieve information about a specific
pet, such as, after a user clicks on a pet profile
from search results.

### Pet adoption interest workflow

When displaying a pet profile, a client app may allow users
to express interest in adopting the pet. The sequence
diagram below shows how this workflow might interact with
a production system that has a more robust architecture:

```mermaid
sequenceDiagram
    actor User as Adopter
    participant App as Client App
    participant Gateway as API Gateway
    participant Auth as Auth Service
    participant PetSvc as Pet Service
    participant AdoptSvc as Adoption Service
    participant AdoptDB as Adoption Database
    
    User->>App: View Pet Details
    App->>Gateway: GET /pets/1
    Gateway->>PetSvc: Fetch Pet
    PetSvc-->>Gateway: Pet Data
    Gateway-->>App: 200 OK - Pet Details
    App-->>User: Display Pet Profile
    
    User->>App: Click "Express Interest"
    App->>Gateway: POST /pets/1/interest
    Gateway->>Auth: Verify API Token
    Auth-->>Gateway: ✓ Valid Token
    
    Gateway->>AdoptSvc: Create Interest Record
    AdoptSvc->>AdoptDB: INSERT adoption_interest
    AdoptDB-->>AdoptSvc: Interest ID Created
    AdoptSvc-->>Gateway: Interest Confirmed
    
    Gateway-->>App: 201 Created - Interest ID
    App-->>User: ✓ Interest Recorded
    
    rect rgba(200, 180, 200, 0.2)
    note right of AdoptDB: Shelter receives notification<br/>of adopter interest
    end
```

### Endpoint structure

```bash
GET /pets/{id}
```

### Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Pet's unique identifier |

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
curl -X GET {base_url}/pets/1
```

### Example responses

| Status | Scenario | Response |
|---|---|---|
| `200` | `id` match | `{ "name": "Luna", "species": "cat",...}` |
| `400` | Invalid `id` | `{ "error": "Bad Request", "message": "Invalid pet ID. Must be a positive integer." ...}` |
| `404` | No matching `id` | `{ "error": "Not Found", "message": "Pet with ID 999 not found.", ...}` |

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
- `shelter_id`: ID of pet's current shelter
- `status`: Pet's adoption status
- `intake_date`: When the pet entered the shelter
- `id`: Pet's unique record ID

### Related topics

- [`/pets` resource](pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
