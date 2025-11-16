# Get all shelter profiles

This operation retrieves all shelter profiles in the PawFinder system.

## Endpoint structure

```shell
GET /shelters
```

## Path parameters

This operation doesn't require parameters.

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

## Request body

This operation doesn't require a request body.

## cURL request

```shell
curl -X GET http://localhost:3000/shelters
```

## Example responses

**Response**: `200 OK`

```json
[
  {
    "name": "Dallas Animal Services",
    "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
    "phone": "+1-214-671-0249",
    "email": "info@dallasanimalservices.org",
    "hours": "Mon-Sat 11:00-18:00",
    "available_pet_count": 22,
    "adoption_fee_range": "75-200",
    "id": 1
  },
  {
    "name": "Fort Worth Animal Care & Control",
    "address": "4900 Martin St, Fort Worth, TX 76119",
    "phone": "+1-817-392-1234",
    "email": "adopt@fortworthanimalcare.org",
    "hours": "Mon-Fri 11:00-18:00, Sat-Sun 12:00-17:00",
    "available_pet_count": 18,
    "adoption_fee_range": "50-175",
    "id": 2
  }
]
```

**Response**: `429 Too Many Requests`

```json
{
  "error": "Too Many Requests",
  "message": "Rate limit exceeded. Try again in 60 seconds",
  "status": 429,
  "retry_after": 60
}
```

**Successful responses includes a list of shelters with the following**:

- `name` : Shelter's name
- `address` : Shelter's location information
- `phone` : Shelter's phone number
- `email` : Shelter's email address
- `hours` : Shelter's hours of operation
- `available_pet_count` : Amount of shelter's available pets
- `adoption_fee_range` : Shelter's fee range in United States Dollar
- `id` : Shelter's unique record ID

## Related topics

- `/shelters` resource _coming soon_
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
