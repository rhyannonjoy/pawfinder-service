# Add a new pet profile

This operation creates a new pet profile in the PawFinder system.

## Endpoint structure

```bash
POST /pets
```

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | Yes |

## Request body

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

## Field requirements

| Field | Validation Rule |
|---|---|
| `species` | Must be either `cat` or `dog` |
| `gender` | Must be `male` or `female` |
| `size` | Must be `small`, `medium`, or `large` |
| `medical.spayed_neutered` | Must be boolean |
| `medical.vaccinations` | Must be array of strings |
| `status` | Must be `available`, `pending`, or `adopted` |
| `intake_date` | Must be valid ISO 8601 date in YYYY-MM-DD format |

## ID generation

PawFinder auto-generates pet unique identifiers, `id`. The system ignores
`id` fields in `POST` request bodies or returns a `400` error.

## cURL request

```bash
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
         "intake_date": "2025-11-12" 
} 
```

## Example responses

**Response**: `201 Created`

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
  "id": 6
}
```

**Response**: `400 Bad Request` - missing required field values

```json
{
  "error": "Bad Request",
  "message": "Missing required field: name",
  "status": 400
}
```

**Response**: `400 Bad Request` - invalid values for fields
`species`, `gender`, `size`, or `status`

```json
{
  "error": "Bad Request",
  "message": "Invalid value for 'species'. Must be one of 'cat', 'dog'.",
  "status": 400
}
```

## Related topics

- `/pets` resource _coming soon_
- [Get all pet profiles](get-all-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
