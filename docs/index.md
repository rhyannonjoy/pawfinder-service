# PawFinder API Overview

## Introduction

PawFinder is a REST API that connects potential pet adopters with animal shelters in the greater
Dallas-Fort Worth area. This platform aggregates real-time data from hundreds of shelters,
making it easier for people to find their perfect companion
and for shelters to reach qualified adopters.
This API enables developers to:

- Search available pets by species, breed, age, location and temperament
- Access detailed shelter profiles and contact information
- Track adoption status updates in real time
- Build custom adoption workflows and notification systems

## Key concepts

### Pets

Each pet in the PawFinder system has a unique identifier and includes standardized information
such as species, breed, age, size, temperament traits, medical history, and current location.
Pets transition through adoption statuses tracked by the API.

### Shelters

Organizations register as shelters to list pets for adoption. Each shelter maintains a profile with
contact information, operating hours, adoption requirements, and geographic service areas.
Shelters can update pet listings and adoption statuses through the API.

### Adoption status

Pets progress through defined status states:

- `available`: Ready for adoption inquiries
- `pending`: Adoption under review
- `adopted`: Successfully placed with a family
- `hold`: Temporarily unavailable
- `transferred`: Moved to another shelter

### Search filters

PawFinder API supports multi-criteria searches including:

- **Location-based**: Postal code, city, radius in miles
- **Species and breed**: Birds, cats, dogs, rabbits, and other small animals
- **Characteristics**: Age range, size, gender, special needs status
- **Behavioral Traits**: activity level, "good with kids," "good with other pets"
- **Shelter-specific**: Filter by specific shelter or shelter network

## Use cases

### Develop for adopters

- Build mobile apps that send push notifications when pets matching user preferences
become available
- Create location-aware web apps that display nearby adoptable pets
- Develop pet comparison tools that help users understand different characteristics

### Develop for shelters

- Integrate PawFinder search into existing shelter websites to increase visibility
- Automate adoption status updates across many listing platforms
- Generate analytics reports on inquiry rates and adtoption trends

### Develop for communities

- Build aggregator sites that compare pets across many shelters
- Create matching algorithms that pair adopters with compatible pets
- Develop volunteer coordination tools that connect shelter needs with community support

## Authentication

All API requests require authentication using API keys passed in the request header:

```shell
Authorization: Bearer YOUR_API_KEY
```

**Get an API key**:

1. Create a free account at developers.pawfinder.com
2. Generate an API key from your dashboard
3. Store your key securely, it grants access to your account

**Security best practices**:

- Never commit API keys to version control
- Rotate keys every 90 days
- Use environment variables to store keys in production
- Use key-specific permissions for team access

**Rate Limits**:

API usage is subject to rate limits based on your account tier:

| Tier | Requests per minute | Daily limit |
|------|---------------------|-------------|
| Free | 60 | 1,000 |
| Standard | 300 | 10,000 |
| Premium | 1,000 | 100,000 |
| Enterprise | Custom | Custom |

Every response includes rate limit headers:

```shell
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 45
X-RateLimit-Reset: 1638360000
```

When you exceed your rate limit, the API returns the `429 Too Many Requests` HTTP status code.
Try exponential backoff in your retry logic to handle rate limiting gracefully.

## Base URL and versioning

Make all API requests to:

```shell
https://api.pawfinder.com
```

**Versioning**

The PawFinder API uses URI versioning.
The current stable version is `v1`:

```shell
https://api.pawfinder.com/v1/pets
https://api.pawfinder.com/v1/shelters
```

**Version support policy**:

- PawFinder supports all major versions for 24 months after a new version releases
- Deprecated endpoints include a `Sunset` header indicating end-of-life date
- Breaking changes are only introduced in major version increments
- Minor updates and bug fixes don't require version changes

## Next steps

- API Reference _*coming soon*_
- Authentication Guide _*coming soon*_
- Quickstart _*coming soon*_
