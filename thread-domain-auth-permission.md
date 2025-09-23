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

- ## [Why use Authentik/Authelia over built in authentication? : r/homelab _202508](https://www.reddit.com/r/homelab/comments/1mfn2k5/why_use_authentikauthelia_over_built_in/)
- Built-in auth means 10 ways to log in. Authentik/Authelia give you one master key—central control, no duplicate logins. Why juggle when you can simplify?

- The benefit of it is it is SSO, single sign on.
- So instead of havin a separate user account for each service, I would just have the account in Authentik and can log into every service which supports SSO?
  - Sort of. You still have an account with each service.
  - Just instead of needing to use a username and password you can just log in with SSO.
  - Like reddit supports login with Google. You still have a reddit account, but you don't have a password, you just login via Google.

- Why: Central user management. Ability to add MFA to services that may not natively support it. Ability to login once and automatically be authenticated across services.
  - And yeah, it either would replace outright, or provide another option to, login to a service.

- In my use case, I have a single login page that protects all my services. Traefik is my reverse proxy and handles all the certificates automatically (setting up and renewing) and Authelia is my middleware.

- A single credential, and centralized RBAC
# discuss-tips/pattern
- ## 

- ## 

- ## 

- ## 
# discuss-auth-client/ui
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Does anyone not like better-auth? : r/nextjs _202507](https://www.reddit.com/r/nextjs/comments/1m3tcg3/does_anyone_not_like_betterauth/)
- I’m the actual maintainer :) We’ll have a lot more people involved soon now that we have some funding to push things forward.

- I wish I could use it without the DB.

- ## [Any drawbacks to using Better-Auth in production? : r/nextjs](https://www.reddit.com/r/nextjs/comments/1mmbfm4/any_drawbacks_to_using_betterauth_in_production/)

- You can't use it if your backend isn't JavaScript. That's about it.

- It’s quite opinionated - even though it’s got a plugin system, multi tenancy was still a bitch to figure out (different users with the same email address)

- ## [Is Better Auth really any better : r/nextjs _202508](https://www.reddit.com/r/nextjs/comments/1mk9219/is_better_auth_really_any_better/)
- Speaking from my limited experience. AuthJS was a hot mess. Even basic things like missing documentation and basic examples not working. For something that was supposed to be the standard back in those days, it was mind-boggling. I straight up gave up on nexjs because of autjs/nextauth.
  - Then sometimes after I tried better auth (still was in early stages), and it was miles better IMO, especially for DX. And I believe its only gotten better and more mature since then.
- Agreed, and also, the 2 parallel version mess (5 beta and 4) is freaking terrible. You may find some doc or smippet that doesnt work because of this, which sucks. I've migrated from Authjs to betterAuth and it was smooth.

- Better Auth is one of the few libraries from my experience that just worked amazing out of the box. Documentation is great and has a good ecosystem of plugins. Highly recommend using it.

- BetterAuth, IMO - which is limited in the Typescript space compared to some of these devs - is by far the best I’ve used.

- I haven't *once* been confused by Better-Auth's documentation. AuthJS was a mess, and Lucia was a bit hard to digest.

- BetterAuth I’d say is an easy second. It’s complex in implementation but the boilerplate and docs made it very easy. And it’s BYO-everything so about as cost efficient as it gets for 2FA, passwordless etc. And the complexity comes in handy in unique situations

- ## [Clerk vs BetterAuth : r/nextjs _202508](https://www.reddit.com/r/nextjs/comments/1mzl34w/clerk_vs_betterauth/)
- You can self host better-auth and keep all your data in the same db as your app, no need for calling separate service with separate db, no need for paying monthly fee just to be able to authenticate your users.

- I like self-hosting (sometimes), but I don't like having a user table in my app DB. I prefer auth being a separate service, which is why I like openauth.
  - I prefer not to store user data in my app's database because it simplifies the overall architecture, it's easier to maintain in the long-term, and reduces the risk of having sensitive information mixed with core app data. Also, it makes it easier to reuse the same auth system across multiple apps or services.
  - There is a reason why most big companies use separate auth services and even pay for third party services.
- You can do it with better-auth, too. You can have your own auth service and use the URL to initiate an auth instance in the other services.

- Clerk is solid. The reason people talk about BetterAuth is control. It lives in your own codebase, works closely with Next js, and avoids vendor lock in. Some folks prefer that approach. If you are happy with Clerk and the pricing works for you, you are not missing much.

