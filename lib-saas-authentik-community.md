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

- ## 🤔 [The redirect_uri is not associated with this application. _202410](https://github.com/reportportal/reportportal/issues/2374)
- 实测github oauth支持测试localhost地址
  - 之前登录失败的callback URL配置为 http://localhost:9000/source/oauth/callback/github, 可正常登录的URL为 http://localhost:9000/source/oauth/callback/github2509, 需要查看idp的配置

- NEXTAUTH_URL= "http://localhost:3000" i found this one in .env file. change this to your original host

- Here you can verify the Homepage URL and the Authorization callback URL which I suspect are set to localhost for you during development. Change them to your hosted domains address.

- The solution was to change an [origin] in the callback URL for http://localhost:3000

- [GitHub OAuth "redirect_uri" is not associated with this application....  - Using Django / Mystery Errors - Django Forum](https://forum.djangoproject.com/t/github-oauth-redirect-uri-is-not-associated-with-this-application/36711)

- [Managing Oauth logins for local testing : r/flask](https://www.reddit.com/r/flask/comments/1ch14bh/managing_oauth_logins_for_local_testing/)
  - Google is a bit of a pain with this. My app also supports GitHub authentication, and they're fine with the app URL set to localhost.
  - You may also want to consider a tunnel that gives your app a public URL to make Google happy. Tailscale can even give you LetsEncrypt-signed certificates for HTTPS without the annoyance of self-signed certificates.

- ## [Duplicate flow inpossible? _202404](https://github.com/goauthentik/authentik/discussions/9422)
  - I need to make another flow same as I have but with a little changes. Is any way I can duplicate the flow or only create new one?

- You can export a flow as a blueprint which is just YAML, and then modify it (currently you'll have to manually adjust/remove all the primary keys) and then re-import it
  - 实测export导出的yaml移除pk后有时无法工作，import源文件yaml可以工作
# discuss-internals
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap/issues
- ## 

- ## 

- ## 

- ## 

- ## [Make branding / customisation of UI more consistent, enhance possibilities _202202](https://github.com/goauthentik/authentik/issues/2364)
  - The branding / customisation of authentik is somewhat inconsistent. While every flow can be branded in some way (wording, background image), a few things like the URL authentik.tld/if/session-end/my-app-name can't, as far as I can see.

- I would love to configure this via Django Templates

- Sorry for the delay. This is indeed a dirty nasty hack. But, FWIW, below is my compose file. The key is to make the server share the same dist directory as the worker instance. It won't work if they don't share a common volume across all instances (in my case I'm using gluster)

- migrate custom CSS to brands

- ## [stages/prompt: Add custom value to RadioButtonGroup and Dropdown  _202304](https://github.com/goauthentik/authentik/issues/5197)
  - we have RadioButtonGroups and Dropdowns in prompts. Sadly we cannot set an internal value.

- The current implementation in the Prompt stage renders dropdown choices where the value and label are identical (${choice}), which doesn't allow for distinct values (e.g., IDs) and display labels (e.g., names) when using dynamic expressions that return a list of tuples or objects like [("1", "Engineering"), ("2", "Marketing")] or [{value: "1", name: "Engineering"}, ...].
  - I'd be happy to propose a fix and submit a PR. The suggested change would update the dropdown rendering to support both value/name pairs, falling back to the current behavior if no value/name structure is provided. 

- ## [Custom Javascript _202402](https://github.com/goauthentik/authentik/issues/8402)
  - I'd like to be able to set different CSS per tenant and sometimes even per flow. I would also like to further customise the functionality of certain things for my specific application.

- If you're looking for a workaround and using kubernetes with the NGiNX ingress, you can do this

- [Custom Development Challenge: Integrating User Management Frontend with Authentik _202311](https://github.com/goauthentik/authentik/issues/7738)
  - I am developing a custom frontend for user management, using Express (Node.js) and Python, designed to integrate seamlessly with Authentik. However, I've encountered an issue related to search queries with pagination and custom attributes, specifically the 'admin_group' attribute.
  - since you are using express/js, I'd recommend using the authentik API client: npmjs.com/package/@goauthentik/api. This should also take care of any kind of encoding for search queries like that

- [Interfaces by BeryJu · Pull Request · goauthentik/authentik _202302](https://github.com/goauthentik/authentik/pull/4748)
  - Add the ability for admins to create custom interfaces with fully custom templates

- ## [Way to add existing user to a group via signup link, similar to Invitation and New User Enrollment with write stage? : r/Authentik](https://www.reddit.com/r/Authentik/comments/1e0gvbn/way_to_add_existing_user_to_a_group_via_signup/)

- ## [Approval User Creation Process : r/Authentik _202407](https://www.reddit.com/r/Authentik/comments/1dxhi8t/approval_user_creation_process/)
  - I'm very new to authentik but I have created a user creation portal so that users can go to my domain and create an account without me sending out an invite.

- Would be also interested into that, how an kind of approval would work. Did you already check out the Prompt Stage? https://docs.goauthentik.io/docs/flow/stages/prompt/ Maybe this could be achived to hand out a secret for the user so that this is handled like an "Approve the user"
  - Yeah that's a decent workaround. How I would view it is that the account gets created but once the process is done the user cannot login until an admin approved the request.

- ## [Self-Registration with Approval : r/Authentik _202502](https://www.reddit.com/r/Authentik/comments/1iq32ux/selfregistration_with_approval/)
- You could leverage python to write a script
  - How would you trigger the script upon account approval?

- ## [Missing CORS header: Cannot perform an API request - can I configure allowed origins? · Issue · goauthentik/authentik _202411](https://github.com/goauthentik/authentik/issues/12159)
- CORS headers are not currently configurable in authentik, they can be added using the reverse proxy you are using

- [Getting the cors policy: no 'access-control-allow-origin' header is present on the requested resource error. · Issue · authts/react-oidc-context](https://github.com/authts/react-oidc-context/issues/460)
  - You probably need to whitelist your application domain name on your authz server.

- ## [application/o/authorize endpoint missing CORS headers · Issue #10057 · goauthentik/authentik](https://github.com/goauthentik/authentik/issues/10057)
- I'm using traefik as forward proxy and solved this issue by setting the Content-Security-Policy Header of authentik

- [`userinfo` endpoint missing CORS headers · Issue · goauthentik/authentik _202209](https://github.com/goauthentik/authentik/issues/3565)
  - There are already some CORS headers that are being set on the userinfo endpoint
# discuss-social-login
- ## 

- ## 

- ## 💄 [New custom CSS support is great _202303](https://github.com/goauthentik/authentik/discussions/4831)
- I also extended the concept a bit by customising the "User Library" view in a similar way

- ## [Google enrolment and login _202111](https://github.com/goauthentik/authentik/discussions/1776)
- I set up google OAuth and set my app to external and added a few email address access for testing. What I found was other gmail users could logon regardless of them being in the allowed list or not.

- ## [Social login confusion : r/Authentik _202410](https://www.reddit.com/r/Authentik/comments/19f587q/social_login_confusion/)
- It prompts for the username because Google does not return it. You can either change the prompt stage of your enrollment flow to ask only for the username (and not a password) or extract the username from the email 

- ## 🧩 [Started using Authentik, how can I get the standard “sign in with google” button? : r/selfhosted _202304](https://www.reddit.com/r/selfhosted/comments/133pp4l/started_using_authentik_how_can_i_get_the/)
- You just need to deactivate the standard login. So only google login is shown. Worked for me.
- Google is a "source" and if you edit the source you can also change the icon. Not sure if you can edit the text, though.

# discuss
- ## 

- ## 

- ## 

- ## [Self Sign In : r/Authentik _202411](https://www.reddit.com/r/Authentik/comments/1gu5ooj/self_sign_in/)
  - How or is is Possible to add a Button so that People can register themself in to Authentik and then they Authenticate with a Email or somehow (not necessary) and then they are user in Authentik
- Should be possible. Either by adjusting the enrollment flow or by using social login provider like Entra AD or others.

- ## [How to hide app name from login page? : r/Authentik _202505](https://www.reddit.com/r/Authentik/comments/1ksjfsl/how_to_hide_app_name_from_login_page/)
- you can add the following CSS under System > Brands > "your-brand" > Custom CSS

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
