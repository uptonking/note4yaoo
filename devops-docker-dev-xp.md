---
title: devops-docker-dev-xp
tags: [dev-xp, devops, docker]
created: 2023-02-09T19:18:57.376Z
modified: 2024-06-30T11:16:43.565Z
---

# devops-docker-dev-xp

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
