---
title: tool-os-linux-ubuntu-xp
tags: [linux, os, ubuntu, xp]
created: 2021-01-01T22:26:18.260Z
modified: 2021-01-01T22:26:57.773Z
---

# tool-os-linux-ubuntu-xp

# guide
- tips
  - launcher/pin-app，很可能是伪需求
    - 最高频的apps可使用收藏或dock
    - 常用apps可使用menu列表
    - 系统级的launcher集成在菜单中，操作方便，第三方launcher需要自动启动和替换默认
  - 桌面甚至是不必要的，更推荐类似mac的spotlight
# usage
- 查看各程序网络带宽占用
  - sudo apt-get install nethogs
  - sudo nethogs  查看网速
  - sudo nethogs -v 3   查看消耗总流量
  - https://github.com/GyulyVGC/sniffnet
    - Cross-platform application to comfortably monitor and analyse network traffic
# gnome-extensions
- [Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
  - https://github.com/MartinPL/Tray-Icons-Reloaded
  - bring back Tray Icons to top panel, with additional features.
  - only works with Xorg and XWayland.
  - If you are on Wayland and app won't run through XWayland you can force it via command: `GDK_BACKEND=x11 app_name`
# ubuntu-starter
- ubuntu查看序列号（serial number）和产品型号（product number）
  - sudo dmidecode | less

- [图吧工具箱，是开源、免费、绿色、纯净的硬件检测工具合集](http://www.tbtool.cn/)

- win 11 & pro
  - https://www.microsoft.com/software-download/windows11

- [Office 2021官方镜像下载安装激活一条龙](https://www.cnblogs.com/hushaojun/p/15967885.html)
# ubuntu-cons

## input-method

- [ctrl+shift+e 会导致键盘停留在e，按键会暂时失效](https://askubuntu.com/questions/1125726)
  - Open Ibus preferences(ibus-setup) in your terminal, visit the Emoji tab, then click the Emoji Annotation to either Delete or change the shortcut
# ubuntu-usage
- [Why does Linux have no user subfolder such as /AppData? - Quora](https://www.quora.com/Why-does-Linux-have-no-user-subfolder-such-as-AppData)
  - Linux’ user subfolder is /home
  - /home/yourusername contains, besides all personal files and data, a number of hidden “dot” directories like .config and .local in which software stores their user-specific configuration.

- 查看gnome桌面环境是wayland还是x11
  - s1: echo $XDG_SESSION_TYPE
  - s2: loginctl show-session 2

- 常用配置
  - alt+tab: 切换到下一个窗口，一个多开的应用是多个窗口，逐个切换
  - win+tab: 切换到下一个应用，可跳过当前应用的多个窗口

- gedit
  - alt+1/2/9: switch to Nth doc
  - ctrl+g: find next match
  - ctrl+h: find and replace; show hidden files
  - ctrl+z/ctrl+shift+z
  - ctrl+d: del current line
  - alt+^/v: move current line up/down
  - alt+</>: move current word left/right
  - ctrl+u/l/~: uppercase/lowercase/invert case

- gnome-extensions
  - extensions
    - 在桌面顶部方便开关和配置所有gnome shell extensions
  - netspeed
  - clock override
    - `%R:%S %F %A`
  - hide top bar
  - removable drive menu
  - easyscreencast
    - video recording
  - screenshot tool
    - 截图还可利用xnview - tools - capture - rectangle
  - more-extensions
    - open weather
    - clipboard indicator
      - caches clipboard history
    - ShutdownTimer
      - Shutdown the device after a specific time.
    - Impatience
      - Speed up the gnome-shell animation speed

## hardware

- https://github.com/TheWeirdDev/Bluetooth_Headset_Battery_Level
  - https://extensions.gnome.org/extension/3991/bluetooth-battery/
  - A python script to get battery level from Bluetooth headsets
  - [Add bluetooth headset battery's percentage in Ubuntu_202209](https://www.goulin.fr/blog/bluetooth-headset-battery-percentage-ubuntu)

## launcher

- https://github.com/Ulauncher/Ulauncher /python/vue/支持扩展
  - https://ulauncher.io/
  - Ulauncher is a fast application launcher for Linux. 
  - It's written in Python using GTK+, and features: App Search (fuzzy matching), Calculator, Extensions, Shortcuts, File browser mode and Custom Color Themes
  - [How Ulauncher launches apps](https://github.com/Ulauncher/Ulauncher/wiki/How-Ulauncher-launches-apps)
  - roadmap
    - [Sort shortcuts](https://github.com/Ulauncher/Ulauncher/issues/1008)

- https://github.com/arunk140/gnome-command-menu /js/基于自定义菜单
  - A GNOME Shell Extension to manage shortcuts in Top Bar (Inspired by Shuttle and SSHMenu)
  - [Standard Icon Names](https://specifications.freedesktop.org/icon-naming-spec/latest/ar01s04.html)
  - [use multiple commands](https://github.com/arunk140/gnome-command-menu/issues/6)
# wayland
- [Boycott Wayland. It breaks everything!](https://gist.github.com/probonopd/9feb7c20257af5dd915e3a9f2d1f2277)
  - Wayland does not work properly on NVidia hardware?
  - Wayland breaks screen recording applications
  - Wayland breaks screen sharing applications
  - Wayland breaks AppImages that don't ship a special Wayland Qt plugin
  - Wayland prevents GUI applications from running as root
# discuss-ubuntu
- refs
  - [Latest Desktop/Team Updates](https://discourse.ubuntu.com/c/desktop/team-updates/23)

- ## 

- ## 

- ## 

- ## 

- ## 
