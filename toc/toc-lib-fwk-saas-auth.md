---
title: toc-lib-fwk-saas-auth
tags: [auth, saas, toc]
created: 2025-09-23T09:27:58.490Z
modified: 2025-09-23T09:28:08.532Z
---

# toc-lib-fwk-saas-auth

# guide
- tips
  - 用户管理的参考方案, 可直接在现有cms的基础上提取部分代码
# popular
- https://github.com/goauthentik/authentik /18.2kStar/MIT+EE/202509/python
  - https://goauthentik.io/
  - open-source Identity Provider (IdP) for modern SSO. 
  - It supports SAML, OAuth2/OIDC, LDAP, RADIUS, and more, designed for self-hosting from small labs to large production clusters.

- https://github.com/keycloak/keycloak /29.7kStar/apache2/202509/java
  - https://www.keycloak.org/
  - Open Source Identity and Access Management solution for modern Applications and Services.
  - Keycloak provides user federation, strong authentication, user management, fine-grained authorization, and more.

- https://github.com/authelia/authelia /25.3kStar/apache2/202509/go
  - https://www.authelia.com/
  - open-source authentication and authorization server providing two-factor authentication and single sign-on (SSO) for your applications via a web portal. 
  - It acts as a companion for reverse proxies by allowing, denying, or redirecting requests.
  - Authelia can be installed as a standalone service from the AUR, APT, FreeBSD Ports, or using a static binary, .deb package, as a container on Docker or Kubernetes.

- https://github.com/casdoor/casdoor /12.3kStar/apache2/202509/go/国人主导
  - https://casdoor.org/
  - open-source UI-first Identity and Access Management (IAM) / Single-Sign-On (SSO) platform with web UI supporting OAuth 2.0, OIDC, SAML, CAS, LDAP, SCIM, WebAuthn, TOTP, MFA and RADIUS

