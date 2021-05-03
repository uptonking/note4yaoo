---
title: thread-devops
tags: [devops, thread]
created: '2021-03-31T06:49:31.508Z'
modified: '2021-03-31T06:50:19.936Z'
---

# thread-devops

# guide

- apache2服务器配置子域名的方法
  - [Ubuntu Apache配置子域名（单IP多域名）](https://www.jianshu.com/p/a9eeac672069)

# pieces

- ## 

- ## 

- ## We recommend to not deploy to Vercel. Vercel is for frontend teams, not fullstack. 
- https://twitter.com/flybayer/status/1373325575553683465
  - You still have to scale your DB which is expensive. 
- Is the DB scaling still an issue with the hosted Supabase?
  - Nope! Since @supabase_io is using PostgREST, it allows you to use HTTP – mitigating any issues with the number of connections.
  - HUGE caveat: that’s if you use their client, not Prisma. If you use Prisma, normal connection issues apply.
  - Yep, I'm talking about Supabase in general with Next.js! Not Blitz.
  - PS. we're working with @prisma to improve this
- @vercel should bring the concept of hybrid front-end (static vs SSR) to the backend (serverless for compute vs long-running for performance and real-time).
