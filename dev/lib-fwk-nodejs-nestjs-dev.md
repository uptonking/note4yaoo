---
title: lib-fwk-nodejs-nestjs-dev
tags: [framework, lib, nestjs]
created: 2020-12-12T19:22:14.437Z
modified: 2022-12-19T01:49:27.545Z
---

# lib-fwk-nodejs-nestjs-dev
- Node.js framework for building scalable server-side applications.
# guide
- pros
  - 支持horizontal scaling

- cons
  - ?

- features
  - scalable architecture for server-side applications
  - ioc container

- who is using #nestjs
  - adidas: as our backend to retrieve GitHub metadata and contents from our CMS.
  - more
    - [Who is using Nest in production?](https://github.com/nestjs/nest/issues/1006)

- usecase
  - crud
  - rest api
  - architecture and platform
    - microservice

- examples
  - libs
  - [nestjs-template](https://github.com/Saluki/nestjs-template)
    - goal of this project is to provide a clean and up-to-date "starter pack" for REST API projects

- tips
# pieces

# module

- Why did nestjs copied the Angular module system I don't know....

- ## The Global decorator from @nestframework is awesome and should find it's way into @angular . 
- https://twitter.com/aaronfrost/status/1079056698311008256
  - Having every single module in the system import a Common or Core module is superfluous(多余的，过多的). I love this Global solution from Nest.
- would grouping everything in one module and name it global help you? 
  - It could help, but would still need to be imported everywhere is used and for every test, etc.
- Interesting idea. Would be helpful especially for lazy loaded angular apps where every module is importing common module.
# ref
- [Modern Full-Stack Development with Nest.js, React, TypeScript, and MongoDB](https://auth0.com/blog/modern-full-stack-development-with-nestjs-react-typescript-and-mongodb-part-1/)
