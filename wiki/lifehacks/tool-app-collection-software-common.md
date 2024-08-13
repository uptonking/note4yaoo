---
title: tool-app-collection-software-common
tags: [app, software, subscription, tool]
created: 2019-07-08T04:10:28.254Z
modified: 2022-11-07T10:26:22.510Z
---

# tool-app-collection-software-common

# guide

- search
  - 搜索某一类资料时，加上.pdf或.docx之类的后缀，可能质量更高
# files
- 打开或查看大文件，可使用主流ide，如kde-kate/sublime/nodepad
# 软件选择参考
- 优先选择: 长期更新，维护活跃，自用免费
- 大公司支持
  - vscode和atom中选择vscode，因为github被microsoft收购了
  - 账户信息、ide配置、插件扩展的同步，一般只有大公司愿意免费提供
- 免费
  - 若不免费，可寻找民间替代品
# 软件使用体验xp
- Ubuntu开启显示隐藏文件后，文件夹的大小会变大，如git项目下的.git目录有时非常大
- 浏览视频网站时，有时会很慢，甚至打不开，如u2b，可以开启手机屏幕移动端浏览
- 常用端口(默认可不写)
  - HTTP：80
  - HTTPS：443
  - SSH：22
  - DNS：53
  - FTP：21
  - MYSQL：3306
- 可用ping检测ip，用telnet检测端口
# productivity
- 局域网传输工具
  - 飞鸽传书

## vim

- vim你们都:wq保存退出么，听说过直接按 shift zz 保存退出么
  - 一直用:x。x跟wq是不同的。如果內容沒有改變，x不會刷新文件時間。而wq是寫入和關閉兩個命令，無論內容是否改變都會執行寫入並刷新文件時間。
  - 原推里的 ZZ 跟 :x 一样的行为

## figma

- 有时原型稿形状的背景色很难选到准确的图形来查看
  - 解决方法是在pages下方的layers点击相近的父层或子层来确认
# pc-dir
- 网易云音乐
  - /home/yaoo/.cache/netease-cloud-music/CachedSongs

- qq-linux
  - /home/yaoo/Documents/opt/portable/message/Feige_for_64_Linux_ipmsg/
# software
- video
  - vlc
    - 3.0.7 - 201907
    - win/linux/mac/android/ios
    - http://www.videolan.org/vlc/
        - https://github.com/videolan/vlc
        - GPLv2
  - splayerX
    - 4.1.16 - 201907
    - win only
    - https://www.splayer.org/
        - https://github.com/chiflix/splayerx
          - GPLv3

- office
  - notable: note-taking
  - pocket
  - wps sheet/pdf
  - pdf: foxit reader/pdf studio
  - draw.io
  - dev
      - poi - Apache2.0
      - itext 5+ - AGPL
      - openpdf 1.2.21 - LGPL/MPL
- social
  - qq/tim
  - wechat
  - skype
  - teamviewer
- finance
  - bank
- health
  - sleep cycle
  - runner/keeper
