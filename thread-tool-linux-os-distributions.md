---
title: thread-tool-linux-os-distributions
tags: [archlinux, fedora, linux, rhel, ubuntu]
created: 2026-06-18T14:27:12.276Z
modified: 2026-06-18T14:27:48.210Z
---

# thread-tool-linux-os-distributions

# guide

- tips
  - 很多vps厂商提供的reinstall选项里面没有arch， 只支持主流的ubuntu/debian/rhel/rocky
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-linux-ai
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Any Linux distro better than others for AI use? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1oh079j/any_linux_distro_better_than_others_for_ai_use/)
  - I’m choosing a new Linux distro for these use cases:
  - Running “power-user” AI tools (e.g., Claude Desktop or similar)
  - Local LLM inference - small, optimized models only

- I'd suggest a distro that CUDA officially supports, so heres the options: 
  - debian, ubuntu
  - fedora, opensuse, rhel, rocky
  - wsl-ubuntu, oracle-linux, azure-linux, kylinos

- Nvidia put the DGX Spark out with Ubuntu. So while there are plenty of options, seems like it could have the least level of effort.

- As I understand it, CUDA support on Arch is great although there may be some edge scenarios where official support from Nvidia may matter.

- I am always using Ubuntu, just because it is common and most things are working OOB. Nvidia drivers are Ubuntu first. Although other distros are listed, it often takes time until they get their support.
  - Furthermore everything should/could be used in a containerized way. Docker/Podman/Toolboxes are freeing you from many issues.
- Mint has no snap.

- Why fedora? Debian based stuff is much less obtuse. Redhat is the microsoft of linux.

- I like Fedora, but it has a lot of annoying issues with NVIDIA that you have to fix before it's usable. 42 broke suspend for me, and I still haven't been able to figure out why...

- you probably want ubuntu so you don't have to translate any install instructions. since everyone in academia and in foss is working on or supporting Ubuntu

- ## [What's the difference between Nvidia DG Spark OS and Ubuntu + CUDA dev stack? : r/LocalLLaMA _202510](https://www.reddit.com/r/LocalLLaMA/comments/1of6m7q/whats_the_difference_between_nvidia_dg_spark_os/)
- DGX OS has a custom Linux kernel.
  - I haven't tried Ubuntu (what's the point if DGX OS is based on Ubuntu 24.04?), but I tried Fedora 43 Beta, and was able to install it and get CUDA working - compiled llama.cpp and successfully ran it, but there are a few issues that need to be solved:
  - Wayland and X11 only work in generic VGA mode.
  - I'm getting worse performance in llama.cpp than in DGX OS, but faster initial model loading.

- if he wants Ubuntu specifically, NVIDIA officially supports it too: https://docs.nvidia.com/dgx/dgx-os-7-user-guide/installing_on_ubuntu.html
# discuss-dist-ubuntu/debian
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-dist-redhat/fedora
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-dist-nixos
- ## 

- ## 

- ## 

- ## 

- ## [古法编程时代过来的程序员，用了快 2 个月 NixOS ，预感这就是 AIOS 的基座，记录下经验和感受  - LINUX DO _202604](https://linux.do/t/topic/1947667)
  - 最重要的还是落到开发环境上，最初让我接触到 NixOS 的那个问题自然也解决了，现在每次进入一个项目后，先 devenv shell 启动开发环境，要运行就 devenv up，再也不用管各种项目的环境了，统一扔给 Coding Agent + devenv 就好了。目前还没踩到啥坑，devenv 也是用的 Nix 语法来配置的，所以也给我一种 NixOS 的生态很规整的感觉 
  - 当时选择 devenv 也是纠结了挺久，尤其是 direnv 确实是有种cd出env随的言出法随效果，但我不一定进文件夹就是为了开发，也可能是为了摸鱼或者纯手误。

# discuss-dist-archlinux
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-linux-cn
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Seriously, except package managers, what's the difference between distros? : r/linux _202607](https://www.reddit.com/r/linux/comments/1ux5vns/seriously_except_package_managers_whats_the/)
- Stability. Some distros are more bleeding-edge while others stay with tried-and-true. And many in between. 

Security. How quickly are security patches applied? How thoroughly are they vetted? How secure are the repositories?

Support. The Arch wiki is known for excellent, detailed documentation. 

Configurability. Gentoo and NixOS (and others I'm forgetting) allow the entire system to be rebuilt based on a configuration change. 

FOSS philosophy. Are non-FOSS things like some video drivers available, and if so how well supported are they. 

- Point (Fedora) vs Rolling release (Arch)

Stable (Debian) vs Bleeding edge (Arch)

Snap-infested (Ubuntu)

Mutable (everything above) vs Immutable (Silverblue)

A/B immutable (Vanilla)

Declarative Config (Nix)

Building everything from Source (Gentoo)

QoL features (CachyOS, Bazzite)

Alternative Init System (Void, Artix)

Extremely Tiny (Alpine)

Alternative userland (Chimera)

- Opinionated for a specific purpose, Bazzit, Secureblue, OpenWRT or even Linux Larp, vs Allrounder like Fedora or Debian. 

- A distribution is essentially just an opinionated collection of software. Debian stable and Arch may use most of the same tools, but someone who needs a stable system would never consider a rolling distro like Arch.
- Distros are just collections of packages. Which packages you get and when is decided by the repo you download packages from. The Ubuntu repo has some packages released at some point, the Arch repo has some packages released at some point. The differences are the distro.
