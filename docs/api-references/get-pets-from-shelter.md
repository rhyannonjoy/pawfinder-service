# Get pet profiles from a specific shelter

This operation retrieves all pets associated with a specific shelter.

## Endpoint structure

```bash
GET /shelters/{id}/pets
```

## Path parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | integer | The unique identifier of the shelter |

## Query parameters

This operation doesn't require query parameters.

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

## Request body

This operation doesn't require a request body.

## cURL request

```bash
curl -X GET {base_url}/shelters/1/pets
```

## Example responses

**Response**: `200 OK` with matches

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
    "id": 1
  },
  {
    "name": "Oliver",
    "species": "cat",
    "breed": "Maine Coon",
    "age_months": 24,
    "gender": "male",
    "size": "large",
    "temperament": "gentle, calm",
    "medical": {
      "spayed_neutered": true,
      "vaccinations": ["fvrcp", "rabies"]
    },
    "description": "Oliver is a gentle giant who loves
                   to be brushed and cuddled.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-08-15",
    "id": 5
  }
]
```

**Response**: `200 OK` without any matches

```json
[]
```

**Successful responses include a list of pets with the following**:

- `name` : Pet's name
- `species` : Pet's species
- `breed` : Pet's breed
- `age_months` : Pet's age in months
- `gender` : Pet's gender
- `size` : Pet's size category
- `temperament` : Pet's personality traits and behavioral characteristics
- `medical` : Pet's medical information
- `description` : Pet's personality, needs, and background
- `shelter_id` : ID of pet's current shelter
- `status` : Pet's adoption status
- `intake_date` : Date the pet entered the shelter
- `id` : Pet's unique record ID

## Related topics

- `/shelters` resource _coming soon_
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
