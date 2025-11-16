# Delete a pet profile

This operation removes a pet record from the PawFinder database.

## Endpoint structure

```shell
DELETE /pets/{id}
```

## Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Pet's unique identifier |

## Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

## Request body

This operation doesn't require a request body.

## cURL request

```shell
curl -X DELETE http://localhost:3000/pets/6 \
  -H "Authorization: Bearer pawfinder-secret-2025"
```

## Example responses

**Response**: `204 NO CONTENT`

```json
(No response body)
```

**Response**: `200 OK`

```json
{
  "message": "Pet with ID 6 successfully deleted",
  "deleted_id": 6
}
```

**Response**: `404 Not Found`- no matching `id`

```json
{
  "error": "Not Found",
  "message": "Pet with ID 6 not found",
  "status": 404
}
```

## Related topics

- `/pets` resource _coming soon_
- [Get all pet profiles](get-all-pets.md)
- [Add a new pet profile](post-pets.md)
- [Replace an existing pet profile](put-pets-by-id.md)
- [Partially update a pet profile](patch-pets-by-id.md)