- ## [Why does everyone recommend Clerk/Auth0/etc when NextAuth is this easy?? : r/nextjs _202504](https://www.reddit.com/r/nextjs/comments/1k02xki/why_does_everyone_recommend_clerkauth0etc_when/)
- Some companies don't want to manage user data. data breaches, GDPR, etc are big risks if you don't do it right. My company doesn't want to manage user data, so we use a third party for user data and authentication instead.

- Because implementing it covers only 1/4 of the whole auth and authorisation and security concerns. 
  - You still need to handle password recovery, user recovery, mfa, securing data at rest. Also it goes without warranty if you use byo auth. Oh also, scaling.

- It definitely is paid promotion by influencers on youtube and X. Right now better auth has the best dev experience to implement on our own - oAuth, anonymous, user-impersonation, organizations, takes a hour to implement complex workflows too.
  - but the only use case I think it's worth for is B2B products in regulated industries like fintech, where compliance is huge factor, and existing enterprise solutions like auth0 are very expensive. but it's definitely a not worth for b2c or free / freemium apps

- ## [Comparing popular auth solutions for Next.js (Lucia, Next Auth v5, Clerk) : r/nextjs _202409](https://www.reddit.com/r/nextjs/comments/1fea4a6/comparing_popular_auth_solutions_for_nextjs_lucia/)
- supabase auth should be here
  - Have been using Supabase for quite a while but I don’t like the way they didn’t handle deduplicate users. Not the worst DX but love to learn new alternatives out there

- Lucia is the best, you presented it in image as bullshit. It is at perfect sweet point of abstraction level. NextAuth is too black boxy and requires like 30 columns in DB. Lucia requires 5.

- I’ve used both Lucia and next-auth/authjs. I feel like the comparison suggested here is, although true, not entirely fair. Lucia is not a complete solution, it is meant to be a utility API

- ## [Comparing Auth from Supabase, Firebase, Auth.js, Ory, Clerk and others : r/selfhosted _202302](https://www.reddit.com/r/selfhosted/comments/114kufp/comparing_auth_from_supabase_firebase_authjs_ory/)
- Keycloak isn't an auth solution (at least in the way of having app integrations or an SDK), it's an identity manager. It's closer to a self hosted Azure active directory than anything else.

# discuss-solutions
- ## 

- ## 

- ## 

- ## 

- ## [Authentik or Authelia: Attack Surface & Disclosed Vulnerabilities : r/selfhosted _202509](https://www.reddit.com/r/selfhosted/comments/1nbnznf/authentik_or_authelia_attack_surface_disclosed/)
- Since Authelia hasn't undergone an audit you can't really compare them.
  - Looking at Authentik in isolation, it's obviously good that they had the audits and that the vulnerabilities were fixed. 
  - You have to keep in mind that these are identity platforms first and authentication second. If you can, use a hard access check: VPN, SSH, mTLS, or IP whitelists.
  - Secondary measures can also be good: keys in custom HTTP headers, basic auth (enforced by the reverse proxy, not by 3rd party apps), country geo-blocking (whitelisting, not blacklisting!) can be good.

- ## [Authentik, Authelia, Zitadel, PocketID, Caddy/Traefik : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jdg374/authentik_authelia_zitadel_pocketid_caddytraefik/)
  - I do not mind Authentik's RAM usage if I get simplicity. 8 GB of additional RAM is cheaper than another hour spend configuring.

- Authentik's outposts make it compatible with basically anything. It's the gold standard of self-hosting SSO. Since turning into a business, the developer's done the opposite of enshittify it, turning enterprise features into FOSS features.

- I’m running Authelia atm (with lldap as LDAP backend), it’s pretty lightweight, all of the config is yaml-based though (can be an up- or downside depending on your preferences)
  - Authentik is somewhat harder to wrap your head around at the beginning, but is an all-in-one solution with more features than Authelia (supports advanced stuff if you care about stuff like e.g. simple onboarding)
  - PocketID looks like an amazing solution, but keep in mind it only supports passkeys via OIDC, which excludes services like Jellyfin which only really support LDAP

- ## [Authelia/Authentik comparison : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1ije2ag/autheliaauthentik_comparison/)
- If you prefer configuration using yaml then authelia would be better for you, 
  - if you prefer doing stuff via the ui then I think authentik would be better. 
  - That's one thing I've found out when researching both, I use authentik myself because I prefer the UI

- My four Authentik containers hover around 900-1000MB on average. Not too uncommon for complex containers, but not the smallest on my system either. 

- Authentik can do everything Authelia can and has a nice GUI. Seems like an easy win to me. But that's just my 2c.

