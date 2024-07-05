---
title: tool-os-linux-app-store
tags: [app-store, linux, tool]
created: 2023-06-22T07:21:24.872Z
modified: 2023-06-22T07:22:04.591Z
---

# tool-os-linux-app-store

# guide

- tips
  - GNOME的Software和KDE的Discover都有snap/flatpak的插件
  - 优先级: flathub(可镜像), snap-store, appimage, ppa/custom-repo/synaptic, apt/yum/dnf
  - 考虑支持用户自定义仓库和搜索 https://launchpad.net/ubuntu/+ppas
# web-apps
- https://github.com/tauri-webapps
# linux-apps
- bauh
  - https://github.com/vinifmor/bauh
  - Graphical user interface for managing your Linux applications.
  - Supports AppImage, Arch packages (including AUR), Debian packages, Flatpak, Snap and native Web applications

- AppOutlet /MIT/202207/ts/archived
  - https://github.com/AppOutlet/AppOutlet
  - https://appoutlet.github.io/tags/app-outlet/
  - A Universal linux app store
  - It currently supports AppImages, Flatpaks and Snaps packages.
  - discontinued

## 星火商店

- 为何热衷于搞发行版的多，搞应用程序开发的少？
  - Linux最多余的就是各种发行版，最缺的就是应用程序，特别是行业应用程序。
  - [星火提供的 Wine QQ、微信 也是经过优化的（主要打包者也是用 ubuntu 的）](https://www.zhihu.com/question/534029323/answer/2705133986)

- [mobile web Spark Store](https://d.store.deepinos.org.cn/store/#/)

- [商店希望尽快引入星火应用商店&Xdroid -](https://forum.openkylin.top/forum.php?mod=viewthread&tid=197106&extra=page%3D1)
  - 这个“星火商店”上的软件很多都存在法律上的风险， 例如上面的linux原生版微信就是使用定制版微信进魔改后重新打包的产物（使用后有用户收到官方的登录异常警告），还有一些软件是使用软件官方原版拆包再重新打包，一些软件是发行方禁止外泄的内测版，一些wine版的软件是使用版权不明的wine版本，还存在一些wine游戏等是未经版权方同意的破解版，这些已经是侵权行为。星火商店目前都是以不盈利为目的并不代表上面的软件是没有问题。

## flatpak

### flatpak-utils

- https://github.com/flattool/warehouse /202312/python
  - a versatile toolbox for managing flatpak user data, viewing flatpak app info, and batch managing installed flatpaks.

### blogs

- [Flatpak is not the future (2021) | Hacker News](https://news.ycombinator.com/item?id=37210397)

- [Graphical front-end to manage apps](https://github.com/flatpak/flatpak/issues/859)

- [Where are all the installed flatpak apps .desktop files located](https://github.com/flatpak/flatpak/issues/1286)
  - /var/lib/flatpak/exports/share/applications/org.gnome. Builder.desktop

- Applications and runtimes that are installed system-wide are available to all users on the system. 
  - Applications and runtimes that are installed per-user are only available to the users that installed them.
  - The same principle applies to repositories
- **Flatpak commands are run system-wide by default**.

- Flatpak is built on top of a technology called **OSTree**, which is influenced by and very similar to the Git version control system. 
  - Like Git, OSTree allows versioned data to be tracked and to be distributed between different repositories. Like Git, Flatpak uses repositories to store data, and it tracks the differences between versions. 
  - However, where Git is designed to track source files, OSTree is **designed to track binary files and other large data**.

## snap

- [Programs installed via snap not showing up in Launcher - Ask Ubuntu](https://askubuntu.com/questions/910821/programs-installed-via-snap-not-showing-up-in-launcher)
  - /var/lib/snapd/desktop/applications

- [Ubuntu 明年将推出完全基于 Snap 的桌面版本_202306](https://www.oschina.net/news/243309/immutable-all-snap-ubuntu-desktop)

## appimage

- [Appimagehub.com](https://www.appimagehub.com/)
  - This catalog has 1282 AppImages
  - https://github.com/prateekmedia/appimagepool
    - modern AppImageHub Client, powered by flutter.

- https://appimage.github.io/apps/
  - https://github.com/AppImage/appimage.github.io
  - Given an URL to an AppImage, the GitHub action in this project inspects the AppImage and puts it into a community-maintained catalog

- https://github.com/TheAssassin/AppImageLauncher
  - https://github.com/TheAssassin/AppImageLauncher/wiki
  - AppImageLauncher is a novel and unique solution of integrating with the system. It intercepts all attempts to open an AppImage to provide its integration features.

- https://github.com/SalaniLeo/Immagini
  - An application made to easily manage and create . AppImage apps

- https://github.com/mijorus/gearlever
  - Manage AppImages with ease 

- https://github.com/ryonakano/pinit
  - Create the shortcut to your favorite portable apps into your app launcher.

- https://github.com/AppImage/AppImageKit
  - https://appimage.org/
  - AppImageKit is a concrete implementation of the AppImage format, especially the tiny runtime that becomes part of each AppImage.
# linux-package-manager

## apt

- [Synaptic Package Manager - Home](https://www.nongnu.org/synaptic/)
# win-apps
- winget作为包管理器，可实现类似package.json的清单配置，用于快速备份还原系统

- https://github.com/marticliment/WingetUI /python
  - https://www.marticliment.com/wingetui/
  - The main goal of this project is to create an intuitive GUI for the most common CLI package managers for Windows 10 and Windows 11, such as Winget, Scoop, Chocolatey, Pip and Npm
# app-store-more
- [Umbrel App Store](https://apps.umbrel.com/)
  - Browse the ever-growing selection of self-hosted apps on umbrelOS
  - [Umbrel — The ultimate home server and OS for self-hosting](https://umbrel.com/)
  - Use umbrelOS from your browser.
  - Run umbrelOS on Ubuntu or Debian on any hardware (or a VM on Mac or Windows) 

- https://gitlab.gnome.org/GNOME/gnome-software /GPL/clang
  - https://apps.gnome.org/Software/
  - Software allows you to find and install new apps and system extensions and remove existing installed apps.
  - A plugin system is used to access software from different sources.
  - Plugins are provided for: debian/rpm/Flatpak/Snap
  - Ratings and reviews using ODRS(GNOME Open Desktop Ratings).
# wine
- [Wine 9.0 · wine / wine · GitLab](https://gitlab.winehq.org/wine/wine/-/releases/wine-9.0)
  - 202401, This release represents a year of development effort and over 7, 000 individual changes. It contains a large number of improvements that are listed below. 
  - The main highlights are the new WoW64 architecture and the experimental Wayland driver.
  - The new WoW64 mode is not yet enabled by default. 
  - The Wayland driver is not yet enabled by default. It
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [wine和crossover有什么本质区别？ - 知乎](https://www.zhihu.com/question/41884034)
- 两者运行的Windows程序的效果是一致的，如果纯属靠Wine的能力去运行Windows，Wine是优于CrossOver的，CrossOver用的是暂时认为稳定的Wine，而Wine是最新版。两者的功能区别在于，CrossOver提供能基本正常运行某些应用程序的保证和一套解决方案，比如某个wine实现的dll已知有暂时无法的bug，CrossOver会提供该dll原版(即Windows里面的原版dll)的安装程序下载，而直接用Wine的用户则可能不知道Wine对该应用程序的兼容性，而CrossOver提供解决方案。说白了CrossOver是用来自动解决Windows程序的“依赖”的。CrossOver还提供以下功能:1. 容器2. 打包已经解决兼容性问题的容器3. Steam优化

- ## If you're going to offer an offline-capable Linux app then no-one wants to use Snap. AppImage or Flatpak is the way.
- https://news.ycombinator.com/item?id=38905605
  - It doesn't work on various distributions, 
  - lots of people disable it because of various issues like it being much slower to start, it can only connect to one backend at a time (which is Canonical's proprietary one) unlike Flatpak, and generally the Linux community has settled on Flatpak and AppImage as the preferred universal packaging formats.

- ## [nautilus - How to set Nemo as the default file manager in Ubuntu? - Ask Ubuntu](https://askubuntu.com/questions/1066752/how-to-set-nemo-as-the-default-file-manager-in-ubuntu/1173861#1173861)

- ## [How to add flatpak & snap app icon to desktop?](https://www.reddit.com/r/pop_os/comments/wa3p50/how_to_add_flatpak_snap_app_icon_to_dekstop/)
- There's a gnome extension called **add to desktop** that I always use that just let's you right click an application in the launcher and it will add it to the desktop.
