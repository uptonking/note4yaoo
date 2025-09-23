---
title: lib-saas-authentik-community
tags: [auth, authentik, community, rbac]
created: 2025-09-23T13:08:13.557Z
modified: 2025-09-23T13:08:29.044Z
---

# lib-saas-authentik-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-issues
- ## 

- ## 

- ## [Missing CORS header: Cannot perform an API request - can I configure allowed origins? · Issue · goauthentik/authentik _202411](https://github.com/goauthentik/authentik/issues/12159)
- CORS headers are not currently configurable in authentik, they can be added using the reverse proxy you are using

- [Getting the cors policy: no 'access-control-allow-origin' header is present on the requested resource error. · Issue · authts/react-oidc-context](https://github.com/authts/react-oidc-context/issues/460)
  - You probably need to whitelist your application domain name on your authz server.

- ## [application/o/authorize endpoint missing CORS headers · Issue #10057 · goauthentik/authentik](https://github.com/goauthentik/authentik/issues/10057)
- I'm using traefik as forward proxy and solved this issue by setting the Content-Security-Policy Header of authentik

- [`userinfo` endpoint missing CORS headers · Issue · goauthentik/authentik _202209](https://github.com/goauthentik/authentik/issues/3565)
  - There are already some CORS headers that are being set on the userinfo endpoint
# discuss
- ## 

- ## 

- ## 

- ## 💡 [Documentation about invitations not telling to add invitation stage to enrollment flow · Issue · goauthentik/authentik _202405](https://github.com/goauthentik/authentik/issues/9719)
- after importing the flows-enrollment-2-stage.yaml file
  - in Flows and Stages --> Stages --> Create --> Select Invitation Stage and give it an appropriate name.
  - go to Flows and Stages --> Flow section, and click on default-enrollment-flow to edit the recently imported flow
  - go to Stage Bindings --> Bind Existing Stage and in the Stage field open the dropdown and click on invitation order: 0 and click on Create button

- ## [How does authentik work on services that already have a login screen? : r/selfhosted _202410](https://www.reddit.com/r/selfhosted/comments/1ge1hqq/how_does_authentik_work_on_services_that_already/)
- you either disable login (for apps that just have 1 user) and use the proxy service or you use oauth or ldap in the case of jellyfin to login. Some services dont support either so you cant do anything about it
- 3rd option is to integrate Authentik in the proxy manager. If a non-authorized user tries to access the URL of the service, they only see the Login-Screen of Authentik, after successfull authorization, they get forwarded to the desired service where they see the service's login screen.
  - That's how I do it with Authelia, so that's probably also possible with Authentik. The downsides are: only works in webbrowsers not apps, double login (Auth-Service + desired service)

- If the service does not offer OIDC/oauth/ldap/saml, you can use reverse proxy auth, this will work with anything and makes use of the reverse proxy in between.

- if service has OIDC support, excellent.
  - If not it's possible to configure proxy auth, but then in such cases there might be double login screens, one for Authentik one for service it self.

- ## [Is Authentik that resource heavy? : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1iungyc/is_authentik_that_resource_heavy/)
  - Authentik's documentation states minimum is 2 CPU's and 2GB RAM for a docker install.

- Not really. A lightly used instance should consume around 800 MB normally.

- Running authentik + vaultwarden on a vm on Raspberry Pi 5 currently with 1.5gb allocated and its using not even that fully

- ## [Shoutout to Authentik, making free, enterprise features even losing money, because people asked for it. You have my loyalty and wallet. : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kclfnh/shoutout_to_authentik_making_free_enterprise/)
  - RDP, VNC, SSH

- Authentik is awesome been using it for a minute never had an issue and it’s easy to roll oauth on apps that you self host.
  - Authentik will even do http basic auth

- I use it on all of my public facing apps. Single sign on with 1Password is amazing.

- I've been using the RAC feature since they added it to the free version. Works great. Authentik is great. Don't have to rollout a different RAC solution now.

- What do homelabers use RAC for?
  - If you have a Mac Mini server, it allows your friends to start a build with Xcode remotely for example.
  - You can remotely control any server with a VNC server on it without sending VNC passwords or having to make these servers available on the public internet

- Wait so does this mean that I'll be able to use Authentik for everything I was using Apache Guacamole for?
  - Yes, thats why its so Awesome

- So using this with SSH is basically the same as using a cloudflare tunnel?
  - no. you sign into authentik and it signs in to ssh/etc for you

- Many apps have their own login implementation and don’t support Oauth or other bring your own auth solution. Can Authentik somehow replace all those individual logins or is it on a case by case basis?
  - The the app has to support oidc, oauth2 or ldap standards, If the app doesn't have support authentik can still lock access to it, to your authenticated users only.

- For apps that don't support any SSO type logins, you can use your reverse proxy to force a login through Authentik prior to accessing the app. You can then disable the login on the app. You would then only have the single login through Authentik to access your app.
  - If you can't disable the built in login of the app, then you would have to log in twice. Once, to get through Authentik, then again to get into the app.

- ## [Introducing authentik - an SSO Provider focused on ease of use and flexibility : r/selfhosted _202104](https://www.reddit.com/r/selfhosted/comments/mrbntm/introducing_authentik_an_sso_provider_focused_on/)
  - A quick overview why authentik compared to Keycloak or Authelia:
  - Simple user interface, unlike keycloak's massive forms
  - Full OAuth and SAML provider support, unlike authelia (yet)
  - Support for applications which don't support SSO through a modified version of oauth2_proxy, which is managed by authentik
  - Ability to do custom logic in policies via Python

- is postgres a strict requirement? sqlite has good performance unless your deployment goes really big
  - Whilst in theory it would be very possible, SQLite would cause issues just because there are two containers accessing the database. Capacity wise I don't think postgres makes much of a difference, using ~70 MB RAM.
