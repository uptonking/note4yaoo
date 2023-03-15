---
title: devops-docker
tags: [devops, docker]
created: 2023-02-09T19:18:57.376Z
modified: 2023-02-09T19:19:11.265Z
---

# devops-docker

# guide

# cli

```shell
# 显示正在运行的img，加上 -a 显示所有img
docker ps
docker container ls

# 禁止docker自动启动
docker update --restart=no container-name
```

# discuss
- ## 

- ## 

- ## 

- ## 

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
