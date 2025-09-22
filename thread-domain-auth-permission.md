---
title: thread-domain-auth-permission
tags: [auth, community, permission, solutions]
created: 2025-09-22T13:53:24.806Z
modified: 2025-09-22T13:53:51.831Z
---

# thread-domain-auth-permission

# guide

- features
  - authentication
  - authorization: rbac
  - docker deploy
  - multi-tenancy
  - scaling

- tips
  - 选择成熟方案的优点: 方便搜索已知问题, ai对已有资源更熟练
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-tips/pattern
- ## 

- ## 

- ## 

- ## 
# discuss-solutions
- ## 

- ## 

- ## 

- ## [What SSO to choose? : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jk1v2x/what_sso_to_choose/)
- Authentik free tier allows social login. I have log in with google and other sources on my homelab

- I tried Authentik, but it was too heavy and too complex for usage. I love Authelia since. Very light, efficient and powerful. I recommend.

- The way Authentik handles filtering and policies is pretty awesome because it's basically just Python. Which means you can do silly things with access policies for users, provided you can write the Python script.

- Authelia is really lightweight, but everything is done with config file, and that's quite annoying for me, but it might be worth it 
  - Authentik is more resources intensive (around 1GB of Ram minimum at all time) , but it's not that hard to use, nice UI, and it's a very very powerful tool, you can really customise it a lot 
  - Keycloak and zitadel are more difficult to use, and not as powerful as authentik 
- I love authelia exactly for that. When I have to setup all my services from scratch (for whatever reason) I don't have to go through all the GUI stuff again and everything works as before.
- Zitadel requires manually using webgui or apis to configure environment. Authelia offers a config file

- If you need SAML and full control, go with Keycloak it’s powerful but a bit complex. For something simpler that focuses on modern OIDC use cases, Zitadel is lighter and easier to set up.

