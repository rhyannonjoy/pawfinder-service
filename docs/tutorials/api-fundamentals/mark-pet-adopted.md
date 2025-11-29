---
layout: page
title: Mark a pet as adopted
permalink: /docs/tutorials/api-fundamentals/mark-pet-adopted/
---

## Mark a pet as `adopted`

Update a pet profile `status` when finalizing adoptions.
Learn how to update pet records using the `PATCH` method
and manage adoption workflows from the shelter perspective.

### Overview

The PawFinder Service API provides an endpoint for updating pet
profiles as adoptions progress. Shelter staff use the `PATCH`
method to mark pets as `adopted` after finalizing paperwork,
ensuring the system reflects current availability, and prevents
duplicate adoption inquiries. Install all
[tutorial requirements](../../overview/tutorial-requirements.md)
before continuing this tutorial.

### Endpoint structure

```bash
PATCH {base_url}/pets/{id}
```

### Path parameters

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `id` | integer | Pet's unique identifier | 1, 2, 3, 4 |

### Request headers

| Header | Value | Required |
|---|---|---|
| `Content-Type` | `application/json` | Yes |
| `X-API-Key` | Admin API key | Yes |

### Request body

Provide a JSON object with the fields to update. Only include
fields that are changing, as `PATCH` only updates the specified fields
and leaves the others unchanged.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `status` | string | Pet's adoption status | `adopted`, `pending`, `available` |
| `medical` | object | Pet's medical information | `{"spayed_neutered": true, "vaccinations": [...]}` |
| `intake_date` | string | Date pet entered shelter | `2025-09-01` |

### Understanding state transitions

Pet `status` moves through a defined workflow:
`available` → `pending` → `adopted`. Once a pet reaches `adopted`,
their profile shouldn't change unless there's an error that needs correction.

### cURL request examples

**Example 1**: mark a pet as `adopted`

An adopter completes paperwork for Luna, pet profile `id` = 1,
at Dallas Animal Services. Update Luna's `status` to reflect
the finalized adoption.

```bash
curl -X PATCH "{base_url}/pets/1" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin-key-12345" \
  -d '{
    "status": "adopted"
  }'
```

**Response** `200 OK` - the response confirms that Luna's status
changed from `available` to `adopted`.

```json
{
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
  "description": "Luna is a playful tabby who loves interactive 
                 toys and sunny windows.",
  "shelter_id": 1,
  "status": "adopted",
  "intake_date": "2025-09-01",
  "id": 1
}
```

**Example 2**: update different fields during adoption finalization

When finalizing an adoption, update both `status` and
any `medical` procedures completed at the shelter.

```bash
curl -X PATCH "{base_url}/pets/4" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin-key-12345" \
  -d '{
    "status": "adopted",
    "medical": {
      "spayed_neutered": true,
      "vaccinations": ["rabies", "dhpp", "leptospirosis"]
    }
  }'
```

**Response** `200 OK` - Bella's record now reflects both the
`adoption` and the completed medical procedures.

```json
{
  "name": "Bella",
  "species": "dog",
  "breed": "Labrador Retriever",
  "age_months": 12,
  "gender": "female",
  "size": "large",
  "temperament": "friendly, energetic",
  "medical": {
    "spayed_neutered": true,
    "vaccinations": ["rabies", "dhpp", "leptospirosis"]
  },
  "description": "Bella is a young lab who loves to play fetch 
                 and swim.",
  "shelter_id": 4,
  "status": "adopted",
  "intake_date": "2025-10-01",
  "id": 4
}
```

**Example 3**: move pet to `status`: `pending` during an adoption form review

Block other applicants from inquiring about a pet while an
adoption form is under review. Update the pet `status` to `pending`.

```bash
curl -X PATCH "{base_url}/pets/2" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: admin-key-12345" \
  -d '{
    "status": "pending"
  }'
```

**Response** `200 OK` - Max is now marked as `pending` while the shelter
reviews a potential adopter's form.