- ## [Authentik and Authelia does it matter ? : r/selfhosted _202401](https://www.reddit.com/r/selfhosted/comments/191879o/authentik_and_authelia_does_it_matter/)
- Depends on your goals to accomplish.
  - Usually, SSO rollout makes sense if there are many end users accessing services and you want to streamline the onboarding process as well as management of those users. Here, keycloak and authentik are good choices, as they support various protocols to sync and do the auth flows (LDAP, OIDC, SAML etc.).
  - However, to really make use of it you would typically run some form of directory service (Active Directory, LLDAP, Azure AD) to manage your users, which are then using the IdP to proof their identify and access services.
  - Note though, that your proxied services must support SSO too. Otherwise, you just have another auth layer in front of the authentication scheme of the proxied service. So you would authenticate via Authentik/Authelia/Keycloak and then also have to login into the actual application again with new creds as no SSO is supported.
  - If you are the single user of your services, then using the normal username + password logins may be easier then setting up SSO and configuring all corresponding applications for it. Also, as most selfhosted apps do not support SSO.
  - Authelia + LLDAP do not allow for password resets by the users itself. So if you plan to have many users, better use Authentik or Keycloak.
  - I recommend starting with Authelia and see how it runs and works with your setup and apps.

- I use Authentik for my office and home lab authentication. Authentik / Keyclock does have a lot of features when compared to Authelia . Try everything and pick whichever fits your needs .

- Having used both, authentik is better, authelia is easier.

- ## [Authelia vs Authentik : r/selfhosted _202110](https://www.reddit.com/r/selfhosted/comments/q721e9/authelia_vs_authentik/)
- if you like GUI go with authentik, or you don’t mind tinkering with config.yml then authilia is another good choice. My only gripe with Authentik is their documentation that only scratches the surface but it can do a lot more such as bypass, proxying, third-party integration with ReCaptcha, duo security, etc.

- ## [Authelia vs Casdoor : r/selfhosted _202301](https://www.reddit.com/r/selfhosted/comments/10kwn1b/authelia_vs_casdoor/)
- Authentik (using Python) can occupy 700MB of memory (or more) just for idling around while Authelia can use less than 30MB while idling. 
  - And the Authentik documentation is even recommending 2GB to be on the safe side (because you're not always just idling and there's actually some work to do when authenticating). 
  - But you're right, Authelia can use a lot of resources with the file-based user database and Argon2 algorithm when authenticating (which you were probably referring to, I guess).
  - I'm using LLDAP for user management, though (which uses 20MB or so) and using roughly 50MB for the same task where Authentik uses at least 700MB is a significant difference, isn't it?

- Regarding Casdoor, it might be a good idea to use it if you're just quickly prototyping an application. However, if you intend to use it in a production environment, you'll be taking on a significant security risk.
  - As a SCIM, Casdoor offers almost no auditable security features. Furthermore, the developers of this project tend to conceal security issues and quietly patch them instead of handling problems publicly, transparently, and informing users.
  - A real-world example is that prior to version 1.811.0, Casdoor had a security vulnerability that allowed anyone to create users without authorization.
  - The developers' response was to quietly merge a patch and pretend the issue didn't exist. You won't find any disclosure about this vulnerability within the Casdoor project itself. I only became aware of this problem after discovering that "oas.fun" was exploiting this vulnerability to create numerous users on my instance.

- Zitadel, Casdoor and Authentik are all great, and each have their use-cases in my opinion, but among the options Authelia seems to be made for personal servers.
  - Authelia uses LDAP as its backend for users. Or files, but the LDAP backend is the reason I went with Authelia. What I found is that a lot of selfhosted apps still don't support OIDC, let alone SAML which was kind of a weird in-between solution that didn't get much adoption in this space, but LDAP is still quite popular. In particular Jellyfin which has a first-party LDAP plugin.
  - Their docs also provide lots of information on integrations with Gitea, Grafana, Traefik, etc. which are the apps I deployed, so it was perfect to work with.

- Casdoor has lots of hidden feature that you need to ask the team, they are responsive but not quite friendly, and some must go through customer support.
- Authelia is only act as SSO portal, there is no functionality regarding ORG/User management. This is to compare with Zitadel. However, Authelia has crowded community since it's existing for quite a long time.

- ## [Golang Auth Dilemma: Clerk vs SuperTokens vs DIY  : r/golang _202409](https://www.reddit.com/r/golang/comments/1ff8nlz/golang_auth_dilemma_clerk_vs_supertokens_vs_diy/)
- I would consider a proper OIDC auth platform. Personally I’d choose keycloak. It can take a little fiddling with to get a production instance up but once you figure it out, everything just works. 
  - Plus it implements the login on the authorization server vs custom implementation client side which is what clerk and supertokens offer. So if you have multiple clients you don’t need a separate implementation for each client. 

