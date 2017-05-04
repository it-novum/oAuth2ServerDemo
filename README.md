oauth2 provider example
===

This example shows a provider which grants tokens in exchange for codes for

  * The client application
  * A user of the client application

Install
===

```bash
git clone https://github.com/ojwiya/oAuth2ServerDemo.git
pushd oauth2orize-demo
npm install
```

Usage
===

```bash
node server.js
```

Visit <http://localhost:3001/login> to see the server running locally.

Provider / Consumer Walkthrough
===

Interacting with this provider directly doesn't showcase it's oauth2 functionality.

1. Visiting `/` takes you to a blank page.
2. `/login` will ask you for credentials.
  * If you login before an oauth request you are taken directly to permission dialog when that request happens
  * Otherwise you will be redirected here and then to the permission dialog
3. `/account` will allow you to see your user details


API
===

Below is a mapping of the API in the context of a passport-strategy

* `/dialog/authorize` is the `authorizationURL`.
* `/oauth/token` is the `tokenURL`
* `/api/userinfo` is a protected resource that requires user permission
* `/api/clientinfo` is a protected resource that requires a token generated from the client's id and secret
* Usage of `scope` is not demonstrated in this example.

The standalone usable resources are

* `GET /` nothing
* `GET /login` lets you login, presented by `/dialog/authorize` if you haven't logged in
* `POST /login` processes the login
* `GET /logout` lets you logout
* `GET /account` lets your view your user info

And then some internal resources that are of no concern for standalone users or consumers

* `POST /dialog/authorize/decision`, processes the allow / deny
