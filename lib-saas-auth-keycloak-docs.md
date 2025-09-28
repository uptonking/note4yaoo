---
title: lib-saas-auth-keycloak-docs
tags: [auth, docs, keycloak]
created: 2025-09-28T16:26:48.732Z
modified: 2025-09-28T16:27:19.954Z
---

# lib-saas-auth-keycloak-docs

# guide

# overview
- Keycloak exposes several endpoints, each with a different purpose. We recognize 3 main endpoint groups:
- Frontend
  - Users and applications use the frontend URL to access Keycloak through a front channel. 
  - For example browser-based flows (accessing the login page, clicking on the link to reset a password or binding the tokens) can be considered as frontchannel requests.
  - bin/kc.[sh|bat] start --hostname my.keycloak.org
- Backend
  - The backend endpoints are related to direct backend communication between Keycloak and a client (an application secured by Keycloak). 
  - Such communication might be over a local network, avoiding a reverse proxy. 
  - Examples of the endpoints that belong to this group are the authorization endpoint, token and token introspection endpoint, userinfo endpoint, JWKS URI endpoint, etc.
  - The default value of `hostname-backchannel-dynamic` option is false, which means that the backchannel URLs are same as the frontchannel URLs.
  - Dynamic resolution of backchannel URLs from incoming request headers can be enabled by setting to true
  - bin/kc.[sh|bat] start --hostname https://my.keycloak.org --hostname-backchannel-dynamic true
- Administration
  - Similarly to the base frontend URL, you can also set the base URL for resources and endpoints of the administration console. 
  - This URL is used for redirect URLs, loading resources (CSS, JS), Administration REST API etc. 
  - It can be done by setting the `hostname-admin` option
  - bin/kc.[sh|bat] start --hostname https://my.keycloak.org --hostname-admin https://admin.my.keycloak.org:8443

- URLs can be resolved in several ways: they can be dynamically generated, hardcoded, or a combination of both
- Dynamic from an incoming request:
  - Host header, scheme, server port, context path
  - Proxy-set headers: Forwarded and X-Forwarded-*
- Hardcoded:
  - Server-wide config (e.g hostname, hostname-admin, etc.)
  - Realm configuration for frontend URL

- A realm manages a set of users, credentials, roles, and groups. 
  - A user belongs to and logs into a realm. 
  - Realms are isolated from one another and can only manage and authenticate the users that they control.
- In the Admin Console, two types of realms exist:
  - Master realm - This realm was created for you when you first started Keycloak. It contains the administrator account you created at the first login. Use the master realm only to create and manage the realms in your system.
  - Other realms - These realms are created by the administrator in the master realm. In these realms, administrators manage the users in your organization and the applications they need. The applications are owned by the users.

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
- [Configuring the hostname (v2) - Keycloak](https://www.keycloak.org/server/hostname)
- By default, Keycloak mandates the configuration of the `hostname` option and does not dynamically resolve URLs. This is a security measure.
  - If the hostname was dynamically interpreted from a hostname header, it could provide a potential attacker with an opportunity to manipulate a URL in the email, redirect a user to the attacker’s fake domain, and steal sensitive data such as action tokens, passwords, etc.
  - By explicitly setting the hostname option, we avoid a situation where tokens could be issued by a fraudulent issuer.
  - 实测设置--hostname后访问keycloak主页会自动跳转到设置的地址

- When a proxy is forwarding http or reencrypted TLS requests, the `proxy-headers` option should be set. 
  - Depending on the hostname settings, some or all of the URL, may be dynamically determined.

- 
- 
- 
- 
- 
- 
- 
- 
- 

- [Server Developer Guide](https://www.keycloak.org/docs/latest/server_development/index.html)
- Keycloak comes with a fully functional Admin REST API with all features provided by the Admin Console.
- To invoke the API you need to obtain an access token with the appropriate permissions. 
- 
- 
- 
- 
- 

- [Authorization Services Guide](https://www.keycloak.org/docs/latest/authorization_services/index.html)
- Keycloak supports fine-grained authorization policies and is able to combine different access control mechanisms such as: RBAC/ABAC/rule-based
- Keycloak is based on a set of administrative UIs and a RESTful API, and provides the necessary means to create permissions for your protected resources and scopes, associate those permissions with authorization policies, and enforce authorization decisions in your applications and services.
# more
