---
title: devops-docker-dev-xp
tags: [dev-xp, devops, docker]
created: 2023-02-09T19:18:57.376Z
modified: 2024-06-30T11:16:43.565Z
---

# devops-docker-dev-xp

# guide

- podman难以完全替代docker，依赖的环境或服务很可能只提供了docker

- resources
  - [Portainer architecture](https://docs.portainer.io/start/architecture)
  - [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
  - [尚硅谷3小时速通Docker教程_雷丰阳_202406](https://www.bilibili.com/video/BV1Zn4y1X7AZ/?spm_id_from=333.788.videopod.episodes&vd_source=deff4d2e2efa3273948dd6911a08fd39&p=18)
    - https://www.yuque.com/leifengyang
    - [ 雷丰阳 小分享 - Feishu Docs](https://shenma-docs.feishu.cn/wiki/RAlqwIZVdi0ujSkQHmrcEHdDnIb)
  - [【GeekHour】30分钟Docker入门教程 _202306](https://www.bilibili.com/video/BV14s4y1i7Vf?spm_id_from=333.788.videopod.sections&vd_source=deff4d2e2efa3273948dd6911a08fd39)
# cli

```shell
# -d是后台启动, -p hostPort:containerPort, --network mynet自定义网络, -e envVars
docker run -d -p 8080:80 --name myNginx nginx
# 目录挂载 -v /outPath:innerPath , 可以用多个-v挂载多个， 挂载时以外部路径下的内容作为数据源
# 卷映射   -v outPath:innerPath , 将容器内路径映射到宿主外，以容器内内容作为数据源
# /var/lib/docker/volumes/volumeName
docker volume ls

# 每个容器都加入了 docker0 网络，使用容器ip访问的缺点，每次重启ip会变化
# docker0不支持域名访问，
docker network create mynet

# 显示正在运行的img，加上 -a 显示所有img
docker ps
docker container ls

# 禁止docker自动启动
docker update --restart=no containerId

docker stop containerId

# stop all containers
docker stop $(docker ps -aq) && docker rm $(docker ps -aq)

docker exec -it containerName /bin/bash
docker exec -it my_container sh -c "echo a && echo b"

docker save -o myImage.tar image
docker load -i myImage.tar image

docker tag originalName username/imageName:v1.0
docker tag username/imageName:v1.0 username/imageName:latest

```
