---
title: tool-os-windows
tags: [iot, operating-system, windows]
created: 2020-11-25T08:20:44.670Z
modified: 2020-12-29T17:48:26.735Z
---

# tool-os-windows

# cmd common
- diskmgmt.msc
  - 打开 disk management 磁盘管理工具
# guide
- apps
  - [吾爱破解 - 52pojie.cn](https://www.52pojie.cn/)

## win缺点

- 需要权衡使用wsl和linux的利弊
  - 使用wsl可利用win应用和linux开发工具的优点，但跨系统访问文件性能差
  - 在开发目标明确单一的情况下，直接使用win版开发工具也不麻烦
- 语言及编码
  - 系统编码设置为utf-8后，很多软件特别是陈旧软件的ui会显示乱码
- 系统级依赖
  - 一些系统依赖包会缺失，如libjpeg-dev, libgif
# WSL子系统
- [WSL发展如此迅速，有没有可能会在未来替代原生Linux？](https://www.zhihu.com/question/396190471)
  - WSL2目前部分功能无法取代桌面Linux，但是日常开发是完全足够的，甚至可以直接跑docker
  - WSL2适用于在Windows上运行Linux的Windows子系统ELF64 Linux二进制文件，其实是Linux内核跑在Hyper-V下，目前能满足linux学习和大部份开发的需求。
  - 由于wsl2作为虚拟机的运行，所以对于硬件的支持还不完善，NVIDIA也仅仅和微软联合发布了WSL CUDA 的预览版本，援引原话为 目前性能不理想。

- [有那些Linux功能是WSL做不到的？](https://www.zhihu.com/question/273664796)
  - WSL磁盘性能非常渣，比原生损失很大；
    - 单纯的存储读写和cpu性能来说，比如编译c/c++，在wsl上编译的时间是原生上花的时间2倍。
    - WSL2下对Linux文件系统访问当然是快了好几倍，但是Linux访问Windows 文件，以及Windows访问Linux文件，速度都非常慢
  - 内核相关
    - 很多Kernel相关功能缺失，例如PAPI5无法测量性能因为缺少计数器
  - 网络相关
    - WSL2内部不可访问Windows的localhost，但是反向是可以的
    - 在连接VPN的情况下，WSL2内无法访问外网

- ref
  - [Comparing WSL 2 and WSL 1](https://docs.microsoft.com/en-us/windows/wsl/compare-versions)
# windows OS

# ref

- win 10 下载地址
  - https://www.microsoft.com/en-us/software-download/windows10ISO
  - https://www.microsoft.com/zh-cn/software-download/windows10
  - [Windows 10 2004升级20h2三种图文教程](https://www.wogu.cc/windows/655.html)
