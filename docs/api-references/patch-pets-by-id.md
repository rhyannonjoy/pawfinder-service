# Partially update a pet profile

This operation edits specific fields of an existing pet record in the PawFinder System.

## PUT vs PATCH

`PUT` replaces an entire profile and `PATCH` only updates
the fields provided in the request body. In a `PUT` request,
missing fields set to `null` or default values. In a `PATCH`
request, fields not present in the request remain unchanged.

## Endpoint structure

```bash
PATCH /pets/{id}
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
| `id` | integer | Pet's unique record ID |

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

## cURL request

```bash
curl -X PATCH {base_url}/pets/4 \
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
       "description": "Bella is a young lab who loves to play fetch and swim.", 
       "shelter_id": 4, 
       "status": "adopted", 
       "intake_date": "2025-10-01",
       "id" : 4 
} 
```

## Example responses

**Response**: `200 OK`

```json
{
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
  "description": "Bella is a young lab who loves to play fetch and swim.",
  "shelter_id": 4,
  "status": "adopted",
  "intake_date": "2025-10-01",
  "id" : 4
}
```

**Response**: `404 Not Found`- no matching `id`

```json
{
  "error": "Not Found",
  "message": "Pet with ID 999 not found",
  "status": 404
}
```

## Related topics

- `/pets` resource _coming soon_
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Delete a pet profile](delete-pets-by-id.md)
- [Replace an existing pet profile](put-pets-by-id.md)
