---
title: thread-tool-linux-android
tags: [android, thread]
created: 2025-02-03T08:37:31.341Z
modified: 2025-02-03T08:37:50.714Z
---

# thread-tool-linux-android

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 由于原生 Android 16 自带的 Debian Linux 越来越完善，接下来购买 Android 设备时，都要关注下设备芯片是否支持 unprotected VM 这一项特性了，
- https://x.com/w7wonder/status/1989865634952589554
  - 因为这是该设备可以基于 AVF 下运行 Linux 的必要条件，你可以在手机上彻底实现使用完整的 Linux，外接显示的话更能直接变身小主机。
  - 满足这一点，意味着你以后每有一台 Android，哪怕报废或不想用，你至少也有了一个 Linux 小主机，不存在无用的旧手机了。很多旗舰机的性能拉满后，已经不输普通笔记本。
  - 那么最大的问题来了，目前主流旗舰纷纷采用的高通骁龙 gen xxx，大概率都是不支持这一特性的，也可能之后来个 OTA 升级，但鬼知道啥时候，高通成了这一特性的绊脚石
  - 已知三星部分使用 Exynos 芯片的旗舰或平板，以及没有使用高通芯片的部分海外版比如小米，是可以支持的。支持最好的自然是 pixel 系列，但谷家芯片目前综合性能…… 只能说也不是不能用。
  - 总之希望这一特性，接下来能持续被越来越多厂商好好对待吧。

- 7a上实测，可以跑docker，但是7a内存太小了，经常杀后台。

- 这要是把chromeos的Linux。图形那一套弄过来就无敌了
  - 目前至少已经可以跑 Linux 图形了，装个什么 xfce 这些就行，并且这一套方案是支持 GPU 加速的，还待完善

- 只要别魔改内核，古早的android都能chroot跑linux啦
  - 你也提到是基于 chroot 去跑，所以比不了一点。 最新这套是基于 AVF，系统框架上做的支持，跑起来是个完整的 Linux 虚拟机，可以有 systemd, 可以跑 docker 等等，更不用说官方层面支持 GPU 加速了，相比之下 chroot 方案就显得太玩具

- 天玑系列能不能支持呀
  - 能，至少新的9400+有可以的，别的不确定，看这条
  - 确认过，例如三星 Galaxy tab S11 系列用的联发科 Dimensity 9400+ ，是支持的，社区有人已经在用

- arm这种能运行主流数据库嘛？没用过
  - 当然可以，本质上你就理解为框架层给你做好了整套虚拟机

- 云服务器50一年，24小时连网。我把我手机变成Linux 干嘛？吃饱了撑着没事干嘛。
  - 云永远替代不了本地，很多需求会需要本地做部署
  - 而且你手机多个完整电脑的功能不香吗，我可以不用它必须得有啊

- Pixel 可以跑桌面安卓和linux容器了

- ## [安卓 16 支持 Linux 子系统了 - V2EX](https://v2ex.com/t/1108636)
- 是基于 namespace 做的吗？
  - 用的 avf
  - 是完整的系统级支持有 systemd 可以装 docker
- 基于虚拟化的，我印象中谷歌有介绍过 Android 硬件虚拟化的文章

- 为什么 Linux 不能内置 Android 子系统，反而是不同内核的 Windows 可以？
  - Android 各类软件客户端也没法满足日常办公需求吧, 不然小米和华为也不会搞把 WPS Office PC 装进 Linux 虚拟机再打包成 apk 这种操作了，直接开发 Android 原生版本岂不更好？
- LSA 的问题是许可证和本身 linux 搞 android 就收益不大

- 谷歌要把 chromeos 从 gentoo 转移到 android 上来

- linux 不是有 waydroid 吗，lxc 容器共享主机内核性能和体验甩 windows 的 WSA 几条街了

- 为什么不能？只是没有知名的发行版这么做，你完全可以自己跑一个 Android 容器或者虚拟机。https://github.com/budtmo/docker-android
