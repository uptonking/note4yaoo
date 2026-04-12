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
    - 悬浮search搜索框打断用户操作影响更小
    - 最高频的apps可使用收藏或dock
    - 常用apps可使用menu列表
    - 系统级的launcher集成在菜单中，操作方便，第三方launcher需要自动启动和替换默认
  - 桌面甚至是不必要的，更推荐类似mac的spotlight
  - 更建议使用系统自带search和spotlight，操作更编辑无覆盖，无需重复索引

- pros-linux/ubuntu
  - 开发方便

- cons-linux/ubuntu
  - 很多热门软件不提供linux版，如ide-trae/kiro
# usage
- 查看各程序网络带宽占用
  - sudo apt-get install nethogs
  - sudo nethogs         查看网速
  - sudo nethogs -v 3    查看消耗总流量
  - https://github.com/GyulyVGC/sniffnet
    - Cross-platform application to comfortably monitor and analyse network traffic

- window
  - 窗口无法拖拽缩放的原因，可能是自定义themes的cursor不支持，注意要慎用自定义cursor图标
  - To take a screenshot of the active window in Ubuntu, you can use the keyboard shortcut `Alt + Print`.
# gnome-extensions
- [Tray Icons: Reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
  - https://github.com/MartinPL/Tray-Icons-Reloaded
  - bring back Tray Icons to top panel, with additional features.
  - only works with Xorg and XWayland.
  - If you are on Wayland and app won't run through XWayland you can force it via command: `GDK_BACKEND=x11 app_name`
# ubuntu-starter
- https://github.com/ohmybash/oh-my-bash
  - https://ohmybash.github.io/
  - A delightful community-driven framework for managing your bash configuration

- https://github.com/magicmonty/bash-git-prompt /不推荐，功能少，直接用ohmybash
  - An informative and fancy bash prompt for Git users

- ubuntu查看序列号（serial number）和产品型号（product number）
  - sudo dmidecode | less
# network
- [Ubuntu 18.04 永久修改DNS的方法 - 姚红 - 博客园](https://www.cnblogs.com/yaohong/p/14817914.html)
  - sudo gedit /etc/systemd/resolved.conf

- [Ubuntu22.04修改dns - 厚礼蝎 - 博客园](https://www.cnblogs.com/guangdelw/p/17493919.html)
  - 通常我们知道，修改dns的几个途径/etc/resolv.conf/etc/netplan/01-netcfg.yaml修改上面两个文件，一般情况下，可以解决，但是在一次使用新安装的ubuntu22.04的时候，发现，无论怎么修改，dig解析域名都是往127.0.0.53发送，哪怕在缓存中的已经生效
  - 如何查看缓存中生效的配置呢 cat /run/systemd/resolve/resolv.conf
  - 需要删掉或者修改 /etc/resolv.conf 文件名
- [Ubuntu 20.04 设置 DNS 的方法 - 刘应杰 - 博客园](https://www.cnblogs.com/mouseleo/p/14976527.html)
# ubuntu-cons

## input-method

- [ctrl+shift+e 会导致键盘停留在e，按键会暂时失效](https://askubuntu.com/questions/1125726)
  - Open Ibus preferences(ibus-setup) in your terminal, visit the Emoji tab, then click the Emoji Annotation to either Delete or change the shortcut
# ubuntu-usage
- turn off screen 命令
  - xset dpms force off 按任意键可激活屏幕

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

- 更建议使用系统自带search和spotlight，操作更编辑无覆盖，无需重复索引

- menulibre在flathub中名字为menu editor，可在系统菜单中修改和添加自定义app图标
  - main menu更好用

- ubuntu的all apps支持自定义顺序
  - 方法1: 使用第三方自定义gnome shell extension Overview Feature Pack
  - 方法2: flathub apps - pin

- https://github.com/cerebroapp/cerebro /MIT/js/支持plugins/electron
  - https://www.cerebroapp.com/
  - an open-source launcher to improve your productivity and efficiency
  - https://github.com/cerebroapp/awesome-cerebro

- https://github.com/Ulauncher/Ulauncher /python/gtk/vue/支持扩展
  - https://ulauncher.io/
  - Ulauncher is a fast application launcher for Linux. 
  - 结合了spotlight的易用性和plugin的扩展性
  - 使用github仓库作为扩展分发方式，优点是现有用户多，缺点是网络不稳定，最好能支持仓库url的代理url
  - It's written in Python using GTK+, and features: App Search (fuzzy matching), Calculator, Extensions, Shortcuts, File browser mode and Custom Color Themes
  - [How Ulauncher launches apps](https://github.com/Ulauncher/Ulauncher/wiki/How-Ulauncher-launches-apps)
  - roadmap
    - [Sort shortcuts](https://github.com/Ulauncher/Ulauncher/issues/1008)
  - extensions
    - https://github.com/friday/ulauncher-gnome-settings
    - https://github.com/jetbug123/ulauncher-ssh
    - https://github.com/NastuzziSamy/ulauncher-custom-scripts
    - https://github.com/kleber-swf/ulauncher-turn-off-screen
    - https://github.com/sa-0001/ulauncher-mongodb-objectid
  - ext-imcompatible
    - https://github.com/sandler31/ulauncher-local-listeners

- https://github.com/arunk140/gnome-command-menu /js/基于自定义菜单
  - A GNOME Shell Extension to manage shortcuts in Top Bar (Inspired by Shuttle and SSHMenu)
  - [Standard Icon Names](https://specifications.freedesktop.org/icon-naming-spec/latest/ar01s04.html)
  - [use multiple commands](https://github.com/arunk140/gnome-command-menu/issues/6)

## nautilus

- pros
  - 批量rename、支持search-replace
  - 支持快捷键: open in terminal

- cons
  - 单位是十进制，不适合文件实际的字节数、网络文件的二进制、内存的二进制
    - [nautilus - How to set Nemo as the default file manager in Ubuntu? - Ask Ubuntu](https://askubuntu.com/questions/1066752/how-to-set-nemo-as-the-default-file-manager-in-ubuntu/1173861#1173861)

- https://github.com/costales/clipboard-to-file /202210/python
  - Paste Linux clipboard (text/image) into a file

- https://github.com/linuxmint/nemo /c
  - file manager for the Cinnamon desktop environment.
  - 尝试添加 open terminal here 快捷键失败
  - 尝试改变右键菜单项的顺序、添加新菜单项到第一个
  - https://github.com/smurphos/nemo_actions_and_cinnamon_scripts
    - A collection of custom context menu items for the Nemo file manager
  - https://github.com/linuxmint/nemo-extensions

## cleaner

- [Useful GUI Tools to Free Up Space on Ubuntu and Linux Mint](https://www.tecmint.com/free-disk-space-ubuntu-linux-mint/)
  1. Stacer
  2. Ubuntu Cleaner
  3. BleachBit
  4. Sweeper
  5. rmLint
# wayland
- wayland下fractional scaling导致chrome模糊的问题
  - 目前202402仍没有通用的解决方案，需要系统级的支持和应用级的支持，非常困难来支持大多应用
  - 考虑浏览器、electron、系统编辑器/文件管理器
  - 变通方案: 不开启fractional scaling, 保持系统缩放比例 100%， 修改fonts-scaling-factor为1.75

## issues-wayland

- [touchpad - Pinch zoom in browsers on Ubuntu 20.04 with Wayland - Ask Ubuntu](https://askubuntu.com/questions/1261961/pinch-zoom-in-browsers-on-ubuntu-20-04-with-wayland)
  - figma在touchpad的捏紧手势不缩放，需要按住ctrl键
- ## 

- ## 

- ## 

- ## 

- ## [图形的未来](http://happyseeker.github.io/graphic/2016/11/10/the-future-of-the-desktop.html)
- xorg因为其原有的架构设计与现如今各种严苛的绘图需求不相匹配，主要表现如：
  - Xorg大管家管事太多，除了管理input，所有的 **绘图请求、窗口管理、窗口合成** 都必须要与Xorg进行交互，导致Xorg上存在性能瓶颈。根源还在于Xorg的架构太复杂。
  - Xorg绘图无法充分利用GPU的硬件加速。所有绘图操作都必须提交到Xorg完成，而Xorg自身，对于2D加速，虽然有EXA；对于3D加速，虽然有Glamour，但仍旧无法充分利用硬件加速。

- Wayland的优势
  - 架构简单，有更好的性能。简单说，就是职责变少，不管闲事，使客户端自己控制绘图操作(比如分配缓冲区)，与客户端的交互减少，消除了性能瓶颈。
  - 硬件加速利用更充分。由于客户端自己控制绘图操作，绘图(比如画个圆)不在通过Xorg，而是客户端自己分配缓冲区，自己绘制，那么客户端就可以直接利用GPU来画(比如OpenGL接口)，不需要经过Xorg中转，显然会有更好的性能

- 什么阻碍了Wayland
  - 最主要的还是生态问题
  - 图形开发工具(上层)。比如GTK+和QT，当前图形环境中的绝大部分应用程序都是基于这两个工具开发的，Wayland要thrive，必然需要这两个的支持
  - 图形桌面环境。比如Gnome、KDE、Mate，用户直接接触是桌面环境，包括面板、桌面(Shell)、登陆管理器、窗口管理器、文件资源浏览器等，需要整个桌面环境都支持Wayland，而这些组件原本都严重依赖于Xorg，要切换，那相应的移植工作量可不是一点点
  - 硬件驱动。这里主要指显卡，在原有的Xorg架构中，显卡驱动通常由两部分组成：位于Xorg中DDX层的用户态驱动和位于内核的drm驱动，切换至Wayland后，看似不需要用户态驱动了，但其实由于绘图操作转由客户应用程序完成，用户态驱动仍然是需要的

- ## 🆚️ [Mir 和 Wayland 等 X11 替代品，相比 X11 有哪些具体的优点？ - 知乎](https://www.zhihu.com/question/22052356)
- X 系统非常复杂。而且这个复杂度的设计目的是为了灵活性而不是为了可靠性。所谓的灵活性就是可以提供很多策略：比如 Window Manager 可以更换，可以支持远端桌面。
- X 系统的灵活性到了今天，很多都是屠龙之技。于是又不得不加上各种 hack。比如说，为了保持原来的标准，支持远端桌面的传统协议还要支持，同时为了显卡硬件加速，又加了一套平行的本地优化。整个系统最初的设计初衷已经被改得乱七八糟。
- 因为 X 开发者的时间并没有像 BSD 或者 Linux 内核那样，始终集中在提高稳定性上，而是在做很多无用功 —— **先花大笔的 performance overhead 来实现一个过于灵活的 framework** ，然后又再上面打补丁取消 performance overhead，同时还要保持向后兼容。这种悠久的历史，反而是稳定性的毒药。

- 🤔 什么是over-designed，Xwindow就是典型的例子。很可惜Wayland也好不到哪儿去。

- ## [Boycott Wayland. It breaks everything!](https://gist.github.com/probonopd/9feb7c20257af5dd915e3a9f2d1f2277)
  - Wayland does not work properly on NVidia hardware?
  - Wayland breaks screen recording applications
  - Wayland breaks screen sharing applications
  - Wayland breaks AppImages that don't ship a special Wayland Qt plugin
  - Wayland prevents GUI applications from running as root

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
# discuss-dist-ubuntu
- refs
  - [Latest Desktop/Team Updates](https://discourse.ubuntu.com/c/desktop/team-updates/23)

- ## 

- ## 🆚️ [Those of you who prefer ZSH to BASH, why? : r/linuxquestions _202108](https://www.reddit.com/r/linuxquestions/comments/p50jvl/those_of_you_who_prefer_zsh_to_bash_why/)
- tab completion and colors

- For interactive use, it is close to 100% compatible with bash syntax, but the interface has various quality of life improvements. Here are a few:
  - The main features involve things like tab completion, which zsh can do by picking items from a menu (bash displays the options, but doesn't let you pick one, you just keep typing and try again).

- For one, due to its licensing zsh is less invasive and therefor not only the prevalent shell in FreeBSD but also for example in macOS, and some other Unix Systems. So there’s that. Other than that I am still myself getting to know zsh better.

- So core feature I like in zsh (and it probably is available in bash) is proper reverse search. Like when you do ctrl-r in bash, and then type in "abc" it finds commands with "abc" in it. If you type in "abc" in my zsh, and then tap "up", it would find the last command starting with "abc" in my history.

- Zsh can compare floats, whereas bash cannot

- ## [Is there any way I could fix or mitigate the blur on applications using XWayland caused by fractional scaling? - Desktop - GNOME Discourse](https://discourse.gnome.org/t/is-there-any-way-i-could-fix-or-mitigate-the-blur-on-applications-using-xwayland-caused-by-fractional-scaling/17052)
- the blurriness for X11 applications running with fractional scaling is expected, and it cannot really be fixed without porting those applications away from X11.
  - What KDE does is precisely what GNOME does when changing the text scaling factor; 
  - the only difference is that KDE modifies the Xrdb settings database, which is what applications using Qt or older X11 toolkits use, whereas GNOME changes a setting that is used by GTK applications. 

- From what I’ve seen, Plasma also offers “Scaled by the system” and “Apply scaling themselves” modes, which looks like a decent “solution” that could (easily?) be used. I’m not sure if GNOME has anything similar to that.

- Open source will always be fragmented because the whole point of it is anyone can change anything, so there is no way to ensure everyone uses the same thing. If that is a problem, I would suggest using something else. Sadly there is no “one size fits all”.

- ## [Fractional scaling makes browser blurred - Ask Ubuntu](https://askubuntu.com/questions/1415924/fractional-scaling-makes-browser-blurred)
- I found a workaround which is not ideal but achieves the same effect as 125% fractional scaling, without making browser text blurred.
  - Instead of enabling fractional scaling, go to settings => accessibility and enable large texts.

- I solved this problem (on my 4k monitor 31.5") by keeping it 100% scaling, but increasing the system font to 30% using the command (adjust the factor for your needs, the effect is visible immediately):
  - gsettings set org.gnome.desktop.interface text-scaling-factor 1.3

- ## [Google Chrome is blurry on Ubuntu 23.04 (Wayland + Nvidia 3050 Ti HiDPI screen with 200% scaling) - Ask Ubuntu](https://askubuntu.com/questions/1472847/google-chrome-is-blurry-on-ubuntu-23-04-wayland-nvidia-3050-ti-hidpi-screen-w)
- It seems to be caused by the new Wayland fractional scaling feature. What worked for me was turning it off using --disable-features=WaylandFractionalScaleV1.

- ## 💡 [Can't use Wayland with Nvidia 510 drivers on Ubuntu 22.04 LTS - Ask Ubuntu](https://askubuntu.com/questions/1403854/cant-use-wayland-with-nvidia-510-drivers-on-ubuntu-22-04-lts)
- sudo gedit /usr/lib/udev/rules.d/61-gdm.rules

```shell
# just comment the last two lines
LABEL = "gdm_prefer_xorg"
#RUN += "/usr/lib/gdm-runtime-config set daemon PreferredDisplayServer xorg"
GOTO = "gdm_end"

LABEL = "gdm_disable_wayland"
#RUN += "/usr/lib/gdm-runtime-config set daemon WaylandEnable false"
GOTO = "gdm_end
```

- ## In GNOME, desktop extensions written in JS and for the new version 45 they all have to be rewritten to ESM.
- https://twitter.com/sitnikcode/status/1690733883392729088
  - It’s cool that if you don’t like the way the battery icon works on Linux, you can write a JS extension in a 10 LOC and everything becomes the way you want.
  - GNOME designers often test new ideas in the form of extensions (and evolve the design by looking at popular extensions).

- ## [How Can I Monitor My Laptop Battery Usage? - Ask Ubuntu](https://askubuntu.com/questions/953770/how-can-i-monitor-my-laptop-battery-usage)
- install an application like PowerTOP (sudo apt install powertop). 
  - It shows which processes are most actively using the CPU. 
  - After PowerTOP has run on battery for some time and has taken enough measurements, it will start showing process power consumption in terms of wattage.
- [How to check Which Application is Draining Your Battery on Linux - DEV Community](https://dev.to/thamaraiselvam/how-to-check-which-application-is-draining-your-battery-on-linux-cbo)
  - sudo powertop --html=powerreport.html
  - 再手动打开powerreport.html文件可查看电池使用报告
- [Powertop - ArchWiki](https://wiki.archlinux.org/title/powertop)

- ## [cpu - 100.0% usage by Audio codec hwC0D0: Realtek - Ask Ubuntu](https://askubuntu.com/questions/91359/100-0-usage-by-audio-codec-hwc0d0-realtek)
- No, it just means that you have (probably digital) sound output enabled. If you have some sound outputs, such as digital (optical/coaxial) or hdmi you are not using, then you can blacklist their drivers and you might save some battery. 
