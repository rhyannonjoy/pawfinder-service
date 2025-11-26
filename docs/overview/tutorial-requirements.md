---
layout: page
title: Tutorial Requirements
permalink: /docs/overview/tutorial-requirements/
---

## Tutorial requirements

Complete these steps to prepare for the PawFinder API tutorials.\
_Estimated preparation ~20 minutes._

### Development environment setup

The following are tutorial prerequisites. Open the links in
separate browser tabs before installing any software.

<!-- vale Google.Acronyms = NO -->

- A [GitHub account](https://github.com)
- A development system running a current version or a long-term support,
also known as _LTS_, version of the Windows, MacOS, or Linux operating system.
- The following software:
    - [Git, command line](https://docs.github.com/en/get-started/quickstart/set-up-git)
    - [GitHub Desktop](https://desktop.github.com) _optional, but recommended_
    - A fork of the [PawFinder Service repository](https://github.com/rhyannonjoy/pawfinder-service)
    - A current or LTS version of [node.js](https://nodejs.org/en/download)
    - Version 0.17.4 of [json-server](https://www.npmjs.com/package/json-server)
    - A current copy of _pawfinder-db-source.json_; get this by syncing the fork.
    - [Postman desktop app](https://www.postman.com/downloads/)
        - Running PawFinder Service in a development system with
          an `http://localhost` host name isn't compatible with
          the web-version of Postman.
  
    **Tip**: while using a fork of the repository, create a working
    branch in which to complete the tutorials. Create a new branch for
    each tutorial to prevent a mistake in one from affecting any
    work in another.

<!-- vale Google.Acronyms = YES -->

### Verify the development setup

1. Create and checkout a test branch of the fork of the PawFinder Service repository.
`GitHub repository workspace` is the directory that contains the fork of
the `pawfinder-service` repository.

    ```bash
    cd <GitHub repository workspace>
    ls
    # (see the pawfinder-service directory in the list)
    cd pawfinder-service
    git checkout -b tutorial-test
    cd api
    json-server -w pawfinder-db-source.json
    ```

    If the installation succeeded, the service should start
    and display the URL of the service: `http://localhost:3000`.

2. Make a test call to the service:

    ```bash
    curl http://localhost:3000/pets
    ```

3. If the service is running correctly it retrieves a list of pets, for example:

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
          "status": "available",
          "intake_date": "2025-07-20",
          "id": 2
        },
        ...
    ```

### Troubleshooting

When encountering errors in any procedure steps, investigate,
and correct the error before moving forward. Common situations
that cause errors:

- Mistyped commands
- Running the service from the wrong directory
- Required software component didn't install correctly
- Required software component isn't up to date

If the service correctly retrieves a list of pet profiles, move on
to the [Quickstart Guide](../tutorials/quickstart-guide.md).
