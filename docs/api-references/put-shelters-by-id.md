# Replace a shelter profile

This operation edits all fields of an existing shelter record in the PawFinder System.

## PUT vs PATCH

`PUT` replaces an entire profile and `PATCH` only updates
the fields provided in the request body. In a `PUT` request,
missing fields set to `null` or default values. In a `PATCH`
request, fields not present in the request remain unchanged.

## Endpoint structure

```bash
PUT /shelters/{id}
```

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | Yes |

## Request body

All fields required.

| Property | Type | Description |
|---|---|---|
| `name` | string | Shelter's name |
| `address` | string | Shelter's address information |
| `phone` | string | Shelter's phone number, E.164 format |
| `email` | string | Shelter's email address |
| `hours` | string | Shelter's hours of operation |
| `available_pet_count` | integer | Shelter's available pets |
| `adoption_fee_range` | string | Shelter's fee range in United States Dollar |

## Field requirements

| Field | Validation Rule |
|---|---|
| `phone` | Must be E.164 format: +1-XXX-XXX-XXXX |

## ID generation

PawFinder auto-generates shelter unique identifiers, `id`. The system
ignores `id` fields in `PUT` request bodies or returns a `400` error.

## cURL request

```bash
curl -X PUT http://localhost:3000/shelters/1 \
  -H "Authorization: Bearer pawfinder-secret-2025" \
  -H "Content-Type: application/json" \
  -d '{ 
         "name": "Dallas Animal Services", 
         "address": "1818 N Westmoreland Rd, Dallas, TX 75212", 
         "phone": "+1-214-671-0249", 
         "email": "info@dallasanimalservices.org", 
         "hours": "Mon-Sat 11:00-19:00", 
         "available_pet_count": 25, 
        "adoption_fee_range": "75-200" 
}   
```

## Example responses

**Response**: `200 OK`

```json
{
  "name": "Dallas Animal Services",
  "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
  "phone": "+1-214-671-0249",
  "email": "info@dallasanimalservices.org",
  "hours": "Mon-Sat 11:00-19:00",
  "available_pet_count": 25,
  "adoption_fee_range": "75-200"
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
`phone` or `adoption_fee_range`

```json
{
  "error": "Bad Request",
  "message": "Invalid value for 'adoption_fee_range'. Must be in USD.",
  "status": 400
}
```

**Response**: `404 Not Found` - no matching `id`

```json
{
  "error": "Not Found",
  "message": "Shelter with ID 999 not found",
  "status": 404 
}
```

## Related topics

- `/shelters` resource _coming soon_
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
