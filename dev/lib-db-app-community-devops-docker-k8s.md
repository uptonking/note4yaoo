---
title: lib-db-app-community-devops-docker-k8s
tags: [database, devops, docker, kubernetes]
created: 2023-12-07T09:32:45.693Z
modified: 2023-12-07T09:33:17.608Z
---

# lib-db-app-community-devops-docker-k8s

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 有大佬知道如何解决 cf 数据库链接链路过长的问题吗？
- https://x.com/zhdsuperman/status/1903349880703299872
  - 同样的请求和后端代码，同一个数据库（us-east-1），vercel 的 function 比 cloudflare worker 快很多（物理上更接近数据库的原因），cf workers 开启了 smart placement 也不行。
- 难搞。 如果不搞异地多活，最佳的解法永远是后端和数据库同一区域甚至同一个局域网，前端通过 cf 网络加速访问后端数据库。
  - 是呀，数据库和后端就得放一起，vercel 的 function 配置就在 us-east-1，和数据库同个区域，10ms 就执行完了，但是我不知道 cf 怎么配置在 us-east-1 计算，这个影响太大了。
  - cf 没有 pg 服务，有的话买就行了。D1 无法满足我的需求，应用依赖很多 PG 的特性。

- 一定要 serverless 么, 感觉其实量没有那么大的时候一台实例蛮好的。
  - 稳定服务有 k8s 集群，但是项目前期不太想管理实例，代码不少写了很快就要删，serverless 适合随手抛。

- 在考虑要不要迁移到 supabase 了
- 你是说把 function compute 迁移到 supabase 吗？我尝试配置了 cf 的 Hyperdrive，有好一点，但不多。vercel 上用的 hono，切换平台很容易。
  - 不仅是 function，还有 db，现在 db size 100+m/d，感觉继续用 workers + d1 不是个办法
- Supabase 背后就是 AWS 的 RDS 实例，如果不用 supabase 的特性，或免费的 t4g.nano，直接买对应型号的 RDS 更便宜，还支持 pg 16 和 multi db（supabase 砍掉了 multidb 功能）。

- 云到云 与端到云 差别基本不可跨越
  - 需要多云的网络方案，像 vercel/supabase 一样，这样增加的 delay 大多数场景都能接受。
# discuss
- ## 

- ## 

- ## 

- ## 感觉kubesphere这个项目好鸡肋，没啥实质意义的功能点，弄了个应用商店我helm chart也能部署，弄了个啥监控我describe node也能看
- https://twitter.com/stephenzhang233/status/1788610739881771062
  - 多装一个组件还消耗资源，长得就跟政府项目的什么“xx智慧大屏”一样
- 太重了，而且和已有自建k8s集群兼容问题很多，放弃了

- ## 感觉kubesphere这个项目好鸡肋，没啥实质意义的功能点，弄了个应用商店我helm chart也能部署，弄了个啥监控我describe node也能看

- ## 🆚️ Docker vs. containerd vs. Podman
- https://twitter.com/iximiuz/status/1751674025191875064
  - Docker relies on `containerd` , a lower-level container runtime, to run its containers. It is possible to use containerd from the command line directly, but the UX might be quite rough at times.
  - contaiNERD CTL ( `nerdctl` ) to the rescue!
- If you want to:
  - Explore the capabilities of containerd
  - Learn more about the internals of Linux containers 
  - Better understand the difference between containerd and Docker
  - Launch a container using containerd's default CLI - `ctr` .
- While both docker(d) and containerd are daemons, containers can actually be launched as regular Linux processes and then left unattended.
  - That's pretty much how `Podman` does it.

- ## 🐛 [2023年11.27日滴滴打车崩溃是什么原因造成的? - 知乎](https://www.zhihu.com/question/632195562)
- 小道消息说是kubernetes升级导致的。很野，一口气节点全给原地升级了，连控制节点都升级了。
- 这里kube-apiserver就对应滴滴文里的master, kubelet对应滴滴文里的node. 官方的要求是kubelet和apiserver之间差不超过3个小版本。apiserver 1.20 + kubelet 1.12 这个版本组合，官方根本就不支持！
  - 官方不支持的东西，不见得一定会挂，测试环境5个节点，很可能不会遇到不支持的那些场景。但你特么生产环境5000个节点，不出问题就怪了。
  - 面试全在背八股文，评绩效就是做ppt. 我怀疑国内都没几个人真懂k8s这种稍微新一些的技术的
  - 所谓互联网降本增效，就是把底层干活的人都裁了吗？ 留下一堆天天写 PPT 的中层领导来维护系统吗？

- ## 🤼🏻 [没错，数据库确实应该放入 K8s 里！_20231207](https://mp.weixin.qq.com/s/rpyNczx0AD_iseMMLioVjw)

- ## 🤼🏻 冯若航: 数据库应该放入K8S里吗？ 当然不！这样做的结果就是双输 —— K8S 失去灵活性，数据库失去可靠性
- https://twitter.com/GobeUncleWang/status/1731895242667049444
  - [数据库应该放入K8S里吗？_20231205](https://mp.weixin.qq.com/s/4a8Qy4O80xqsnytC4l9lRg)
- 有状态应用跑到 K8S 怕是💊
- 虽然对k8s的存储了解不深，但至少知道Rancher的Longhorn既可以使用本地高性能磁盘，又可以不绑死在某一台工作节点上。
- 我都是裸机直接部署，开发个 OA 系统一天还没 500 个并发，上个锤子容器架构…

- 已经约架了，kubeblocks 的曹老板应该也有一篇

- 这种争论一般都主打一个各说各的
  - 核心在于各自顺便给自家产品带货

- 都没怼到点子上，扯了半天，对稳定性，就一个方案，交给专业技术团队

- ## 🔥 [Running Databases on Kubernetes | Hacker News_202303](https://news.ycombinator.com/item?id=34999039)
- 
- 
- 

- ## 🔥 [Why Databases Are Not for Docker Containers | Hacker News_201702](https://news.ycombinator.com/item?id=13582757)
- 
- 
- 
