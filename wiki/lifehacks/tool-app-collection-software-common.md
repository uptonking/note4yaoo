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
- music
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
- learning
  - goldendict
      - 1.5.0-RC2 - 201907
      - win/linux
      - http://goldendict.org/
          - https://github.com/goldendict/goldendict
          - GPLv3
  - dict:eudic
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
# calendar
- https://github.com/lwlsw/Chinese-Lunar-Calendar-ics
  - 现成的中国农历ics文件 2015-2100
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
# more
- https://github.com/coolshou/dukto
  - /cpp
  - Dukto LAN file transfer tool
