---
title: lib-saas-auth-better-docs
tags: [better-auth, docs]
created: 2025-09-24T14:51:49.248Z
modified: 2025-09-24T14:52:17.131Z
---

# lib-saas-auth-better-docs

# guide

# overview
- Better Auth supports multiple social providers, including Google, GitHub, Apple, Discord, and more

- Email is a key part of Better Auth, required for all users regardless of their authentication method. 
  - Better Auth provides email and password authentication out of the box, and a lot of utilities to help you manage email verification, password reset, and more.

- Better Auth comes with built-in support for OAuth 2.0 and OpenID Connect. 
  - This allows you to authenticate users via popular OAuth providers like Google, Facebook, GitHub, and more.

- Better Auth includes a built-in rate limiter to help manage traffic and prevent abuse. 
  - By default, in production mode, the rate limiter is set to: Window: 60 seconds Max Requests: 100 requests

- Better Auth manages session using a traditional cookie-based session management. 
  - The session is stored in a cookie and is sent to the server on every request. 
  - The server then verifies the session and returns the user data if the session is valid.

- Beyond authenticating users, Better Auth also provides a set of methods to manage users. This includes, updating user information, changing passwords, and more.

- 
- 
- 
- 
- 

# docs
- Once a user is signed in, you'll want to access the user session. Better Auth allows you to easily access the session data from both the server and client sides.
- Client Side `useSession` hook is implemented using nanostore and has support for each supported framework and vanilla client, ensuring that any changes to the session (such as signing out) are immediately reflected in your UI.
- The server provides a `session` object that you can use to access the session data. It requires request headers object to be passed to the `getSession` method.

- When you create a new Better Auth instance, it provides you with an `api` object. This object exposes every endpoint that exists in your Better Auth instance. And you can use this to interact with Better Auth server side.
  - Any endpoint added to Better Auth, whether from plugins or the core, will be accessible through the `api` object.

- Cookies are used to store data such as session tokens, OAuth state, and more. 
  - All cookies are signed using the `secret` key provided in the auth options.
- By default, Better Auth cookies follow the format `${prefix}.${cookie_name}`. The default prefix is `better-auth`. 

- 🛢️[Database | Better Auth](https://www.better-auth.com/docs/concepts/database)

- Better Auth requires a database to store user data. 
  - You can easily configure Better Auth to use SQLite, PostgreSQL, or MySQL, and more
- The database will be used to store data such as users, sessions, and more. 
  - Plugins can also define their own database tables to store data.

- [JWT | Better Auth](https://www.better-auth.com/docs/plugins/jwt)
  - The JWT plugin provides endpoints to retrieve a JWT token and a JWKS endpoint to verify the token.
  - This plugin is not meant as a replacement for the session. 
  - It's meant to be used for services that require JWT tokens. If you're looking to use JWT tokens for authentication, check out the Bearer Plugin.

- 
- 
- 
- 
- 
- 
- 
- 
- 

# more
