# Get shelter profiles by id

This operation retrieves a shelter's profile by their ID.

## Endpoint structure

```shell
GET /shelter/{id}
```

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Shelter's unique identifier |

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

## Request body

This operation doesn't require a request body.

## cURL request

```shell
curl -X GET http://localhost:3000/shelters/1
```

## Example responses

**Response**: `200 OK`

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

**Response**: `400 Bad Request` - invalid `id`, either non-numeric or negative integer

```json
{
  "error": "Bad Request",
  "message": "Invalid shelter ID. Must be a positive integer",
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
