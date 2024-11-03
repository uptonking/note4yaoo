---
title: lib-utils-codesandbox-community-runtime
tags: [codesandbox, community, docker]
created: 2024-05-12T17:19:42.440Z
modified: 2024-05-12T17:20:03.132Z
---

# lib-utils-codesandbox-community-runtime

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚️🐳 [Docker vs. containerd vs. Nabla vs. Kata vs. Firecracker and more | by Benjamin | Medium _202303](https://benriemer.medium.com/docker-vs-containerd-vs-nabla-vs-kata-vs-firecracker-and-more-108f7f107d8d)
- Containerd is a container runtime originally part of Docker but has since been spun off into its project. 
  - It provides a powerful and flexible way to manage containers at scale, with features such as image distribution, container execution, and network and storage management. 
  - In addition, Containerd is designed to be lightweight and fast, making   it a good choice for large-scale deployments.

- Nabla is a secure container runtime designed to provide isolation and protection for containerized workloads. 
  - It uses a microkernel-based architecture to minimize attack surfaces and prevent container escape. 
  - As a result, Nabla is ideal for running untrusted code or sensitive workloads that require high security

- Kata Containers is a container runtime that uses hardware virtualization to provide substantial isolation between containers. 
  - It combines the lightweight and fast nature of containers with the security and isolation of virtual machines. 
  - As a result, Kata Containers is a good choice for running multi-tenant applications or workloads that require strict isolation.

- Firecracker is a lightweight, fast virtual machine manager designed to run serverless workloads. 
  - It uses a minimalist approach to virtualization, creating microVMs that are lightweight and efficient. 
  - Firecracker is ideal for running serverless functions in a secure and isolated environment.

- Whether you need scalability, security, isolation, or efficiency, a container runtime can meet your needs. By understanding the strengths of each runtime, you can choose the one best suited for your specific use case.

- ## 🆚️ [My VM is lighter (and safer) than your container (2017) | Hacker News _202209](https://news.ycombinator.com/item?id=32764501)
- stuff like Kata Containers exist exactly because containers alone is not enough. WebAssembly on the cloud is only re-inventing what other bytecode based platforms have been doing for decades, but VC need ideas to invest into apparently.

- I would say that firecracker VMs are not more lightweight than Linux containers.
  - Linux containers are essentially the separation of Linux processes via various namespaces e.g. mount, cgroup, process, network etc. Because this separation is done by Linux internally there are not that many overheads.
  - VMs provide a different kind of separation one that is arguably more secure because it is backed up hardware -- each VM thinks it has the whole hardware to itself. When you switch between the VM and the host there is quite a heavyweight context switch (VMEXIT/VMENTER in Intel parlance). It can take a long time compared to just the usual context switch from one Linux container (process) to another host (process) or another Linux container (process).
  - But coming back to your point, no firecracker VMs are not lighter/lightweight than a Linux container. They are quite heavyweight actually. But the firecracker VMM is probably the most nimble(迅速的；敏捷的) of all VMMs.

- This reminds me: in 2015 I went to Dockercon and one booth that was fun was VMWare's. Basically they had implemented the Docker APIs on top of VMWare so that they could build and deploy VMs using Dockerfiles, etc. I've casually searched for it in the past and it seems to not exist anymore. 
  - For me, one of the best parts of Docker is building a docker-image (and sharing how it was done via git). It would be cool to be able to take the same Dockerfiles and pivot them to VMs easily.
- https://github.com/weaveworks/ignite can apparently do this. It looks exciting!

- Isn't that essentially what Vagrant and Vagrantfiles do?
  - Vagrant images are always huge. But docker images are small. You can deliver and share docker images with ease.
  - Vagrant never targeted production so not much money/resource/interest invested?

- 🐛 The issue with unikernels and things like Firecracker are that you can't run them on already-virtualized platforms
  - (Yes, I know about Firecracker-in-Docker, but I mean real production use)
- This is a limitation of whatever virtualized instance you're running on, not Firecracker itself. Firecracker depends on KVM, and AWS EC2 virtualized instances don't enable KVM. But not all virtualized instance services disable KVM.
  - Google Cloud, for instance, allows nested virtualization, IIRC.
  - Azure and Digital Ocean allowed nested virt as well!
- 💡 Firecracker runs in hosts that support nested virtualization. GCP and Github Codespaces do, but unfortunately EC2 and Macs don't.

- Firecrackers being originally based on a fork of crosvm might even benefit from this if they ever decide to play around this space, but also it'd need to be enabled on the platform level.

- Not surprising that VMs running unikernels are as nimble as containers, but not quite useful either, at least in general. Much easier to just use a stock docker image.

- Kubernetes says no... The article is light on detail. Containers and VMs have different use cases. If you self host lightweight VMs is likely the better path, however, once you in the cloud most managed services only provide support for containers.
  - You can also use a firecracker runner in k8s to wrap each container in a VM for high isolation and security.
- There is a huge difference running on VMs that you have zero access to, and actually owning your own VM infrastructure. Yes AWS Lambda runs on Firecracker, however, it could as well running on a FireCheese VM platform and you would be none the wiser, unless AWS publishes this somewhere.
  - There is a huge difference running on VMs that you have zero access to, and actually owning your own VM infrastructure. Yes AWS Lambda runs on Firecracker, however, it could as well running on a FireCheese VM platform and you would be none the wiser, unless AWS publishes this somewhere.

- Containers are great because they are small and fast, low overhead etc. And that is why they replaced virtual machines. This article however proves that this is also achievable with virtual machines.
- VMs don't need a full OS. You can run a single process directly from the kernel with no init system or other userland
- VMs can have private networks between each other just as containers do. That's pretty much what EC2 is about.

- 
- 
- 

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
- 👉🏻 Linux系列，kvm负责cpu虚拟化+内存虚拟化，实现了cpu和内存的虚拟化，但kvm不能模拟其他设备；qemu是模拟IO设备（网卡，磁盘），kvm加上qemu之后就能实现真正意义上服务器虚拟化。因为用到了上面两个东西，所以一般都称之为qemu-kvm。
  - libvirt则是调用kvm虚拟化技术的接口用于管理的，用libvirt管理方便，直接用qemu-kvm的接口太繁琐。
  - 对应Windows的，大概就是Hyper-V，还有一个就是开源的VirtualBox，比较轻量；另外一个独立发展的就是VMWare ESXi。
- wine和wsl1差别还挺大的，wsl是自己搞了套和windows系统调用平级的linux系统调用，wine是加了个api中间层，用的系统调用还是linux自己的。

- 👉🏻 准确来说，qemu是模拟器，换句话说qemu模拟的环境里不依赖硬件平台。
  - kvm是虚拟机，用来在某一个操作系统下，提供一个虚拟的硬件环境（CPU和内存）

- Docker不是虚拟化软件，它是一串cgroup 的命令链，收窄以此运行的软件的权限
- Wine是一套提供Windows API 的软件
- Qemu是电脑处理器模拟器，包括而不限于x86, arm, mips...，而以此基础上构成的电脑模拟器
- KVM不是一个模拟器，是一个可以让上面软件绕过kernel 访问硬件(主要是cpu 和pci)的kernel 模组

- Docker不能运行windows程序吧，也并不是完全的虚拟化，只是实现了资源限制和隔离。
- Qemu是模拟器，KVM是内核模块，一般是一起用来达到虚拟化的功能。

- 在Linux上的Docker和Wine不提供任何虚拟化。
  - Docker是一款容器软件，里面跑的环境是没有内核的，也不运行在虚拟机器上。
  - Wine是一款用于在Linux上运行Windows程序的运行时，既不提供虚拟化也不提供容器化（除非你使用包含容器功能的第三方wine发行版）。
- KVM是Linux的一个内核模块，提供内核级的虚拟化支持。
- Qemu是一款虚拟机软件。在Linux上通常和KVM配合使用。

- ## 🤔 请问 StackBlitz 和 CodeSandBox 这类 Web IDE 的技术栈是如何实现的？
- https://www.zhihu.com/question/279268026/answers/updated
- 我想提供一个思路：利用 es module + service worker + browser file system + 浏览器端即时编译实现不依赖服务端能力的 Web IDE.
  - 类似于 CodeSandBox 的方案是在浏览器端实现了一套兼容于 webpack 的打包系统，这主要是为了解决前端构建过程中对模块系统的依赖。
  - 而目前市面上所有主流浏览器（排除掉 IE）都已经很好的支持了 es module，我们其实可以充分的利用这个技术点来替代 webpack（即 bundless 构建）。
  - 在浏览器加载 es module 的过程中会不断的发出 http 请求去获取被依赖的 es module，对于不依赖服务端能力的 Web IDE，我们需要补全这部分本该由静态资源服务器提供的能力。
  - 所以，可以拦截请求并定制响应的 service worker 正好可以提供这个能力。
  - 我们需要将所有的代码资源存储在浏览器端，也就是说需要实现一套 browser file system。
- es module发出的http请求，是以scripts脚本加载的形式。而service worker只能拦截fetch。
  - service worker 中监听 fetch 事件当然是可以拦截脚本的请求的，不信你可以试试
  - 包括esm加载时的请求都可以被拦截

# discuss-runtime-vm
- ## 

- ## 浏览器中运行的 Linux 虚拟机环境 https://webvm.io
- https://x.com/geekbb/status/1816265787113627786
  - 通过 HTML5 和 WebAssembly 技术实现客户端执行 x86 二进制文件，支持网络功能，并提供了部署和定制的指南。

- ## [csb: We clone a running VM in 2 seconds | Hacker News _202312](https://news.ycombinator.com/item?id=38651805)
- Firecracker is the same VM technology used by Fly.io although they don’t have memory cloning as seen here. 
  - A VM can be cloned and the clone started in seconds though this heavily depends on image / rootfs size so it’s likely more in the order of 30 seconds or so (number pulled out of thin air).
- Can't you use CoW to make the clone essentially instant? (I thought BTRFS supported it, but I'm not sure)
  - I did a bit of searching and if the image is a file (qcow2, say) I'm pretty sure you could just cp --reflink=always old.qcow2 new.qcow2 and it would take way less than 30 seconds. (Again, assuming BTRFS; I guess ex. XFS has some sort of reflink support these days but I don't know)
