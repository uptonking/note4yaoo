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

# discuss-stars
- ## 

- ## 

- ## 

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
- Docker不存在模拟，也不存在虚拟。
  - 它是隔离工具，需要运行特定的image，就是你想运行的软件大集合。不同image帮你隔离开互相不可见。 
  - 这一切让你误以为是OS级别，**其实是软件级别**。
- **Wine也是软件级别的模拟**，只模拟windows，让Linux也能运行win程序，
  - 这个和微软提供WSL提供windows上模拟Linux道理是一样的，只是正好相反。
- KVM是虚拟硬件的，非常底层。但是它是内核的一部分，所以强绑Linux平台。
  - Qemu在中层配合KVM使用。上层的客户OS可以完全不知道自己在哪，是谁。
- **KVM和Qemu都是用在OS级别的模拟或者虚拟**。他们都支持。 到底是哪个，决定在于你怎么使用他们。
  - 你可以单独使用Qemu进行OS模拟。这个时候就无所谓底层是什么操作系统了。但是实现不了完全虚拟化。
- Linux系列，kvm负责cpu虚拟化+内存虚拟化，实现了cpu和内存的虚拟化，但kvm不能模拟其他设备；qemu是模拟IO设备（网卡，磁盘），kvm加上qemu之后就能实现真正意义上服务器虚拟化。因为用到了上面两个东西，所以一般都称之为qemu-kvm。
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
# discuss-container-dev
- ## 

- ## 发现同节点的两个容器之间的吞吐量只有跨节点的 30%，
- https://twitter.com/liumengxinfly/status/1727680591917973607
  - 一开始以为可能收发包在一个CPU上资源被抢占了，今天 profile 一下发现同节点的时候内核处理多了个 ip_local_deliever 直接占了快 30% 的 CPU。图1同节点，图2跨节点。
  - 试了下调大 udp_mem 吞吐量上升了不少，不过profile瓶颈还是在这块，应该是buffer多大最终都被占满了。估计是同主机通信数据包进了接收队列就等另一边去拿了，另一侧处理不过来buf就满了，跨主机直接扔出去buf就不会满了
- 在uds dgram也碰到过类似的情况 多个客户端通过uds dgram往服务端写数据 当recv buf满的时候客户端会加到sock waitq上, 这个过程会拿锁 因为conetless 没有建连 都在一个sock上导致竞争 后来就改成了stream

# discuss-k8s
- ## 

- ## 

- ## 

- ## K8s的kubelet默认的maxPods是110个，不知道这样设计的缘由是什么
- https://twitter.com/stephenzhang233/status/1773648671940149460
- 早期版本 kubelet 有个本地的 kube API burst 和 qps 5 还是10的限制，这也会导致节点pod 太多，同步状态都会卡住。这也是为了减小apiserver压力， 一个节点qps5，kube qps 1000只能支撑 200个节点。而最初kube设计可能是几百个节点，～10000pod的数量级。才会有这些限制。
- 不希望集群太大了，规模太大了的话会各种组件都要魔改

- ## Google 当时的Borg 是没做网络虚拟化的，服务启动后前分配随机端口，启动后注册端口。这些都是在SDK里实现的。
- https://twitter.com/9hills/status/1730829030239117766
  - 这套方案社区根本接受不了。上下游全都要对接服务发现，否则你端口号都拿不到！至于负载均衡直接在SDK中实现。
  - 不是说Google藏着内部基建不愿意开源，而是内部基建别人根本就用不起来。
  - 所以说当年K8s 竟然能仅依靠现有的条件糊出一层虚拟网络加LB，大家都觉得真厉害。 当然现在都有各种方案了，以VxLAN 为主。

- ## k8s的黑点不在于那套实现 实现都能改，无非多花几个人月。
- https://twitter.com/ayanamist/status/1729942162249543996
  - 在于那套API，不管用go用java，甚至从零用C艹把apiserver重写一遍，你为了保证其它人用起来像个k8s，就得保留那套渣到爆炸的API
  - 没有精细的权限控制，workload+pod的设计导致防御面放在pod维度就要接受workload controller的ddos，而放workload维度就要穷举各种workload，哪天有人新弄了个workload就又要爆炸。

# discuss
- ## 

- ## 

- ## 

- ## 

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
