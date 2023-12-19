---
title: pattern-local-first-community-auth-permission
tags: [auth, community, local-first, permission]
favorited: true
created: 2023-12-18T12:42:47.845Z
modified: 2023-12-18T12:43:20.532Z
---

# pattern-local-first-community-auth-permission

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-auth
- ## 

- ## how does single sign-on (sso) work
- https://twitter.com/milan_milanovic/status/1737027285549490434
  - Single sign-on (SSO) is an authentication process that allows a user to access multiple applications with a single login. 
  - This is accomplished using a central authentication server that stores the user's credentials and verifies them for each application.
  - Some common types of SSO are: SAML-based SSO, OAuth 2.0, OpenID Connect

# discuss
- ## 

- ## 

- ## Guys building SPA's, how do you design authorization checks in your apps? Especially when it's not a simple RBAC system.
- https://twitter.com/AmanVirk1/status/1736669755728130342
  - For example, check if the "user x is allowed to edit the post with id 1" or hide the edit button.
  - How and when do you communicate with the backend for this?

- For each object / resource that has to be displayed comes a list of permissions the actor has. Basically a collection of CRUD rights passed along the resource. currently implementing that system in our kotlin backend and will be implementing the frontend part in the coming weeks
  - Yeah, seems like a common practice as per other replies too.

- I normally keep whole permission object locally using state management library and then hide/disable button based on that. Only time backend call happens is if for some reason local state is not synced with DB, in that case backend communication will happen.
- What if the permissions is not a static list. For example, show the "Edit post" button, if user is the creator of the post?
  - In that case I return allowed actions list in API, using computed decorators. Where I can match current user ID with post creator ID.

- I usually create acls for each action and assign to users Then at the time of login i store in a local state and make a protected component that can accept 1 or many acl and based on that show hide the slot in between
- What if the list of permissions is not static. 
  - I make dependent ACL’s, so i can check whatever condition before checking the ACL. 
  - Checking condition is always a static thing as that object will be having creator id and all in each block

- With HATEOAS you can state that an action is often associated to a link. You can then display the button if the action is in the resource.
  - Yeah, this is the approach I took with an app. The client was not much in following "HATEOAS", so we went hybrid and return a list of actions can perform on each resource and collection

- JWT with claims as part of the user payload

- Include the permissions associated with the user in each resource. Lazy, async & method based computed properties on lucid models would be neat for that
