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

- ## 

- ## 

- ## 

- ## #infrastructure  #Azure 如何选择 app service 还是 vm？
- https://twitter.com/ThaddeusJiang/status/1433367427203559426
  - 前提：
  1. 同样的价格vm的性能更好
  2. app service 不能停机
  3. app service 默认提供弹性扩容，SSL证书，custom domain，高可用性等功能
- 结论：
  - 如果不需要 app service 提供的高级功能，推荐 vm。

- ## Containers are fun. Recently, one of the applications was migrated to run inside a container environment. Suddenly, the GC pauses have increased significantly.
- https://twitter.com/SerCeMan/status/1432278202806784005
  - The application is on Shenandoah GC, so the GC pauses would typically be below 10 ms as most of the GC work would be done concurrently. 
  - However, once the app started running inside the container, the pauses increased up to ~100ms. 
- After looking at the pauses in the GC logs, one line stood out - 16 workers, which seems like a bit too many given the specified ActiveProcessorCount was 3 based on the CPU shares
  - The next step was to compare the VM options, and the only difference between the previous setup and the container setup was the difference in ConcGCThreads and ParallelGCThreads. 
  - Reducing the number of GC threads to the lower values brought GC pauses back to the below 10ms range as it was before
- The issue was already fixed - starting from JDK14, the GC thread configuration in ShenandoahGC is container-aware 
- The conclusion is - know your environment. 
  - Small changes, like changing the number of threads, can affect the performance significantly. 
  - And use the latest JDK! The fix to your issue might already be out there! 

- ## We recommend to not deploy to Vercel. Vercel is for frontend teams, not fullstack. 
- https://twitter.com/flybayer/status/1373325575553683465
  - You still have to scale your DB which is expensive. 
- Is the DB scaling still an issue with the hosted Supabase?
  - Nope! Since @supabase_io is using PostgREST, it allows you to use HTTP – mitigating any issues with the number of connections.
  - HUGE caveat: that’s if you use their client, not Prisma. If you use Prisma, normal connection issues apply.
  - Yep, I'm talking about Supabase in general with Next.js! Not Blitz.
  - PS. we're working with @prisma to improve this
- @vercel should bring the concept of hybrid front-end (static vs SSR) to the backend (serverless for compute vs long-running for performance and real-time).
