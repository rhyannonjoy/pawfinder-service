# Delete a shelter profile

This operation removes a shelter record from the PawFinder database.

## Endpoint structure

```bash
DELETE /shelters/{id}
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

```bash
curl -X DELETE {base_url}/shelters/5 \
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
  "message": "Shelter with ID 5 successfully deleted",
  "deleted_id": 5
}
```

**Response**: `404 Not Found`- no matching `id`

```json
{
  "error": "Not Found",
  "message": "Shelter with ID 5 not found",
  "status": 404
}
```

## Related topics

- `/shelters` resource _coming soon_
- [Get all shelter profiles](get-all-shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
