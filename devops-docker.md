---
title: devops-docker
tags: [devops, docker]
created: 2023-02-09T19:18:57.376Z
modified: 2023-02-09T19:19:11.265Z
---

# devops-docker

# guide

- resources
  - [Portainer architecture](https://docs.portainer.io/start/architecture)
# cli

```shell
# 显示正在运行的img，加上 -a 显示所有img
docker ps
docker container ls

# 禁止docker自动启动
docker update --restart=no containerId

docker stop containerId
```

# discuss
- ## 

- ## Lazydocker: 在终端可以使用图形化的方式来管理 docker 的一系列服务。
- https://twitter.com/vikingmute/status/1656477474518347779
- 用的 portainer 管理，还能管理远程的

- ## [既然有了Docker， 为什么还要Kubernetes ? - 知乎](https://zhuanlan.zhihu.com/p/77308665)
- Docker容器技术是Kubernetes平台的基础。容器技术主要作用是隔离，通过对系统的关键资源的隔离，实现了主机抽象。Kubernetes平台则是在抽象主机的基础上，实现了集群抽象。
  - 容器，提供应用级的主机抽象; Kubernetes，提供应用级的集群抽象。

- ## 简单说下这么些年 #Docker base镜像碰到的坑：
- https://twitter.com/liumengxinfly/status/1641808918715453440
  1. 永远不要用alpine,musl的概率性DNS错误和性能问题总会让你在某个时刻崩溃
  2. 如果提供企业服务，选一个背后有商业公司支持的 base，不然安全扫描别人update一下就好了，你要从上游手动编译
  3. 选了不熟悉的 base，总有一天出莫名其妙问题时你会绝望

- 推荐下base镜像？
  - 我在用 ubuntu
- debian / ubuntu 的 base 尺寸和 alpine 差的非常少了, 不知道为什么还有人坚持用 alpine

- ## I thought Podman attempts to mimic Docker behavior as close as possible? What is different in its architecture exactly?
- https://news.ycombinator.com/item?id=35154025
- The endless war of usability and security
- By default Podman doesn't have a daemon running as root, although you can opt into it. 
  - Podman instead really encourages setting up systemd units to keep your images running.
- Podman is very different internally than Docker. 
  - It might mimic commands and OCI image standard, but other things are quite different.
  - Docker is daemon-based and and Podman is not. 
  - Podman uses SELinux by default with additional features and other practices for better security. You can use it without root user.

- The primary difference is you’ll attempt to use Podman and begrudgingly go back to Docker after banging your head debugging SELinux.
  - Ha! My experience exactly, although I have to admit that this was for personal use at home where my patience is usually thin to non-existent. Docker CE on the home server saved me a lot of aggravation, where podman got me wondering if virtual machines were really that bad... Net effect is that I'm back on docker, plus two vm's I stood up during podman's interregnum.
