---
title: devops-docker-dev-xp
tags: [dev-xp, devops, docker]
created: 2023-02-09T19:18:57.376Z
modified: 2024-06-30T11:16:43.565Z
---

# devops-docker-dev-xp

# guide
- tips
  - 使用要点: image, container, volume, network
  - podman难以完全替代docker，依赖的环境或服务很可能只提供了docker，反而会造成使用时的混乱

- resources
  - [Portainer architecture](https://docs.portainer.io/start/architecture)
  - [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
  - [尚硅谷3小时速通Docker教程_雷丰阳_202406](https://www.bilibili.com/video/BV1Zn4y1X7AZ/?spm_id_from=333.788.videopod.episodes&vd_source=deff4d2e2efa3273948dd6911a08fd39&p=18)
    - https://www.yuque.com/leifengyang
    - [ 雷丰阳 小分享 - Feishu Docs](https://shenma-docs.feishu.cn/wiki/RAlqwIZVdi0ujSkQHmrcEHdDnIb)
  - [【GeekHour】30分钟Docker入门教程 _202306](https://www.bilibili.com/video/BV14s4y1i7Vf?spm_id_from=333.788.videopod.sections&vd_source=deff4d2e2efa3273948dd6911a08fd39)
# config-xp
- tips
  - 卷映射需要顶级声明，而目录挂载不需要

- 制作镜像
  - 基础系统环境， 软件包， 启动命令
# cli

```shell
# -d是后台启动, -p hostPort:containerPort, --network mynet自定义网络, -e envVars
docker run -d -p 8080:80 --name myNginx nginx:v1.2
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

docker inspect containerId

docker exec -it containerName /bin/bash
docker exec -it my_container sh -c "echo a && echo b"

```

```shell

docker save -o myImage.tar image
docker load -i myImage.tar image

# 在 . 当前目录下构建镜像, 这里手动指定了tagName作为镜像名
docker build -f Dockerfile -t myImage:v1.0 .

docker tag originalName username/imageName:v1.0
docker tag username/imageName:v1.0 username/imageName:latest

```

# more
- On macOS,  `/var/lib/docker/volumes` does not exist as it does on Linux systems. This is because Docker Desktop for macOS runs Docker inside a lightweight virtual machine (VM) using HyperKit, qemu, or Apple Virtualization Framework (depending on version).
  - Docker Desktop stores its data inside the VM, not directly on your macOS filesystem.
  - Volumes are stored in the Docker VM's disk image (usually `~/Library/Containers/com.docker.docker/Data/vms/0/Docker.raw`), but do not modify this file directly.
  - For Development: Prefer bind mounts (e.g. `-v $(pwd):/app`) to edit files directly on macOS.
  - `docker volume inspect <volume_name>`

- Default Network in the Docker VM
  - On macOS (i.e. when you’re running Docker Desktop), there simply is no `docker0` interface on the host machine. Docker runs inside a tiny Linux VM (HyperKit) and the traditional Linux‐bridge (docker0) lives inside that VM, not on your macOS host stack
  - What you will see if you run ifconfig on macOS is Docker’s HyperKit‐side NAT/bridge interface, typically called `bridge100`, and the VPN‑kit userspace interface (often `vnic0` or similar). 
  - look for bridge100 (and possibly vnic0 for the VPN‑kit tunnel).
