# FusionAuth Node.js example

## 🌠Background

### OAUTH + PKCE

This project is a simple example Node.js application that illustrates how to integrate with FusionAuth's OAuth system using the Authorization Code grant.

This application will use an OAuth Authorization Code workflow and the PKCE extension to log users in. PKCE stands for Proof Key for Code Exchange, and is often pronounced "pixie".

From https://oauth.net/2/pkce/
```text
RFC 7636: Proof Key for Code Exchange
tools.ietf.org/html/rfc7636

PKCE (RFC 7636) is an extension to the Authorization Code flow to prevent several attacks and to be able to securely perform the OAuth exchange from public clients.

It was originally designed to protect mobile apps, but its ability to prevent authorization code injection makes it useful for every OAuth client, even web apps that use a client secret.
```
### NODEJS + EXPRESS
- This project uses Node and Express to power a server side rendered view
	```js
	const express = require('express');
	const router = express.Router();
	```
## 🌠Explanation of important code setup

- This client was built for you by the team at FusionAuth 🔐.
	```js
	const {FusionAuthClient} = require('@fusionauth/typescript-client');
	```

- This is the clientId (AKA, application id).  This identifies the application that you have created and registered using FusionAuth.
- The client secret should be obfuscated (is that not a 100 dollar word!).  Consider using something like `dotenv` or local exports to make sure this is not shared via a VCS like Github.
	```js
	const clientId = 'YOUR CLIENT ID';
	const clientSecret = 'YOUR CLIENT SECRET';
	```

- This creates a new class called 'client' from the previous import.  In this example we are using OAuth2, so `noapikeyneeded` means that we are not authenticating through FusionAuth's equally available API.  
- If you would like to consider this API as an authentication alternative, you can read all about it [here](https://fusionauth.io/docs/v1/tech/apis/)
	```js
	const client = new FusionAuthClient('noapikeyneeded', 'http://localhost:9011');
	```

- As referenced above, this will assist in Authenticating through Oauth2 in this example application.
	```js
	const pkceChallenge = require('pkce-challenge');
	```
## 🌠TL;DR To run 🚀

This assumes you already have a running FusionAuth instance, user and application running locally. If you don't, please see the [5-Minute Setup Guide](https://fusionauth.io/docs/v1/tech/5-minute-setup-guide) to do so.

* :one: update your FusionAuth application to allow a redirect of `http://localhost:3000/oauth-redirect`
* :two: make sure your user has a first name.
* :three: `npm install`
* :four: update `routes/index.js` with the client id and client secret of your FusionAuth application.
* :five: `npm start`

Go to http://localhost:3000/ and login with the previously created user.

You should see 'Hello NAME_OF_PERSON_LOGGED_IN'
