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
