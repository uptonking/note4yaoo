---
title: lib-saas-auth-keycloak-dev
tags: [dev-xp, keycloak]
created: 2025-09-28T16:27:45.298Z
modified: 2025-09-28T16:28:00.008Z
---

# lib-saas-auth-keycloak-dev

# guide

- pros
  - license: apache2
  - 集成示例非常丰富, github上示例仓库及sdk示例也较多
  - 文档丰富

- cons
  - java tech stack: hibernate, quarkus
  - 配置混乱: hostname, http-port, proxy-headers
    - 但身份认证的反向代理本身就是业界难点，同类技术和产品也存在这个问题

- features
  - No need to deal with storing users or authenticating users.
  - ⚖️ Standard Protocols: Keycloak is based on standard protocols and provides support for OpenID Connect, OAuth 2.0, and SAML.
  - Single-Sign On and logout: Users authenticate with Keycloak rather than individual applications
  - Social Login
  - User Federation: built-in support to connect to existing LDAP or Active Directory servers
  - Admin Console: enable and disable various features, create and manage applications and services
  - Account Management Console: update the profile, change passwords, and setup two-factor authentication
  - Authorization Services: rbac, custom fine-grained authorization services 
  - Login flows - optional user self-registration, recover password, verify email, require password update, etc.
  - Session management - Admins and users themselves can view and manage user sessions.
  - Two-factor Authentication - Support for TOTP/HOTP via Google Authenticator or FreeOTP.
  - CORS support - Client adapters have built-in support for CORS.

- who is using #keycloak
  - lasuite-docs
  - grist
  - opencloud
  - outline
# draft

# dev-xp

- 启动时设置 `--hostname=http://localhost:8083`, 会导致在浏览器打开 http://localhost:8080 时自动跳转到到 http://localhost:8083, 就算8083端口本身未开放url也会从8080自动变为8083
# devops
- [All configuration - Keycloak](https://www.keycloak.org/server/all-config)

- If you wish to expose the Admin Console on a different host, you can do 
  - bin/kc.[sh|bat] start --hostname https://my.keycloak.org --hostname-admin https://admin.my.keycloak.org:8443
  - This allows you to access Keycloak at `https://my.keycloak.org` and the Admin Console at `https://admin.my.keycloak.org:8443`, while the backend continues to use `https://my.keycloak.org`.

- 🤔 Keep in mind that hostname and proxy options do not change the ports on which the server listens. 
  - Instead it changes only the ports of static resources like JavaScript and CSS links, OIDC well-known endpoints, redirect URIs, etc. that will be used in front of the proxy. 
  - You need to use HTTP configuration options to change the actual ports the server is listening on. 

- [Configuring the Management Interface - Keycloak](https://www.keycloak.org/server/management-interface)
  - The management interface provides the possibility to hide endpoints like `/metrics` or `/health` from the outside world 
  - exposed on the default management port `9000`
  - If management interface properties are not explicitly set, their values are automatically inherited from the default HTTP server.
# changelog
- [v25.0.0 _202406](https://www.keycloak.org/2024/06/keycloak-2500-released)
  - Keycloak now supports OpenJDK 21, as we want to stick to the latest LTS OpenJDK
  - Hostname v2 options are supported by default
# more
