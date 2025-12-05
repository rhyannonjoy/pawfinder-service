---
layout: page
title: Get a shelter profile by ID
permalink: /docs/api-reference/get-shelters-by-id/
---

![PawFinder paws image](../images/paws.svg)

## Get shelter profiles by `id`

This operation retrieves a shelter's profile by their `id`.
Use this operation to display shelter details on pet listings,
show contact information and hours for potential adopters, or
populate shelter data in administrative dashboards and reporting
tools.

### Endpoint structure

```bash
GET /shelter/{id}
```

### Path parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | integer | Yes | Shelter's unique identifier |

### Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | No |

### Authentication

This operation doesn't require authentication.

### Request body

This operation doesn't require a request body.

### cURL request

```bash
# Retrieve the shelter profile with `id`= 1
# -X GET is optional, as GET is the default operation
# Recommended base_url = http://localhost:3000
curl -X GET {base_url}/shelters/1
```

### Response fields

Each shelter profile object contains the following properties:

| Property | Type | Description | Value Format |
|---|---|---|---|
| `name` | string | Shelter's name | Any text |
| `address` | string | Shelter's location information | Any text |
| `phone` | string | Shelter's phone number | E.164 format: "+1-XXX-XXX-XXXX" |
| `email` | string | Shelter's email address | Any text |
| `hours` | string | Shelter's hours of operation | Any text |
| `available_pet_count` | integer | Shelter's available pets | Numeric value |
| `adoption_fee_range` | string | Shelter's fee range | United States Dollars |
| `id` | integer | Shelter's unique identifier | Auto-generated, read-only |

### Success response `200`

Returns a shelter profile object:

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

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `400` | Malformed `id` | `{ "error": "Bad Request", "message": "Invalid shelter 'id'. Must be a positive integer.", ... }`|
| `404` | Invalid `id` | `{ "error": "Not Found", "message": "Shelter with 'id' 1 not found.", ... }`|

### Related topics

- [`/shelters` resource](shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
