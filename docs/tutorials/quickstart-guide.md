---
layout: page
title: Quickstart Guide
permalink: /docs/tutorials/quickstart-guide/
---

## Quickstart guide

Quickly integrate the PawFinder Service API. This guide covers
making a `GET` request to the `/pets` endpoint to retrieve
a list of available pets.

### Prerequisites

Read-only operations don't require authentication, but install the
recommended tools in the [Tutorial Requirements](../overview/tutorial-requirements.md)
before continuing this tutorial.

### Use cURL

```bash
curl -X GET "{base_url}/pets" \
  -H "Content-Type: application/json"
```

### Use Postman

1. Open Postman Desktop
2. Create a new request
3. Set the method to `GET`
4. Enter the URL: `{base_url}/pets`
5. Click **Send**
6. Observe the response

### Response details

A successful request returns a `200 OK` status code with a JSON
array of pet profiles, for example:

```json
[
  {
    "id": 1,
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
    "description": "Luna is a playful tabby who loves
                   interactive toys and sunny windows.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-09-01"
  }
]
```

#### Pet profile field descriptions

| Property name | Type | Description |
| ------------- | ----------- | ----------- |
| `name` | string | Pet's name |
| `species` | string | Pet's animal type, `cat` or `dog` |
| `breed` | string | Pet's breed or breed mix, if known |
| `age_months` | integer | Pet's age in months |
| `gender` | string | Pet's gender, `female` or `male` |
| `size` | string | Pet's size category, `small`, `medium`, `large` |
| `temperament` | string | Pet's personality traits, behavioral characteristics |
| `medical` | object | Pet's medical information |
| `medical.spayed_neutered` | boolean | Pet's spay/neuter status |
| `medical.vaccinations` | array | List of pet's current vaccinations |
| `description` | string | Pet's personality, needs, background |
| `shelter_id` | integer | ID of pet's current shelter|
| `status` | string | Pet's current adoption status, `available`, `pending`, or `adopted` |
| `intake_date` | string | When the pet entered the shelter, ISO 8601 format |
| `id` | integer | Pet's unique identifer |

### Filter pet profile results

Filter results by adding query parameters to the request.

```bash
# Find all available dogs
curl -X GET "{base_url}/pets?species=dog"
```

```bash
# Find all cats at a specific shelter
curl -X GET "{base_url}/pets?species=cat&shelter_id=1"
```

```bash
# Sort pet profiles by name, in ascending order
curl -X GET "{base_url}/pets?_sort=name&_order=asc"
```

For more filtering options, visit
[Get pet profiles using filters](../api-reference/get-pets-with-filters.md).

### Paginate large result sets

Use `_limit` and `_start` to paginate through results.

```bash
# Get the first 10 results
curl -X GET "{base_url}/pets?_limit=10&_start=0"

# Get the next 10 results
curl -X GET "{base_url}/pets?_limit=10&_start=10"
```

### Common errors

| Code | Description  |
|------|--------------|
| `400` | Bad Request, verify query parameters |
| `404` | Not Found, verify `base_url` |
| `429` | Too Many requests, exceeding rate limit |
| `500` | Something is wrong with the server, try again later |

### Next steps

- Explore the [API Index](../api-reference/api-index.md)
for complete endpoint documentation.
- Check out the [Find the Perfect Pet](find-perfect-pet.md)
tutorial for advanced filtering.
- View the [PawFinder source code on GitHub](https://github.com/rhyannonjoy/pawfinder-service).

### Get help

- Review the [`/pets` resource](../api-reference/pets.md)
for field requirements.
- Review [common errors](../api-reference/api-index.md).
- Open an issue on [GitHub](https://github.com/rhyannonjoy/pawfinder-service/issues).
