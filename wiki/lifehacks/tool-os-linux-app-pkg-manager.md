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
# discuss
- ## 

- ## 

- ## 

- ## [ubuntu: 国内就没有一个能用的 snap 镜像源！ - V2EX](https://www.v2ex.com/t/549889)
- snap 只有一个官方仓库，flatpak 倒是可以自选（/建）仓库。

- ## [Some Flatpak Qt Apps fail to start after latest Update](https://forum.manjaro.org/t/some-flatpak-qt-apps-fail-to-start-after-latest-update/99973)
  - flatpak upgrade -y
