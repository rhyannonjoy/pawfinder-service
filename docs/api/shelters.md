# `shelters` resource

The `shelters` resource provides information about animal shelters and rescue
organizations in the PawFinder network. Shelters must register in the service
before listing pets for adoption. Visit the [pets resource](pets.md).

Base endpoint:

```shell
https://api.pawfinder.com/v1/shelters
```

## Example shelter resource

```json
{
  "name": "Dallas Animal Services",
  "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
  "phone": "+1-214-671-0249",
  "email": "info@dallasanimalservices.org",
  "hours": "Mon-Sat 11:00-18:00",
  "available_pet_count": 22,
  "adoption_fee_range": "75-200",
  "id": 1
}
```

| Property name | Type | Description |
| ------------- | ----------- | ----------- |
| `name` | string | Shelter or rescue organization official name |
| `address` | string | Shelter full street address |
| `phone` | string | Shelter phone number |
| `email` | string | Shelter email address |
| `hours` | string | Shelter operating hours |
| `available_pet_count` | number | Number of shelter's available pets |
| `adoption_fee_range` | string | Typical adoption fee range |
| `id` | number | Shelter's unique record ID |

## Property specifications

- `available_pet_count`: PawFinder automatically calculates this field and
users can't change it directly.
- `adoption_fee_range`: In United States Dollar, format "min - max"
- `id`: PawFinder auto-generates this field and users can't change it directly.

## Operations

- [Get all shelters](shelters-get-all-shelters.md) _coming soon_
- [Get shelter by ID](shelters-get-shelter-by-id.md) _coming soon_
- [Create new shelter](shelters-create-shelter.md) _coming soon_
- [Update shelter](shelters-update-shelter.md) _coming soon_
- [Delete shelter](shelters-delete-shelter.md) _coming soon_
