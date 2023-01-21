---
title: lib-fwk-nodejs-feathers-community
tags: [backend, community, feathers]
created: 2023-01-12T16:33:42.410Z
modified: 2023-01-12T16:33:52.048Z
---

# lib-fwk-nodejs-feathers-community

# guide

# discuss
- ## 

- ## 

- ## 

- ## [Component-based architecture](https://github.com/feathersjs/feathers/discussions/2915)
- Since we have @feathersjs/schema and resolvers, now, there's less of a need for Model-based adapters. 
  - We can focus more on adapters that don't have the Model class overhead, like Knex, MongoDB, and Memory. 
  - With the new data loader that @DaddyWarbucks is working on, I feel like we'll finally have a unified solution for populating data, removing even more dependency on Model-based adapters.

- ## [Dove: We want to cheer... but have some mixed feelings about v5](https://github.com/feathersjs/feathers/issues/2760)
- The thing is that everybody will have to define their data model and validations somewhere somehow. 
  - So while everything in Feathers used to look super simple at the first glance, you end up getting that complexity somewhere else (how to convert the query, do validation, define and populate associations or get shared types were always big topics that didn't really have a good answer).

- ## [[Dove] v5 Migration Learnings and Feedback](https://github.com/feathersjs/feathers/discussions/2410)
- socket.io has reduced the max size of socket messages to lessen the effect of DoS attacks.