- This isn’t about cloning an image, it’s the full running VM state, including memory.

- Super cool technology, but when cloning entire VMs, one needs to be very careful to not accidentally leak crypto material.
  - If you run server A, give me the copy Server B of it and Alice logs into B, I could log into Server A as Alice. Same thing if we both run copies of the same original VM.

- Very cool. Seems like this could also be great for an integration test runner when the test environment requires a lot of setup. I thought this might use some of the underlying page tracking support for live network migration that nearly every hypervisor has now, but it doesn't seem like they needed it!

- They're using firecracker, which is a KVM-backed VM manager.

- ## 📝 [Why We Replaced Firecracker with QEMU | Hocus Blog _202307](https://hocus.dev/blog/qemu-vs-firecracker/)
- 
- 

- 📝 [Virtualizing Development Environments in 2023 | Hocus Blog _202308](https://hocus.dev/blog/virtualizing-development-environments/)
  - There was no silver bullet we could use to virtualize development environments. VMs are not very memory-efficient, and containers can't isolate all workloads. 
  - Many of our users would not need the virtualization capabilities of VMs, and could save costs by putting more containers on a single machine. 
  - However, Hocus itself depends on low-level kernel features, and can't be fully developed inside a container. We wanted to use Hocus to develop Hocus as soon as we could, so the first version of Hocus uses VMs 🎯. 
  - However, we designed the system in a way that allows us to add container support later.
  - Hocus is a work in progress, a proof of concept, and we want to finish it in collaboration with people who need it.
  - if you're just interested in what we've built so far, you can check out the alpha version on GitHub.

- ## 🤼🏻 [hocus: Why We replaced Firecracker with QEMU | Hacker News _202307](https://news.ycombinator.com/item?id=36666782)
- At CodeSandbox we use Firecracker for hosting development environments, and I agree with the points. Though I don't think that means you should not use Firecracker for running long-lived workloads.
  - We reclaim memory with a memory balloon device, for the disk trimming we discard (& compress) the disk, and for i/o speed we use io_uring (which we only use for scratch disks, the project disks are network disks).
  - It's a tradeoff. It's more work and does require custom implementations. For us that made sense, because in return we get a lightweight VMM that we can more easily extend with functionality like memory snapshotting and live VM cloning.
- Firecracker has a balloon device you can inflate (ie: acquire as much memory inside the VM as possible) and then deflate... returning the memory to the host. You can do this while the VM is running.
  - The first footnote says If you squint hard enough, you'll find that Firecracker does support dynamic memory management with a technique called ballooning. However, in practice, it's not usable. To reclaim memory, you need to make sure that the guest OS isn't using it, which, for a general-purpose workload, is nearly impossible
- Yes, we use this at CodeSandbox for reclaiming memory to the host (and to reduce snapshot size when we hibernate the VM).
- for many mostly "general purpose" use cases it's quite viable, or else ~fly.io~ AWS Fargate wouldn't be able to use it
- A bit disingenuous to make a broad sweeping claim, then have a footnote which contradicts that claim, and upon closer inspection even that claim is incorrect. It's absolutely usable in practice, it just makes oversubscription more challenging.
- That and the fact that this was after "several weeks of testing" tells me this team doesn't have much virtualization experience. Firecracker is designed to quickly virtualize 1 headless stateless app (like a container), not run hundreds of different programs in a developer environment.

- while Firecracker was designed for thing running just a few seconds, there are many places running it with jobs running way longer then that
  - the problem is if you want to make it work with long running general purpose images you don't control you have to put a ton of work into making it work nicely on all levels of you infrastructure and code ... which is costly ... which a startup competing on a online dev environment compared to e.g. a vm hosting service probably shouldn't wast time on
  - So AFIK the decision in the article make sense the reasons but listed for the decision are oversimplified to a point you could say they aren't quite right. Idk. why, could be anything from the engineer believing that to them avoiding issues with some shareholder/project lead which is obsessed with "we need to do Firecracker because competition does so too".
- That being said, firecracker also runs long-running tasks on AWS in the form of Fargate

- yes, it was created originally for AWS Lambda. 
  - mainly it's optimized to run code only shortly (init time max 10s, max usage is 15min, and default max request time 130s AFIK)
  - also it's focused on thin server less functions, like e.g. deserialize some request, run some thin simple business logic and then delegate to other lambdas based on it. This kind of functions often have similar memory usage per-call and if a call is an outlier it can just discard the VM instance soon after (i.e. at most after starting up a new instance, i.e. at most 10s later)

- No mention of Cloud Hypervisor…perhaps they don’t know about it? It’s based in part on Firecracker and supports free page reporting, virtio-blk-pci, PCI passthrough, and (I believe) discard in virtio-blk.
  - We do, and we'd love to use it in the future. We've found that it's not ready for prime time yet and it's missing some features. The biggest problem was that it does not support discard operations yet.

- Fly uses Firecracker, and they host long-running processes. I wonder what's their opinion about it.
  - I think their usecase makes a lot of sense as their workloads consume a predefined amount of ram. As a customer you rent a VM with a specified amount of memory so fly.io does not care about reclaiming it from a running VM.

- I came to the same conclusion as OP. QEMU is the most stable, hackable, well-supported VM hypervisor on the market. Setting it up is a pain, but once you get it set up with all your custom scripts, you never have to do it again. Ever. Even in your next project.

- I know that Firecracker does not let you bind mount volumes, but QEMU does. So, we changed to QEMU from Firecracker. If you run the workloads in Kubernetes, you just have to change a single value in a yaml file to change the runtime. 
  - I would be scared to let unknown persons use QEMU that bind mounts volumes as that is a huge security risk. 
  - Firecracker, I think, was designed from the start to run un-sanitized workloads, hence, no bind mounting.

- don't use virtualization.
  - In this context (the blog post) and the reason firecracker was created, was to isolate workloads.
  - And if youre running untrusted code, then using a virtualized environment is the easiest (id even say best) way to go about it.

- Listen people, Firecracker is NOT A HYPERVISOR. A hypervisor runs right on the hardware. KVM is a hypervisor. Firecracker is a process that controls KVM. If you want to call firecracker (and QEMU, when used in conjunction with KVM) a VMM ("virtual machine monitor") I won't complain. But please please please, we need a word for what KVM and Xen are, and "hypervisor" is the best fit. Stop using that word for a user-level process like Firecracker.

- 
- 
- 

- ## [Firecracker internals: Inside the technology powering AWS Lambda (2021) | Hacker News _202302](https://news.ycombinator.com/item?id=34964197)
- A large part of the Cloud Hypervisor code is based on either the Firecracker or the crosvm project's implementations. Both of these are VMMs written in Rust with a focus on safety and security, like Cloud Hypervisor.
  - The goal of the Cloud Hypervisor project differs from the aforementioned projects in that it aims to be a general purpose VMM for Cloud Workloads and not limited to container/serverless or client workloads.
- They're both built on the same rust-vmm crates, the code is very similar, as are the interfaces. Both very cool projects.

- We're using Firecracker at our company to allow API companies build interactive demos like this one we built for Prisma

- At CodeSandbox we use Firecracker to run our VMs 
- What do you use to build the 'micro' images
  - We created a CLI that creates a rootfs from a Docker image. It pulls the image, creates a container and then extracts the fs from it to an ext4 disk. For the init, we forked the open sourced init from the Fly team
- You guys don't happen to have a public writeup about how this works, do you? Maybe it's as simple as it sounds, but Fly and CodeSandbox both have some magic to turn Docker images into VM disks that I'd like to know how to build
  - Fly is doing fancy stuff to avoid using docker entirely, but with docker you can just run "docker export" to dump an image to a .tar file that contains the whole filesystem. Built-in feature. I use this as a convenient way to grab a foreign platform sysroot for clang cross-compilation; just pick a Docker image and rip the filesystem out.
  - There's been a writeup on this topic by the Fly team -- https://fly.io/blog/docker-without-docker/

- As an old school unix sysadmin that’s aware of the “containers don’t contain”, people ditching proper isolation for containers everywhere for performance reasons has been alarming. now with Firecracker we have isolation and performance.

- I’ve always thought Firecracker would be great for CI runners.
  - This is basically what CodeBuild does.
  - The default Docker containers that CodeBuild uses (you can create your own) and the shell script it uses to parse the yaml configuration file (mostly a list of shell scripts) are all open source and the entire process can be run locally.

- I’ve been playing with Firecracker on a Raspberry Pi 4, but never could get Docker inside a Firecracker uVM to work. Should this be supported at all?
  - Depends how your starting the VM. I’ve run Docker on Firecracker with a Raspberry PI 4 before but it needed some fixes.
  - One possibly is if your running directly from a Initramfs without a block device then docker needs DOCKER_RAMDISK set as a environment variable.

- Any tooling like Docker/Podman to make it as easy to kick off Firecracker VMs as it is to kick off containers?
  - Kata containers https://katacontainers.io/

- ## [csb: We clone a running VM in 2 seconds | Hacker News _202209](https://news.ycombinator.com/item?id=32683834)
- 
- 
- 
- The bit about turning a dockerfile into a rootfs. A docker image is just a tarball of tarballs. We do something like this:
  - you can dump the image using `docker save <name>`. - you can then get a list of the tarballs in this image by extracting this tarball and reading the file manifest.json; Config -> Layers will give you a list of tarballs (see undocker for how to do this: https://github.com/larsks/undocker) - Untar these in a directory and use linux tools to convert this dir to a rootfs.

- also interested in the upper limit of a micro vm, like how big can it get? 64gb memory? not really micro any more and maybe a traditional VM would be a better fit.
  - AWS’s serverless Docker solution - Fargate - based on Firecracker supports up to 30GB of RAM and 4 vCPUs.

- 
- 
- 

- ## [Ignite – Use Firecracker VMs with Docker images | Hacker News _202209](https://news.ycombinator.com/item?id=32990127)
- This is a great idea and something I would love to use, but it's a lot less docker compatible and user friendly than it may seem. 
  - For instance there is no way to automatically run the image's specified command, effectively leaving you with a dead VM
  - You also simply can not share directories with the host (out of scope for Firecracker).
- microVMs for running containers are definitely a great idea; 
  - another project aiming to do it (a little differently) is Kata Containers. 
  - It has a lot more industry support, can also run on Firecracker (though QEMU microVMs are just as good) and can (theoretically, I haven't gotten it to work) interact with many container runtimes that are not Docker (the focus appears to be on Kubernetes).
  - While more powerful, Kata Containers are also much, much more complicated (and honestly under- and misleadingly documented). 

- Firecracker has a number of limitations, however. Firecracker is tailored to the highly vertical 'lambda' use case and too much of the power of the kernel and userspace is stripped away. You can't even live migrate a firecracker VM right now.
  - VMs are great and will ultimately resurge to the detriment of 'everything is a container' serverless orchestration, but Firecracker in its current form won't cut it. 

- Running Docker in a VM is not new at all. This is even how Docker for Windows/Mac works. The GitHub page states that Ignite does more than just "wrapping a container in a VM layer" but I'm not sure how that matters, since the notion of a "container" is purely about configuration. It seems like a distinction without a difference.
  - Docker for Windows/Mac uses a single VM for all your containers. Firecracker/Ignite has a dedicated micro-VM for each container - a completely different architecture, with much better isolation between containers. And the 125ms boot time is not something you get with a typical VM.
  - But I do agree that they don't explain how Ignite is different from "wrapping a container in a VM layer" that Kata/gVisor does.
- Ignite is running a VM per container. Docker for Windows/Mac runs all containers in a single VM.

- ## [Firecracker: Start a VM in less than a second | Hacker News _202101](https://news.ycombinator.com/item?id=25883253)
- 
- 
- 

- ## [如何评价aws开源的firecracker，它对接下来的虚拟机、容器发展方向带来什么变化吗？ - 知乎](https://www.zhihu.com/question/303920344)
- 又一个针对 container 应用场景的轻量级 device model，和别人家最大的不同之一就是为 AWS 做了更好的适配。
  - 利用传统硬件虚拟化的强隔离保护 container 应用并不是一个太新的想法，也是业界一直在尝试的方向之一。稍微远一点的有 hyper.sh，近的有 Kata Containers (The speed of containers, the security of VMs)，更不要说常见的 container 本身就可以直接跑在虚拟机中。
  - 替代 QEMU 的轻量级的 device model 也有不少，例如 Kata Containers 中使用的针对 container 应用场景的追求极限启动速度和低 memory footprint 的 QEMU-lite，针对现代云计算环境的 NEMU (intel/nemu)，以及使用 Rust 开发的 Google Chrome OS 中的 crosvm 
  - 实际上，各大云计算厂商都在或者计划使用 QEMU 以外的 device model 支撑它们的平台。作为最大和技术实力最顶尖的云计算厂商之一，Amazon 在从 Xen 转向 KVM 的过程中，选择在部分业务中使用自研的轻量级 device model 也不是一件令人意外的事情。

- 这是 Serverless（无服务器） 前进的一步，也是开源前进的一步。125ms 启动时间、5 MiB 内存占用的 microVM ，让容器/函数轻易获得隔离性的加持（现阶段容器和函数的安全性还是靠虚拟化了），而 AWS 开源此项技术，表明基础技术的未来还是开源。

- 2年前大家做FaaS的时候，就已经在猜测和追赶AWS在轻量级VM这块的技术。到现在开源，大家已经或多或者形成了类似的技术，例如Kata Container，google gVisor等。 而且在17年逐步形成了一定的影响力。但是Lambda和Fargate已经成为Serverless的事实上的标准的时候，把这项技术开源出来, 一方面是显示AWS本身在serverless infrastructure方面的革新能力，另外一方面也是对逐步火热的轻量级VM技术的统治力的争夺。至于对VM和container技发展方向的变化，我理解变化并不是firecracker带来的，而是Lambda，Fargate等带来的，而这个变化早已经出现。
# discuss-firecracker
- ## 

- ## Docker is not the optimal way to run serverless workloads; hence, AWS Lambda or even an online judge like CodeChef, uses Firecracker as its execution environment.
- https://x.com/arpit_bhayani/status/1852550914638537196
  - This week, I’m reading about Firecracker which is Amazon’s lightweight VM built specifically for serverless applications like AWS Lambda and Fargate. The paper covers how Firecracker supports thousands of short-lived containers and functions on shared hardware without sacrificing security or efficiency.
  - I skimmed the paper once, and it is pretty interesting to understand the story behind how Amazon found the right trade-offs between traditional hypervisors and containers and balanced both really well. 

- It is also interesting to read how Aws  fast load docker containers on lambda. 
- Docker has added lot of features, and continously evolving, abd has become bit heavy, so if you just need containers, then all features are not needed. That's the main reason kubernetes also uses 'containerd' which is mini version of docker, and extracted from docker.
# discuss-runtime-docker
- ## 

- ## 

- ## 
# discuss-kata-containers
- ## 

- ## [Kata Containers: Virtual Machines that feel and perform like containers | Hacker News _202307](https://news.ycombinator.com/item?id=36757688)
- Kata used “Linux kernel Direct Access filesystem (DAX)” to directly share access of the host filesystem to the guest kernel. I thought this was pretty interesting, but it sounds like a possible spot to start a jailbreak. I’m guessing these kinds of optimizations along with using super simple virtualized devices is what gives Kata its almost-cgroups-like performance.

- Is it possible to add kata containers in eks or gke?
  - Not in EKS. EC2 doesn't support nested virtualization today.
- Peer pods are meant to solve this (one day) by running the "containers" (ie VMs) to the side as regular AWS instances and peering the communications
  - AWS already has an implementation of this, namely, Nitro Enclaves. A Nitro Enclave is an isolated VM used for confidential computing purposes. You provide the Enclave an EIF file, which is basically an OCI image with cryptographic measurements. The Nitro hypervisor launches the VM and allows communications with its parent VM only over a Linux vsock connection.
  - Also, AWS has Fargate, which is basically containers-as-VMs. Every ECS task or EKS Pod is launched as a separate EC2 instance under the hood. This obviates a lot of the need for a solution like Kata there.

- So why would you use this over regular containers? Is this for people who think containers are insecure?
  - Containers are not appropriate for some scenarios. If your threat model is "attacker has arbitrary code execution" you should be very wary of a container holding them for long - you're one kernel privesc away from a container escape.
  - By contrast, running attacker code in Firecracker is much safer - for one thing, the attacker needs to escalate within the VM in order to then expose the necessary primitives to then escape the VM. So it immediately adds an additional required vuln. But also, instead of the entire Linux kernel being the attack surface (it is for the first vuln, but...) you have to attack a much smaller codebase that implements the VM.

- ## [Kata Containers: The speed of containers, the security of VMs | Hacker News _202310](https://news.ycombinator.com/item?id=37762380)
- What I don't like about Docker is that it spews stuff all over the place. After installation, it is constantly running.
  - I was on a train in Germany recently and could not use the Wifi because of that. Turned out the docker daemon occupied the IP range the Train Wifi uses. While I was not using docker at all.
- Podman is probably close to what you want. It runs "daemonless" - while no containers are running, podman doesn't have a running process either. Also, as long as the containers are run in rootless mode, podman creates no virtual network interfaces. Rootless Podman makes use of network namespaces instead to separate the processes in the container from the host network. Processes on the host cannot see Podman's network namespaces and therefore are completely unaffected by any IP configuration therein.
- Podman is what Docker should have been, for me. Security first, no daemon, more Linux-like behavior (You can manage them with SystemD unit files if you wish) and it supports the same, usual container images you build/use with Docker. The main part it was lacking is the compose equivalent, but that too is coming along.
- You can use docker-compose with podman using podman's docker compatibility API.

- Is it coming along? Last I saw they were moving away from the compose Schema to a k8s manifest and... Those are absolutely disgusting.
- Podman has docker-compatible CLI, Dockerfiles and even docker-compose compatibility. It won't be as painful as you worry. So just give it a try. And besides the advantages already mentioned (rootless, no-daemon and isolated network namespaces), podman has some additional nifty features like pods (like in K8s), quadlets (containers managed by systemd), compatibility with k8s manifests, etc.

- Isn’t podman just IBMs version of docker?

- We use Kata Containers to create Firecracker VMs from Kubernetes. Works really well for us. Though I am hoping there will be a more specific solution for Firecracker, as we don't need any other runtimes (which kind of ruins the purpose of Kata).

- Is there a good reason why kata containers don't seem widely adopted?
  - TBH their docs aren't that great. There should probably be a 'curl | sh' solution to install it at the top of the readme followed by a `<run this command and you're in an ubuntu shell in kata!>` command right after.
  - Another issue is the lack of nested virtualization in EC2 instances that aren't the very expensive i3 metals. That turns this from a "it's a drop in replacement" to "I'm spending thousands of dollars on this".
- The proposed solution to the nested virtualization problem (apart from somehow persuading Amazon to switch that on) is something called peer pods, where the containers run in separate AWS instances. Arranging the traffic between the peer pods and the instance which is acting as host is quite challenging and I've never seen this successfully deployed in production

- Amazon’s Firecracker, another project with similar goals, has seen a lot of adoption however.
  - To add, firecracker is an alternative to qemu like katacontainers are an alternative to containerd or runc. But both focus of security by isolation, as you mentioned.

- "Like VMs but containers" doesnt tell me anything
  - By running the containers in VMs, and attempting to make the VMs boot very quickly by carefully tuning qemu (or Firecracker) and the guest kernel. The main problem with this approach is surprisingly not the time overhead - Kubernetes is fscking slow at scheduling regular containers - but the memory overhead, since you need to allocate sufficient memory up front for the largest possible memory usage of the container. Most containers expect to get more memory from the system simply by doing sbrk/mmap, and VMs simply don't work this way.

- LXC does it better, you can even have virtualization
  - The difference here is that katacontainers are OCI and CRI complaint - meaning that it can immediately be used with K8s, Nomad and possibly others. You get all the features of these orchestration platforms. LXC doesn't have that (it actually predates OCI and CRI).
  - There are other orchestration systems that can use LXC - LXD, libvirt, Proxmox, and may be others. Also, LXC doesn't have traditional virtualization - that's a feature of LXD using KVM. (Do you mean system containers, as opposed to regular app containers?)
# discuss
- ## 

- ## 

- ## 
