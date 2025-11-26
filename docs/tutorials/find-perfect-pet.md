---
layout: page
title: Find the perfect pet
permalink: /docs/tutorials/find-perfect-pet/
---

## Find the perfect pet

Use PawFinder to discover the perfect furry friend.
Learn how to search for adoptable pets using filtering
options including species, breed, shelter, and more.

### Overview

The PawFinder Service API provides an endpoint for searching
adoptable pets from shelters in the Dallas-Fort Worth area.
Filter results with query parameters to find a perfect match.
Install all [tutorial requirements](../overview/tutorial-requirements.md)
before continuing this tutorial.

### Endpoint structure

```bash
GET {base_url}/pets
```

### Query parameters

`/pets` currently only supports exact-match filtering
for the following parameters:

#### Core filters

| Parameters  | Type | Description | Examples |
|-----------|------|-------------|----------|
| `species` | string | Pet's animal type | `dog`, `cat` |
| `breed` | string | Pet's breed | `Maine Coon`, `Golden Retriever`|
| `gender` | string | Pet's gender | `male`, `female`|
| `shelter_id` | integer | Shelter's unique identifier | 1, 2, 3, 4 |

#### Size and status filters

| Parameters  | Type | Description | Examples |
|-----------|------|-------------|----------|
| `size` | string | Pet's size category | `small`,  `medium`, `large` |
| `status` | string | Pet's availability | `available`,  `pending` |

#### Pagination

_Recommended software json-server uses underscores as a naming convention
for its special query parameters - this is different from standard
REST API naming._

| Parameters  | Type | Description | Notes |
|-----------|------|-------------|----------|
| `_limit` | integer | Results per page | Default: all results |
| `_offset` | integer | Results to skip | Use with `_limit` |
| `_sort` | string | Field to sort by | `name`, `age`, `intake_date` |
| `_order` | string | Sort direction | default `desc` |

#### Exact-match filtering only

_PawFinder currently supports exact-match filtering only._
Partial matching isn't currently supported. Query parameters
must match field values exactly:

| Parameter  | Syntax | Notes |
|-----------|------|-------------|
| `breed` |`breed=Maine Coon`| Works ✅ |
| `breed` |`breed=maine coon`| Doesn't work ❌ |
| `breed` |`breed=Maine`| Partial match doesn't work ❌ |

### cURL request examples

**Example 1**: find all available dogs

```bash
curl -X GET "{base_url}/pets?species=dog" \
  -H "Content-Type: application/json"
```

**Response** `200 OK`

```json
[
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
      "vaccinations": [
        "rabies",
        "dhpp",
        "leptospirosis"
      ]
    },
    "description": "Max is an active dog who needs regular exercise
                   and responds well to commands.",
    "shelter_id": 2,
    "status": "available",
    "intake_date": "2025-07-20",
    "id": 2
  },
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
      "vaccinations": [
        "rabies",
        "dhpp"
      ]
    },
    "description": "Bella is a young lab who loves to
                   play fetch and swim.",
    "shelter_id": 4,
    "status": "pending",
    "intake_date": "2025-10-01",
    "id": 4
  }
]
```

**Example 2**: find all available cats at Dallas Animal Services

```bash
curl -X GET "{base_url}/pets?species=cat&shelter_id=1&status=available" \
  -H "Content-Type: application/json"
```

**Response** `200 OK`

```json
[
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
    "description": "Luna is a playful tabby who loves 
                   interactive toys and sunny windows.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-09-01",
    "id": 1
  },
  {
    "name": "Oliver",
    "species": "cat",
    "breed": "Maine Coon",
    "age_months": 24,
    "gender": "male",
    "size": "large",
    "temperament": "gentle, calm",
    "medical": {
      "spayed_neutered": true,
      "vaccinations": ["fvrcp", "rabies"]
    },
    "description": "Oliver is a gentle giant who loves to be
                   brushed and cuddled.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-08-15",
    "id": 5
  }
]
```

**Example 3**: search for a specific cat breed

```bash
curl -X GET "{base_url}/pets?species=cat&breed=Maine%20Coon" \
  -H "Content-Type: application/json"
```