- os
  - app store
  - browser
  - email
  - im
    - [基于rime配置的类搜狗输入法](https://github.com/fkxxyz/rime-cloverpinyin)
  - screen time    
  - contacts
  - camera
  - qr code scanner
  - shadowsocks
  - calendar
  - calculator
- tools
  - wps note/google keep
  - netdisk
  - emarket
# im-wechat
- https://github.com/lovechoudoufu/wechat_for_linux
  - 安装包丢在Releases中了，一共三个版本：wechat-beta_1.0.0.145_amd64.deb, wechat-beta_1.0.0.150_arm64.deb, wechat-beta_1.0.1.212_loongarch64.deb

- [微信为什么不弄个文字转语音？ - 知乎](https://www.zhihu.com/question/607788362)
  - 这个功能已经出了，需要更新到版本。操作步骤：`我→设置→关怀模式→开启→打开“听文字消息”`开启后，点一下聊天中的文字消息就能听到了
# search
- 网盘搜索
  - [有哪些好用不火的网盘资源搜索工具，求推荐？ - 知乎](https://www.zhihu.com/question/449835465/answers/updated)
  - [有哪些比较好用的网盘搜索引擎？ - 知乎](https://www.zhihu.com/question/552116773/answers/updated)
  - [小云搜索 - 轻松简单的云盘搜索 | 网盘搜索引擎](https://www.yunso.net/)
  - [猫狸盘搜 - 阿里云盘搜索神器](https://www.alipansou.com/)
  - [易搜-网盘搜索](https://yiso.fun/)
  - [咔帕搜索 - 资源超丰富的综合云盘资源搜索网站！](https://www.cuppaso.com/)
# music
- local: clementine 
  - 1.31 - 201907
  - win/linux/mac
  - 支持last.fm，支持播放列表保存到本地
  - 可手动添加歌词并显示在左侧面板
  - https://www.clementine-player.org/
    - https://github.com/clementine-player/clementine
    - GPLv3
  - [last.fm plugin not submitting scrobbles when track has finished](https://github.com/clementine-player/Clementine/issues/6829)
    - 对Linux，创建 `mkdir ~/.local/share/Last.fm` 目录
    - 对win10，In order to have Clementine scrobble tracks on Windows you need to create a folder at:` %HOMEPATH%\AppData\Local\Last.fm` 目录
- local-more
  - Tauon Music Box: linux only
    - 可显示滚动歌词/synced lyrics，但歌词的时间戳毫秒位不能是3位
  - quodlibet 显示歌词的界面较简单

- online: 洛雪音乐助手
  - 整合第3方音乐搜索与下载
  - 可选择同时下载歌词
- online-more
  - netease cloud music
  - spotify
  - apple music 资源较全，元数据较全

- music-tag-id3
  - last.fm: 记录听歌信息
  - kid3 支持编辑各种标签，缺点是year属性格式只能到年，不能到月日(月份前是否有0)
  - mp3tag: win only
- lyric
  - 歌词要考虑
    - 歌词自身格式：lrc，txt，每行是否带有时间戳，时间戳毫秒支持几位，是否要去头无效行
    - id3版本，很多itunes下载的音乐是mp4标签，mp4标签难修改
    - 读写id3的播放器
    - 推荐方案：单文件包含所有信息，附加歌词用于滚动显示
  - 歌词搜索
    - 直接搜索歌词lrc文件，国外歌词很少有带时间戳的lrc
    - 类似洛雪音乐助手可直接下载音乐文件及歌词，但很多都有版权问题
    - https://www.azlyrics.com/
    - https://mojim.com/ 魔镜歌词网
    - https://www.kugeci.com 酷歌词，带时间戳
    - 木兰词

- 音乐资源aac/mp3
  - [无损生活 - 音乐搜索, 音乐在线试听, 下载, 在线解析网](https://flac.life/)
- 音乐资源-album
  - [CD包音乐网 - 专业的无损音乐论坛, APE, FLAC, WAV, CD, MP3专辑网站！](https://www.cdbao.net/)
  - [易音 - SACDR. NET](https://sacdr.net/)
  - [91flac](https://www.91flac.com/album_list)
    - 主页无法访问，但二级页面可访问
  - ❌ 已倒闭
    - [mixrnb](http://www.mixrnb.com/)

- https://github.com/lyswhut/lx-music-desktop /apache2/202406/ts/vue
  - https://lyswhut.github.io/lx-music-doc/
  - 洛雪音乐助手桌面版, 基于 Electron + Vue 开发的音乐软件
  - [洛雪音乐助手+六音自定义音源 v1.2.0-六音](https://www.sixyin.com/8498.html)
  - [自己收集的几个可用源 _202402](https://github.com/lyswhut/lx-music-desktop/issues/1769)
  - [LX Music 项目发展调整与新项目计划 _202405](https://github.com/lyswhut/lx-music-desktop/issues/1912)
    - 最初 LX 的开发线路是抱着对技术的学习与研究的目的，集成国内常用音乐平台以解决音乐查找与播放问题，但随着大家对音乐版权的重视，以及来自官方音乐平台的压力，这条路已难以走下去
    - 我决定发起一个全新的项目，用于提供一套面向个人用户的个人私有云音乐解决方案。
  - [LX 以后的发展方向 _202310](https://github.com/lyswhut/lx-music-desktop/issues/1643)
    - LX于2023年10月18日收到了腾讯的警告信，要求停止提供软件内置的连接到他们平台的在线播放及下载服务，所以我们决定关停内置的“临时接口”与“测试接口”。
# calendar
- https://github.com/lwlsw/Chinese-Lunar-Calendar-ics
  - 现成的中国农历ics文件 2015-2100

- https://github.com/lanceliao/china-holiday-calender
  - 中国节假日、调休、补班日历，ICS格式，可供IPhone、Google Calendar、Outlook等客户端订阅，包含节假日API
# toolkit
- browser
  - chrome
  - firefox/opera/yandex/vivaldi/brave/edge
- java反编译
  - jd-gui，win/linux/mac, GPLv3
    - https://github.com/java-decompiler/jd-core
  - Android反编译gui工具Jadx
  - java反编译类库 fernflower，由intellij idea作为插件开源，Apache2.0
    - https://github.com/fesh0r/fernflower
- ide
  - vscode
  - intellij idea community edition
  - jedit
- db
  - dbeaver
  - sqlpower-architect
- uml
- astah communtiy 6.9 (discontinued)
- web
  - postman
- file
  - transfer: dukto, filezilla
- geo
  - qgis
  - udig
- map
  - baidu
  - gaode
  - openstreetmap
- capture
  - PrtSc key
  - os hotkey
  - peek(ubuntu)
  - gif/video: obs studio  
- image
  - XnView
  - GIMP
  - inkscape
- markdown
  - marp
  - flexmark-java
- ppt
  - PptxGenJS
      - https://github.com/gitbrent/PptxGenJS/
      - https://gitbrent.github.io/PptxGenJS
      - js to pptx
  - webslides
      - https://github.com/webslides/webslides
- network
  - wireshark
- blog
  - jbake
  - hexo
  - gatsby
# device

## Chromebook

## FydeOS

- 原名Flint OS，基于驱动Chrome OS及谷歌浏览器的开源项目二次开发，继承Chrome OS所有特性，适配更多硬件品类，为中国用户定制的本土化修改
# company
- https://github.com/xuthus5/fedora-packager
  - 目前维护了 fedora 下的 wechat, wxwork, deepin-wine6-stable, deepin-wine-helper 等.
# os-ip
- [站长工具 - 站长之家](https://tool.chinaz.com/)
  - 首页默认显示ip地址，还有单独页面 https://ip.chinaz.com/

- [ip138.com iP地址查询--手机号码查询归属地](https://www.ip138.com/)
  - [iP测漏 - 全方位检测您的IP地址](https://ipcelou.com/)
# download
- https://github.com/agalwood/Motrix
  - https://motrix.app/
  - Motrix 是一款全能的下载工具，支持下载 HTTP、FTP、BT、磁力链等资源。它的界面简洁易用，希望大家喜欢 
  - 我是个兴趣使然的桌面应用开发者，利用搬砖之余开发了 Motrix
  - 建议使用安装包（Motrix-Setup-x.y.z.exe）安装 Motrix 以确保完整的体验，例如关联 torrent 文件，捕获磁力链等。
  - 支持BT和磁力链任务
  - 单任务最高支持 64 线程下载
  - UPnP & NAT-PMP 端口映射
  - [关于资源分享](https://github.com/agalwood/Motrix/discussions/1221)
    - 我在资源分享里面看到其他客户端分享给我们的资源，唯独迅雷在线 (Xunlei) 只有上传数据，没有下载数据，我们是不是在某个地方设置个屏蔽某些客户端或者某些IP。 迅雷违背了BT协议，只索取，不付出。迅雷不具备有分享精神，我们也应该拒绝分享资源给他，没有奉献精神。
    - 你可以尝试使用qbittorrent，那个可以开反吸血
# more
- https://github.com/coolshou/dukto
  - /cpp
  - Dukto LAN file transfer tool
