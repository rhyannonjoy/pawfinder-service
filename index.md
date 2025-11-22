---
layout: default
title: Home
---

# PawFinder API Documentation

Welcome to the API for animal adoption. Learn how to connect
adoptable pets with potential families by integrating pet
adoption data into apps, websites, and services.

## Overview

Get familiar with the fundamentals and core concepts
in the [PawFinder API Overview](./docs/overview/overview.md). Learn more
about pets, shelters, adoption status, and search filters. Discover
how different development audiences use the API.

## Developer environment setup

Install all [tutorial requirements](./docs/overview/tutorial-requirements.md)
before proceeding to the tutorials.

## Quickstart

Get up and running in the [Quickstart](./docs/tutorials/quickstart.md), _coming soon_. \
View a real JSON example with field-by-field annotations.
Make a `GET` request to `/pets`.

## Tutorials

Tour task-based guides for common workflows and use cases.

- [Find the perfect pet](./docs/tutorials/find-perfect-pet.md)\
  Filter pets by species, breed, shelter, and other criteria.

- [Get Shelter Information](tutorials/get-shelter-information.md,), _coming soon_ \
  Retrieve shelter directory listings and availability data.

- [Track Adoption Status](tutorials/track-adoption-status.md), _coming soon_ \
  Follow pet availability and adoption status in real-time.

- [Build a Location-Based Search](tutorials/location-based-search.md), _coming soon_ \
  Apply proximity filtering and distance calculations.

- [Handle Pagination](tutorials/handle-pagination.md), _coming soon_ \
  Work efficiently with large result sets and pagination controls.

## API Reference

Survey [the complete technical](./docs/api-reference/api-index.md) reference
for all endpoint operations, parameters, and responses.

### `/pets`

- [GET /pets/](./docs/api-reference/get-all-pets.md) \
  Search and filter available pets with different criteria.

- [GET /pets/{id}](./docs/api-reference/get-pets-by-id.md) \
  Retrieve detailed information for a specific pet.

- [GET /pets/{id}/status](./docs/api-reference/get-pets-with-filters.md) \
  Check current adoption status and availability.

### `/shelters`

- [GET /shelters](./docs/api-reference/get-all-shelters.md) \
  List all participating shelters with filtering options.

- [GET /shelters/{id}](./docs/api-reference/get-shelters-by-id.md) \
  Get detailed shelter information and contact details.

- [GET /shelters/{id}/pets](./docs/api-reference/get-pets-from-shelter.md) \
  Retrieve all pets currently available at a specific shelter.

## Authentication guide

Learn how to create API keys for write operations in the [Authentication guide](./docs/overview/authentication-guide.md).

## Get help

- Check real-time API status at [status.pawfinder.com](status.pawfinder.com)
- Found an error or have a suggestion?
[Report it here](https://github.com/rhyannonjoy/pawfinder-service/issues).
- Need help integrating? [Contact support@pawfinder.com](support@pawfinder.com)
