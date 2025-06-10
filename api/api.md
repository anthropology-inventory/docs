# Anthropology Inventory API Setup

This document will cover the setup of a development environment for the Anthropology Inventory Management software's API server.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Testing with Postman](#testing-with-postman)

## Introduction

The Anthropology Inventory Management software's API server is the bridge between the frontend and the database. It processes all requests and routes them accordingly. The diagram below illustrates where the API fits into the Anthropology Inventory Management software as a whole.

![System Architecture](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749503690/Screenshot_2025-06-09_141422_iidtie.png)

## Prerequisites

This document assumes that you have already installed and are familiar with using the following programs / software 

- Node.js
- Node Package Manager
- Postman

Additionally, you must be in contact with a repository maintainer for access to required environment variables & user accounts.

## Project Setup

First, clone the [api](https://github.com/anthropology-inventory/api) repository to your local computer and open it in your IDE of choice. Next, open a terminal, navigate to the project root and run the following command:

`npm install`

This will install the required packages and dependencies for the api server to function. After the packages finish installing, create a new file named `.env` in the root of the project folder. Your project should structure should mirror the following image:

![Directory Structure](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749513802/image_xfenk3.png)

Open the .env file and add the following variables:

```
PORT=3001

MONGO_URI=<your_connection_string>

JWT_SECRET=<jwt_secret>

CLOUDINARY_CLOUD_NAME=<cloud_name>

CLOUDINARY_API_KEY=<api_key>

CLOUDINARY_API_SECRET=<api_secret>
```

Fill in the rest with the values you obtained from a repository maintainer.

After setting your environment variables, go back to your terminal and run:

`npm run dev`

If you set the variables correctly, then you should see the following messages in the terminal:

![successful-api-setup](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749514472/image_1_fmwllg.png)

## Testing with Postman

To test out the db connection, open up Postman and make a GET request to:

`localhost:3001/api/specimens/`

You should see a 403 error and the following message:

![sample-get-request](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749515014/image_3_lmqqjb.png)

This error occurred because the API has all routes (minus login) secured with json web tokens (JWT). To get around this, you will need to "login" with a set of valid credentials. You can obtain these credentials from a repository maintainer.

Create a new POST request to:

`localhost:3001/api/login/`

And include the following in the body of the request:

```
{
    "email": "<your_email>",
    "password": "<your_password>"
}
```

![login-post-request](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749516055/image_4_qom2pc.png)

If there is an issue with your credentials, the server will let you know. Upon successfully logging in, you will receive a response containing the user id and a token that you can use to authorize requests.

![successful-login](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749516193/image_5_pw9kpt.png)

Once you have successfully "logged in" and generated a valid token, go back to your GET request and click on the "Authorization" tab in between the "Params" and "Headers" tabs.
From the "Auth Type" dropdown, select "Bearer Token" and paste the token you generated earlier into the "Token" field.

![setting-token](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749516255/image_6_lkvpbd.png)

Once you have set your token, try sending the GET request again. This time it should succeed.

![successful-get-request](https://res.cloudinary.com/dmwuiz3ad/image/upload/v1749516319/image_7_j63m0i.png)

These tokens expire after 24 hours, so remember to regenerate them periodically. You will need to set this token across all requests you wish to make in postman.

If you have successfully make a request to the API using a valid token, then you have completed the setup.
