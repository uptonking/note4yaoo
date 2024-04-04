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
# discuss-stars
- ## 

- ## 

- ## 准备花点时间，把 17 个域名全部从 godaddy 迁移到 Cloudflare 了！推上的域名达人们，有啥建议吗？
- https://twitter.com/xqliu/status/1775530817978298699
  - 不知道是不是我的理解有问题，Godaddy 的续费价格普遍是 Cloudflare 的 150% 以上，甚至 200%
  - 所有可转移的域名已经转移完成！整个过程还是很顺利的！.cn 和 .com.cn 后缀的转移失败，CF 不支持这两个后缀域名的注册
- cloudflare的网页加速，以及他的全球dns服务器，新加坡小公司GoDaddy没法比的。
  - GoDaddy搞了一堆服务，好用的只有域名购买
- 我之前也把Godaddy的10几个域名全部转移到阿里云了。阿里云还是比较便宜的，也可以修改NS，在用的域名NS基本都用Cloudflare。
  - 好奇，域名在阿里云，做解析不需要备案吗？
- 几年前花了点时间把自己所有域名从各个渠道全部转到了 Cloudflare。现在已经完全离不开它了，用的最多的除了域名管理就是 Zero Trust 里的功能。
- Cloudflare Tunnel 这个又是做什么的呀
  - 你在自己家里电脑上跑个agent之后，可以通过域名直接访问到那台电脑上的服务。
- 如果真的是这样，这个倒是确实好用，我现在用的是 ngrok ，也挺好用的。

- 部分后缀还有更便宜的选择
  - 比如 .re .lu 之类，以及 .org。部分是 CF 不支持，部分是有更便宜的注册商。可以在 http://tld-list.com 查到每一个后缀的注册商比价

- ## 我们有几个在线服务，流量和计算压力很小，不想买vps了，准备在本地部署一个物理台式机（二手thinkpad）然后买点端口转发服务，靠谱吗？
- https://twitter.com/franklinHaHaHa/status/1769314440086962449
- 但是一台物理机器，要考虑数据可靠性吗？要经常备份
- 既然都用二手笔记本了估计运算量不大，为什么不考虑二手intel NUC或者rasberry pi，耗电会更低。
  - 有点担心arm的兼容性，另外，二手nuc 不便宜吧？
- 靠谱，我有些吃性能的服务就是放在本地主机上的，不过转发用的是自己在VPS上部署的NPS。
- 可能需要两台，不过如果电池无法拆卸可能有些风险
- 靠谱，在路由器上设置一下VLAN，把服务器和自己常用的网络隔离开，再配置端口转发。便宜VPS的一个月3USD，但是是固定IP，固定IP比较方便。如果IP会变化，还要再配置DDNS。

# discuss-known
- ## 

- ## 

- ## 

- ## [Post Mortem on Cloudflare Control Plane and Analytics Outage_202311](https://blog.cloudflare.com/post-mortem-on-cloudflare-control-plane-and-analytics-outage/)
- Beginning on Thursday, November 2, 2023, at 11:43 UTC Cloudflare's control plane and analytics services experienced an outage. 
  - The incident lasted from November 2 at 11:44 UTC until November 4 at 04:25 UTC.

# discuss-security
- ## 

- ## 

- ## 

- ## 才知道还有这种 CRLF 漏洞... 通过在网址里塞入 %0d%0aSet-Cookie: xxxx 的方式，让一些跳转登录页的网站被注入cookie。
- https://twitter.com/zQwQs/status/1718893609905455519
  - 不过也有前提就是 server 侧读取 pathname 的时候 decode 了

# discuss
- ## 

- ## 

- ## 我问 infra 能不能搞灰度部署，我说可以一个一个 pod 部署就行。infra 说不能，因为真正的灰度部署，流量是要能按比例分配。
- https://twitter.com/yfractal/status/1775014098335658211
  - pod 级别的，能解决 99% 的问题了。剩下的 1%，不是没用，而是 99% 的问题还没解决呢，想那 1% 干啥。

- 确实，单个 pod 金丝雀发布比控制流量比例的灰度发布的技术含量低很多，很解决问题 

- 有需要精准按流量分配的一般是 AB Test 这种，为了看数据的时候
  - 对，上 featureflag 反而容易控制

- ## Caddy is the best thing to happen to the world of web servers since nginx. So I invite you to try it out with this interactive guide I prepared.
- https://twitter.com/ohmypy/status/1764978049274065112
  - All examples work from the browser, no need to download or install anything.

- ## 我使用 Caddy 做本地开发，经常载入页面需要好几秒。让 ChatGPT 帮我 debug 了一下，发现是 namelookup 花时间最多，在 hosts 文件中加了后面两行解决了
- https://twitter.com/beihuo/status/1741600998035165639
- Caddy很方便，跑起来配置少写好多
- 看起来是 mDNS 问题，其实是不很建议用 .local 的。
- babel.local ?
  - *.local 我用来做本地用。这个产品叫 babel 

- ## Recently I noticed that chrome sent some DNS requests bypassing my router (which is my system's DNS server), 
- https://twitter.com/baffin_lee/status/1726239447937950182
  - which prevented my from controlling traffic base on DNS and IP address. 
  - After some digging, disable "Async DNS resolver" flag in Chrome solved the problem.

- ## 把域名从 http://name.com 迁到 cloudflare 了，便宜一半
- https://twitter.com/fuyufjh/status/1726166801854451881
- 为啥你们迁移都更省钱……我的域名从阿里云迁移过来，99->150
- cloudflare域名只收成本费，不盈利

- ## yaml 多按了个 tab 调试几小时
- https://twitter.com/zhdsuperman/status/1718617613092475257
  - 不喜欢也得用，很多系统都用 yaml 来配置：AWS CloudFormation、K8S、Spring boot config、Github Action、AWS Codebuild……
  - yaml 的语法太飘了，string 数组就有 n 种写法，不同平台支持的写法还不一样。

- ## tail -F will monitor a file, such as a log file, until you type Ctrl-c.
- https://twitter.com/abhi9u/status/1712892253944139949
- The -F option forces tail to periodically check that the file has not been moved or has not been shortened. 
  - If either of those events has happened, it reopens the file, dumps the existing content on stdout and continues to tail the new content just like usual. 
  - This is handy in situations such as when the log file gets automatically rotated and you want to automatically start following the new file. 

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
