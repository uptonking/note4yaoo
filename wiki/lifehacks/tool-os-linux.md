---
title: tool-os-linux
tags: [iot, linux, operating-system]
created: 2020-11-25T08:20:22.803Z
modified: 2020-12-22T12:42:14.745Z
---

# tool-os-linux

# guide

- [主流linux发行版分为几个派系](https://www.zhihu.com/question/399967127/answer/3015229817)
# linux-cli-shell
- https://github.com/Xfennec/progress
  - Linux tool to show progress for cp, mv, dd, ... (formerly known as cv)
  - Progress 可以显示当前一些耗时操作的进度，比如 大文件的 cp/mv/dd, 甚至还可以显示下载进度等等。它还提供了一个类似 top 的界面，可以全面监控各种进度。
  - It simply scans `/proc` for interesting commands, and then looks at directories fd and fdinfo to find opened files and seek positions, and reports status for the largest file.

- https://github.com/andreafrancia/trash-cli /python
  - Command line interface to the freedesktop.org trashcan
  - trash-cli trashes files recording the original path, deletion date, and permissions. 
  - It uses the same trashcan used by KDE, GNOME, and XFCE, but you can invoke it from the command line (and scripts).
# ubuntu
- 系统升级的困扰
  - 可能变化的ui：系统图标、字体
  - ubuntu18版的postgresql-10数据库会保留到u20
    - u20再安装数据库的扩展时会安装postgresql-12，但不会启动!!!
    - 变通方法
      - 备份p-10数据库数据，卸载原数据库，升级到u20，再安装p-12，然后导入备份数据

- ubuntu发行版的软件生态较为丰富

- [Ubuntu UnitsPolicy](https://wiki.ubuntu.com/UnitsPolicy)
  - Applications must use IEC standard for base-2 units:
    - 1 KiB = 1,024 bytes (Note: big k)
    - 1 MiB = 1,024 KiB = 1,048,576 bytes
  - Applications must use SI standard for base-10 units:
    - 1 kB = 1,000 bytes (Note: small k)
    - 1 MB = 1,000 kB = 1,000,000 bytes
  - It is not allowed to use the SI standard for base-2 units:
    - 1 kB != 1,024 bytes
    - KB (with a big k) does not exist
- 单位
  - 文件管理器显示文件的大小基于1KB=1000bytes(SI standard)
  - 而终端`ls -lh`显示大小基于1KiB=1024bytes(IEC standard)
# centos
- CentOS 8将在2021年结束支持，往后CentOS 7作为长期支持版本将继续被支持直到其生命周期结束，CentOS Stream将作为工作重点
  - centos 7的支持，持续到2024年
  - CentOS 创始人开辟新项目 Rocky Linux，一个社区版的企业操作系统，旨在与 Red Hat Enterprise Linux 100％ 兼容
- CentOS 7以及更早的版本是RHEL的社区版，所有的更新都是追随RHEL的。
  - 红帽公司在Fedora上支持最新的软件，给桌面用户使用。
  - 基于Fedora，再加上企业级的改良，做成商业版RHEL, 在RHEL的基础上，社区重制了CentOS. 可以看到，由于RHEL注重稳定性，软件更新速度很慢，所以CentOS 7和更早的版本软件都很老。
- 从CentOS 8开始，CentOS不再直接追随RHEL, 而是直接继承Fedora的更新。
  - CentOS Stream就成为了介于Fedora和RHEL中间的那个发行版，centos stream就是rhel beta的定位
  - CentOS Stream，既可以提供一个下一代RHEL的公测平台，又可以让CentOS社区完成一部分RHEL的开发工作，还可以给无法接受Fedora更新频率，但希望使用RPM系列操作系统的人一个选择，这才是对Red Hat有用的子项目。
- Oracle Linux 8，这个发行版也是基于RHEL8的重构发行版，和CentOS 8没什么区别，软件基本通用。
# linux-open
- https://github.com/app-outlet/app-outlet
  - http://app-outlet.github.io/
  - App Outlet is a Universal application store.
  -  It currently supports AppImages, Flatpaks and Snaps packages.

- https://github.com/pacstall/pacstall
  - https://pacstall.dev/
  - An AUR-inspired package manager for Ubuntu

- https://github.com/fsquillace/junest
  - The lightweight Arch Linux based distro that runs, without root privileges, on top of any other Linux distro.
  - JuNest is a lightweight Arch Linux based distribution that allows the creation of disposable and partially isolated GNU/Linux environments within any generic GNU/Linux host OS and without requiring root privileges to install packages.
  - JuNest is built around pacman, the Arch Linux package manager, which allows access to a wide range of packages from the Arch Linux repositories.
  - Run on a different architecture from the host OS via QEMU.