- [Should I build a simple Auth service in GO instead of Keycloak/Authentik? : r/golang](https://www.reddit.com/r/golang/comments/1jsqdnq/should_i_build_a_simple_auth_service_in_go/)
  - If you don't need multi-tenancy, try Ory

- ## [Keycloak vs Authentik : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1j04p6x/keycloak_vs_authentik/)
- I have keycloak at home, it was a massive pain to get right and the learning curve was a vertical wall. But it's an enterprise grade solution, I'm so glad I did it.
  - Same here. I used both and settled on Keycloak due to its stability and code maturity. Nothing wrong with Authenik, it just needs more time to polish out to match the maturity of Keycloak.

- I’m using Authelia with Lldap auth and nginx reverse-proxy. Easy to setup, lightweight solution.
  - From authelia.com: "With a compressed container size of less than 20 megabytes and observed memory usage generally below 30 megabytes."
  - My own experience is the same. The configuration is a simple static yaml file that you can easily replicate to additional nodes.
- Mine runs on .05% cpu utilization and 50mb of ram

- Authelia is great they just haven't progressed on their roadmap in over a year, while their competitors and the wider oidc spec have both moved forward.

- My setup currently is with Authelia + file based user configuration (it supports LDAP as well) + Caddy for reverse proxy, it's working great and has a lower memory footprint.

- Authentik is much easier to maintain while still providing all functionality we need. Of course, keycloak can do more, but we simply don’t need that.

- I chose Authentik because it supports passwordless login flows

- Authentik is pretty resource intensive for what it is

- ## [What are people using for authentication in late 2024? : r/selfhosted _202409](https://www.reddit.com/r/selfhosted/comments/1fnn6fp/what_are_people_using_for_authentication_in_late/)
- Can't go wrong with Authentik. SSO, SAML, ODIC, Radius, LDAP. You name it, it does it.
  - It also either works with proxyAuth (nginx/traefik will "ask" authentik if the user is authorized, without everything being proxied through authentik).
  - And- if all else fails, it supports proxy mode, where it will fully proxy the given application, and wrap auth around it.

- I also use authelia. Overall happy with it but it has a fairly slow development and it seems like there’s mostly one guy doing all the work.

- I am using Keycloak as it’s backed by Red Hat, so it gives me some additional assurance of its longevity

- Tried oidc recently with Authelia (was using it with forward-auth so far), found it pretty easy to implement actually
  - Authentik is certainly simpler and easier to use, authelia is based on a text configuration and it's more work, but straightfoward once you have something to copy and paste for different apps

- ## [Keycloak vs. Authentik vs. Authelia, help choose SSO : r/selfhosted _202305](https://www.reddit.com/r/selfhosted/comments/13rr6i7/keycloak_vs_authentik_vs_authelia_help_choose_sso/)
  - Authentik has everything. You're going to find all your apps have spotty/different auth methods, and that's what makes authentik great because it'll adapt to whatever auth. LDAP? Authentik has it. SSO? Authentik has it. None? Authentik will auth via reverse proxy.

- I prefer Authelia because it's just a config file with a bunch of secrets. So much simpler and easier to manage. 
- Something to add: Authelia is significant faster than Authentik.

- I’ve been using Authelia for the better part of 2 years and really really like it. It is definitely not the most beginner friendly without a GUI but the docs are clear and easy to follow.
  - I have nothing against Authentik, but I tried it last year and didn’t think it was robust enough with features. That may have since changed. The UI is really nice.

- I see a lot of votes for Authentik, but as far as i've seen there hasn't been an audit for it?
  - And also what was said today about the issue with LDAP that still isn't fixed, I'm wondering why still a lot of people vote for it
- If you have seen the issues with KeyCloak, you wouldn't like that either.

- I would recommend another one: Casdoor written in Go. 
  - I have used Authelia and it uses a lot more reousrces and Casdoor, which is small but packed with features.

- I got tempted to use casdoor for its nice WebAuthn options, in which authelia is very lacking (non-exists). Just tried my best to run casdoor in docker with sqlite as db driver, it did not work. Documentation did not help much either.

- How much resources does Casdoor use? On the systems that I know Authelia and LLDAP use less than 100 MB RAM alltogether hence I'm curious how much Casdoor might be able to save then.
  - When idle: 0.13 vCPU, 12.66 MiB

- I am using Authentik. I can recommend it. It's complex but I would argue that Keycloak is even more complex and Authelia is not complex enough.

- Keycloak has the upside of being under the stewardship of Red Hat.

- Over the years I have run all three. I started with Authelia. It was good but didn't have many features. I then added Keycloak but it was very difficult to upgrade when new versions came out. Then once Authentik matured I started migrating to it. I do like Keycloak is very light and can run on sqlite where Authentik requires a whole stack. I currently no longer run Authelia. I migrated all Authelia stuff to Authentik. I do still have keycloak because configuring apps for SAML can be very difficult so I haven't gone back to all of them and moved them to Authentik.

- I personally use Authentik backed by FreeIPA. FreeIPA is where I have my canonical set of users/groups and works for stuff that can only use LDAP/Kerberos. Authentik pulls users/groups from FreeIPA for OIDC and proxy auth flows set up in Nginx Proxy Manager.

- ## [Lightweight keycloak alternative : r/selfhosted _202305](https://www.reddit.com/r/selfhosted/comments/13sa28x/lightweight_keycloak_alternative/)
- I'm using Authelia, with https://github.com/lldap/lldap as backend to create and store users.

- authentik 1 user used ~500MB RAM
  - authelia ~30-50MB RAM but no web UI for users to manage their own info
  - casdoor at least 100MB memory
  - ZITADEL consumes around 512MB Ram

- I’ve recently set up Caddy Security (or authp) and was impressed. Much easier to set up than Authelia and does more.

- ## [Open source alternative to Keycloak and Ory for user auth _202110](https://www.reddit.com/r/golang/comments/q3zg70/open_source_alternative_to_keycloak_and_ory_for/)
  - SuperTokens.io recently launched our Go SDK for user auth.
  - https://github.com/supertokens/supertokens-core /202509/java
  - license: apache2 + EE

- Does casbin do Oidc and SSO ?
  - If you want Oidc and SSO, you should consider to use Dex.

- ## [Stateless alternative to Keycloak? : r/selfhosted _202105](https://www.reddit.com/r/selfhosted/comments/n8jhxu/stateless_alternative_to_keycloak/)
  - it seems like Keycloak maintains its own internal in-memory Infinispan cluster, which means the various instances of Keycloak container have to be coordinated together AND since each container stores state, it’s much less feasible to randomly spin up/spin down containers since it’ll cause a large disruption in signouts.

- You can run Keycloak in cluster mode, where the infinispan cache is clustered, allowing for new nodes to join, and leave, the cluster without disruption.

- Authelia uses Redis.
  - Authentik uses Redis and Postgres.

- Authelia by itself cannot work as OIDC provider, which scratches it off my list.
  - Authelia version 4.29.0 added beta support for OIDC 
# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
