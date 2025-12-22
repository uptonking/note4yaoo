---
title: tool-os-linux-app-pkg-manager
tags: [linux, pkg-manager]
created: 2023-07-01T07:14:08.182Z
modified: 2023-07-01T07:14:31.456Z
---

# tool-os-linux-app-pkg-manager

# guide

- tips
  - GNOME的Software和KDE的Discover都有snap/flatpak的插件

- snap问题太多了：
  1、不能更换软件仓库地址，国内使用太慢了
  2、需要修改内置配置文件，不能直接修改，传统文件目录能修改的配置文件，snap你是无法修改的
  3、没有图形界面浏览软件列表
  - flatpak安装后命令行默认无命令
  - flatpak安装的chrome默认使用系统代理，但edge却不使用系统代理
  - 拖拽问题
# nix
- [nix.dev documentation](https://nix.dev/)
  - Reproducible development environments
  - Easy installation of software over URLs
  - Easy transfer of software environments between computers
  - Avoidance of version conflicts with already installed software
  - First-class cross compilation support
# discuss-appimage
- ## 

- ## 

- ## 

- ## [cursor v0.47 Appimage for Linux x64 won't run · Issue #2905 · getcursor/cursor _202503](https://github.com/getcursor/cursor/issues/2905)
- Getting the same error on Arch Linux. Frankly, the whole AppImage distribution mechanism has started feeling quite unreliable in the recent past

- [Add RPM and DEB packages for Linux · Issue #933 · getcursor/cursor](https://github.com/getcursor/cursor/issues/933)
  - Just found that they offer the .deb. It's just that they are shy.
  - https://downloader.cursor.sh/linux/deb/x64 (For x86 chips)
# discuss
- ## 

- ## 

- ## [Flatpak vs Native : r/Fedora _202512](https://www.reddit.com/r/Fedora/comments/1pskalj/flatpak_vs_native/)
  - Does flatpak have any advantages over native Rpm ? Why was it invented and what are its disadvantages?

- Not really. It's containerized so it's probably a bit more secure, if it is important for you. But a standard usage do not need such precaution.
  - The main goal of flatpak is to provided cross platforms and cross Linux apps, because each flatpak embedd all needed dependencies. So you can install it the same way on all OSes, maintainers do not have to build rpm version, deb one etc
  - Disadvantage : i find it less configurable than ordinary packages, it uses a bit more of disk space, and theming is not always consistently as each flatpak can have its own design and Ui, not fitted with the OS general theme.

- Another (small) advantage of flatpaks is that they're all sandboxed in the same location. So, if you install/remove a lot of apps it won't leave your /home all messy with a bunch of configs/caches/tmps in various subdirs scattered throughout your /home. Rather, the entire app and its config gets dumped into /home/.var/apps (at least for Fedora). To completely purge an app, you flatpak uninstall `<app-id>` then you can just delete the app folder in /home/.var/app and viola. Your main /home & all of its subdirs are still spotless. Small win

- I use flatpaks almost exclusively. I like having all the user data in one place instead of things going all over the home directory. Warehouse lets you take snapshots of user data as well for easy backups of specific apps.

- flatpak allows you to run stuff without having to remember what versions of shared libraries you have on the system

- 
Advantages:

works on all distributions, and is more robust to packaging errors (though it may still have them)

sandboxed for improved security: programs are heavily restricted in what they can do without explicitly giving them permissions (either at install time or manually later).

install software without root privileges, no root password needed.

some flatpak providers, especially Flathub, don't feel the need to follow patent licensing, so you get patent-encumbered codec support built-in.

- Disadvantages:

configuration files (and sometimes program data) are not directly compatible and require tedious manual intervention if you want to go from flatpak to something else (distro package, self-compiled sources, other formats...) or from something else to flatpak. Otherwise, all the adjustments and data you have in programs may just vanish.

some software requires manual fiddling with permissions, or really complicated tweaks, to run properly for your use cases, due to flatpak limitations.

development is in some ways much more inconvenient (will need to build more and take longer, if you want to test a small change in some library you have to rebuild all the software, etc.)

often uses much more disk space in practice - deduplication helps a little, but you will generally still end up with different runtime versions, bundled library versions, etc, that can't be deduplicated.

installs programs in your home by default, which has advantages but also requires you to think more about your backups and may make them take a lot longer.

is exceptionally tedious for command-line programs

some things can't be installed as flatpak period, like core Desktop Environment things

cross-application integration is much harder

- ## [ubuntu: 国内就没有一个能用的 snap 镜像源！ - V2EX](https://www.v2ex.com/t/549889)
- snap 只有一个官方仓库，flatpak 倒是可以自选（/建）仓库。

- ## [Some Flatpak Qt Apps fail to start after latest Update](https://forum.manjaro.org/t/some-flatpak-qt-apps-fail-to-start-after-latest-update/99973)
  - flatpak upgrade -y
