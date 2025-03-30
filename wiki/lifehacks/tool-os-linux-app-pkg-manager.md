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

- ## 

- ## [ubuntu: 国内就没有一个能用的 snap 镜像源！ - V2EX](https://www.v2ex.com/t/549889)
- snap 只有一个官方仓库，flatpak 倒是可以自选（/建）仓库。

- ## [Some Flatpak Qt Apps fail to start after latest Update](https://forum.manjaro.org/t/some-flatpak-qt-apps-fail-to-start-after-latest-update/99973)
  - flatpak upgrade -y
