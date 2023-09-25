---
title: thread-devops
tags: [devops, thread]
created: 2021-03-31T06:49:31.508Z
modified: 2021-03-31T06:50:19.936Z
---

# thread-devops

# guide

- apache2服务器配置子域名的方法
  - [Ubuntu Apache配置子域名（单IP多域名）](https://www.jianshu.com/p/a9eeac672069)
    - 在/etc/apache2/sites-available目录下，建立单独文件，如kanban.conf
    - 保存后执行a2ensite kanban.conf，执行后会自动在/etc/apache2/sites-available建立相应的文件链接。
    - 注意要做域名解析
# discuss
- ## 

- ## 

- ## 

- ## 开源 Linux 服务器管理面板： 1Panel。完全可以代替商业化的宝塔面板
- https://twitter.com/vikingmute/status/1706122320660873526
- 几台到几十台机器，Portainer + Docker更好用，还能集中管理。

- ## 多租户的应用以 uuid 做主键解决了我的精神内耗……
- https://twitter.com/chloerei/status/1651868638650187776
  - 不能排序也不太方便嘞

- ## One of the ideas from yesterday Yjs meetings: package managers using BitTorrent protocol.
- https://twitter.com/Horusiath/status/1651102613012611073

- ## 以前是 Nginx、PHP、MySQL 啥的一个个装，现在是一个 Docker 搞定了。
- https://twitter.com/im2gua/status/1650428284583411712
  - 没用 Docker 时，一个个装，装几年、几十次上百次也不觉得烦，但你一旦用了 Docker，乍一发现这甜头太大了些，就再也不想回去了。
- 主要是版本、组件兼容性问题不需要考虑了，不然只要一个一个装上就能用，那也不怎么费事。

- ## kill 一个特定 port 上面的进程都需要两个命令。发现一个 npm 库，一行优雅的搞定：
- https://twitter.com/vikingmute/status/1648136292402876418
  - npx kill-port 3000
- 还是shell稳，node一换就没了，依赖太强，shell几乎不会换

```shell
lsof -i tcp:$port | awk '{if(NR>1) print $2}'| xargs -I{} kill -9 {}
```

- ## I want to make the application private but the library public.
- https://twitter.com/steveruizok/status/1636741287641579520
- Two repos and "npm link" is one of the easiest ways to do it 
- [How to Utilize Submodules within Git Repos | by Paige Niedringhaus | Bits and Pieces](https://blog.bitsrc.io/how-to-utilize-submodules-within-git-repos-5dfdd1c62d09)

- ## 收集了去年几个较为知名故障的公开复盘文档，发出来供大家重温下
- https://twitter.com/mr_easonyang/status/1623754899510145025
- 我觉得故障复盘的核心有三个点，即「及时性」、「有深度」和「有后续」，由于大多数的公开复盘只会列出 todo 而不会再发布后续，所以我们着重关注前两点。按这样的标准来看，Cloudflare 的复盘排名是最高的。
- 首先，是 Cloudflare 对其去年 6 月大宕机所做的复盘
  - B站这篇其实写得挺详实的，与云厂商不同，C 端产品极少会披露故障细节，所以这篇复盘我觉得是很难能可贵的。但既然间隔了一年才发布，那按上面的标准自然还是要扣些分的。
- 接着就是去年年末大家津津乐道的阿里云香港 Region 故障
- 最后是前科累累的 LastPass ，我觉得大概率以前相关问题的复盘是白做了，「后续」纬度应该可以直接打负分

- ## 在我看来，大型系统的开发，核心的挑战其实只有一个，就是“控制复杂性”。
- https://twitter.com/xuwenhao/status/1593469165892820992
  - 即使是工程师，也不要自己被自己骗了。无论是“高并发”还是“大数据”，并不是大部分互联网公司遇到的核心技术挑战。
  - 事实上，过去几年这些问题，其实根本不是拿着高薪资的软件工程师们解决的。大部分是靠硬件解决的。
- 持久层存储从机械硬盘变成SSD，以及I/O走PCI/E通道，解决了IOPS和吞吐量问题
  - 硬件的持续降价，使得大家用得起几百GB级别的Redis Cache
- 软件和系统上，从BigTable到Spanner其实都是Google解决的。Google让跨数据中心，跨州的分布式系统的一致性问题，得到了解决。
- 那当我们回到业务系统之后，其实面对的核心技术问题，就是“如何管理复杂性”。

- ## There’s a very real possibility local dev may be dead in 10 years. (The Death of Localhost)
- https://twitter.com/swyx/status/1533910738942562304
  - @isamlambert “Planetscale doesnt believe in localhost”
  - @ericsimons40 Stackblitz runs Node fast in the browser 
  - @GitHub runs entirely on Codespaces 
  - This would be the biggest shift in dev workflow since git.
- only 2 ways to make money in dev infra
  - bundling and unbundling the mainframe

- ## I’m a @Cypress_io fan. But, it’s not perfect.
- https://twitter.com/housecor/status/1525087602545762305
  1. Can’t trigger keyboard tab key
  2. Can’t switch in/out of iframes
  3. Can’t hover
  4. Can't test content-security-policy headers
  5. Can't change domains in a test
  - There are workarounds for some of these, but they’re not perfect.
- Wow, what timing: Cypress launched multi-domain support today - so number 5 is solved
- I can relate to this a lot. After creating several hacks and workaround, I ended up switching to Playwright.
  - Playwright is a lot faster, provides most of the items in this list (not sure about 5), and a VSCode extension to run tests without opening the browser
- It's slow when things get bigger, is there any solution not to store fixtures as json locally? Any clue?
  - I prefer to run my Cypress tests against mocked API calls via mock service worker
- These are actually great reasons to consider @Storybookjs Interaction Testing.

- ## edge functions are cool but your database is probably in us-east-1 or us-west-2
- https://twitter.com/sambreed/status/1523317291764514816

- ## 用微信云托管弄了个 Serverless 处理博客同步到微信公众号的流程，今天发个文章发现接口 400 了，
- https://twitter.com/_Xheldon/status/1518082813085761536
  - 问了客服才知道他们的服务器为了节约资源默认是半小时无请求自动关闭，直到下一个请求到来后才自动冷启动…
- 一个简单的做法就是每 29 分钟给一次心跳……用 uptime 这个服务还免费
- 我是用每次发两次请求解决的，启动服务只需要两秒，两个请求之间间隔 5 秒

- ## What’s a good database provider to use with Prisma? I just got an email saying I’ve spent $230 with AWS during a month I barely used the db for dev work
- https://twitter.com/mattgperry/status/1519609372288110593

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
