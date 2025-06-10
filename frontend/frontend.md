# Anthropology Inventory Frontend Setup

This document will cover the setup of a development environment for the Anthropology Inventory Management software's Frontend.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Running in development mode](#running-in-development-mode)
- [Running in production mode](#running-in-production-mode)

## Introduction

The Anthropology Inventory Management software's Frontend is the bridge between end users and the API. It allows authorized users to securely send requests and make changes to the database. The diagram below illustrates where the Frontend fits into the Anthropology Inventory Management software as a whole.

![System Architecture](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749503690/Screenshot_2025-06-09_141422_iidtie.png)

## Prerequisites

This document assumes that you have already installed and are familiar with using the following programs / software 

- Node.js
- Node Package Manager

Additionally, you must be in contact with a repository maintainer for access to required environment variables & user accounts.

## Project Setup

First, clone the [inventory](https://github.com/anthropology-inventory/inventory) repository to your local computer and open it in your IDE of choice. Next, open a terminal, navigate to the project root and run the following command:

`npm install`

This will install the required packages and dependencies for the frontend to function. After the packages finish installing, create two new files named `.env.development` and `.env.production` in the root of the project folder. Your project should structure should mirror the following image:

![Directory Structure](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749516796/image_8_imt10o.png)

Open the `.env.development` file and add the following variable:

`VITE_API_BASE_URI=http://localhost:3001`

Open the `.env.production` file and add the following variable:

`VITE_API_BASE_URI=https://api-849y.onrender.com`

The reason for creating two .env files is to run the frontend using either a locally hosted instance of the API server or the production API server (hosted on render at https://api-849y.onrender.com).

## Running in development mode

To run frontend using the a locally hosted API server, make sure you have successfully set up a local instance of the API server and that the server is running. For instructions on how to do so, please see the [Anthropology Inventory API Setup guide](https://github.com/anthropology-inventory/docs/blob/main/api/api.md).

Open a terminal, navigate to the project root and run the following command:

`npm run dev`

You should see the following output in the terminal if successful:

![successful-frontend-setup](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749517271/image_9_r9plhn.png)

Click on the link to open it in a browser window and navigate to the "Sign In" page

![login](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749520954/image_10_eifexl.png)

Enter a valid set of credentials (can be obtained from a repository maintainer) and click the "Login" button. You should then be automatically redirected to the "Dashboard". If the login fails, then the local server is likely not running.

![dashboard](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749521056/Screenshot_2025-06-09_125141_uik48h.png)

## Running in production mode

To run frontend using the production server, first, visit https://api-849y.onrender.com/ and make sure that the server is up and running.

![server-running](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749521284/Screenshot_2025-06-09_190749_rxniqj.png)

If you see the "Server is running" message, then the server is running.

If it is not running, then you should see something like this:

![server-starting](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749521346/image_12_efimea.png)

Give it a minute or two and it will eventually start up. Once its started up, and run the following command in your IDE instance that is running the frontend: 

`npm run dev -- --mode production`

You should see the same output in the terminal as running in development mode, but this time, the frontend will use the production API. You may or may not have to log in depending on if you have before, but it should behave exactly the same as development mode.

Testing in production mode is good if you are only making changes to the frontend.

If you have made it this far without issue, then you are all set and ready to start contributing to the project!
