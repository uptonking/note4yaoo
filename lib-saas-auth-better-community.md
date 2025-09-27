---
title: lib-saas-auth-better-community
tags: [better-auth, community]
created: 2025-09-24T14:52:48.413Z
modified: 2025-09-24T14:53:03.421Z
---

# lib-saas-auth-better-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [OAuth login without database and Sign-up? · better-auth/better-auth _202503](https://github.com/better-auth/better-auth/discussions/1934)
- sure with the generic OAuth plugin

# discuss-roadmap
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Map additional fields by using mapProfileToUser in OAuth _202507](https://github.com/better-auth/better-auth/discussions/3290)
  - I am using better-auth with a self-hosted keycloak oauth provider. I need to map roles that defined in keycloak to the user object.

- ## [getting error while setting microsoft sso _202509](https://github.com/better-auth/better-auth/discussions/4473)

- 🌰 [How to share login state and accounts across multiple apps using the same Better Auth server (like Google/YouTube)? _202507](https://github.com/better-auth/better-auth/discussions/3505)

- I turned my main app (myauthserver) into an IdP using the OIDC Provider plugin .

- ## [Admin plugin: allow to override built-in access control _202507](https://github.com/better-auth/better-auth/issues/3270)
  - Currently, the admin plugin enforces its built-in RBAC-like access control model. 
  - In our project, it's not enough - we are using Casbin. It would be nice if we could integrate Casbin with the admin plugin.

- Custom hasPermission isAdmin implementation.

- [Admin and Organization plugins Attribute Based Access Control _202504](https://github.com/better-auth/better-auth/issues/2167)
  - I have a use case where I want to enable ABAC, and I think it can be done in better-auth, but it seems the library focuses too strongly on RBAC.

- [Dynamic Roles and Permissions  _202505](https://github.com/better-auth/better-auth/issues/2743)
  - Currently, better-auth only supports hardcoded roles in the codebase, which makes it impossible to manage access control dynamically without deploying code changes or when the permissions and roles are not already known beforehand.
- It seems like a good idea, but with dynamic roles, wouldn’t we lose the benefits of TypeScript?
  - there is no type safety in any RBAC system where there is dynamic control. Unless the values are predefined. Or unless they are generated or handled manually. Kind of like prisma generate
  - Since this feature was added in version 1.3.8, we can close this issue.
# discuss-internlas
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## [Better Auth, by a self-taught Ethiopian(埃塞俄比亚人, 黑人) dev, raises $5M from Peak XV, YC | Hacker News _202506](https://news.ycombinator.com/item?id=44380185)
- RPC-like TypeScript client that you also get for free is so good I don’t know how I could live without that.

- Why does a JavaScript auth library have to raise five million?
  - Because the author of this library is an ambitious startup founder and would like to grow his tool into a business.

- I remember how basically better auth got a huge lead because lucia was shutdown by its dev for their own reasons which I admittedly have forgotten but they made sense and the community had accepted it.
  - This is why I love Lucia. They took the "teach a man to fish" route when they converted to a docs only approach. Now I've got my own auth system and understand a lot more about security.
  - And you don't get surprise updates that trigger a cascading dependency hell.

- Lucia has been converted into a kind of tutorial, which is another way of saying the author is going to college now and is busy or interested in other things.

- I hope they will also develop a self-hosted standalone service/node which hosts accounts and can support JWTs which I could verify on my own servers so the BetterAuth node would issue JWTs signed with a secret key I provided as an ENV var, then I could verify the JWTs on my own servers. This would be a neat decoupling. Could be offered as a SaaS service as well.
  - I'm in the auth space. It's usually best to verify JWTs using an asymmetric keypair, that way the BetterAuth node can sign the JWT, and your servers can use something like JWKS to get the public key.

- I didn't like the fact that it doesn't have a built-in sign-in ui components, but glady https://github.com/daveyplate/better-auth-ui solves it.

- Kratos and Better Auth are almost orthogonal to one another. Kratos provides a comprehensive back end, but no front end at all - you have to write it yourself.
  - Better Auth is mostly focused on the front end.
  - You could use the two together, although I haven't seen anyone do that.
  - I have wasted so much time on third-party authentication frameworks like Ory Kratos that I wish we'd just written our own internal auth library. With Kratos we ended up customising it so heavily we could have just written our own. Same goes for ones that provided a frontend such as Keycloak.

- > And what would the projected revenue stream be?
  -  Basically open-core and hosting.

- The killer feature is that it's embeddable into your app. You don't have to host anything besides your app and your app's database.

- Another reason to use Firebase is because they can provide a lot the advanced security (e.g. blacklists for 2FA phone numbers/emails coming from an algorthm whose innards are only known to Google).

- 🐛 Better Auth is brilliant! My only criticism is that it's too tightly coupled with Kysely.

- The fact that better-auth doesn't come with barebone dashboard is criminal.

- If Better Auth came with a simple builtin email implementation (i.e. just plug in SMTP credentials), I’d consider it perfect. (I’m not sold on Resend!)
  - Agreed that a builtin dashboard would be nice, but it’s not necessary by any means – you’ll still be building your own dashboard around your ORM models, which is of course what Better Auth uses, too.
  - But if you’re looking for something more like Clerk, maybe try Logto or Authentik?

- supertokens did the same thing from bengaluru. didn’t start loud. just showed up with clean abstractions that didn’t leak. you could tell someone had wrestled with real auth mess before touching a single line. it worked, across teams, stacks, workflows
  - better auth gives off the same shape. that gets well adopted because it survives scaling without needing a rewrite same pattern and diff origin place. someone holding the whole stack in their head long enough to ship something
- Too bad that the Supertokens docs became an absolute dumpster fire with their "recipes" and reading the source made me lose confidence in the product's quality to rely on.
  - Not saying better-auth is strictly better, but at least you can read the docs and know what you're getting into yourself instead of 12 variations of the same thing

- 
- 
- 
- 

- ## [Show HN: Comprehensive authentication library for TypeScript | Hacker News _202409](https://news.ycombinator.com/item?id=41678652)
- With direct dependencies on Node.js modules, you outright prevent using other runtimes like Cloudflare workers, Deno, etc.
  - Node has decent support for WebCrypto, for example, which renders all usages of node:crypto obsolete.
- The only place where "node" is necessary is for password hashing, and as there’s no cryptographically secure way to hash passwords on CF Workers or other edge runtimes it's not really an option. 

- The problem with those packages that are "all inclusive" is that you end up depending on a very large number of third party packages, even if your use case probably doesn't require it

- Likely the most comprehensive library lacking JWT support.
  - I was wondering about this too. The project explicitly states it as a non-goal, which seems odd to me as I haven't dealt with a REST api that was session based in a decade. Pretty much everything is JWT based

- JWT-Based Authentication: We won’t support JWT-based auth unless provided by a third-party plugin.
  - I don’t think a single library should support two fundamentally different session methods—it adds unnecessary complexity, especially with the plugin ecosystem. That said, I could see it being added as a plugin if there’s a real need.

- i dislike auth libraries directly messing up with db forcing particular table schema on apps but i keep seeing it in most auth libraries in typescript/js ecosystem.
  - It isn't uncommon to keep auth in a separate DB from the rest of your application. Your application shouldn't care about the schema of anything auth related, other than how you match an authenticated session to an application identity.
