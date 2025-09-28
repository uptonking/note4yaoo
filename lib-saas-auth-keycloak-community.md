---
title: lib-saas-auth-keycloak-community
tags: [community, keycloak]
created: 2025-09-28T16:27:24.192Z
modified: 2025-09-28T16:27:34.679Z
---

# lib-saas-auth-keycloak-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 
# discuss-changelog
- ## 

- ## 

- ## 

- ## [Remove KEYCLOAK_ADMIN, KEYCLOAK_ADMIN_PASSWORD, and the associated system properties. · Issue · keycloak/keycloak _202407](https://github.com/keycloak/keycloak/issues/31229)
  - [Add a deprecation warning when old `KEYCLOAK_ADMIN` , `KEYCLOAK_ADMIN_PASSWORD` env vars are used ](https://github.com/keycloak/keycloak/issues/31491)

- [Upgrading Guide](https://www.keycloak.org/docs/latest/upgrading/index.html)
  - Consequently, the environment variables `KEYCLOAK_ADMIN` and `KEYCLOAK_ADMIN_PASSWORD` have been deprecated. 
  - You should use `KC_BOOTSTRAP_ADMIN_USERNAME` and `KC_BOOTSTRAP_ADMIN_PASSWORD` instead. 
# discuss-internals
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 🤔 [Setting hostname-admin=localhost redirects to keycloak.example.com · Issue · keycloak/keycloak _202207](https://github.com/keycloak/keycloak/issues/13063)
  - I have configured `keycloak.conf` with `hostname=keycloak.example.com` and `hostname-admin=localhost` .
  - In the browser I load http://localhost:8080 and the welcome page loads.
  - The link to the Administration Console is http://localhost:8080/admin/.
  - When I click the link, I end up being redirected to keycloak.example.com and the page shows Invalid parameter: redirect_uri.

- Please consider looking the latest releases as we did some improvements to the hostname configuration.

- 202407: I'd suggest opening a new issue for this. We rewrote the whole Hostname provider in Keycloak 25, the issue might not be present there anymore.
