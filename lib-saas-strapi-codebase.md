---
title: lib-saas-strapi-codebase
tags: [codebase, strapi]
created: 2024-03-20T15:11:29.948Z
modified: 2024-03-20T15:11:37.860Z
---

# lib-saas-strapi-codebase

# guide

- resources
  - 👷🏻 [Strapi contributor documentation | Doc](https://contributor.strapi.io/)
# overview
- The event hub is a central system that processes a variety of events in a Strapi application. 
  - These events can be emitted from a variety of sources to trigger associated subscriber functions.
  - Events are mainly used in Strapi to power the webhooks and audit logs features. 
- However, plugin developers can also access the event-hub using the plugin API. 
  - This means plugins can listen to events emitted by Strapi and emit new events to the event hub.
- The event hub is a store of subscriber functions. 
  - When an event is emitted to the hub, each subscriber function in the store will be called with the event's name and a variable number of arguments.
  - This design was inspired by the way Strapi handles lifecycle hooks. It was chosen over the Node.js event emitter because it provides the ability to have a single subscriber function per feature, and does not cause memory leak concerns.
- Performance: Strapi emits a lot of events, so you need to make sure your subscriber functions aren't too expensive to run.
# plugins

# admin

# server

# content-type-builder

# content-manager

# media-library

# user-permissions
- The RBAC permission system relies under the hood on the CASL library.
  - A permission is the combination of an action, a subject, some properties and some conditions. 
  - The logic is that: a user can perform an action on a subject and some of its properties only if it its role has the permission and if the conditions associated to the permission pass.
- Each role can have different permissions independentely. There is no inheritance system.
  - To check if an action can be performed by a user, frontend and backend simply retrieve the list of the permissions associated with the user's roles and check if it contains the permission associated with the action about to be performed
- 
- 
- 

# more
