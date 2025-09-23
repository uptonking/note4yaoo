---
title: lib-saas-authentik-docs
tags: [authentik, docs]
created: 2025-09-23T13:07:59.781Z
modified: 2025-09-23T13:08:10.325Z
---

# lib-saas-authentik-docs

# guide

# overview
- authentik is an IdP (Identity Provider) and SSO (Single Sign On) platform that is built with security at the forefront of every piece of code
- You can use authentik in an existing environment to add support for new protocols, so introducing authentik to your current tech stack doesn't present re-architecting challenges. 
- We support all of the major providers, such as OAuth2, SAML, LDAP, and SCIM, so you can pick the protocol that you need for each application.

- authentik consists of a few larger components:
  - authentik — the actual application server
  - outpost-proxy — a Go application based on a forked version of oauth2_proxy, which does identity-aware reverse proxying.
  - outpost-ldap — a Go LDAP server that uses the authentik application server as its backend.
  - outpost-radius — a Go RADIUS server that uses the authentik application server as its backend.
  - web — the web frontend, both for administrating and using authentik. It is written in TypeScript using `lit-html` and the PatternFly CSS library.
  - website — the website/documentation, which uses Docusaurus.

- authentik is primarily a Django application running under gunicorn, proxied by a Go application that serves static files.
- authentik is at its very core a Django project. 
  - It consists of many individual Django applications. These applications are intended to separate concerns, and they may share code between each other.
  - This Django project is running in gunicorn, which spawns multiple workers and threads. Gunicorn is run from a lightweight Go application that reverse-proxies the application and handles static files.
  - There are also several background tasks that run in Dramatiq, via the django-dramatiq-postgres package, with some additional helpers in authentik.tasks.

- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 
- 

# docs
- Terminology
- An application links together Policies with a Provider, allowing you to control access. 
  - It also holds Information like UI Name, Icon and more.
- A Provider is a way for other applications to authenticate against authentik. 
  - Common Providers are OpenID Connect (OIDC) and SAML.
- Policy: At a base level a policy is a yes/no gate. 
  - It will either evaluate to True or False depending on the Policy Kind and settings. 
  - For example, a "Group Membership Policy" evaluates to True if the user is member of the specified Group and False if not. 
  - This can be used to conditionally apply Stages, grant/deny access to various objects, and for other custom logic.
- Sources are locations from which users can be added to authentik. 
  - For example, an LDAP Connection to import Users from Active Directory, or an OAuth2 Connection to allow Social Logins.

- Flows are an ordered sequence of stages. 
  - These flows can be used to define how a user authenticates, enrolls, etc.
- A stage represents a single verification or logic step. 
  - They are used to authenticate users, enroll users, and more. 
  - These stages can optionally be applied to a flow via policies.

- Property Mappings allow you to make information available for external applications, and to modify how information from sources are stored in authentik.

- An outpost is a separate component of authentik, which can be deployed anywhere, regardless of the authentik deployment. 
  - The outpost offers services that aren't implemented directly into the authentik core, e.g. Reverse Proxying.

- There are longer-running tasks which authentik runs in the background. 
  - This is used to sync LDAP sources, backup the database, and other various tasks.

- authentik Server consists of two sub-components, the actual core-server itself and the embedded outpost. 
  - Incoming requests to the server container(s) are routed by a lightweight router to either the Core server or the embedded outpost. 
  - This router also handles requests for any static assets such as JavaScript and CSS files.
- The core-server sub-component handles most of authentik's logic, such as API requests, flow executions, any kind of SSO requests, etc.
- Embedded outpost allows using Proxy providers without deploying a separate outpost.
- worker executes background tasks, such as sending emails, the event notification system, and everything you can see on the System Tasks page in the frontend.

- authentik uses PostgreSQL to store all of its configuration and other data (excluding uploaded files).

- authentik uses Redis as a message-queue and a cache. 
  - Data in Redis is not required to be persistent, however you should be aware that restarting Redis will cause the loss of all sessions.

- Events are authentik's built-in logging system. Every event is logged, whether it is initiated by a user or by authentik.

- Service accounts are specialized user accounts designed for machine-to-machine authentication and automation purposes rather than interactive human use. They're ideal for integrating authentik with external systems, APIs, and services.
  - User-created Service Accounts: Created by administrators for integrating with external systems or for automation purposes.
  - Internal Service Accounts: Created and managed automatically by authentik for internal purposes, such as outpost communications. These cannot be created manually.

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