- https://github.com/nextauthjs/next-auth /21.4kStar/ISC/202403/ts
  - https://authjs.dev/
  - a set of open-source packages that are built on Web Standard APIs for authentication in modern applications with any framework on any platform in any JS runtime.
  - Designed to work with any OAuth service, it supports 2.0+, OIDC
  - Built-in support for many popular sign-in services
  - Built-in email/passwordless/magic link authentication
  - Built-in support for MySQL, MariaDB, Postgres, Microsoft SQL Server, MongoDB, SQLite, etc.
  - [database adapters](https://authjs.dev/reference/adapters)
    - 支持sequelize、prisma、drizzle
  - When JSON Web Tokens are used, they are encrypted by default (JWE) with A256CBC-HS512
  - [NextAuth.js is becoming Auth.js_20221215](https://twitter.com/balazsorban44/status/1603082914362986496)
    - Runtime/framework agnostic
  - [Integration with an existing project _202006](https://github.com/nextauthjs/next-auth/issues/296)
    - These are the options that are probably most relevant
  - https://github.com/nextauthjs/next-auth-example
    - Example showing how to use NextAuth.js with Next.js

- https://github.com/logto-io/logto /6.9kStar/MPLv2/202403/ts
  - https://logto.io/
  - https://docs.logto.io/
  - a modern Auth0 alternative for building identity infrastructure with minimal effort
  - offers a comprehensive identity solution covering both the front and backend, complete with pre-built infrastructure
  - OIDC-based authentication and RBAC authorization.
  - Flexible connectors, scalable with community contributions, customizable with SAML, OAuth, and OIDC protocols.
  - Various sign-in options, such as social, email, phone number, and username, including passwordless authentication
  - User management and audit logs help you understand user identity-related information and keep your security on track.
  - https://github.com/logto-io/js
    - The monorepo for SDKs and working samples written in JavaScript (Well, mostly in TypeScript).

- https://github.com/better-auth/better-auth /MIT/202503/ts
  - https://better-auth.com/
  - Better Auth is framework-agnostic authentication (and authorization) library for TypeScript
  - It provides a comprehensive set of features out of the box and includes a plugin ecosystem that simplifies adding advanced functionalities
  - Whether you need 2FA, multi-tenant support, or other complex features.
# examples
- https://github.com/auth0-blog/spa-jwt-authentication-tutorial /201507/js
  - Add authentication to a vanilla js single page app

- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend

- https://github.com/LeeSoMyoung/Express-NodeJS-Auth-with-JWT /202202/js
  - NodeJS, Express, MySQL, Vanilla JS로 구현한 Authentication

- https://github.com/cornflourblue/node-mongo-registration-login-api /202007/js
  - NodeJS + MongoDB API for User Management, Authentication and Registration
  - [NodeJS + MongoDB - Simple API for Authentication, Registration and User Management | Jason Watmore's Blog](https://jasonwatmore.com/post/2018/06/14/nodejs-mongodb-simple-api-for-authentication-registration-and-user-management)
# jwt
- https://github.com/rajeshpillai/node-jwt-step-by-step /202005/js
  - A simple express jwt server with vanilla javascript client for testing
  - backend + frontend

- https://github.com/braitsch/node-login /MIT/202104/js
  - A template for quickly building login systems on top of Node.js & MongoDB

- https://github.com/cornflourblue/node-mongo-registration-login-api /MIT/202007/js
  - NodeJS + MongoDB API for User Management, Authentication and Registration
  - 依赖mongoose、express-jwt、jsonwebtoken、bcryptjs
  - https://github.com/cornflourblue/react-redux-registration-login-example /202008/js
  - https://github.com/cornflourblue/react-redux-jwt-authentication-example /202006/js
- https://github.com/cornflourblue/node-mysql-registration-login-api /MIT/202008/js
  - Node.js + MySQL API for User Management, Authentication and Registration
  - 依赖sequelize6、express-jwt、express-jwt、bcryptjs
# fwk-authentik
- https://github.com/alicrossnet/sso-frontend-app /202409/js/inactive
  - This a Demo app for implementing SSO.
  - [Implementing SSO using Authentik _202407](https://medium.com/@ali.ravian1308/implementing-sso-using-authentik-74a727826c3b)

- https://github.com/authentik-community/sdk-integrations /MIT/202409/python
  - Examples on how to integrate authentik with various SDKs (Oauth2/OpenID, SAML, etc.) in various languages

- https://github.com/OpenRailAssociation/authentik-user-manager
  - Manage users and their groups on Authentik instances by local configuration YAML files

- https://github.com/svetlyopet/authentik-cli /apache2/202508/go
  - CLI tool for managing Authentik in a way that allows multi-tenancy
  - Creates a tenant abstraction with RBAC controls over resources
  - Create, list, update, and delete Authentik resources
  - Designed for scripting & automation (JSON/YAML output)

- https://github.com/patchmonkey/opencloud-authentik-specific-config /202505/yaml
  - My personal configuration for integrating authentik with opencloud 2.3.0 for external OIDC.

- https://github.com/burritosoftware/Outline-Authentik-Connector
  - Syncs groups between Authentik and Outline
  - https://github.com/mnixry/outline-authentik-groupsync

- https://github.com/UltimatumGamer/unleash-sso-authentik
  - Unleash configuration that supports authentik as sso provider

- https://github.com/tagoKoder/idp-auth-flow /202509/go/dart/java
  - Multi-platform OpenID Connect (OIDC) authentication using a single IdP (Authentik).
  - Both the mobile app (Flutter) and the web admin (Angular) share the same login flow.
  - A Go gateway validates issued tokens (multi-issuer support) and communicates with a Spring Boot identity microservice via gRPC to link/upsert users and return a compact profile.
# authentication
- https://github.com/libregraph/lico /51Star/apache2/202507/go
  - LibreGraph Connect implements an OpenID provider (OP) with integrated web login and consent forms.
  - LibreGraph Connect has it origin in Kopano Konnect and is meant as its vendor agnostic successor.
  - Lico can provide user login based on available backends.

- https://github.com/casbin/node-casbin /ts
  - https://casbin.org/
  - An authorization library that supports access control models like ACL, RBAC, ABAC in Node.js and Browser

- https://github.com/stalniy/casl /5.4kStar/MIT/202401/ts
  - https://casl.js.org/
  - CASL is an isomorphic authorization JavaScript library which restricts what resources a given user is allowed to access
  - designed to be incrementally adoptable and can easily scale between a simple claim based and fully featured subject and attribute based authorization.
  - Heavily inspired by cancan(from ruby-on-rails).
  - ⚖️ CASL implements Attribute Based Access Control
  - who is using #casl
    - strapi
  - https://github.com/fratzinger/feathers-casl /ts
    - a convenient layer to use CASL in feathers.js.
    - Fully powered by Feathers 5 & CASL 6
# authorization

# auth-client/ui
- https://github.com/stack-auth/stack-auth /5.9kStar/MIT/202506/ts
  - https://stack-auth.com/
  - Open-source Auth0/Clerk alternative
  - It is developer-friendly and fully open-source (licensed under MIT and AGPL). MIT for the client libraries, AGPL for the serverside
  - Our managed service is completely optional and you can export your user data and self-host, for free, at any time.
  - We support Next.js, React, and JavaScript frontends, along with any backend that can use our REST API. 
  - Authentication components that support OAuth, password credentials, and magic links
  - Multi-tenancy & teams
  - Role-based access control
  - Impersonate(扮演) users for debugging and support, logging into their account as if you were them
  - You can now open the dev launchpad at http://localhost:8100. From there, you can navigate to the dashboard at http://localhost:8101, API on port 8102, demo on port 8103, docs on port 8104, Inbucket (e-mails) on port 8105, and Prisma Studio on port 8106. 
  - [Show HN: Stack, an open-source Clerk/Firebase Auth alternative | Hacker News _202404](https://news.ycombinator.com/item?id=40031090)

- https://github.com/openauthjs/openauthjs /202411/ts
  - openauthjs

- https://github.com/oslo-project/jwt /MIT/202409/ts
  - https://jwt.oslojs.dev/
  - https://oslojs.dev/
  - Oslo is an open-source project that aims to provide high-quality auth packages for server-side JS. 
  - Runtime agnostic. Zero third-party dependencies. Fully typed.
- https://github.com/lucia-auth/lucia /6.8kStar/MIT/202403/ts
  - https://lucia-auth.com/
  - a simple and flexible user and session management library that provides an abstraction layer between your app and your database. 
  - Middleware allows Lucia to read the request and response since these are different across frameworks and runtime
    - 支持express、fastify、nextjs、astro
  - [A database is required for storing your users and sessions](https://lucia-auth.com/database/)
    - 支持mongoose、sqlite、pg、prisma、drizzle-orm、kysely
  - [Future plans · lucia-auth/lucia _20241007](https://github.com/lucia-auth/lucia/discussions/1707)
    - I am planning to deprecate the library early next year. It has become abundantly clear to me that Lucia, in the current state, is not working. 
    - I now implement sessions from scratch and don't use the library for my personal projects.
    - I could make Lucia into something more of a framework, akin to Auth.js. However, they come with their own issues on top of Lucia's, and it should be its own package anyway.
    - https://x.com/pilcrowonpaper/status/1843258855280742481
    - I will continue to maintain all my other projects, including Oslo and Arctic
    - This is exactly what make dev’s lose total trust in small half baked libs.
  - [Lucia 3.0 · Discussion _20240127](https://github.com/lucia-auth/lucia/discussions/1361)
    - Lucia doesn't use JWTs
    - We used to support JWT and it was a broken mess. Token rotation requires additional complexity, you need to sync state in the client, and the added security risks requires you to just do more. Even if it was simple, sessions and JWTs are 2 totally different things and require different db tables. Supporting both with a single library doesn't make any sense.
    - I would prefer a jwt session. Is it possible with Lucia? Any reason why a db approach is used instead?
      - it's beyond the scope of what lucia was initially designed to do (manage sessions), and maintaining the implementation was a mess.
      - Refresh token rotation is really tricky to abstract away in a flexible manner. 
      - And on the other hand, in-memory DB nicely pollyfills all of the benefits of JWT, so it might actually not make a lot of sense to maintain that solution.

- https://github.com/nickredmark/ooth /MIT/201902/ts/archived
  - https://nickredmark.github.io/ooth/
  - a user identity management system for node.js
  - Architecture - A typical scenario has 3 components:
    - The authentication/identity management server
    - A resource API (optional, can be integrated with the auth server or standalone)
    - The client
  - example with a starting UI with all the main user account flow is programmed with next.js. 

- https://github.com/Swizec/useAuth
  - The simplest way to add authentication to your React app.
  - You'll need an account with Auth0 or Netlify Identity and the appropriate access keys.
  - We use XState behind the scenes to manage authentication state for you.
# more
