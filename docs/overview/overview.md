---
layout: page
title: Overview
permalink: /docs/overview/
---

# PawFinder API Overview

## Introduction

PawFinder is a REST API that connects potential pet adopters with animal shelters
in the greater Dallas-Fort Worth area. This platform aggregates real-time data from
hundreds of shelters, making it easier for people to find their perfect companion
and for shelters to reach qualified adopters. This API enables developers to:

- Search available pets by species, breed, age, location and temperament
- Access detailed shelter profiles and contact information
- Track adoption status updates in real time
- Build custom adoption workflows and notification systems

## Key concepts

### Pets

Each pet in the PawFinder system has a unique identifier and includes standardized
information such as species, breed, age, size, temperament traits, medical history,
and current location. Pets transition through adoption statuses tracked by the API.

### Shelters

Organizations register as shelters to list pets for adoption. Each shelter maintains
a profile with contact information, operating hours, and adoption details. Shelters
can update pet listings and adoption statuses through the API.

### Adoption status

Pets progress through defined status states:

- `available`: ready for adoption inquiries
- `pending`: adoption applications under review
- `adopted`: successfully placed with a family

### Search filters

PawFinder API supports multi-criteria searches including:

- **Species and breed**: cats and dogs only
- **Characteristics**: age range, gender, size, medical information
- **Behavioral Traits**: activity level, "good with kids," "good with other pets"
- **Shelter-specific**: filter by specific shelter

## Development use cases

### For adopters

- Build mobile apps that send push notifications when pets matching user preferences
become available.
- Create location-aware web apps that display nearby adoptable pets.
- Develop pet comparison tools that help users understand different characteristics.

### For shelters

- Integrate PawFinder search into existing shelter websites to increase visibility.
- Automate adoption status updates across many listing platforms.
- Generate analytics reports on inquiry rates and adoption trends.

### For communities

- Build aggregator sites that compare pets across many shelters.
- Create matching algorithms that pair adopters with compatible pets.
- Develop volunteer coordination tools that connect shelter needs with
community support.

## Next steps

- [API Index](../api-reference/api-index.md)
- [Authentication Guide](authentication-guide.md)
- [Quickstart Guide](../tutorials/quickstart-guide.md)
- [Tutorial Requirements](tutorial-requirements.md)
