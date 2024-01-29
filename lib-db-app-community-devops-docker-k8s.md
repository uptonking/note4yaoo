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
# discuss
- ## 

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