**Response** `200 OK`

```json
[
  {
    "name": "Oliver",
    "species": "cat",
    "breed": "Maine Coon",
    "age_months": 24,
    "gender": "male",
    "size": "large",
    "temperament": "gentle, calm",
    "medical": {
      "spayed_neutered": true,
      "vaccinations": ["fvrcp", "rabies"]
    },
    "description": "Oliver is a gentle giant who loves
                   to be brushed and cuddled.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-08-15",
    "id": 5
  }
]
```

**Example 4**: get the first 2 results sorted by `name` in ascending order

```bash
curl -X GET "{base_url}/pets?_limit=2&_start=0&_sort=name&_order=asc" \
  -H "Content-Type: application/json"
```

**Response** `200 OK`

```json
[
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
      "vaccinations": [
        "rabies",
        "dhpp"
      ]
    },
    "description": "Bella is a young lab who loves to
                   play fetch and swim.",
    "shelter_id": 4,
    "status": "pending",
    "intake_date": "2025-10-01",
    "id": 4
  },
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
      "vaccinations": [
        "fvrcp",
        "rabies"
      ]
    },
    "description": "Luna is a playful tabby who loves
                   interactive toys and sunny windows.",
    "shelter_id": 1,
    "status": "available",
    "intake_date": "2025-09-01",
    "id": 1
  }
]
```

**Example 5**: search dogs from Fort Worth Shelter, sorted by `intake_date`

```bash
curl -X GET "{base_url}/pets?species=dog&shelter_id=2&_sort=intake_date&_order=desc" \
  -H "Content-Type: application/json"
```

**Response** `200 OK`

```json
[
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
      "vaccinations": [
        "rabies",
        "dhpp",
        "leptospirosis"
      ]
    },
    "description": "Max is an active dog who needs regular
                   exercise and responds well to commands.",
    "shelter_id": 2,
    "status": "available",
    "intake_date": "2025-07-20",
    "id": 2
  }
]                                                            
```

### Common responses

**Empty response** `200 OK`

If no pets match the criteria, PawFinder returns an empty array:

```json
[]
```

**Error response** `400 Bad Request` indicates a malformed set
of query parameters, verify the cURL syntax.

```json
{
  "error": "Bad Request",
  "message": "Invalid query parameter format",
  "status": 400
}
```

### Best practices

- **Start broad, then refine**\
Begin with filters like  `species` and `shelter_id`, then
add more specific criteria to narrow results.
- **Use pagination for large result sets**\
Always use pagination when displaying results to handle
large datasets efficiently. Set an appropriate `limit`
and use `offset` to fetch the next pages.
- **Cache results locally**\
Consider caching search results on the client-side with
a reasonable time to live to reduce API calls and improve
user experience.
- **Verify user input**\
Always sanitize and verify filter parameters on the
client-side before sending requests to prevent unnecessary
API errors.
- **Handle rate limiting**\
Use exponential backoff when encountering the rate limit
response: `429 Too Many Requests`.
- **Combine filters logically**\
Use `AND` logic when combining many filters. For example,
`species=dog&temperament=calm` returns dogs that are
calm, not all dogs plus all calm pets.

### Common use cases

- **Family looking for friendly dogs**\
Search with `species=dog` and `temperament=friendly`.
- **Apartment dweller seeking small pet**\
Use `size=small` to find the right pet.
- **First-time cat owner**\
Filter with `species=cat`, `temperament=calm`.

### Troubleshooting

- **No results returned**\
Filters are too restrictive. Try removing filters
one at a time to identify which criteria is limiting results.
- **Invalid parameter error**\
Check that all parameter values match the accepted values listed
in the documentation. For example, use `dog` not `dogs`.
- **Slow response times**\
While using pagination with a high total count, consider adding
more specific filters to reduce the dataset size.

### Next steps

- Explore the [shelter profiles endpoint](../api-reference/shelters.md)
to get information about specific shelters.
- Check the [pet profiles endpoint](../api-reference/pets.md)
to fetch comprehensive information about individual pets.
- Visit the [Contribution Guide](../overview/contribution-guide.md)
to suggest improvements or report issues.
