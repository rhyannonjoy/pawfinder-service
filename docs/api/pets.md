# `pets` resource

Contains information about adoptable pets stored in the PawFinder system.
Shelters must register in the service before listing a new pet.
Visit the [shelters resource](shelters.md).

Base endpoint:

```shell
https://api.pawfinder.com/v1/pets
```

## Example `pet` resource

```json
{
  "id": 1,
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
  "description": "Luna is a playful tabby who loves interactive toys and sunny windows.",
  "shelter_id": 1,
  "status": "available",
  "intake_date": "2025-09-01"
}
```

| Property name | Type | Description |
| ------------- | ----------- | ----------- |
| `name` | string | Pet's name |
| `species` | string | Animal type |
| `breed` | string | Pet breed or breed mix |
| `age_months` | number | Pet's age in months |
| `gender` | string | Pet's gender |
| `size` | string | Pet size category |
| `temperament` | string | Pet personality traits and behavioral characteristics |
| `medical` | object | Pet medical information |
| `medical.spayed_neutered` | boolean | Pet spay/neuter status |
| `medical.vaccinations` | array | List of pet's current vaccinations |
| `description` | string | Pet's personality, needs, background |
| `shelter_id` | number | ID of pet's current shelter|
| `status` | string | Pet's current adoption status |
| `intake_date` | string | When the pet entered the shelter |
| `id` | number | Pet's unique record ID |

## Property specifications

- `species` : `cat`, `dog`, `bird`, `rabbit`, `other`
- `gender`: `male`, `female`, `unknown`
- `size`: `small`, `medium`, `large`, `extra_large`
- `status`: `available`, `pending`, `adopted`, `hold`, `transferred`
- `intake_date`: International Standard 8601 format, such as "2025-09-01"

## Operations

- [Get all pets](pets-get-all-pets.md) _coming soon_
- [Get pet by ID](pets-get-pet-by-id.md) _coming soon_
- [Create new pet](pets-create-pet.md) _coming soon_
- [Update pet](pets-post-patch-pets.md) _coming soon_
- [Delete pet](pets-delete-pets.md) _coming soon_
