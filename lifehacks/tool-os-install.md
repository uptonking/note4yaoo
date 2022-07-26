---
title: tool-os-install
tags: [iot, linux, operating-system]
created: 2020-11-25T08:20:22.803Z
modified: 2020-12-22T12:42:14.745Z
---

# tool-os-install

# guide

# ubuntu22.04

## guide

## os-starter

- [装了5次Ubuntu，告诉你win10+Ubuntu双系统的正确打开方式](https://zhuanlan.zhihu.com/p/101307629)

- 在ubuntu software update打勾可选源，以及配置apt mirror

- ubuntu开机自动挂载win-ntfs硬盘
  - [ubuntu 配置/etc/fstab参数实现开机自动挂载硬盘](https://blog.csdn.net/u010632165/article/details/89597522)
  - [UbuntuHelp: fstab](https://wiki.ubuntu.org.cn/UbuntuHelp:Fstab)
    - [Device] [Mount Point] [File System Type] [Options] [Dump/backup] [Pass]
    - [pass]: Controls the order in which fsck checks the device/partition for errors at boot time. The root device should be 1. Other partitions should be 2, or 0 to disable checking.

- 当三方apt源很慢时，可以尝试手机移动网络，而不是电信宽带网络
  - 特别是安装 vscode、git-core/ppa

- [Qv2ray 使用详解](https://www.rultr.com/tutorials/4200.html)
  - 和win平台的v2ray客户端一样简单，导入账号信息即可科学上网

- chinese-input
  - rime输入法配置的迁移比想像中要快得多，只需要拷贝文件夹
  - sogou ubuntu
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
  - 字体对所有用户生效， /usr/local/share/fonts
  - [Ubuntu 18.04 LTS 上安装Windows 字体](https://zhuanlan.zhihu.com/p/40434062)
  - [Linux 安装 Windows 字体教程](https://www.bilibili.com/read/cv16481012/)

- ubuntu定时关机
  - gshutdown
  - sudo shutdown -h now
  - sudo shutdown -h +60 (just replace 60 with whatever number of minutes you want)

## software

- 常用软件都可以直接在ubuntu官方包repository找到
  - 包括 vlc，clementine，goldendict, gimp, inkscape
  - https://packages.ubuntu.com/

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