- I’ve tested Supertokens in a side project and I didn’t have a good experience. I’ve tried to use a custom UI at first, but the lack of documentation discouraged me. 
  - I’m testing Zitadel now, and it’s working well so far. They have a SDK for Go and also for React. I like the documentation and all the features they offer, it seems a really complete project. And on top of that they have a self host option well documented, even with more advanced examples like a setup with a reverse proxy. Other aspect is that their SDK’s seems really well written and small (most frontend stuff is a wrapper on top of a OIDC library). When I dig through the Supertokens for React, it seemed really bloated and confuse to me.

- I used clerk in 2 different project both with go backends and react frontends, I have to say it’s pretty nice they have both a simple sdk that’s basically plug and play and a detailed api so you can implant things on your own more deeply. Highly recommend them

- I chose to do a DIY JWT issuer that integrates with our existing LDAP. It uses asymmetric certificates to sign the JWTs that applications can verify. Applications just need to keep a current public cert to verify tokens. The source is at https://github.com/hppr-dev/stoke-auth .
  - The main reason I chose DIY was our existing infrastructure. I had considered keycloak, but I wanted something a bit more streamlined that would make sense being deployed with the application or independently. As for other cloud based solutions, a SaaS product would probably be a hard sell. I do think that DIY takes more work (obviously) but I felt many solutions out there either offer too much or too little.

- ## [Best self hosted authentication solution? : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1eohsds/best_self_hosted_authentication_solution/)
- I had authelia running but it was a nightmare with way too many config file settings, environment variables, and nginx proxy configurations. 

- If resources matter: KanIDM
  - Authelia is not as usability friendly as Authentik, but uses more resources and has less features than KanIDM
  - Keycloak is more complicated than Authentik and uses more resources than KanIDM
  - LLDAP supports LDAP only while KanIDM supports LDAP, OIDC, RADIUS, SSH etc and it even has a user self service UI

- Authelia: Doesn’t really have an UI though.
  - Authelia without UI is easier to use than authenthik with UI

- Happy with authelia here, but there's no admin gui... which to my mind removes a risk, but makes initial setup harder. But like most tool of this ilk, once it's set up you don't really need to touch it

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

- Keycloak, because Authentik just doesn’t support many features that I want to use like Kerberos.

- Tried oidc recently with Authelia (was using it with forward-auth so far), found it pretty easy to implement actually
  - Authentik is certainly simpler and easier to use, authelia is based on a text configuration and it's more work, but straightfoward once you have something to copy and paste for different apps

- Can you use Authentik without reverse proxy, so just locally? I'm not really planning to expose anything.
  - You can use a reverse proxy locally without exposing any ports and even get domain names and ssl certs.

- Authelia but I was finding OIDC too difficult so have Authentik for that. Probably will switch to Authentik completely sometime soon. LDAP backend for both.

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
# discuss-rbac/permissions
- ## 

- ## 

- ## 

- ## [Any recommendations for Open Source RBAC? : r/devops _202501](https://www.reddit.com/r/devops/comments/1hsq81f/any_recommendations_for_open_source_rbac/)
  - Each Role has different permissions (View, Edit, Delete)

- In order of preference
  - OpenFGA
  - OpenPolicyAgent
  - Casbin
  - Roll your own

- As you've seen open source system RBAC systems do exist, but as you've probably also noticed they tend to get complex quickly becuase they are designed a generic solution for every RBAC scenario. Take a moment to decide how fine grained you need to get.
  - If it's just "User with Role X can List resource type Y", roll your own.

- Keycloak has rbac built in no? Its a full AAA solution. Authenticate Authorize Audit.

- Sadly, all the allegedly RBAC libs I found some years ago were either hugely overcomplicated or didn't even support nested roles. It was frustrating. I rolled my own.

- LDAP is a data store. You can define your roles there but it lacks the Access Control part.

- For RBAC implementation, I'd strongly recommend looking into Casbin (https://casbin.org/). 
  - It's a mature, widely-adopted open source authorization library that integrates well with Keycloak and provides exactly what you're looking for out of the box. 
  - It supports fine-grained RBAC with custom permissions, has adapters for multiple databases, and includes a management UI called Casdoor that can save you significant development time. 
  - The learning curve is reasonable, and there's excellent documentation and community support.

- RBAC for what? The app, or for other apps? For your directory? I'm not understanding what you're trying to build RBAC on top of.

- Have you heard of the Ory stack https://ory.sh

- We had a similar problem at my company. Used Keycloak for authentication only, but implemented RBAC in our Postgres database. Tried casbin, but it's not flexible enough.
# discuss
- ## 

- ## 

- ## 

- ## 
