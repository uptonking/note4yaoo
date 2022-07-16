---
title: tool-os-install
tags: [iot, linux, operating-system]
created: '2020-11-25T08:20:22.803Z'
modified: '2020-12-22T12:42:14.745Z'
---

# tool-os-install

# guide

# starter

# ubuntu22.04

## guide

## os-starter

- 当三方apt源很慢时，可以尝试手机移动网络，而不是电信宽带网络

- [装了5次Ubuntu，告诉你win10+Ubuntu双系统的正确打开方式](https://zhuanlan.zhihu.com/p/101307629)

- [Qv2ray 使用详解](https://www.rultr.com/tutorials/4200.html)
  - 和win平台的v2ray客户端一样简单，导入账号信息即可科学上网

- chinese-input
  - sogou ubuntu
  - [在Ubuntu下安装讯飞输入法linux版以及卸载方法](https://yoki.moe/Intstu/24.html)
    - xunfei  http://packages.deepin.com/deepin/pool/non-free/i/iflyime/
  - baidu https://srf.baidu.com/site/guanwang_linux/index.html

- [How to Install Fonts on Ubuntu 20.04 Focal Fossa Linux](https://linuxconfig.org/how-to-install-fonts-on-ubuntu-20-04-focal-fossa-linux)
  - sudo cp ~/Downloads/Bitwise.ttf /usr/local/share/fonts/sample/

- ubuntu开机自动挂载win-ntfs硬盘
  - [ubuntu 配置/etc/fstab参数实现开机自动挂载硬盘](https://blog.csdn.net/u010632165/article/details/89597522)
  - [UbuntuHelp: fstab](https://wiki.ubuntu.org.cn/UbuntuHelp:Fstab)
    - [Device] [Mount Point] [File System Type] [Options] [Dump/backup] [Pass]
    - [pass]: Controls the order in which fsck checks the device/partition for errors at boot time. The root device should be 1. Other partitions should be 2, or 0 to disable checking.

- 如何运行 . AppImage 文件
  - chmod a+x *. AppImage
  - ./qq. AppImage

- 国内 nvm
  - https://gitee.com/RubyKids/nvm-cn
  - bash -c "$(curl -fsSL https://gitee.com/RubyKids/nvm-cn/raw/master/install.sh)"

## software

- 常用软件都可以直接在ubuntu官方包repository找到
  - 包括 vlc，clementine，goldendict
  - https://packages.ubuntu.com/

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
# win11

## guide

## os-starter

- pe安装系统需要鼠标，键盘操作太困难
  - 需要pe支持12代触摸板才可以
  - [AnglePE](https://www.angel-pe.cn/2022/26/20/angeltspeclksddnzzxttwjc%d1%81ax.html)

- [预装Windows 11系统的新电脑怎么跳过联网验机？](https://zhuanlan.zhihu.com/p/4253264 03)
  - 开机出现如下界面，同时按下组合键Ctrl+Shift+F3。（部分机型没反应可以试试Ctrl+Shift+F3+Fn）

- [使用WinNTSetup安装win10时提示efi part有红叉(win10安装UEFI系统安装）](https://www.cnblogs.com/sjdn/p/8975583.html)
  - 引导盘要选esp分区，也就是第一个分区100/300M空间的那个

## software

- ms-Office 2021官方镜像下载安装激活一条龙
  - https://www.cnblogs.com/hushaojun/p/15967885.html

- adobe 大师版全家桶、sp版独立包
  - https://www.nite07.com/adobe/
  - 密码 nite07
