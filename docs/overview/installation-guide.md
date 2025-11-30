---
layout: page
title: Installation Guide
permalink: /docs/overview/installation-guide/
---

## Installation guide

Complete these steps to prepare for the PawFinder API tutorials.\
_Estimated preparation ~20 minutes._

### Development environment setup

The following are tutorial prerequisites. Open the links in
separate browser tabs before installing any software.

- A [GitHub account](https://github.com)
- A development system running a current version or a long-term support,
also known as _LTS_, version of the Windows, MacOS, or Linux operating system.
- The following software:
    - [Git, command line](https://docs.github.com/en/get-started/quickstart/set-up-git)
    - [GitHub Desktop](https://desktop.github.com) _optional, but recommended_
    - A fork of the [PawFinder Service repository](https://github.com/rhyannonjoy/pawfinder-service)
    - A current or LTS version of [node.js](https://nodejs.org/en/download)
    - Version 0.17.4 of [json-server](https://www.npmjs.com/package/json-server)
    - [Postman desktop app](https://www.postman.com/downloads/)
        - Running PawFinder Service in a development system with
          an `http://localhost` host name isn't compatible with
          the web-version of Postman.
  
    **Tip**: while using a fork of the repository, create a working
    branch in which to complete the tutorials. Create a new branch for
    each tutorial to prevent a mistake in one from affecting any
    work in another.

### Clone the repository

After forking the PawFinder Service repository, clone it locally.

**Using GitHub Desktop:**

1. Open GitHub Desktop
2. Click **File** > **Clone Repository**
3. Select the **GitHub.com** tab
4. Find the forked `pawfinder-service` repository
5. Choose a local path for the project
6. Click **Clone**

**Using the command line:**

```bash
git clone https://github.com/USERNAME/pawfinder-service.git
cd pawfinder-service
```

After cloning, the repository contains the `pawfinder-db-source.json`
database file in the `api` directory.

### Install dependencies

Navigate to the cloned repository and install the required packages,
which includes `json-server` and other dependencies needed to
run the API locally.

```bash
cd pawfinder-service
npm install
```

### Verify the development setup

#### Step 1: create and checkout a test branch

**Using GitHub Desktop:**

1. Open GitHub Desktop
2. Click the **Current Repository** dropdown in the top-left corner
3. Select `pawfinder-service` from the list
4. Click the **Current Branch** dropdown in the top center, it likely says "main"
5. Click the **New Branch** button
6. In the "Name" field, type: `tutorial-test`
7. Ensure "Create branch based on" shows the main branch
8. Click **Create Branch**

GitHub Desktop automatically switches to the new `tutorial-test` branch.
The Current Branch dropdown should display "tutorial-test."

**Using the command line:**

```bash
cd pawfinder-service
git checkout -b tutorial-test
```

#### Step 2: start `json-server` from the command line

```bash
# Option #1: using npm (recommended)
npm start
```

```bash
# Option #2: using json-server directly
cd api
json-server -w pawfinder-db-source.json
```

#### Step 3: test the service

**Using cURL**

```bash
curl http://localhost:3000/shelters
```

**Using Postman desktop app**

1. Open the Postman desktop app
2. Create a new request
3. Set the method to `GET`
4. Enter the URL: `http://localhost:3000/shelters`
5. Click **Send**
6. Observe the response

If the service is running correctly it retrieves a list of shelters:

```json
[
    {
      "name": "Dallas Animal Services",
      "address": "1818 N Westmoreland Rd, Dallas, TX 75212",
      "phone": "+1-214-671-0249",
      "email": "info@dallasanimalservices.org",
      "hours": "Mon-Sat 11:00-18:00",
      "available_pet_count": 22,
      "adoption_fee_range": "75-200",
      "id": 1
    },
    {
      "name": "Fort Worth Animal Care & Control",
      "address": "4900 Martin St, Fort Worth, TX 76119",
      "phone": "+1-817-392-1234",
      "email": "adopt@fortworthanimalcare.org",
      "hours": "Mon-Fri 11:00-18:00, Sat-Sun 12:00-17:00",
      "available_pet_count": 18,
      "adoption_fee_range": "50-175",
      "id": 2
    },
    ...
]
```

### Troubleshooting

When encountering errors in any of the installation steps,
investigate, and correct the error before moving forward.
Common situations that cause errors:

- Repository not cloned to local machine
- Dependencies not installed, run `npm install`
- Mistyped commands
- Running the service from the wrong directory
- Required software component didn't install correctly
- Required software component isn't up to date
- Port 3000 already in use by another app

If the service correctly retrieves a list of pet profiles,
move on to the [Quickstart Guide](quickstart-guide.md).
