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

# discuss-wasm/wasi
- ## 

- ## 

- ## [Kubernetes reinvented virtual machines in a good sense | Hacker News _202207](https://news.ycombinator.com/item?id=32298058)
- "Containers" are just a pattern, the real technology behind it is kernel namespaces (plus ordinary process boundaries). (For that matter container security is still half-baked in many ways. The kernel namespacing has been added after-the-fact and it can't really be trusted to make an effective "sandbox" on its own.)

- I know most configurations don't use it, but k8s supports different runtimes and today you can use Kata or firecracker to run each pod in it's own "microvm."
  - You then get the security benefits of a "real" VM while still distributing your software as an OCI (Docker) container, and can operate it like any other k8s cluster.
- Launching a container is implementation detail for Kubernetes. I could totally see Kubernetes which runs some pods in containers and some pods in VMs with tiny kernel. May be it even exists, I'm too lazy to google it.

- Did JVM reinvent VM? Is it a VM or a container?
  - No one (not enough people?) asked (cared?) for this about the JVM for like 25 years till Linux Cgroups came around and Docker capitalized on it. Its not VM v/s container question that we care about. (I am aware this is a very poor comparison but so is comparing a vm to a container, which is my point)
  - K8S brings complexity yes, and in a consistent, predictable way. The biggest difference between a k8s based shop vs a DIY VM/Container shop is the former can (in theory) hire some people with intermediate K8S experience, and have them sort out the mess that the people without that experience (or more typically the ones who don't have clear requirements) may have created. With k8s it becomes more predictable to find the boundaries and start pulling things apart in production and make incremental changes. Without k8s, making changes to a production setup is a nightmare that folks who have done that sort of thing don't ever want to repeat.

- ## [WASIX, the Superset of WASI Supporting Threads, Processes and Sockets | Hacker News _202305](https://news.ycombinator.com/item?id=36126032)
- I think server side WASM has the potential to be the next thing after containers.
- Since I've been web applications and distributed systems, the evolution has been something like this.
  1. Copy files around, into the web or application servers directory. This was simple but isolation, repeatability and testability was hard. The application dependencies were directly tied to the host, so you had to be very careful about your upgrades breaking applications. The lack of isolation is not suitable for multi-tenant environments for security and capacity planning reasons. It's pretty hard to run multiple-applications
  2. Things like bundler, and other language specific tools that let you bundle your application dependencies together. Avoids some of the host OS related upgrade issues, but again, no real isolation.
  3. VMs. The whole cloud industry started on this. You get true isolation of your whole application at the cost of complexity and weight. Scheduling new VMs is not a fast process because you're copying around or at least booting a whole OS. You still have to manage OS images. There is also generally a tax on memory that you have to pay, so you waste some resources with VMs to get the isolation. Amazon invested in Nitro to avoid paying a lot of this tax.
  4. Containers. Lighter than VMs, good enough isolation in a lot of cases, especially inside of an organization. Lower tax than VMs. More testable. But containers are still fairly heavy, startup time can be slowish. So you have some limitations on how fast you can scale up and down in response to load. Also isolation isn't good enough for some workloads. So we see things like firecracker VMs being used to improve isolation.
  5. Wasm on the server side. Much lighter than containers. Less memory overhead, way less startup time. Probably faster startup time than even firecracker. So for lambda like workloads you could could have a lot better cold start latency. You probably have good enough isolation that you don't need to resort to things like firecracker to isolate customer workloads. Because of the fast startup time you could probably pack your long tail of workloads even tighter to get better effective utilization out of your server infrastructure.

- Excited for threads, sockets, futexes, but not excited for fork, signals and setjmp. They didn't include POSIX stuff like shared memory, select(2), unix sockets, and had to draw a line somewhere. Why include error-prone cruft?
- A few points there:
  - A big goal here is to make existing software compile to Webassembly, with only a relatively small amount of changes.
  * classical shared memory (mapped into the main address space) is very hard to do in the context of Webassembly, especially in a performant way. Not impossible, but complicated. It would be valuable to add, but there are different approaches as well (like sharing additional Webassembly-level memories between instances, for example)
  * WASI already has a concept similar to select
  * unix sockets would be a pretty straight-forward addition

- WASI is not meant for browsers, it's for using WebAssembly as platform-independent bytecode in non-browser environments.
# discuss-cloud-env
- ## 

- ## 

- ## [Cloud, why so difficult? (2022) | Hacker News _202306](https://news.ycombinator.com/item?id=36488733)
- Cloud is difficult because it stiched together from fragments of old applications and approaches.
  - Cloud will be easy with consistent approach. One or very few languages for everything, from configuring resources, to configuring policies and writing code.
  - Cloud will be easy with opinionated tooling. No Dockerfile and supporting of miriads languages. Just file with dependencies and folder with source code.
  - Cloud will be easy with opinionated approach to configuration. No need to support PASSWORD env, PASSWORD_FILE env, some secret access service. Only one secure and simple way.

- 
- 

- ## [Cloud desktops aren't as good as you'd think | Hacker News _202210](https://news.ycombinator.com/item?id=33106234)
- Latency for every keystroke, your brain starts to add latency to latency that is not there to compensate for a life lived wearing citrix latency goggles.

- Nothing beats working directly on a fast but quiet workstation sitting next to my table.

- With cloud gaming you can stream 4K games at 60FPS, with clarity and quality for fast moving objects.
  - Why does remote desktop still shit itself when I move around MS Word with a few pictures?

- 
- 

# discuss-runtime-vm
- ## 

- ## 

- ## 

- ## 🚀🧊 I'm excited to launch Arrakis: an open-source and self-hostable sandboxing service designed to let AI Agents execute code and operate a GUI securely. _20250403
- https://x.com/abshkbh/status/1907480355529203809
  - AI agents become incredibly capable when given access to a full Linux VM environment.
  - Self-hostable: Run it on your own infra or Linux server.
  - Secure by Design: Uses MicroVMs for strong isolation between sandbox instances.
  - Snapshotting & Backtracking: First-class support allows AI agents to snapshot-and-restore a running sandbox.
  - Ready to Integrate: Comes with a Python SDK py-arrakis and an MCP server arrakis-mcp-server out of the box.
  - Customizable: Docker-based tooling makes it easy to tailor sandboxes to your needs.

- When's the typescript SDK dropping?
  - One of the top things on my plate. But it has a REST API so you can use whatever for the time being.

- firecracker support when? Also, any guide on how to deploy it?
  - Arrakis uses `cloud-hypervisor` underneath. Both Firecracker and chv are based on `crosvm`.
- 🆚 any reason why you chose hypervisor over firecracker?
- When I started the project -
  1. Chv had stable snapshot/restore support. Firecracker didn't
  2. Hotplugging of memory that I thought would help with memory management
  3. I didn't want to be at the mercy of Amazon close sourcing Firecracker

- I can't really deploy your project on aws because EC2 doesn't support virtualization
  - Yes, exactly why I also went with GCP/GCE. AWS does have a bare metal offering, it's just expensive.

- ## same.dev literally hosts a vm for your project
- https://x.com/aidenybai/status/1901019106234732938
  - you get basically a full agent + operating system (which you can play doom / minecraft on if you want)

- surely it's docker; no way youre giving 32gb ram vms to agents lol
  - docker
- interesting that you didn’t go for a pre-made solution like e2b or scrapy though
  - figured we can just built it ourselves at 50% the costs

- Few crypto miners and your AWS account is cooked, just fyi
- Can't wait for you to see your first AWS bill

- ## 👷🏻 I 100% agree with this. We needed an orchestrator that understands VM snapshotting/cloning and can spin up a new VM extremely quickly.
- https://x.com/CompuIves/status/1853478202569617647
  - We tried different solutions, but ultimately we had to build our own because nothing fit the bill.
  - This was also a big challenge for us, so we had to customize how VM snapshots are created and loaded.

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
- 👷🏻 At CodeSandbox we use Firecracker for hosting development environments, and I agree with the points. Though I don't think that means you should not use Firecracker for running long-lived workloads.
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
# discuss-e2b-sandbox
- ## 

- ## 

- ## 

- ## We run close to 1 million sandboxes a day _20250314
- https://x.com/mlejva/status/1900275519943282781
  - It's not so long ago that running this many sandboxes took us a month

- ## [Notes on the new Claude analysis JavaScript code execution tool | Hacker News _202410](https://news.ycombinator.com/item?id=41943662)
- That's an interesting idea to generate javascript and execute it client side rather than server side. I'm sure that saves a ton of money for Anthropic not by not having to spin up a server for each execution.
  - I imagine this is a broader push to be able to have Claude pilot in your browser (and other applications) in the future. This is the right way to go about it versus having a headless agent: users can be in the loop and you can bootstrap and existing environment.
  - Otoh it’s going to be a security nightmare.

- Google Collab are all individual VMs. It seems Anthropic doesn’t want to be in the “host a VM for every single user” business.

- 🤔 I've been trying to figure out the right pattern for running untrusted JavaScript code in a browser sandbox that's controlled by a page for a while now, looks like Anthropic have figured that out. Hoping someone can reverse engineer exactly how they are doing this - their JavaScript code is too obfuscated for me to dig out the tricks, sadly.
  - The key is running the untrusted code in a cross-origin iframe so you can rely on the same-origin policies and `sandbox`.
  - You can control the code in a number of ways - loading a trusted shim that sets up a postMessage handler is pretty common. You can be careful and do that in a way that untructed code can't forge messages to look like their from the trusted code.
  - 💡 Another way is to use two iframes to the untrusted origin. One only loads untrusted code, the other loads a control API that talks to the trusted code. You can then to the loading into the iframe with a service worker. This is how the Playground Elements work (they're a set of web components that let you safely embed a mini IDE for code samples) https://github.com/google/playground-elements
- The cross origin iframe method is the same I’ve employed in A few browser extensions I’ve built

- You should check out how Figma plugins work. They have blog posts on all the tradeoffs they considered. What I believe they settled on was a JS interpreter compiled to WASM -- it can run arbitrary JS but with very well-defined and restricted interfaces to the outside world (the browser's JS runtime environment).
  - > We now use QuickJS, a JavaScript VM written in C and cross-compiled to WebAssembly.

- Much easier in the browser that has V8 isolate, however even with webworkers you still want to control CPU/network hijacking which is not ideal.
  - If it's only the user's own code it's fine but if they can run code from others it's a massive pain indeed.
  - On the server it's still not easy in 2024, even with Firecracker (doesn't work on mac), Workerd (is a subset of NodeJS),  `isolated-vm` (only pre-compiled code, no modules).

- What are the attack vectors for a web browser js environment to do malicious things? All browser code is sandboxed via origin controls, and process isolation. It can’t even open an iframe and read the contents of that iframe.
  - It's a fine place to run code trusted by the server (or code trusted by the client within the scope of the app).
  - But for code not trusted by either, it's bad -- user data in the app can be compromised/exfiltrated.
  - Hence for third-party plugins for a web app, the built-in JS runtime doesn't have sufficient trust management capability.

- duckdb-wasm would be a good addition here. We use it in Definite and I can't say enough good things about duckdb in general.

- ## [Show HN: Riza - Safely run untrusted code from your app | Hacker News _202404](https://news.ycombinator.com/item?id=40159630)
  - we’ve been working on Riza (https://riza.io), a project to make WASM sandboxing more approachable. We’re excited to share a developer preview of our code interpreter API with HN.
  - The Riza Code Interpreter API is an HTTP interface to various dynamic language interpreters, each running inside a WASM sandbox without access to the outside world (for now). We modeled the API to align with a POSIX shell-style interface.

- Been using Riza for the past few months at our startup for executing code generated by GPT4.
- We use it for local dev, running model eval (when changing prompts), in CI and production work loads.
  - It's the easiest to setup. It took us just a few minutes to execute our first function call.
  - Multiple languages support - we use both JS and Python for code generated by LLM , Riza works great with both out of the box.
  - No cold start - this is important because latency matters in our product.
  - No infra management - even if we use AWS lambda or similar serverless product we felt like we still needed to a bunch of setup to make sure its fast + secure.

- ## [Spin 3.0 – open-source tooling for building and running WASM apps | Hacker News _202411](https://news.ycombinator.com/item?id=42118496)
- everything, including the infra is open-source (below), but it currently requires more than just your laptop (gcp, nomad, firecracker, postgres, etc.)
  - this way, we're able to run millions secure sandbox environments

- GCP supports nested virtualisation

- wasmtime works as long as you make sure to include the lib directory
  - This is just a limitation of the wasmtime CLI. The full Rust API let's you mount filesystems as read-only. Not sure why it's not exposed as an argument.

- WASM is basically similar to JVM bytecode. So the comparison would be like using compiled code from Java, Scala and/or Kotlin for example. The source language only determines how the code is expressed in WASM and whether or not it also needs to bundle / compile-in some runtime code baggage for it to work.

- I develop the Scala-to-Wasm compiler, and also maintain the JVM backend of Scala. I can tell you that Wasm is very different from JVM bytecode.
  - The fundamental difference is that the JVM bytecode has an object model. When they talk to each other, Java, Scala and Kotlin do so at the abstraction level of the JVM object model. You can directly call methods between them because virtual dispatch of methods is a concept with semantics in the bytecode.
  - There's no such thing in Wasm, even with the GC extension. You get structs and arrays, but nothing like methods. If you want virtual dispatch, you encode it yourself using your own design of virtual method tables. That means Java, Scala and Kotlin, despite all having their Wasm GC backend at this point, cannot call each other's methods in Wasm.

- https://news.ycombinator.com/item?id=38712521
  - Our sandboxes are isolated microVMs (Firecrackers) that you can quickly spawn (~1s) and control with our SDK. It's like a playground for AI agents.

- [Ask HN: AI agent devs, how do you sandbox LLM generated code? | Hacker News](https://news.ycombinator.com/item?id=42132329)
  - There are a few tools here like e2b and modal 

- ## [Show HN: Desktop Sandbox for Secure Cloud Computer Use | Hacker News _202410](https://news.ycombinator.com/item?id=41938888)
  - We're using Firecrackers to power our sandboxes. Funnily enough, we had this repo sitting on our GitHub for about 6 months. We originally made this for one of our customers because they were running evals on the desktop-like environment with GUI for their model.
  - You can use PyAutoGUI to control the whole environment programmatically.
  - The desktop-like environment is based on Linux and Xfce at the moment. We chose Xfce because it's a fast and lightweight environment that's also popular and actively supported. However, this Sandbox template is fully customizable and you can create your own desktop environment.

- We are building a similar thing but with Windows environments. If you need Windows, shoot me an email to victor+borg.games No public SDK yet, but our client is a fork of old Parsec codebase. It is relatively straightforward: you connect using WebRTC, and send your actions over a datachannel.

- ## [Show HN: Open-source SDK for creating custom code interpreters with any LLM | Hacker News _202404](https://news.ycombinator.com/item?id=40093257)
  - The way our code interpret SDK works is by spawning an E2B sandbox with Jupyter Server. We then communicate with this Jupyter server through Jupyter Kernel messaging protocol 
- I have something similar but with a different philosophy. Basically, a docker container running and you can execute code against with ability to set timeouts, auto install and uninstall dependencies and a bunch of other cool stuff. The pain point of all of this is dependencies and making sure someone doesn’t use your infrastructure to DDOS other folks.  And crypto mining!

- Another challenge is how to make the whole product cost efficient for our users. You don't want them to pay for idle sandboxes running on E2B but only when they actually need them for serverless execution. Firecracker and its snapshots are really helpful with this.

- ## [e2b - Show HN: We are building an open-source IDE powered by AI | Hacker News _202304](https://news.ycombinator.com/item?id=35440552)
  - Our new project - e2b - is using some of the technology we built for Devbook in the past. Specifically the secure sandbox environments where the AI agents run are our custom Firecracker VMs that we run on Nomad.

- I have question for these AI powered editors: what advantage would a dedicated editor like this have over just using an AI plugin for VsCode? How do you fundamentally build the editor differently if you are thinking about AI from the ground up?
  - Our editor isn't a regular coding editor. You don't actually write code with e2b. You write technical specs and then collaborate with an AI agent. Imagine it more like having a virtual developer at your disposal 24/7. It's built on a completely new paradigms enabled by LLMs. This enables to unlock a lot of new use cases and features but at the same time there's a lot that needs to be built.

- I built this https://github.com/campbel/aieditor to test the idea of programming directly with the AI in control. Long story short, VS Code plugin is better IMO.

- My biggest concern with tools like this is reproducibility and maintainability. How deterministically can we go from the 'source' (natural language prompts) to the 'target' (source code)? Assuming we can't reasonably rebuild from source alone, how can we maintain a link between the source and target so that refactoring can occur without breaking our public interface?

- 
- 
- 

# discuss-firecracker
- ## 

- ## 

- ## 

- ## [ForeverVM: Run AI-generated code in stateful sandboxes that run forever | Hacker News _202502](https://news.ycombinator.com/item?id=43184686)
- 🔒 why are you allowing network requests in the VM? (Tested in the python REPL which is available on your homepage) What are you doing to prevent the abuse?
  - We allow outgoing requests because a common use case of ForeverVM is making API calls or fetching data files.
  - We give every repl its own network namespace and virtual ethernet device. We also apply a set of firewall rules to lock it out from making non-public-internet requests.

- Does this use CRIU? https://criu.org/Main_Page
  - I don't think so. This looks like to be using an actual VM instead of container tech.

- 🤔 It’s trivial to build something that does what this describes. I’m sure there’s more too it, but based on the description the pieces are already there under permissive open source licenses. 💡 For a clean implementation I’d look at socket-activated rootless podman with a wasi-sdk build of Python.
  - It was an afternoon to prototype, followed by a lot of work to make it scale to the point of giving everyone who lands from HN a live CPython process
- This is the sort of thing that would touch a lot of my data so I’d much prefer to have it self hosted but you mention Claude rather than deepseek or mistral so know your audience I guess.
  - Fair enough. Our audience is businesses rather than consumer, so our equivalent to self-hosting is that we can run it in a customer's cloud.
  - We mention Claude a lot because it is a good general coding model, but this works with any LLM trained for tool calling. Lately I've been using it as much with Gemini Flash 2.0, via Codename Goose.
- Is it possible to run cython code with this as well? Since you can run a setup.py script could you compile cython and run it? Looking at the docs, it seems only suited for interpreted code
  - We are working now on support for arbitrary imports of public packages from PyPi, which will include cython support, but only for public pypi packages. Soon after that we'll be working on a way to provide proprietary packages (including cython).

- I tried to do this myself about ~1.5 years ago, but ran into issues with capturing state for sockets and open files (which started to show up when using some data science packages, jupyter widgets, etc.)
  - Good insight! We also initially tried to use Jupyter as a base but found that it had too much complexity (like the widgets you mention) for what we were trying to do and settled on something closer to a vanilla Python repl. This really simplified a lot.

- 🆚️ How is this different than chatgpt's python code execution?
  - ChatGPT's code interpreter is mostly used as a calculator / graphing calculator. It can run arbitrary Python code, but it is limited in practice because it can't (e.g.) make external web requests or install arbitrary packages.

- Fun fact: this is very similar to how Smalltalk works. Instead of storing source code as text on disk, it only stores the compiled representation as a frozen VM. Using introspection, you can still find all of the live classes/methods/variables. 
  - Is this the best way to build applications? Almost assuredly not. But it does make for an interesting learning environment, which seems in line with what this project is, too.

- it swaps idle sessions to disk, so that they don't consume memory. From what I read, apparently "traditional" code interpreters keep sessions in memory and if a session is idle, it expires. This one will write it to disk instead, so that if user comes back after a month, it's still there.

- Is it possible to reuse the same paused VM multiple times from the same snapshot?
  - Check out why Togerther. AI acquired CodeSandbox.

- The API could be used for non-AI use cases if you wanted to, but it’s built to be integrated with an LLM through tool calling. We provide an MCP (model context protocol, for integration in Claude, Cursor, Windsurf etc.) server.

- ## [Fast CI with MicroVMs | Hacker News _202211](https://news.ycombinator.com/item?id=33656767)
- Firecracker is nice but still very limited to what it can do.
  - My gripe with all CI systems is that an an industry standard we've universally sacrificed performance for hermeticity and re-entrancy, even when it doesn't really gives us a practical advantage. Downloading and re-running containers and vms, endlessly checking out code, installing deps over and over is just a waste of time, even with caching, COW, and other optimizations.
- The perceived practical advantage is the incremental confidence that the thing you built won't blow up in production.
  - Many CI systems do employ caching. For example, Circle.

- Hermeticity is precisely what allows you to avoid endlessly downloading and building the same dependencies. Without hermeticity you can't rely on caching.

- 

- ## 🤔 [Deno raises $21M | Hacker News _202206](https://news.ycombinator.com/item?id=31827387)
- Lambda and Fargate use the Firecracker VM
  - The Lambda service team always emphasizes the level of isolation that Firecracker VMs gives you that containers don’t.

- And Google Cloud Run use gVisor, which is also not a container.

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

- ## 🆚️ [Ask HN: Pros and cons of V8 isolates? | Hacker News _202206](https://news.ycombinator.com/item?id=31740885)
  - I was reading this article on Cloudflare workers https://blog.cloudflare.com/cloud-computing-without-containe... and seemed like isolates have significant advantage over serverless technology like lambda etc.
  - What are the downsides of v8? Is it poor security isolation?

- The downside of v8 isolates is: you have to reinvent a whole bunch of stuff to get good isolation (both security and of resources).
  - Here's an example. Under no circumstances should CloudFlare or anyone else be running multiple isolates in the same OS process. They need to be sandboxed in isolated processes. Chrome sandboxes them in isolated processes.
  - Process isolation is slightly heavier weight (though forking is wicked fast) but more secure. Processes give you the advantage of using cgroups to restrict resources, namespaces to limit network access, etc.
  - My understanding is that this is exactly what Deno Deploy does (https://deno.com/deploy).
  - Once you've forked a process, though, you're not far off from just running something like Firecracker. This is both true and intense bias on my part. I work on https://fly.io, we use Firecracker. We started with v8 and decided it was wrong. So obviously I would be saying this.
  - Firecracker has the benefit of hardware virtualization. It's pretty dang fast. The downside is, you need to run on bare metal to take advantage of it.
  - My guess is that this is all going to converge. v8 isolates will someday run in isolated processes that can take advantage of hardware virtualization. They already _should_ run in isolated processes that take advantage of OS level sandboxing.
  - At the same time, people using Firecracker (like us!) will be able to optimize away cold starts, keep memory usage small, etc.
  - The natural end state is to run your v8 isolates or wasm runtimes in a lightweight VM.

- The future of compute is fine-grained. Cloudflare Workers is all about fine-grained compute, that is, splitting compute into small chunks -- a single HTTP request, rather than a single server instance. This is what allows us to run every customer's code (no matter how little traffic they get) in hundreds of locations around the world, at a price accessible to everyone.
  - The finer-grained your compute gets, the higher the overhead of strict process isolation gets. At the point Cloudflare is operating at, we've measured that imposing strict process isolation would mean an order of magnitude more overhead, in terms of CPU and memory usage. It depends a bit on the workload of course, but it's big. Yes, this is with all the tricks, zygote processes, etc.
  - We have plenty of defense-in-depth that we can do instead of process isolation, that doesn't have such enormous cost.

- > containers aren't a mechanism to increase compute granularity
  - Yes they are. Instead of thinking in terms of a whole running operating system with dozens of services, now you are thinking in terms of individual (micro?)services that are relatively isolated from each other. We stuff a lot more containers per box than we used to stuff VMs per box.
  - But it's true containers (of the namespace/cgroup/seccomp variety) have failed to be a sufficiently secure isolation mechanism to use them for multi-tenant scenarios, so instead we mostly pack containers from the same owner together.
  - I'd sort of argue that Firecracker and gVisor are actually container engines that happen to use CPU features meant for hardware VMs for additional security hardening. The granularity of compute that you put in them is more container-ish than traditional VM-ish.

- Answering the security question specifically: v8 is a runtime and not a security boundary. Escaping it isn't trivial, but it is common. You should still wrap it in a proper security boundary like gVisor.
- V8 is still very hard to escape -- an escape is a remote hole in Chrome isn't it? To be honest, I'm happy to base my security on "as safe as Chrome".
  - 💡 Chrome runs each origin in a different process. Chrome also runs all the privileged code in separate processes, so like file, network, GPU, and many OS calls are not actually happening from within the same process as v8 executing web JS code. Process isolation is also necessary to mitigate CPU and OS level timing attacks between origins (and the privileged process).
  - v8 is a pretty good security boundary, but to be as secure as Chrome you need the other layers too.

- 🐛 We did pretty much the same thing as Cloudflare does for workers in the Parse Cloud Code backend many years ago--when possible, we ran multiple V8 isolates in the same OS process. There are certain issues we ran into:
  - Security-wise, isolates aren't really meant to isolate untrusted code. That's certainly the way Chrome treats them, and you would expect that they would know best. For instance, if you go to a single webpage in Chrome that has N different iframes from different origins, you will get N different Chrome renderer processes, each of which contain V8 isolates to run scripts from those origins.
  - Isolation is not perfect for resources either. For instance, one big issue we had when running multiple isolates in one process is that one isolate could OOM and take down the all the isolates in the process. This was because there were certain paths in V8 which basically handled hitting the heap limit by trying to GC synchronously N times, and if that failed to release enough space, V8 would just abort the whole process. Maybe V8 has been rearchitected so that this no longer occurs.
  - Basically, the isolation between V8 isolates is pretty weak compared to the isolation you get between similar entities in other VMs (e.g. Erlang processes in the BEAM VM). And it's also very weak when compared to the isolation you get from a true OS process.
- > isolates aren't really meant to isolate untrusted code.
  - They totally are meant for that. That's arguably the main thing they are designed to do. The fact that people add defense-in-depth layers on top of it doesn't mean that the first layer isn't expected to be effective.

- wasm has its place, especially for contained workloads that can be wrapped in strict capability boundaries compile-time (think, file-encoding jobs that shouldn't access anything else but said files)
- > Containers are still the defacto standard.
  - afa FaaS is concerned, wasmedge [0], atmo [1], tarmac [2], krustlet [3], blueboat [4] and numerous other projects are turning up the heat

- 🤔 Containers do not provide sufficient isolation to run untrustedd binaries. That's why aws built and uses firecracker for lambda.
  - VMs are also full of side channels. Depending on how much isolation is a concern, you need to own the host.
  - I don't trust VMs particularly more than containers in this respect: Containers have a lot of attack surface, but VMs also have a lot of complicated in the code in the kernel, in addition to having complicated emulated device drivers and a large silicon-based attack surface.

- There is also an issue of compatibility.
  - Underneath the hood other serverless technologies like lambda are running lightweight VMs running linux. Therefore they can easily accept any linux compatible container and they can run it for you in a serverless way.
  - Cloudflare Workers are running modified Node.js runtimes. You can only run code that is compatible with their modified Node.js runtime. For Cloudflare to be able to offer a product that runs arbitrary linux compatible containers they would have to change their tech stack to start using lightweight VMs.
  - If you want to run Node.js, then Cloudflare Workers probably works fine. But if you want to run something else (that doesn't have a good WASM compatibility story) then Cloudflare Workers won't work for you.

- The JVM has a similar feature since in the early 2000s. I don't know how popular it was in Java's heydays, but it doesn't seem used today. Being tied to a handful of languages may have been an issue.
  - As far as I know, the JSR-121 proposal was never actually implemented (or if it was, it was never publicly released). The OpenJDK issue is marked as "Won't Fix".
  - Not really a surprise after the `SecurityManager` was not very successful in managing security. It turned out to be a huge undertaking and a constant burden.
- Sounds similar to . Net's AppDomains which were deprecated in . Net Core

- 🤔 if a process is running multiple Isolates simultaneously, they're multi threaded and still require context switching? (accepted, thread switches are less resource intensive than process switches). Interestingly when Chrome runs on Windows desktops it seems to allocate separate processes for each Isolate anyway, but I'm guessing this is not baked into V8?
  - Thread switching is much cheaper than process switching.
  - Threads are just stacks. Processes are whole address spaces. All kinds of caches need to be flushed when you switch processes (especially if you have more processes than you have PCID entries), but not when switching threads.

- For me, Cloudflare's decision to go with V8 Isolates was really smart and that blog post is a brilliant explanation of how one looks at trade-offs in engineering. Truly amazing work.
  - That said, no I don't believe V8 Isolates are the future of computing - and I think I'll explain why by comparing it to shared PHP hosting.
  - PHP became so big because it solved something that was very important for a lot of people 
  - If you deployed Python, your app would be running the whole Python stack just for you. You'd need resources for a python interpreter, all the HTTP libraries, all your imports, and then your code. 
  - On the other hand, if you ran PHP, you'd be sharing the PHP interpreter, the PHP standard library (which was written in C and not in PHP), and the server would only need to run your code. If your code was basically `mysql_select($query); foreach ($result in $results)...`, then the server was executing basically nothing. All the hard work was in C and all the request/response stuff was in C and all of that code was being shared with everyone else on the box so there was almost not RAM usage.
  - V8 Isolates are similar in a lot of ways. You get to share the V8 runtime and pay its cost once and then just run the code needed for the user. It makes sharing space really good.
  - So how isn't this the future? Not to knock PHP, but PHP isn't dominating the world. Most of the time, you're working at a place you have services that will be getting consistent traffic and you can put lots of endpoints into a service and you just run that service. There are things like having well-JIT'd code that can be good with long-running processes, you can use local caches with long-running processes, you pay the startup costs once (even if they might be tiny in some cases).

- Does dart isolate have any similarity to this ?
  - Would say, super generally and speaking loosely, yes: simply because I knew "isolate" from Dart, not V8, and didn't miss a beat with the article: in a sense, I'm surprised find the exact same concept in V8. I assume it was in V8 first, IIRC Dart/Flutter started from Chrome.

- 🆚️ It seems to me that WASM is clearly a better suited technically as the core runtime of the future for serverless platforms... but the question is are isolates the VHS and WASM the Betamax in this story?
  - They're not comparable in that way. WASM runs inside a v8 runtime environment (or in other places), I'm pretty sure you can run wasm inside an isolate. You can basically think of WASM and JS as two different interpreters you can run inside of V8's little mini operating system.
- Actually that's incorrect, there are a number of wasm runtimes that don't use v8. Here's links to a couple: wasmtime, fastly-edge-compute
