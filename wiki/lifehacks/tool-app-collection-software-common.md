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

## dict

- tips
  - 平时用谷歌就行了
- 美式英语
  - American Heritage
  - Webster
  - 买美式词典一般可选梅–韦氏、美国传统
- 英式英语
  - oxford
  - collins
  - Chambers
  - 买英式词典一般可选牛津、朗文、麦克米伦
- esl(English as a second or foreign language
)
  - Cambridge
  - Longman
  - Macmillan

- dicts
  - [词库使用心得: 同一系列词典中，只留下最精美的和最大的](https://forum.freemdict.com/t/topic/1090)
  - [十大mdict——对你最有用的十大mdict是哪些？](https://forum.freemdict.com/t/topic/9012)

- goldendict /GPLv3
  - 1.5.0-RC2 - 201907
  - win/linux
  - https://github.com/goldendict/goldendict
    - http://goldendict.org/
  - https://github.com/xiaoyifang/goldendict-ng
    - Some significant features of this fork
    - webengine with latest html/css feature support
    - support >4GB dictionary
    - support Qt5.15.2 and higher ,include latest Qt6

- 欧路词典支持mdx
  - [欧路词典客户端实用大更新，在线词典和翻译引擎开源](https://forum.freemdict.com/t/topic/11002)

- https://github.com/ikey4u/wikit
  - Wikit is a free and open-source dictionary program that enable you translate word for different languages
  - Desktop application for Windows, Linux and MacOS which is developed using tauri and yew.
  - [全新的mdx/mdd词典制作工具](https://forum.freemdict.com/t/topic/6621)
  - wikit 的本地词典可以从 mdx 直接生成, 或者从 mdx 的源码生成.
  - wikit 的server端可以去加载另外一个 server 端的词典, 也就是词典中继, 你可以中继另外一个人的词典

- 词库资料
  - [【教学】三、MDX MDD 基础知识](https://forum.freemdict.com/t/topic/1823)
  - [词库种类及使用方法](https://forum.freemdict.com/t/topic/17795)
  - mdx一般是主体的文本，网页，索引头
  - mdd是对应的媒体文件，发音，图片，czss，甚至视频等
  - 有可能只有mdx，也可能是mdx+mdd，即使后者，也只是一部字典，而非多部。但是不可能只有mdd。
  - 坛内常见某字典的mdx（文字）和css文件（排版）更新，mdd（音频和图片数据）却一直不变的情况，这时你也许需要找好几个帖子才能凑齐三个（或更多个）同名但不同后缀的文件才能安好一本词典

- [FreeMdict - mdx mdd download](https://freemdict.com/)
  - https://downloads.freemdict.com
  - https://search.freemdict.com/
  - https://forum.freemdict.com/
- [MW Online 2020四合一](https://forum.freemdict.com/t/topic/8284)
  - [Merriam-Webster Unabridged Online 2020 - 英英](https://forum.freemdict.com/t/topic/2684)
  - [Merriam-Webster Dictionary Online(2020) - 英英](https://forum.freemdict.com/t/topic/4030)
- [關於AHD，有沒有推薦的mdx？ - 词典及语言学习交流](https://forum.freemdict.com/t/topic/18087)
- [Oald10(3月5日修复词汇列表一些词汇链接错误的问题) - 英英](https://forum.freemdict.com/t/topic/10925)
  - [隆重推出 牛津英语同义词学习词典](https://forum.freemdict.com/t/topic/21884)
- [LDOCE5+++Activ (2021-12-23) - 英汉](https://forum.freemdict.com/t/topic/9947)
- [柯林斯cobuild高阶双解词典第八版+反查 - 英汉汉英-英式](https://forum.freemdict.com/t/topic/9207)

- [关于21世纪大英汉词典的版本 另外求隔壁站 henices 的版](https://forum.freemdict.com/t/topic/1976/39)
  - 大家惦记的henices版本来了。37万的词头，加上词组

- [汉英词典（第三版）A Chinese-English Dictionary - 汉英 外研社](https://forum.freemdict.com/t/topic/2071/1)

- [现代汉语词典7-[施工现场]](https://forum.freemdict.com/t/topic/12102)
  - [现代汉语词典第7版](https://forum.freemdict.com/t/topic/4445)
- [一些汉语词典（恢复部分词典的图片等数据） - 汉汉](https://forum.freemdict.com/t/topic/16533)

- [掌上百科 - PDAWIKI](https://www.pdawiki.com/forum/forum.php)
  - [PDAWIKI 2008-2023 存档 - 资源分享 - FreeMdict Forum](https://forum.freemdict.com/t/topic/20443)
  - [一个告别声明 - 掌上百科站务处_202303](https://www.pdawiki.com/forum/forum.php?mod=viewthread&tid=48789&extra=page%3D1)
  - 从2008年开始，掌上百科作为词典爱好者论坛，为大家提供了一个分享MDict等软件自制词库的平台，近两年由于部分用户利用版权数据牟利，打击了出版方数字化的积极性，也给管理团队造成不必要的法律困扰，
  - 决定自2023年4月1日起，关闭涉版权部分板块，如MDict 词库资源区、掌上百科编纂处、资源专区等，此去江湖有缘再见！
- [一百多GB的MDX词库资源集合下载](https://mdict.org/post/mdx/)
  - https://mdx.mdict.org/
- https://github.com/Dictionaryphile/All_Dictionaries
  - 最全在线词典网站导航

## wiki

- zhwiki dump
  - https://dumps.wikimedia.org/zhwiki/
  - [中文喂鸡百科20230320文字版](https://www.pdawiki.com/forum/forum.php?mod=viewthread&tid=22626&extra=page%3D1)
  - [英文喂鸡百科20190401文字试用版](https://www.pdawiki.com/forum/forum.php?mod=viewthread&tid=17377&extra=page%3D1)

- wiki-like
  - [第三次基本结束・Wiktionary2023 + OxfordreFerence+中英专业词典](https://forum.freemdict.com/t/topic/10746)
  - [中国文学大辞典[1991][马良春]](https://forum.freemdict.com/t/topic/13400)
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
