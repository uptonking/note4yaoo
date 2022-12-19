---
title: tool-os-install
tags: [iot, linux, operating-system]
created: 2020-11-25T08:20:22.803Z
modified: 2020-12-22T12:42:14.745Z
---

# tool-os-install

# guide

# proxy-usecase
- browser-proxy
  - edge浏览器右上角一直无法登录同步因为国内网络问题，折中方案是点击右侧边栏的outlook或office按钮，在侧边栏登录后，整个浏览器也会登录
  - flatpak安装的chrome默认支持系统代理，但edge浏览器未支持，所以edge不能访问特殊网站
    - [edge: Add proxy support?](https://github.com/flathub/com.microsoft.Edge/pull/181)

- chrome应用商店 #镜像站点
  - [极简插件\_Chrome扩展插件商店\_优质crx应用下载](https://chrome.zzzmh.cn/)
  - [收藏猫插件](https://chrome.pictureknow.com/)
# ubuntu22.04

## guide

- 不要过于执着寻找linux下对应的windows软件体验，双系统切换使用省时省力
  - 录屏时显示键盘按键，类似screenkey，但wayland不支持，可解决
  - 腾讯会议不支持wayland

- 查看已安装
  - apt list --installed
  - snap list / snap list --all 包含旧版本
  - flatpak list / flatpak list --app 只包含app，不包含runtime

- apt install --reinstall pkg 重新安装

## os-starter

- [装了5次Ubuntu，告诉你win10+Ubuntu双系统的正确打开方式](https://zhuanlan.zhihu.com/p/101307629)

- 在ubuntu software update打勾可选源，以及配置apt mirror

- 当三方apt源很慢时，可以尝试手机移动网络，而不是电信宽带网络
  - 特别是安装 git-core/ppa

- snap安装的软件包无法访问隐藏目录。默认安全模式太严格了。
  - 改安全模式必须重新安装软件
  - sudo snap remove firefox
  - sudo snap install firefox --devmode 
- flatpak支持自动更新软件包 firefox, chrome, vscode
  - flatpack常用：shadowsocks、v2ray
  - 缺点是flathub软件少，且安装体积大，snap体积也大
  - 优点是支持自动更新，支持替换为国内源sjtu
  - flatpak也存在无法访问目录的问题
    - 方法1: 使用软件添加目录权限 Flatseal
    - 方法2: flatpak override pkg.id --filesystem=/home/user
- sudo apt-get install flatpak
  - sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
  - sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub
  - [给flatpak添加国内镜像源](https://seekstar.github.io/2021/12/30/%E7%BB%99flatpak%E6%B7%BB%E5%8A%A0%E5%9B%BD%E5%86%85%E9%95%9C%E5%83%8F%E6%BA%90/)
    - sudo flatpak remote-add --if-not-exists flathub https://mirror.sjtu.edu.cn/flathub/flathub.flatpakrepo
  - 应用图标不可见的问题
    - /var/lib/flatpak/app/*application_name*/current/active/files/share/applications 拷贝到 /usr/share/applications
    - /var/lib/flatpak/app/org.mozilla.firefox/current/active/export/share/applications/

- pip安装的包在用户目录
  - /home/yaoo/.local/lib/python3.10/site-packages/meson-0.63.2.dist-info/
  - sudo pip install meson 安装在root目录 
    - /usr/local/lib/python3.10/dist-packages/
  - 还可以安装本地 pip install local-ss-master.zip -U

- ubuntu开机自动挂载win-ntfs硬盘
  - [ubuntu 配置/etc/fstab参数实现开机自动挂载硬盘](https://blog.csdn.net/u010632165/article/details/89597522)
  - [UbuntuHelp: fstab](https://wiki.ubuntu.org.cn/UbuntuHelp:Fstab)
    - [Device] [Mount Point] [File System Type] [Options] [Dump/backup] [Pass]
    - [pass]: Controls the order in which fsck checks the device/partition for errors at boot time. The root device should be 1. Other partitions should be 2, or 0 to disable checking.

- 代理 shadowsocks
  - 如何在 Ubuntu 中使用网络代理
- [Qv2ray 使用详解](https://www.rultr.com/tutorials/4200.html)
  - 和win平台的v2ray客户端一样简单，导入账号信息即可科学上网
  - [Qv2ray使用教程](https://xtrojan.org/client/qv2ray%E4%BD%BF%E7%94%A8%E6%95%99%E7%A8%8B.html)

- chinese-input
  - rime输入法配置的迁移比想像中要快得多，只需要拷贝文件夹
    - emoji需要安装 apple-color-emoji
    - 改为水平方向，需要新建文件，设置内容
      - ibus_rime.custom.yaml
      - patch: style: horizontal: true
  - 搜狗 ubuntu
  - [在Ubuntu下安装讯飞输入法linux版以及卸载方法](https://yoki.moe/Intstu/24.html)
    - xunfei  http://packages.deepin.com/deepin/pool/non-free/i/iflyime/
  - baidu https://srf.baidu.com/site/guanwang_linux/index.html

- [How to Install Fonts on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/how-to-install-fonts-on-ubuntu-20-04-focal-fossa-linux)
  - sudo cp ~/Downloads/Bitwise.ttf /usr/local/share/fonts/sampleName/

- 国内 nvm
  - https://gitee.com/RubyKids/nvm-cn
  - bash -c "$(curl -fsSL https://gitee.com/RubyKids/nvm-cn/raw/master/install.sh)"

- Pending Update of Snap Store 的解决方法

```shell

# Close all open `snapd` process
sudo killall -s KILL snapd
sudo snap refresh
```

- ubuntu以非图形界面启动
  - sudo systemctl set-default multi-user
  - sudo systemctl set-default graphical

- ubuntu安装nvidia显卡驱动
  - 最简单的方式是使用ubuntu系统自带推荐的驱动，而不是到官网下载的驱动
  - sudo ubuntu-drivers autoinstall 会安装n卡驱动
  - 未避免开机黑屏，重启电脑前先删除或重命名备份文件 /etc/X11/xorg.conf
  - ubuntu 22.04使用nvidia驱动使默认使用x11桌面，要使用wayland需要注释部分行
    - /usr/lib/udev/rules.d/61-gdm.rules
  - 貌似安装完n卡后，只能默认用n卡了，就算 prime-select intel 改为集成显卡，重启后也会变成用n卡
- [Ubuntu 18.04 安装 NVIDIA 显卡驱动](https://zhuanlan.zhihu.com/p/59618999)
  - 安装好驱动程序之后，进入系统无法显示图形化界面，黑屏，左上角有一条白色短线
  - 这个问题这两天遇到好多次了，这里没人列出具体方法，我回答一下，就是驱动和显卡不匹配原因。
    - 如果白线不闪烁，按Ctrl+ shift+F2，进入tty2，用 sudo apt remove --purge  nvidia*，删除安装的驱动，如果是自行下载安装的官方驱动，则sudo ./驱动.run --uninstall。
    - 若白线闪烁，在grub页面进入Ubuntu高级选项，选择低版本的内核可以进入系统，在系统中用终端卸载显卡驱动就可以了
- [Ubuntu 21. 友	Dr. 十月		07-18 01:16
你的身材和你喜欢的身材04 & NVIDIA RTX3080 Ti 驱动安装](https://zhuanlan.zhihu.com/p/396680736)
- [3080电脑安装ubuntu系统及显卡驱动的若干问题总结](https://www.ai2news.com/blog/972612/#google_vignette)
  - 安装完显卡驱动，重启后黑屏，左上角有光标
  - 删除 /etc/X11/xorg.conf后重启即可
- [Can't use Wayland with Nvidia 510 drivers on Ubuntu 22.04 LTS](https://askubuntu.com/questions/1403854)
  - sudo gedit /usr/lib/udev/rules.d/61-gdm.rule
- [Install NVIDIA Driver & Switch Between Intel and NVIDIA in Ubuntu 22.04](https://ubuntuhandbook.org/index.php/2021/06/install-nvidia-driver-switch-between-intel-nvidia-ubuntu/)
  - 切换n卡时只支持 xorg，没有完美的方案

- ubuntu安装字体ttf
  - 创建目录 ~/.fonts，只需将字体粘贴到那里，支持 .ttf 或 .otf
  - 要使字体对所有用户生效，/usr/local/share/fonts
  - [Ubuntu 18.04 LTS 上安装Windows 字体](https://zhuanlan.zhihu.com/p/40434062)
  - [Linux 安装 Windows 字体教程](https://www.bilibili.com/read/cv16481012/)

- ubuntu定时关机，可flatpak安装time-switch
  - sudo apt install -y gshutdown
  - sudo shutdown -h now
  - sudo shutdown -h +60 (just replace 60 with whatever number of minutes you want)

- [System limit for number of file watchers reached](https://stackoverflow.com/questions/53930305)
  - 先修改系统配置，再重载配置
  - echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
  - sudo sysctl --system

- nodejs 版本管理 nvm
  - https://gitee.com/RubyKids/nvm-cn
- jdk 版本管理 sdkman
  - https://sdkman.io/install
- golang 版本管理 g
  - https://github.com/voidint/g

- ubuntu默认的包或旧版包可以在第三方网站下载，但一般包的传递依赖较多，不推荐自己一个个下载
  - https://ubuntu.pkgs.org/

- audio support

```shell
sudo apt-get install -y libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio
```

- [Pin your favorite apps to the dash](https://help.ubuntu.com/stable/ubuntu-help/shell-apps-favorites.html.en)
  - Right-click the application icon and select Add to Favorites.
  - Alternatively, you can click-and-drag the icon into the dash.
  - 直接在spotlight搜索界面将图标拖到dock

- [Adding A Custom 'Open With' Program In Ubuntu 20.04](https://blog.robertelder.org/custom-open-with-program-ubuntu/)
  - 方法很简单，只要将.desktop文件复制到指定位置即可，直接支持设置default open

- [How to Change Mouse Cursor on Ubuntu](https://www.omgubuntu.co.uk/2022/03/how-to-change-mouse-cursor-on-ubuntu)

## software

- 常用软件都可以直接在ubuntu官方包repository找到
  - apt支持 vlc，clementine，goldendict, gimp, inkscape
  - 更推荐使用flatpak安装，支持自动更新
  - https://packages.ubuntu.com/

```shell
sudo apt install -y  sqlite3 libsqlite3-dev sqlitebrowser
```

- 如何运行 . AppImage 文件
  - chmod a+x *. AppImage
  - ./qq. AppImage

- Clementine不支持抓取到last.fm的解决方法
  - mkdir ~/.local/share/Last.fm
  - [Last.fm plugin not submitting scrobbles when track has finished](https://github.com/clementine-player/Clementine/issues/6829)
    - 提供了linux和windows的解决方法，未直接提供了mac的方法，但提供了源码参考
    - https://github.com/lastfm/liblastfm/blob/master/src/misc.cpp#L58

- 腾讯会议的linux版本发布之后，我去体验了一把，提示不支持wayland
  - https://blog.csdn.net/m0_52640673/article/details/124911402
  - sudo vim /etc/gdm3/custom.conf
  - 取消注释 # WaylandEnable=false
  - sudo service gdm3 restart
  - 也可以不使用wayland不支持的产品，比如不用腾讯会议而用飞书

- chrome ubuntu版每次打开都要手动点 restore 恢复上次网页
  - [chrome needs to restore tabs on every reboot](https://askubuntu.com/questions)
  - 在设置里面关闭退出chrome后在后台继续运行app
  - chrome点击标题栏不能全屏，方法1是打开系统标题栏，方法2是拖拽到屏幕顶部会自动全屏

- typora
  - [Typora软件打不开了](https://www.csdn.net/tags/MtTaMgzsNDE4OTgzLWJsb2cO0O0O.html)
    - https://download.typora.io/linux/typora_0.9.98_amd64.deb
    - https://download.typora.io/windows/typora-update-x64-1213.exe

- screenkey不支持wayland的解决方案
  - GDK_BACKEND=x11 screenkey
  - [Missing support for wayland](https://gitlab.com/screenkey/screenkey/-/issues/61)

## dev

- ubuntu-mysql
  - [ubuntu20.04安装MySQL以及MySQL-workbench可视化工具](https://blog.csdn.net/delilahy123/article/details/124834998)

- ubuntu-postgresql
  - [PostgreSQL之Ubuntu 20.04下的简单安装与相关设置](https://www.cnblogs.com/among-the-stars/p/15585198.html)
  - [如何在 Ubuntu 20.04 上安装 PostgreSQL](https://zhuanlan.zhihu.com/p/143156636)
  - [postgresql安装配置](https://www.xzhongwei.com/post/480)
  - [Ubuntu18.04安装Postgresql与配置](https://www.blog8090.com/ubuntu18-04an-zhuang-postgresqlyu-pei-zhi/)
# win11

## guide

## os-starter

- pe安装系统需要鼠标，键盘操作太困难
  - 需要pe系统支持12代触摸板才可以
  - [AnglePE](https://www.angel-pe.cn/2022/26/20/angeltspeclksddnzzxttwjc%d1%81ax.html)

- [预装Windows 11系统的新电脑怎么跳过联网验机？](https://zhuanlan.zhihu.com/p/4253264 03)
  - 开机出现如下界面，同时按下组合键Ctrl+Shift+F3。（部分机型没反应可以试试Ctrl+Shift+F3+Fn）
  - 更推荐直接重装

- [使用WinNTSetup安装win10时提示efi part有红叉(win10安装UEFI系统安装）](https://www.cnblogs.com/sjdn/p/8975583.html)
  - 引导盘要选esp分区，也就是第一个分区100/300M空间的那个

## software

- ms-office 2021官方镜像下载安装激活一条龙
  - https://www.cnblogs.com/hushaojun/p/15967885.html

- adobe 大师版全家桶、sp版独立包
  - https://www.nite07.com/adobe/
  - 密码 nite07
# mac
- [macos 如何实现 windows 的双击触摸板进行拖动 - V2EX](https://v2ex.com/t/846111)
  - 触控板拖动有三种方式可以设置。
