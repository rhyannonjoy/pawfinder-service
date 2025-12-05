---
layout: page
title: Get all shelter profiles
permalink: /docs/api-reference/get-all-shelters/
---

![PawFinder paws image](../images/paws.svg)

## Get all shelter profiles

This operation retrieves all shelter profiles in the PawFinder system.
Use this operation to populate adoption listings, enable browse
and discovery features, or sync shelter data with external platforms.

### Endpoint structure

```bash
GET /shelters
```

### Path parameters

This operation doesn't require parameters.

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
# -X GET is optional, as GET is the default operation
# Recommended base_url = http://localhost:3000
curl -X GET {base_url}/shelters
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

Returns an array of shelter profile objects:

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
]
```

### Error responses

| Code | Scenario | Response |
|---|---|---|
| `404` | Incorrect endpoint | `{ "error": "Not Found", "message": "The requested endpoint does not exist.", ... }`|
| `429` | Rate limit exceeded | `{ "error": "Too Many Requests", "message": "Rate limit exceeded. Try again in 60 seconds.", ... }`|

### Related topics

- [`/shelters` resource](shelters.md)
- [Add a new shelter profile](post-shelters.md)
- [Delete a shelter profile](delete-shelters-by-id.md)
- [Replace an existing shelter profile](put-shelters-by-id.md)
- [Partially update a shelter profile](patch-shelters-by-id.md)