```json
{
  "name": "Max",
  "species": "dog",
  "breed": "Golden Retriever Mix",
  "age_months": 36,
  "gender": "male",
  "size": "large",
  "temperament": "energetic, loyal",
  "medical": {
    "spayed_neutered": true,
    "vaccinations": ["rabies", "dhpp", "leptospirosis"]
  },
  "description": "Max is an active dog who needs regular 
                 exercise and responds well to commands.",
  "shelter_id": 2,
  "status": "pending",
  "intake_date": "2025-07-20",
  "id": 2
}
```

### Verifying updates

After updating a pet record, use the `GET` method to retrieve the
full profile. Confirm that the fields requiring updates reflect
the intended changes.

```bash
curl -X GET "{base_url}/pets/1" \
  -H "Content-Type: application/json"
```

**Response** `200 OK` - `GET` request confirms that Luna's
`status` persisted as `adopted`.

```json
{
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
  "description": "Luna is a playful tabby who loves interactive 
                 toys and sunny windows.",
  "shelter_id": 1,
  "status": "adopted",
  "intake_date": "2025-09-01",
  "id": 1
}
```

---

### Common error responses

**Response** `400 Bad Request` indicates invalid values for fields
`species`, `gender`, `size`, or `status`

```json
{
  "error": "Bad Request",
  "message": "Invalid value for 'status'. Must be
             'available', 'pending', or 'adopted'.",
  "status": 400
}
```

**Response** `401 Unauthorized` indicates that the API key is
missing or invalid. All `PATCH` requests to pet profiles
require authentication.

```json
{
  "error": "Unauthorized",
  "message": "Valid API key required.",
  "status": 401
}
```

**Response** `404 Not Found` indicates that the pet profile
`id` doesn't exist in the PawFinder system.

```json
{
  "error": "Not Found",
  "message": "Pet with ID 999 not found.",
  "status": 404
}
```

### Best practices

- **Authenticate every update**\
Always include a valid API key in the `X-API-Key` header.
Production systems should rotate keys regularly.
- **Update `status` promptly**\
To prevent conflicting inquiries, mark pets as `pending`
as soon as applications arrive. Mark pets as `adopted` when finalizing
adoption paperwork. Update the `status` back to
`available` if the shelter rejects an adoption inquiry, so
that other applicants can apply.
- **Include required medical records**\
To ensure that adoptive families have access to a pet's accurate
medication information, ensure that the spay/neuter and vaccinations
are present in the pet profile.
- **Verify changes with `GET`**\
Prevent data inconsistencies by confirming that the intended
changes persist. Retrieve the recently updated record with
the `GET` method.
- **Only update necessary fields**\
Use the `PATCH` method to only update the intended fields.
Don't unnecessarily resend the entire pet object.
- **Handle errors gracefully**\
If an update fails, check the error response to determine
whether it's an authentication issue, invalid `id`, or
malformed request body.

### Troubleshooting

- **401 Unauthorized response**\
Verify the API key is valid and included in the `X-API-Key`
header. It's possible that the key requires rotation or resetting.
- **404 Not Found response**\
Confirm the pet profile `id` is correct. Use
[Get pet profiles using filters](../../api-reference/get-pets-with-filters.md)
and cross-check the pet profile's `id` with another field.
- **Changes didn't persist**\
Verify the request succeeded with a `200 OK` response.
Confirm the update by retrieving the pet record with a `GET` request.
- **Unsuccessful partial updates**\
Ensure the request body only includes intended fields.
If updating nested objects like `medical`, include the full
object structure.

### Next steps

- Check out [Track Adoption Status](track-adoption-status.md)
to observe pet availability from the adopter perspective.
- Return to [Find the Perfect Pet](find-perfect-pet.md) to
understand search workflows.
- For shelter management features, explore the
[/shelters endpoint](../../api-reference/shelters.md).
- Visit the [Contribution Guide](../../overview/contribution-guide.md)
to suggest improvements or report issues.
