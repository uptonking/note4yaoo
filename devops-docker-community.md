---
title: devops-docker-community
tags: [comunity, docker, k8s]
created: 2024-06-30T11:17:15.672Z
modified: 2024-06-30T11:17:28.971Z
---

# devops-docker-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 💡 [How can I use environment variables in docker-compose? - Stack Overflow](https://stackoverflow.com/questions/29377853/how-can-i-use-environment-variables-in-docker-compose)
- Docker Compose has native support for default environment variables in a file.
- [Interpolation | Docker Docs](https://docs.docker.com/compose/how-tos/environment-variables/variable-interpolation/)
- Docker Compose can interpolate variables into your Compose file from multiple sources.
  - Variables from your shell environment
  - If --env-file is not set, variables set by an `.env` file in local working directory (PWD)
  - Variables from a file set by - `-env-file` or an `.env` file in project directory
  - You can check variables and values used by Compose to interpolate the Compose model by running `docker compose config --environment` .
  - `COMPOSE_DEBUG=${DEV_MODE:-false}`

- ## 又有人遇到 Docker 网络问题，之前分享的操作方法我又分享一下。这是最稳妥的做法：
- https://x.com/jaywcjlove/status/1894825834390921678
  - 1️⃣ 本地下载镜像
  - 2️⃣ 上传到服务器
  - 3️⃣ 服务器加载镜像 
  - 这个方法已经使用很久了，稳如老狗，不折腾，效果稳定可靠。

- mac芯片可以拉取 amd的镜像么
  - 要看镜像是否支持，如果支持就可以，只需要制定平台就可以了 --platform linux/amd64

- 单机是可以的。记得以前搞k8s，还是要搞个软路由搭梯子。腾讯云香港主机，计时收费，用完就销毁

- https://x.com/ProbiusOfficial/status/1894486674123669989
  - 上手改 docker config 和 systemd 配置 registry proxy，然后设置 http_proxy 能解决 90% 的问题。

- ## docker 是不能做到不同的用户之前相互隔离的吗？ 比如我有 A 和 B 两个不是 root 的账户，授予 docker.sock 的访问以后他们俩就都可以成为 root 并管理内容了？？？
- https://x.com/Lakr233/status/1844993521113055437
- 你要找的其实是 rootless container。 不过 podman 确实算是一个 rootless container。
  - 不干扰 podman rootless 每个用户有自己的容器，使用podman generate 生成systemd文件，让systemd 托管各个用户podman 容器生命周期

- docker也可以装成rootless的，就是不知道是否可以如预期那样

- 是的 如果希望隔离的话，可以用 rootless 的 podman，作为 docket 的 drop-in replacement

- 对，这是通过 Docker 进行本地权限提升的常见手段，所以在很多情况下安装 Docker 会被认为是一种攻击面
- docker socket API可以认为是root
- 容器内访问 Docker Socket 是一种提权手段，因为 Docker Daemon 是 Root 权限运行的

- runc 是共用一个host kernel，要做到容器安全隔离可以看看kata container ，不同容器独用一个guest kernel

- docker 守护进程默认 root 权限运行的，容器里的 root 用户也映射到宿主机 root 账户。 要完全隔离得配置 rootless，每个账户下运行各自的daemon，这样创建出的容器，内部 root 用户才会映射到当前账户，不过会遇到些奇奇怪怪的问题。 感觉用 podman 玩一玩 rootless 比较方便。

- ## Why we wrote Docker in Go instead of Python:
- https://x.com/solomonstre/status/1842342755194048981
  - A compiled binary that didn't require installing a language runtime and therefore didn't trigger tribalism(效忠部落主义; 效忠集体主义).
  - We were all Python/C programmers and Go gave us the best of both.
  - The syntax was "mainstream" without too many niche or radical concepts. 

- I’d say binary size should also be a factor.

- Did Kubernetes in anyway influenced the rewrite? Kubernetes was released in 2014, while Docker was released in 2013, and the Go rewrite happened in 2015.
  - Docker was already in Go before Kubernetes was made public. Kubernetes was influenced by Docker’s use of Go and chose Go as a result.

- ## ⌛️ 容器技术经历了几个历史阶段：
- https://x.com/HappyQQ_CN/status/1829217593946669360
  1、隔离文件：chroot
  2、隔离访问：名称空间
  3、隔离资源：cgroups
  4、封装系统：LXC
  5、封装应用：Docker
  6、封装集群：Kubernetes

- 在我看来是作业控制，进程管理机制的进步。

- ## 🆚️ What is the difference between Virtual Machines and Containers?
- https://twitter.com/Franc0Fernand0/status/1768614813335208237
- VMs are made up of two parts:
  - a Hypervisor which manages the resources of virtual machines that run on real hardware
  - a guest OS that is an operating system that is different from the host OS
- Containers put all the code and tools needed to run a single app into one unit. Each container has a very small OS and uses the host OS when more resources are necessary.

- The main benefit of virtual machines is the superior isolation level. There is a clear separation between the processes on the host OS and the guest OS.
  - Containers offer less isolation but use less memory and CPU, start up faster, and are more portable.

- VMs use hardware virtualization, containers use OS virtualization.

- [Build Your Own Docker | Coding Challenges](https://codingchallenges.fyi/challenges/challenge-docker/)

- ## 🆚️ [虚拟化软件Docker、Wine、Qemu、KVM有什么区别？ - 知乎](https://www.zhihu.com/question/540942002)
- 你把模拟和虚拟混淆掉，OS级别和软件级别也混淆了，当然傻傻分不清了。
- 💡 Docker不存在模拟，也不存在虚拟。
  - 它是隔离工具，需要运行特定的image，就是你想运行的软件大集合。不同image帮你隔离开互相不可见。 
  - 这一切让你误以为是OS级别，**其实是软件级别**。
- 💡 **Wine也是软件级别的模拟**，只模拟windows，让Linux也能运行win程序，
  - 这个和微软提供WSL提供windows上模拟Linux道理是一样的，只是正好相反。
- 💡 KVM是虚拟硬件的，非常底层。但是它是内核的一部分，所以强绑Linux平台。
  - Qemu在中层配合KVM使用。上层的客户OS可以完全不知道自己在哪，是谁。
- **KVM和Qemu都是用在OS级别的模拟或者虚拟**。他们都支持。 到底是哪个，决定在于你怎么使用他们。
  - 你可以单独使用Qemu进行OS模拟。这个时候就无所谓底层是什么操作系统了。但是实现不了完全虚拟化。
- 💡 Linux系列，kvm负责cpu虚拟化+内存虚拟化，实现了cpu和内存的虚拟化，但kvm不能模拟其他设备；
  - qemu是模拟IO设备（网卡，磁盘），kvm加上qemu之后就能实现真正意义上服务器虚拟化。因为用到了上面两个东西，所以一般都称之为qemu-kvm。
- libvirt则是调用kvm虚拟化技术的接口用于管理的，用libvirt管理方便，直接用qemu-kvm的接口太繁琐。
- 对应Windows的，大概就是Hyper-V，还有一个就是开源的VirtualBox，比较轻量；另外一个独立发展的就是VMWare ESXi。
- wine和wsl1差别还挺大的，wsl是自己搞了套和windows系统调用平级的linux系统调用，wine是加了个api中间层，用的系统调用还是linux自己的。

- 👉🏻 准确来说，qemu是模拟器，换句话说qemu模拟的环境里不依赖硬件平台。
  - kvm是虚拟机，用来在某一个操作系统下，提供一个虚拟的硬件环境（CPU和内存）

- Docker不是虚拟化软件，它是一串cgroup 的命令链，收窄以此运行的软件的权限
- Wine是一套提供Windows API 的软件
- Qemu是电脑处理器模拟器，包括而不限于x86, arm, mips...，而以此基础上构成的电脑模拟器
- KVM不是一个模拟器，是一个可以让上面软件绕过kernel 访问硬件（主要是cpu 和pci)的kernel 模组

- Docker不能运行windows程序吧，也并不是完全的虚拟化，只是实现了资源限制和隔离。
- Qemu是模拟器，KVM是内核模块，一般是一起用来达到虚拟化的功能。

- 在Linux上的Docker和Wine不提供任何虚拟化。
  - Docker是一款容器软件，里面跑的环境是没有内核的，也不运行在虚拟机器上。
  - Wine是一款用于在Linux上运行Windows程序的运行时，既不提供虚拟化也不提供容器化（除非你使用包含容器功能的第三方wine发行版）。
- KVM是Linux的一个内核模块，提供内核级的虚拟化支持。
- Qemu是一款虚拟机软件。在Linux上通常和KVM配合使用。
# discuss-virtualized-cloud
- ## 

- ## 

- ## Cloud virtualization: Red Hat, AWS Firecracker, and Ubicloud internals provides a great conclusion to cloud virtualization in the 2020s.
- https://x.com/OnlyXuanwo/status/1887015517745242186
  - [Cloud virtualization in the 2020s](https://xuanwo.io/links/2025/02/cloud-virtualization/)

# discuss-security
- ## 

- ## 

- ## 生怕大家搞不全云上横向路径，阿里云安全团队也是操碎了心 ，给大家搞了个图 #云攻击路径图
- https://x.com/tariweet/status/1898195099022201315
- 这不是最经典的攻击路径吗

# discuss-container
- ## 

- ## 

- ## 

- ## 发现同节点的两个容器之间的吞吐量只有跨节点的 30%，
- https://twitter.com/liumengxinfly/status/1727680591917973607
  - 一开始以为可能收发包在一个CPU上资源被抢占了，今天 profile 一下发现同节点的时候内核处理多了个 ip_local_deliever 直接占了快 30% 的 CPU。图1同节点，图2跨节点。
  - 试了下调大 udp_mem 吞吐量上升了不少，不过profile瓶颈还是在这块，应该是buffer多大最终都被占满了。估计是同主机通信数据包进了接收队列就等另一边去拿了，另一侧处理不过来buf就满了，跨主机直接扔出去buf就不会满了
- 在uds dgram也碰到过类似的情况 多个客户端通过uds dgram往服务端写数据 当recv buf满的时候客户端会加到sock waitq上, 这个过程会拿锁 因为conetless 没有建连 都在一个sock上导致竞争 后来就改成了stream

# discuss-gui-manager
- ## 

- ## 

- ## 

- ## 据说 OrbStack 是更好的 docker desktop，但是我根本不用 docker desktop，直接在终端里使用 podman，岂不是更轻量吗
- https://x.com/imvihv/status/1903141569022267722
- 不是一码事，Docker Desktop / Podman (machine) 和 OrbStack 本质上不只是 GUI，还是虚拟机引擎，做的是在 macOS 上开启一个 Linux 虚拟机 + 安装必要的容器化工具
  - 而 docker / podman 才是一个层级的，都是 CLI 工具，可以理解成是调用容器化 API 的前端
  - 所以说，macOS 买来，直接装 docker cli 是不可以用的，然后 podman cli 在 Homebrew 那边自带了虚拟机启动器，反而是变得不接耦了
  - OrbStack 给了许多可以直接在 macOS 侧操作 Linux 虚拟机的能力和命令（传输文件，无缝远程调用），也自带一套还不错的界面，性能也不错

- OrbStack 如何链接远程服务器的 Docker?
  - 能这么玩吗，不是先ssh到服务器上，然后再运行docker命令吗

- 观察到orbstack确实比podman少用了200兆内存，很好，就用它吧
  - orbstack性能好一点，做了一下虚拟机和内存分配上的优化。

- ## [OrbStack 1.0 is here! Fast, light, easy way to run Docker containers and Linux | Hacker News _202309](https://news.ycombinator.com/item?id=37599549)
- I recently installed docker, podman, Colima, and Orbstack. Orbstack was the only one that overwrote the docker socket instead of connecting to the docker socket. The containerization on my Mac is locked into using Orbstack because no other container engine can bind to that, now overridden, socket.
  - you can actually use `docker context` to choose which system you want to use for all of your tools. That docker socket you're referencing is just for the default context if you never chose anything

- orbstack provides a docker engine and sets the socket to point at that. It's a complete system, it's not "just a gui for an existing docker instance".
  - You can use Docker contexts to run OrbStack and Colima side-by-side

- It is not open source like Lima.
  - The goal is that OrbStack is just a lot nicer to use. Better performance, lower resource usage, and many DX features (several of which are covered) that go together to create a delightful experience.
  - Orbstack even comes with working ipv6 out of the box unlike Docker Desktop for Mac which STILL doesnt have support for ipv6
  - You're paying a premium because it's designed specifically for MacOS systems. Docker desktop is terrible on Mac, but Orbstack is awesome for this group of users.
# discuss-physical
- ## 

- ## AWS itself claims sub-millisecond latency within a AZ. In this poll, many people guess it’s in single digit milliseconds, which is what AWS claims for inter-AZ latency.
- https://x.com/penberg/status/1850794649440432193
- I measured in eu-central-1 and it’s 500us for cross az traffic and less than 500us within the same az

# discuss-docker-proxy
- ## 

- ## 

- ## 

- ## 目前 Docker Hub 被墙，拉取镜像比较困难，如果你有 HTTP 代理，可在 daemon.json 配置文件中添加代理，重启服务后就能正常访问了。
- https://x.com/linuxtoy/status/1863768873239294163
  - 若是 SOCKS 代理的话，用 gost 转一下即可
- 不需要用 gost 转一下，这里直接写 socks5://127.0.0.1:1080 是可以的，支持直接使用 socks5 代理。

# discuss-registry/docker-hub
- ## 

- ## 

- ## [Docker Hub, or GHCR, or ECR: Lazy man’s guide _202402](https://blog.devops.dev/docker-hub-or-ghcr-or-ecr-lazy-mans-guide-4da1d943d26e?gi=ccf8216e773b)
- docker-hub downsides
  - First of all, Docker Hub is no longer (very) friendly to open source project.
  - 100–200 pulls per 6 hours limit
  - Docker Hub is not the best integration with GitHub

- GHCR, or GitHub Container Registry, seems to be an okay solution. It’s part of the GitHub offering. For OSS project, it’s free and easy to use. There is no pull limit as Docker Hub (at least much relaxing)
  - download counts are confusing. I want to get fair numbers, not just a pretty number. 
  - GHCR is not always accessible globally. I got complain from friends/users in China
  - Other major issues, such as the image URL is same as the GitHub project. So it’s timeplus-io/proton We prefer timeplus/proton if possible.
# discuss-podman
- ## 

- ## 

- ## 

- ## 

- ## 🤔 [Is it worth switching some containers to Podman for security, or is Docker still king? : r/selfhosted _202512](https://www.reddit.com/r/selfhosted/comments/1pm8a1d/is_it_worth_switching_some_containers_to_podman/)
- The big security gain from podman is from running as a user. If you're going to do the work to move services to their own users or your user then it can be worth it for security. 
  - IMO the biggest upgrade is features. Running as a user being one of them, but pods and quadlets are the big draw too for qol.
- To me one of the core security features of Podman is `--userns=auto` , not running as a separate user. I haven’t used Docker much, but I don’t think it has an equivalent.
  - That is also nice. Most of my services share access to directories so I've had to mess with specifying users (zfs is a bitch). Being able to specify --userns is a big plus. 

- Or just run docker rootless. It is possible and not too much work
  - It looks like it's a bit more than one line of code but it's nice to see they moved away from user access to the rootful daemon.

- Quadlets are not as nice to deal with as compose files.
  - The files themselves are a bit more fiddly to handwrite, but them being functionally systemd units makes them more powerful. 
- Systemd dependency and dealing with systemd, makes them useless as far as I'm concerned.
  - Yeah, I mean if you don't use systemd then it won't be useful. 

- I run all my containers with podman quadlets. The fact that they run rootless with systemd integration is the security boost for me.
- Last time i switched I had problems with dependent containers. How do you deal with that?
  - Networking between containers is a little different with podman. The easiest way to handle dependent containers is to put them all in a pod together where they share the same namespace and can communicate via localhost. I run immich in a pod for example, and all those containers communicate with localhost.
  - Alternative is to use your host's IP address and the port that is bound to the container you want to reach with another container.

- How easy is conversion from compose?
  - Pretty easy, there's also tools like Podlet that can generate Quadlets from compose files.

- Nope. It is only more secure out of box due to defaults. Nothing is stopping you from doing the same thing using Docker and there plenty of other ways to secure stuff in a way to make even their defaults moot.

- A lot of docker images are not built with rootless operation in mind. Unless you are building your own docker images / using rootless images.
  - The only reason I prefer Podman is due to the auto-update features built in without the use for additional tools compared to Docker.

- Made the switch and am happy, because the systemd integration is great.

- Containers are for packaging, not security.
  - Podman, docker, lxc, all rely on the same set of namespaced syscalls, and all will be broken (to an extent) when a bug is found in the kernel.

- Run a webserver with "podman run --network none ..." to improve security. The same is not possible with docker. Only podman supports socket activation of containers. 

- Switched to podman. Dont use quadlets. Use compose files. Its possible to have the same level of security with docker but it requires some work.

- ## 🆚 [Why do so many people use Docker over Podman, even though Podman is theoretically better? : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1olt7op/why_do_so_many_people_use_docker_over_podman_even/)
- alias docker=podman
  - It used to be once upon a time, when podman was merely trying to be a fully open reimplementation of docker. They have diverged quite a bit since then.

- I do use Podman, but I think the answer here is clear: Podman has changed a lot in the last couple of years. Especially in terms of rootless containers, there's a bunch of gotchas in terms of networking, starting on boot ("lingering"), etc. which have changed significantly since version 3.
  - Also, people love Docker Compose. And Podman doesn't really have that. I think Podman's solutions with systemd and Kubernetes-compatible YAML might actually be better than Docker Compose, but that doesn't change the fact that most people use Docker Compose, and switching from that to Podman is a pain in the ass.
- Yeah, it's pretty insane how many people still use Docker compose in actual production setups.
  - It's really intended more for development. You miss out on many of the advantages of containerization by using it instead of a more robust solution like Kubernetes or Docker Swarm. Single point of failure if the host goes down, no zero downtime deployments, no auto-scaling, etc.

- Podman compose is a great shim but it doesn't always work with every project. It's not as reliable as Docker compose itself. I've ran into Podman compose crashes in certain configs.
  - Also some basic features. I tried to migrate a script that used "docker-compose cp" for instance. Nope. Not implemented.

- Lots of reasons, but three that are important:
  - Other than Fedora, Arch, and other distros that receive updates frequently, there are no repositories for slower cadence distros like Debian that you can add to update Podman.
  - Podman is NOT a drop in replacement for Docker. It will work for the most part, but there are differences that will cause issues 
  - A lot of container apps have instructions for getting up and running with Docker, but not as much for Podman. If there are differences, YOU are responsible for figuring out why Podman doesn't work with the Docker configuration if it doesn't work or breaks.

- does podman have a modern swarm mode?
- Try Nomad
  - Not FOSS.

- ## [Docker socket notification appearing continuously when podman VM stopped _202504](https://github.com/podman-desktop/podman-desktop/issues/12262)
- 
- 

# discuss-docker-devops
- ## 

- ## 

- ## 

- ## 

- ## Everyone uses Docker, but very few people know how debug a Docker container.
- https://x.com/livingdevops/status/1986873209262907485
  - I’m not talking about "docker logs", or "docker inspect", or "docker exec"
  - I’m talking about "docker events".
  - it streams low-level, real-time event logs from the Docker daemon; not just your container.
  - `docker events --filter container=<your_container_id>`

- In terms of debugging, it's cleaner to see error events or logs first, then to hop on the host and look for specifics.
# discuss
- ## 

- ## 

- ## [PSA: Docker still bypasses UFW by default. Here is why your "Firewall" might be lying to you. : r/selfhosted _202603](https://www.reddit.com/r/selfhosted/comments/1ruz3v9/psa_docker_still_bypasses_ufw_by_default_here_is/)

- ## [Why are Makefiles not the norm while using docker : r/docker](https://www.reddit.com/r/docker/comments/1atcomp/why_are_makefiles_not_the_norm_while_using_docker/)
  - docker compose 支持windows

- Make has a bunch of things you get out of the box. 
  - For example, dependencies and parallelism. 
  - You also get a declarative style which is quite beneficial for understanding what's going on, don't use shell scripts longer than say 10 lines, it's just asking for trouble.

- I like to create Makefiles with common stuff instead of having to type in `docker-compose build --no-cache <some-service>` etc.

- You should not be building anything in your docker-compose files. They should be pulling tagged images from your docker registry, which should have tagged images pushed to it by your CI process.

- I've been in situations where Makefiles are used to hide away some build processes that are way more complex than they need to be. Like, 5+ different docker compose files for a single Flask service.

- 💡 My solution for local development is to avoid using docker if at all possible, because rebuilding images every time something changes is a real pain -- or if I have to, make a development container that I can work inside without rebuilding it.

- When I'm doing local development, my preference is to not do that inside an image you rebuild every time you change anything, because building images is very slow. I'll just build and run things outside of a container if possible, or if it needs to be done inside a specific environment, make a development container that I can work in without rebuilding it every time I change anything.

- some people hate make and come up with some other solution like ant … scons and others

- I wonder how much of this can be handled with composition of docker compose files. Make a base `docker-compose.yml` for your services, but extend it with `docker-compose.dev.yml` if you need specifics for local dev.
  - I tried it but it gets increasingly complex, if you have docker compose file with container volume data separation for dev, staging, prod. Some setup require auth, some don’t. And in the pipeline u have huge script logic for pushing to aws ecr. I think Makefile is a good solution, personally
- I'm surprised that that complexity doesn't also propagate into your makefile then. As for pushing to ecr we handle that through a common github action, so most of the complexity is abstracted away (terraform managed resources for environment config/secrets etc)

- ## [docker真的好难用啊，为什么说它移植性好啊？ - 知乎](https://www.zhihu.com/question/400400231)
- 移植性好是因为 Docker 是基于 Linux 的 Cgroups 和 Namespace 的功能实现的，能跑 Linux 的地方他就能跑，Docker 的 rootfs 根文件系统 和联合文件系统使得他泛用性更广了，并且支持跨架构平台构建镜像，例如 MySQL 官方的镜像就支持amd64和arm64
  - Docker 容器简单说的话，就是在 Linux 基础上，通过约束与限制，来创造出一个进程边界，让不同容器之间形成一种隔离的效果
  - Namespace 就是用来隔离各类资源用的，例如网络设备、配置、挂载的硬盘等等
  - Cgroups 就是用来分配资源的，例如cpu、内存、io等资源
  - 切换进程根目录, 
- 这一套就是 Docker 的底层文件系统 rootfs（根文件系统）
  - bootfs（boot file system，左图下方）主要包含 bootloader 和 kernel。bootloader 主要是引导加载 kernel，引导完成后整个内核就都在内存中了。此时内存的使用权已由 bootfs 转交给内核，系统卸载 bootfs。可以被不同的 Linux 发行版共用。
  - rootfs（root file system，左图上方），包含典型 Linux 系统标准目录和文件。相当于各种不同操作系统发行版（例如 Debian，右图 Base Image 层）。因为底层直接用 Host 的 kernel（所有容器共享宿主机操作系统的内核），rootfs 只包含最基本的命令、工具和程序就可以了。当进行修改或者更新时，会在当前镜像层上新建新的层级（右图 Image 层）。运行起来的容器内容为可写层（右图 Container 层）

- 联合文件系统是 Docker 镜像的基础。镜像可以通过分层来进行继承，基于基础镜像（没有父镜像），可以制作各种具体的应用镜像。

- 虚拟化技术主要是去虚拟或半虚拟硬件资源，将计算机虚拟化为完整的硬件平台，也叫平台虚拟化
- 而容器化技术主要是OS层面的隔离，实现多个隔离的用户空间实例
- 当然，你也可以在虚拟机上跑容器，我就都是这么干的，

- 
- 
- 
- 
- 

- ## The smaller your Docker image, the fewer points of vulnerability.
- https://x.com/sitnikcode/status/1904111163090063531
  - One approach is “distroless”, even without a package manager. You install everything you need in Alpine, then copy only the necessary binaries into an empty image `FROM scratch` .
  - https://github.com/hplush/slowreader/blob/main/proxy/Dockerfile

- ## [macos - Docker command not found when running on Mac - Stack Overflow](https://stackoverflow.com/questions/64009138/docker-command-not-found-when-running-on-mac)
- Inside Docker desktop, go to Settings > Advanced Settings
  - I changed it from User to System. It resolved the issue for me.

- ## 如果不用docker咋给mac/linux/win的用户统一开发环境啊?
- https://twitter.com/hylarucoder/status/1775365292459499625

- 方便管理，配置文件管理比手动调配置方便多了
  - 很环保，搞坏了直接删掉重新up一下，所有服务全搞定
- docker 现在新版本相对统一还是比较好用的吧。如果用 docker，可以把一天半天的部署调试时间压缩到一两个小时，花点钱加内存也不是啥事儿。如果对内存 几百 G 很敏感的，可能也不会用 docker 去频繁替换架构了。

- 统一环境的是部署过程，是包管理，而不是docker
  - 你干过运维就该清楚什么都往docker里扔，维护起来是多么痛苦，时间长了没文档，当初做镜像的人还搞成了黑盒，排错的时候这没有那没有，反而增加了维护成本。
  - docker并不能解决部署混乱的问题，它只是把混乱的环境从主机移到了容器

- 三套脚本吧。Windows bat, Linux 和 Mac 用 shell。 脚本比 Docker 好的一点是它们方便做调整。docker封装好之后迁移肯定方便，但是调整和版本维护也麻烦啊。脚本只要改语句就行了，docker要更新和分发就笨重了。
- 我最讨厌配置环境，想起以前给toG客户开发全是离网环境，自己还要拿光盘把安装包和依赖一个个拷到服务器然后手动安装，真的是操蛋；尤其是碰到Python这种没办法像Java或Go这样没法直接打包部署，就连Linux版解释器都得自己编译一个的更想死
- 一个组的开发机器如果不是统一的OS。装了Docker也没用。遇到问题反而更难调试。

- ## 🤔 Do you use Docker during development with a Node.js project?
- https://twitter.com/AmanVirk1/status/1763471630171349201
- My issues are:
  - Running npm scripts is slow
  - File watchers needs polling
  - Installing dependencies is confusing. Should I stop container, install deps and re-run container?
  - Debugging code inside editors like VSCode is a nightmare

- I use it with nodemon. 
  - In dev, node project folder is mounted as a volume and watched by nodemon. 
  - In prod it’s built with dockerfile and run with ‘node server.js’ command (not using npm in prod).
- That's the best approach, IMO.

- If you’re using vscode, try devcontainers ! It’s awesome as it allows you to develop inside your container. You need to configure it the right way but once done, you have the same experience as developing without docker. Of course, with the benefices of it

- Nop, docker only for external services like a database, redis or mail but too many issues and start time is slow to be something usable.

- ## 查了一个月的性能问题，containerd 换成 docker 后好了，CNCF 出来赔钱
- https://twitter.com/liumengxinfly/status/1734399431271944670
- 啥问题 ？ docker 也用 containerd
  - 猜测是 cpu cgroups 什么配置设置的不一样，等着其他同事去查了
- 用nri查下oci spec？
- 多runtime的咋办
- 蹲个结论

- https://twitter.com/liumengxinfly/status/1734877332538884361
  - 同步下进度，和 seccomp 应该没关系，k8s 1.25 seccompDefault featureGate 是默认打开了，但是还要去 kubelet 开启才行，开启后确实性能会下降，但默认是不开启的。对比了 docker 和 containerd 环境生成的 state.json 几乎一模一样，对比了sysctl的系统参数也几乎一模一样，现在彻底迷茫中
- 内核好像上了 4.x 之后，容器网络 netns 内的系统参数会有区别
  - 一样的之前就是一批机器降k8s换docker

- ## 我用Docker的时候也遇到了很多坑，而且特别难调
- https://twitter.com/PenngXiao/status/1729460664585080872
  - 从某种程度上说这些容器技术好用、不出事儿的时候真好用，出了事儿真难定位。
- 容器自身的 bug 确实很难定位解决，但没有容器更难规范和定位其他问题。
  - 这个是不对的，当你没有容器的时候，这种toc的公司会被强制雇懂操作系统原理的人才能够放心。现在有了容器，很多公司就觉得花这么多钱养懂操作系统的人不上算。所以才会出现出事了n个小时都定位不到bug。如果是裸机分布式，有懂操作系统的工程师，基本上起码能诊断出来。
- 不过从原理上，容器并没有降低任何问题的发生概率。容器仅仅解决了环境的复制成本

- “从某种程度上说这些容器技术好用、不出事儿的时候真好用，出了事儿真难定位。” 这句话感觉可以把 “容器技术” 改成 “Java Lambda” (最近似乎讨论很激烈).
  - 对，也可以说大部分试图增加一层抽象的技术都是这样——比如Vue/React、Camel、Firestore。这些技术毫不相关，但是他们都是在某个底层技术上增加一层抽象。如果底层技术不向上泄露（或者说抽象做的足够好）那么大家就相安无事。一旦底层技术开始向上泄露了，那么就会出现还不如直接用底层技术的情况。抽象做的足够好的例子——Java、Database、REST。

- 我已经被云开发低代码的调试搞崩溃了
- 我也一样，或许是自己用不好，一直只敢停留在compose的阶段，只能接受自己可以控制的链路
- 用docker可能遇到的坑没法和k8s的相提并论。
- 

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
