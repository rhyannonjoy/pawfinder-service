# PawFinder API Documentation

Welcome to the API for animal adoption. Learn how to connect
adoptable pets with potential families by integrating pet
adoption data into apps, websites, and services.

## Overview

Get familiar with the fundamentals and core concepts
in the [PawFinder API Overview](./overview/overview.md). Learn more
about pets, shelters, adoption status, and search filters. Discover
how different development audiences use the API.

## Developer environment setup

Install all [tutorial requirements](./overview/tutorial-requirements.md)
before proceeding to the tutorials.

## Quick start

Get up and running in the [Quick Start](./tutorials/quick-start.md), _coming soon_. \
View a real JSON example with field-by-field annotations.
Make a `GET` request to `/pets`.

## Tutorials

Tour task-based guides for common workflows and use cases.

- [Search for Adoptable Pets](tutorials/search-adoptable-pets.md), _coming soon_ \
  Filter pets by species, breed, location, age, and other criteria.

- [Get Shelter Information](tutorials/get-shelter-information.md,), _coming soon_ \
  Retrieve shelter directory listings and availability data.

- [Track Adoption Status](tutorials/track-adoption-status.md), _coming soon_ \
  Follow pet availability and adoption status in real-time.

- [Build a Location-Based Search](tutorials/location-based-search.md), _coming soon_ \
  Apply proximity filtering and distance calculations.

- [Handle Pagination](tutorials/handle-pagination.md), _coming soon_ \
  Work efficiently with large result sets and pagination controls.

## API Reference

Survey [the complete technical](./api-references/api-reference.md) reference
for all endpoint operations, parameters, and responses.

### `/pets`

- [GET /pets/](./api-references/get-all-pets.md) \
  Search and filter available pets with different criteria.

- [GET /pets/{id}](./api-references/get-pets-by-id.md) \
  Retrieve detailed information for a specific pet.

- [GET /pets/{id}/status](./api-references/get-pets-with-filters.md) \
  Check current adoption status and availability.

### `/shelters`

- [GET /shelters](./api-references/get-all-shelters.md) \
  List all participating shelters with filtering options.

- [GET /shelters/{id}](./api-references/get-shelters-by-id.md) \
  Get detailed shelter information and contact details.

- [GET /shelters/{id}/pets](./api-references/get-pets-from-shelter.md) \
  Retrieve all pets currently available at a specific shelter.

## Authentication guide

Pick-up API keys, receive credentials, and keep up with rate limits
in the [Authentication guide](./overview/authentication-guide.md).

## Get help

- Check real-time API status at [status.pawfinder.com](status.pawfinder.com)
- Found an error or have a suggestion?
[Report it here](https://github.com/rhyannonjoy/pawfinder-service/issues).
- Need help integrating? [Contact support@pawfinder.com](support@pawfinder.com)
