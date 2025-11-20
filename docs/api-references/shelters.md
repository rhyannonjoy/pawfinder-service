# `shelters` resource

Provides information about animal shelters and rescue organizations
in the PawFinder network. Shelters must register in the service
before listing pets for adoption. Visit the [pets resource](pets.md).

Base endpoint:

```shell
{base_url}/shelters
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
| `name` | string | Shelter's official name |
| `address` | string | Shelter's address information |
| `phone` | string | Shelter's phone number |
| `email` | string | Shelter's email address |
| `hours` | string | Shelter's operating hours |
| `available_pet_count` | integer | Number of shelter's available pets |
| `adoption_fee_range` | string | Shelter's typical adoption fee range |
| `id` | number | Shelter's unique record ID |

## Field requirements

- `phone` : Must be in  E.164 format, such as +1-XXX-XXX-XXXX
- `adoption_fee_range` : Must be in USD, format "min - max"
- `id` : PawFinder auto-generates this field and users can't change it directly.

## Operations

- Get all shelter profiles, _coming soon_
- Get shelter profiles by ID, _coming soon_
- Get shelter profiles by filters, _coming soon_
- Get pets from a specific shelter, _coming soon_
- Create new shelter profiles, _coming soon_
- Delete shelter profiles, _coming soon_
- Partially update shelter profiles, _coming soon_
- Replace shelter profiles, _coming soon_
