---
title: lib-saas-strapi-issues
tags: [issues, strapi]
created: 2024-02-15T05:46:16.207Z
modified: 2024-02-15T05:46:32.456Z
---

# lib-saas-strapi-issues

# guide

# issues-done
- ## 

- ## [Can't install strapi - Questions and Answers - Strapi Community Forum](https://forum.strapi.io/t/cant-install-strapi/33500)
- TypeError: Cannot read properties of undefined (reading 'addBreadcrumb')

```shell
# cd to your project and
npm install --legacy-peer-deps
npm run develop
```

# issues-not-yet
- ## 

- ## 

- ## [Why doesn't Strapi have a built-in refresh token feature? - Questions and Answers - Strapi Community Forum _202304](https://forum.strapi.io/t/why-doesnt-strapi-have-a-built-in-refresh-token-feature/27543)
- JWTs usually have an expiration time (e.g., 15 minutes, 1 hour) to limit their validity. 
  - When a token expires, the client needs to obtain a new one. 
  - This is often done using a refresh token, which is a separate, longer-lived token that the client can exchange for a new JWT. 
  - This is a standard procedure that pretty much every api uses. 
  - So, why is no such feature implemented in Strapi?

- ## [Sharp - Media Upload Memory Leak](https://github.com/strapi/strapi/issues/14417)

- ## [Dissatisfaction with Strapi: Stability, Scalability, and Support - General - Strapi Community Forum _202301](https://forum.strapi.io/t/dissatisfaction-with-strapi-stability-scalability-and-support/24854)
- After spending 3 weeks on the customization of a large-scale e-commerce application, I ultimately decided to move away from Strapi permanently.
  - the lack of basic transaction rollback capabilities was a significant limitation for my use case.
  - the exception handling in the lifecycle hooks was not an effective solution and often resulted in a “400” error.
- For most large-scale projects, we have our users going for the enterprise edition that provides access to solution engineers. 

- I was also very surprised by the very heavy changes made from V3 to V4. Is ok to introduce breaking changes, but V4 broke everything. If you do the same for V5 I’m not switching.

- ## 🐛 [Inconsistency between responses gotten from the REST API and the Entity service API_202401](https://forum.strapi.io/t/inconsistency-between-responses-gotten-from-the-rest-api-and-the-entity-service-api/34975)
- strapi-plugin-transformer plugin was what I was going to recommend. Another approach you can use, is to write a transformer function to flatten the response.

- Yes, the transform plugin is the way to go. 
  - But I’ve recently learned that it’s all a joke. 
  - You see, core controllers invoke the transformResponse function which iterates over the service response and produces this highly impractical data/meta/attributes structure. This takes time. Then, the middleware offered by the transform plugin iterates again over that transformed response and flattens it. Which takes time again. 
  - A performant way would be to disable that transformResponse function alltogether, or at least the part that wraps all non-id field within attributes. Maybe patch-package could be used for that.
