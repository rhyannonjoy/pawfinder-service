---
layout: page
title: Track Adoption Status
permalink: /docs/tutorials/api-fundamentals/track-adoption-status/
---

## Track adoption status

Observe pet availability and adoption progress in real time.
Learn how to query individual pet profiles and understand
adoption status transitions throughout the adoption workflow.

### Overview

The PawFinder Service API provides an endpoint for retrieving
individual pet profiles and tracking adoption status changes.
Use this to track whether the perfect pet is still available,
has adoption applications pending review, or has settled
with a new family. Install all
[tutorial requirements](../../overview/tutorial-requirements.md)
before continuing this tutorial.

### Endpoint structure

```bash
# Recommended base_url = http://localhost:3000
GET {base_url}/pets/{id}
```

### Path parameters

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `id` | integer | Pet's unique identifier | 1, 2, 3, 4 |

### Understanding adoption status

Pets transition through defined `status` states as they move
through the adoption process:

| Status | Meaning | Next step |
|--------|---------|-----------|
| `available` | Ready for adoption inquiries | Submit an adoption form |
| `pending` | Adoption form under review | Wait for shelter response |
| `adopted` | Successfully placed with a family | Pet is no longer available |

### cURL request examples

```bash
# Check if a specific pet is still available
curl -X GET "{base_url}/pets/1" \
  -H "Content-Type: application/json"
```

**Response** `200 OK` - `"status": "available"` indicates Luna
is ready for adoption inquiries.

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
  "status": "available",
  "intake_date": "2025-09-01",
  "id": 1
}
```

---

```bash
# Check the status of a pet with pending adoption inquiries
curl -X GET "{base_url}/pets/4" \
  -H "Content-Type: application/json"
```

**Response** `200 OK` - `"status": "pending"` means someone's adoption
form is under review. Check back later for updates.

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
    "spayed_neutered": false,
    "vaccinations": ["rabies", "dhpp"]
  },
  "description": "Bella is a young lab who loves to play fetch 
                 and swim.",
  "shelter_id": 4,
  "status": "pending",
  "intake_date": "2025-10-01",
  "id": 4
}
```

---

```bash
# Check a pet's profile to understand their medical history
curl -X GET "{base_url}/pets/3" \
  -H "Content-Type: application/json"
```

**Response** `200 OK` - Individual pet profiles include essential medical information,
making a pet's health status accessible before committing to adoption.

```json
{
  "name": "Whiskers",
  "species": "cat",
  "breed": "Siamese",
  "age_months": 60,
  "gender": "male",
  "size": "medium",
  "temperament": "vocal, intelligent",
  "medical": {
    "spayed_neutered": true,
    "vaccinations": ["fvrcp", "rabies", "felv"]
  },
  "description": "Whiskers is a talkative senior Siamese who 
                 enjoys gentle attention.",
  "shelter_id": 3,
  "status": "available",
  "intake_date": "2025-06-10",
  "id": 3
}
```

### Common error responses

**Response** `400 Bad Request` indicates an invalid pet profile `id`.
An `id` can't be non-numeric or a negative integer.

```json
{
  "error": "Bad Request",
  "message": "Invalid pet ID. Must be a positive integer.",
  "status": 400
}
```

**Response** `404 Not Found` indicates that the pet profile `id`
doesn't exist in the PawFinder system.

```json
{
  "error": "Not Found",
  "message": "Pet with ID 999 not found.",
  "status": 404
}
```

### Common use cases

- **Confirm availability before applying**\
Always retrieve the full pet profile before submitting an adoption form.
Confirm the pet is `available` and get the latest medical information.
- **Track pending applications**\
After sending an adoption form, check the pet's `status` to see if it
has changed from `pending` to `adopted`. Contact the shelter directly
for detailed status updates.
- **Review medical history**\
Use the `medical` field to understand vaccinations and spay/neuter status.
Contact the shelter about any concerns before finalizing adoption.
- **Understand a pet's needs**\
Check the `intake_date` field for how long the pet has been in the
shelter and `description` field for context about their behavior.
- **Poll for `status` updates**\
If developing with this demo API, poll this endpoint manually
and periodically to track `status` changes and test app workflows.
Production implementations might integrate
[webhooks](https://www.geeksforgeeks.org/blogs/what-is-a-webhook-and-how-to-use-it/)
for updates instead.

### Troubleshooting

- **`404 Not Found` response**\
The pet profile `id` doesn't exist. Double-check the `id` matches
a pet profile from the [search results](find-perfect-pet.md).
- **Unexpected status change**\
If the perfect pet's profile `status` suddenly shows `adopted`,
the shelter approved another applicant. Search for
[similar pets](find-perfect-pet.md) with the same criteria.
- **Missing medical information**\
All pet profiles should have medical data. If a pet profile seems
incomplete, contact the shelter directly for details.

### Next steps

- Return to [Find the Perfect Pet](find-perfect-pet.md) to search for
pets matching that match specific criteria.
- For shelter staff: [Mark a Pet as Adopted](mark-pet-adopted.md)
when finalizing adoption.
- Explore
[Build a Location-Aware Search](../../tutorials/building-applications/build-location-aware-search.md)
for a development use case that enables nearby shelter discovery.
- Visit the [Contribution Guide](../../overview/contribution-guide.md)
to suggest improvements or report issues.
