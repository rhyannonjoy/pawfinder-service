# PawFinder API Documentation

Welcome to the API for animal adoption. Learn how to connect
adoptable pets with potential families by integrating pet
adoption data into apps, websites, and services.

## Overview

Get familiar with the fundamentals and core concepts
in the [PawFinder API Overview](overview.md). Learn more about
pets, shelters, adoption status, and search filters. Discover
how different development audiences use the API.

## Authentication guide

Pick-up API keys, receive credentials, and keep up with rate limits
in the [Authentication guide](authentication-guide.md).

## Quick Start

Get up and running in the [Quick Start](quick-start.md).
View a real JSON example with field-by-field annotations.
Make a `GET` request to `/pets`.

## Tutorials

Tour task-based guides for common workflows and use cases.

- [Search for Adoptable Pets](tutorials/search-adoptable-pets.md)  
  Filter pets by species, breed, location, age, and other criteria.

- [Get Shelter Information](tutorials/get-shelter-information.md)  
  Retrieve shelter directory listings and availability data.

- [Track Adoption Status](tutorials/track-adoption-status.md)  
  Follow pet availability and adoption status in real-time.

- [Build a Location-Based Search](tutorials/location-based-search.md)  
  Apply proximity filtering and distance calculations.

- [Handle Pagination](tutorials/handle-pagination.md)  
  Work efficiently with large result sets and pagination controls.

## API Reference

Survey [the complete technical](api-reference.md) reference for
all endpoint operations, parameters, and responses.

### `/pets`

- [GET /pets/](api-reference/pets/get-pets.md)  
  Search and filter available pets with different criteria.

- [GET /pets/{id}](api-reference/pets/get-pet-by-id.md)  
  Retrieve detailed information for a specific pet.

- [GET /pets/{id}/status](api-reference/pets/get-pet-status.md)  
  Check current adoption status and availability.

### `/shelters`

- [GET /shelters](api-reference/shelters/get-shelters.md)  
  List all participating shelters with filtering options.

- [GET /shelters/{id}](api-reference/shelters/get-shelter-by-id.md)  
  Get detailed shelter information and contact details.

- [GET /shelters/{id}/pets](api-reference/shelters/get-shelter-pets.md)  
  Retrieve all pets currently available at a specific shelter.

## Integration

Review supportive documentation for effective API integration.
Examine complete schemas for Pet and Shelter objects in
[Data Models](resources/data-models.md). Check out
API updates, new features, and deprecation notices in the
[Changelog](resources/changelog.md).

## Get help

- API Status: Check real-time API status at [status.pawfinder.com](status.pawfinder.com)
- Documentation Issues: Found an error or have a suggestion? [Report it here](https://github.com/rhyannonjoy/pawfinder-service/issues).
- Technical Support: Need help integrating? [Contact support@pawfinder.com](support@pawfinder.com).
