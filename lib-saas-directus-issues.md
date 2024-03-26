---
title: lib-saas-directus-issues
tags: [directus, issues]
created: 2024-03-14T13:51:18.929Z
modified: 2024-03-14T13:51:32.122Z
---

# lib-saas-directus-issues

# guide

# issues-stars
- ## 

- ## 

- ## 
# issues-not-yet
- ## 

- ## 

- ## 

- ## 🧐 [Support nested relational values in conditional fields _202109](https://github.com/directus/directus/issues/8228)
- 
- 
- 

- ## [Custom fields in `directus_fields` doesn't show up in App when editing/creating a field _202211](https://github.com/directus/directus/discussions/16432)
- Since we're able to create custom fields in system collections, it would be nice to have a place to set those values on all the collections.

- ## [How to custom field type? _202204](https://github.com/directus/directus/discussions/12674)
- You can create custom interfaces by extension

- ## 🔒 [Public User Registration ](https://github.com/directus/directus/discussions/3083)

- How to determine role with public registration?
  - email domain, default role no permissions, ...
  - create invite link endpoint (role associated with the endpoint), public page option

- [user signup not possible? ](https://github.com/directus/directus/discussions/10445)
  - 202112: There's currently no native "public registration" functionality through the regular login. You can already configure the SSO providers to create the user on first login.
  - use the `AUTH__ALLOW_PUBLIC_REGISTRATION` setting

- [how can I implement registering user functionality? _202202](https://github.com/directus/directus/discussions/12135)
  - Seeing that you'd like to use JWT based auth, and allow SSO logins etc etc, I would recommend simply using `directus_users` for these users as well, rather than trying to rebuild the auth system on a custom `users` table. That way, you get everything out of the box. 
  - You could create a new role for these app-users, that doesn't have access to the Directus app (meaning that they're still users in the API, but can't access the admin app)

- ## 🛒 [Extension Marketplace](https://github.com/directus/directus/discussions/2820)
- 202305: This feature request has received over 15 votes from the community. This means we'll move this feature request to the Under Review state

# issues-done
- ## 

- ## 

- ## 
# issues
- ## 

- ## 

- ## 
