---
title: tool-app-collection-saas-xp
tags: [app, saas, tool, xp]
created: 2020-07-12T15:27:22.003Z
modified: 2022-11-07T10:25:12.034Z
---

# tool-app-collection-saas-xp

# guide

- username
  - uptonking/yorke/yaork
  - [names.org - The Meaning Of Names](https://www.names.org/)

- 提高feed内容流中有效信息的密度
  - 暂停浏览较长时间后，平台recsys推荐流的信息更有效
  - 长时间高频率浏览时，个人的follow关注流信息更有效

- https://github.com/iamadamdev/bypass-paywalls-chrome
  - help bypass paywalls for selected sites.
  - Bypass the following sites' paywalls: bloomberg, fortune, glassdoor, medium, national geographic, quora, vanity fair, vulture
# tech-community
- discord
  - tiptap
  - plate
  - lexical
  - tanstack
  - luckysheet
  - evolu/cr-sqlite
  - yjs
  - more: nocodb, payloadcms

- slack
  - slate
  - automerge
  - couchdb
  - react-data-grid
  - sequelize
  - lightdash
  - elm
  - more: d3, prisma

- forum-site
  - prosemirror
  - [TiddlyWiki: Talk TW - Community discussion forum about TiddlyWiki](https://talk.tiddlywiki.org/)
# search-google
- [Tips for efficiently Googling. Search by:](https://twitter.com/addyosmani/status/1444195449095737346)
  - Exact match > `"javascript modules"`
  - Scope to site > `site:github.com js`
  - After a date > `javascript after:2021`
  - Before > `javascript before:2019`
  - Exclude a phrase > `javascript -es5`
  - Number range > `javascript 2015..2021`
  - Wildcard > `"fix the * error"`

- 实测 `after:2020` 的搜索结果都是2021年的，after:2021当前年份就显示搜索结果为空了

- [知乎怎么查看自己评论过的问题？](https://www.zhihu.com/question/35126639/answers/updated)
  - [如何找到自己在知乎里发表的评论？](https://www.zhihu.com/question/19585656/answers/updated)

- dogedoge 多吉搜索被知乎屏蔽了

- [根据需求进行定向搜索，以下是常用的语法和规则（比如：找竞品调研，只找pdf「filetype:pdf」），参见图片的示例](https://twitter.com/xianlezheng/status/1729505482212008157)
  - 查询子域名下的关键词（不包含www站点）： ssl -site:http://ilikejobs.com site:*.ilikejobs.com
# 知乎/掘金/v2ex/链滴
- 有时候评论的内容比回答的内容更有意思

- [知乎违规记录](https://www.zhihu.com/community/reported)

- alternatives
  - B站博客
  - [CNode：Node.js专业中文社区](https://cnodejs.org/)
  - [NodeSeek - v2ex-like](https://www.nodeseek.com/)
# 数据库/pingcap
- [TiDB 社区](https://asktug.com/)
- [TiDB Internals](https://internals.tidb.io/)
# reddit

# hacker-news

- usage-xp
  - 有时网站无法登录或内容无法显示，可能不是网络原因而是服务器宕机了，可在twitter社交平台搜索 `hacker news down` 按时间倒序判断最新状态

- [搜索版](https://hn.algolia.com/)
  - 支持rss订阅，如https://hn.algolia.com/userfeed/nullwasamistake

- 检测github或其他url是否在hn/reddit讨论过
  - [Discussions around the Web - discu.eu](https://discu.eu/)

- hn-like
  - https://lobste.rs/
# twitter
- search
  - 搜索关键词时，可加上'min_replies:1'的条件，筛选出被讨论过的质量更高的内容
  - https://github.com/igorbrigadir/twitter-advanced-search
  - 搜索转发的内容
    - [Use Twitter Advanced search to find retweets made by a single account? ](https://webapps.stackexchange.com/questions/92616)
    - from:@username include:nativeretweets filter:nativeretweets logseq

- export
  - 支持导出tweets、replies、likes
  - 不支持导出bookmarks

- how-to follow hashtag
  - twitter-deck，添加搜索关键词作为自定义栏
    - https://github.com/eramdam/BetterTweetDeck
    - [不支持添加bookmark](https://github.com/eramdam/BetterTweetDeck/issues/730)
  - 使用twitter search，然后保存搜索
  - 不使用hashtag，使用list收集相关用户
  - [How To Follow a Hashtag on Twitter - Qwitter](https://useqwitter.com/how-to-follow-a-hashtag-on-twitter/)

- tweetdeck
  - 点击一条tweet的右上角时间，可以在新标签页打开原网站；知乎也才用这种设计

- tweetdeck-alternatives

## download-video/image

- 浏览器扩展经常失效，更好的方式是在github查找下载工具的源码，自己修改

- https://github.com/okikio/inthistweet
  - Futuristic sparkles twitter image, gif and video downloader. 
  - Enter a Tweet URL, click search, and download the image/videos in it.

- video-url-4test
  - https://twitter.com/ZiqiPeng/status/1347840219966423042
  - https://twitter.com/mondaydotcom/status/1346413150913130498
- tools
  - https://github.com/Stress-Free-AI/twitter_downloader
    - https://easiersave.com/
    - 有的广告视频下载不了
  - https://videodownloaderbot.com/
  - https://github.com/Momo707577045/m3u8-downloader
    - http://blog.luckly-mjw.cn/tool-show/m3u8-downloader/index.html
    - 当前下载卡住时，可以尝试刷新页面，再次输入url开始下载
    - 一个m3u8的视频经常会提供320/480/720多种分辨率，可是换一种m3u8地址
# mastodon
- tips
  - bookmarks支持export，favorites不支持export

- ui-alternatives
  - https://phanpy.social/ 类似tweetdeck的看板界面

- yaoo-accounts-social
  - cons
    - 用户的toots和retweet服务器可能不会保存，需要用户自己手动备份
  - pros
    - 用户可以自己搭建server

- mastodon
  - https://fosstodon.org/
    - open source software
  - https://mastodon.social/
    - twitter-like
  - https://vis.social/
    - data viz and d3
  - https://en.osm.town/
    - OpenStreetMap
  - https://mapstodon.space/
    - map
  - https://m.cmx.im/
    - 中文社区

- [Does mastodon has advance search](https://stackoverflow.com/questions/74570622/does-mastodon-has-advance-search)
  - This is not possible (intentionally / by design).
  - Mastodon supports full-text search when ElasticSearch is available. Mastodon’s full-text search allows logged in users to find results from their own statuses, their mentions, their favourites, and their bookmarks. It deliberately does not allow searching for arbitrary strings in the entire database.
# telegram
- 资源搜索
  - [Meow. TG-做最懂你的TG搜索](https://meow.tg/)
  - [sssoou.com](https://www.sssoou.com/)
  - [千帆搜索 - 资源超丰富的电报中文搜索引擎，需注册](https://tg.qianfan.app/)

- https://github.com/Neet-Nestor/Telegram-Media-Downloader /202311/js
  - A Tampermonkey script allowing you to download images and videos from Telegram web even if the group restricts downloading

- [TG中文群 - TGCNG. COM](https://www.tgcng.com/)
  - 不建议随意搜索，从相关群或论坛的讨论信息能找到更准确的信息
  - [电报频道，群组，机器人列表](https://telegramchannels.me/zh)
  - [telegram群组-电报群大全- Telghub](https://www.telghub.com/)
  - [电报telegram群全网检索 - TgSql.com](https://tgsql.com/search)

- https://github.com/morethanwords/tweb /webk
  - Telegram Web K, GPL v3
- https://github.com/Ajaxy/telegram-tt /webz/weba
  - Telegram Web A, GPL v3

- [Why there are two web versions? WebZ and WebK](https://www.reddit.com/r/Telegram/comments/yjzdq3/why_there_are_two_web_versions/)
  - Made by two different devs and thus have different code bases, which means they work at different speeds, they might have different features, etc. Both are official.
  - There’s an internal competition running between the two and eventually one will prevail.
- [Telegram released 2 new web apps](https://www.reddit.com/r/Telegram/comments/mqp2m4/telegram_released_2_new_web_apps/)
  - [What is the difference between webk.telegram.org and webz.telegram.org ?](https://www.reddit.com/r/Telegram/comments/mzicwm/what_is_the_difference_between_webktelegramorg/)
  - Telegram believes that having multiple teams that compete will be beneficial. 
  - if you look at the dependencies and code, WebZ is written in React/teact, WebK does not have any popular libraries (React, Vue, Angular, Svelte...) in the dependencies and in the source code is written in native js (ts)
  - I noticed that WebK is running way faster on my potato pc than WebZ, Z has more features tho
# discord
- https://github.com/bb010g/betterdiscordctl
  - A manager for BetterDiscord on Linux.
  - https://github.com/BetterDiscord/BetterDiscord
  - https://betterdiscord.app/

- [Use SOCKS5 proxy with Discord on Linux](https://gist.github.com/mzpqnxow/ca4b4ae0accf2d3b275537332ccbe86e)

```shell
flatpak run com.discordapp.Discord --proxy-server="socks5://127.0.0.1:1080"
```

# 邮箱注册
- 不需要手机号的邮箱
  - mail.protonmail.com
  - ref
    - [请问现在有什么不用手机号可以注册的邮箱](https://v2ex.com/t/683308)
# 图片资源
- unsplash镜像战
  - https://unsplash.dogedoge.com/
# video/tv
- 资源搜索
  - 搜索资源前先确定资源准确或替代品，豆瓣 doulist 名著 电影
  - 可直接查找资源典型名称，参考字幕组的命名规则

- 资源下载
  - 各个网盘有的已限速，有的即将限速

- 迅雷技巧
  - 种子或磁力无法下载时，可尝试添加到云盘，然后直接从迅雷云盘下载，大多很快有时也慢
  - 针对有版权问题的资源，在下载时可重命名任务或文件，但仍可能失败
  - 新建任务时，可选择下载到 本地 和或 迅雷云盘，若下载到本地的任务失败，可检查下载到云盘的任务是否成功，若成功则可以取消本地任务，直接从云盘下载资源
  - 磁力转种子
    - https://magnet-vip.com/
  

- https://github.com/fanmingming/live
  - 一个国内可直连的直播源分享项目

- 在线影视
  - closed

- 下载资源
  - [BT天堂 - 最新高清电影720P|1080P免费下载](https://www.bt-tt.com/)
  - https://www.domp4.net/
  - 磁力猫 https://clm8.in/
  - 电影天堂 https://dytt89.com/
  - 人人电影网 https://www.rrdynb.com/movie/2022/1210/31616.html
  - domp4.com
  - bt世界 btsj5.com
  - www.bdys.me
  - 66影视 https://www.66yingshi.com/
  - 电影镇 https://dy.town/
  - sites-blacklist
    - uump4悠悠 蓝光特效字幕系列 画质偏红
    - 不喜欢黄色字幕样式且不可隐藏
  
- 历史/文学/小说/名著
  - 阿里云盘
    - https://www.aliyundrive.com/s/ihS2xuUjrEq/folder/6219e157b4212ec85ef94bb7b597f11efd57a227
    - https://www.aliyundrive.com/s/WAsmRweh9QP/folder/629f5a635a2062e682d94f6fb5473c2fe62fdba2
  - 资源参考
    - [中国小说改编的电影](https://www.douban.com/doulist/42582881/)

- 网盘
  - yunpan1域名更换频繁, https://yunpan1.cc/

- youtube-download
  - https://save.tube/
    - 支持video、audio
  - https://x2mate.com/
    - 下载速度快
  - https://yt1s.ltd/
  - https://downloaderto.com/
  - https://entiretools.com/youtube-downloader

- youtube-playlist-download
  - https://github.com/shaked6540/YoutubePlaylistDownloader
    - windows only
  - https://y2down.cc/en/youtube-playlist.html
  - https://playlist.downloader.is/
  - https://ytshorts.savetube.me/youtube-playlist-downloader-1
# gfw-proxy
- [googlehosts 作者放弃维护了吗？几个月没更新了](https://github.com/googlehosts/hosts/issues/503)
  - 新发现了个正在活跃维护的
    - https://github.com/StevenBlack/hosts
  - 自用 github-hosts
    - https://raw.githubusercontent.com/Leon406/pyutil/master/github/hosts
    - https://search.gitee.com/?skin=rec&type=repository&q=GitHub520&sort=updated_at
  - https://github.com/ineo6/hosts
    - GitHub最新hosts
- 备用方法
  - 直接百度搜索 github-hosts，选择条件时间1月内，执行二次搜索
  - gitee上搜索hosts (github520)
    - https://search.gitee.com/?skin=rec&type=repository&q=GitHub520&sort=updated_at
    - https://gitee.com/monkeycc/GitHub520
      - https://raw.hellogithub.com/hosts

- https://github.com/hwanz/SSR-V2ray-Trojan
  - SSR-V2ray-Trojan机场推荐
- https://github.com/limbopro/paolujichang
  - 跑路机场名单收集（2020-2023）
  - Rixcloud/喵帕斯/Blinkload/速蛙云/世外桃源等等一系列已经跑路的机场告诉我们，机场的尽头就是跑路。
  - 本跑路名单未记录但实际已跑路的机场还有很多，改头换面重复收割韭菜的也有。

- 机场gfw
  - [VPS虚拟主机测评_IDC主机测评](https://shuziren.github.io/ssrvps/)
  - [FlowerCloud - 产品套餐](https://huacloud.dev/product.html)
    - 128￥/年: 20G/月
    - 低等级套餐没有性价比，但是他家有0.2倍率的实验性节点，也就是说你只用实验性节点的话流量可以按照5倍来看。
    - 0.2倍率的实验性节点三条线路也是广港+沪日，这点很良心。
    - 开业时间: 2020
    - domains
      - [FlowerCloud - 国际网络加速服务，致力于提高网络质量！](https://huacloud.net/)
      - [购物车 - FlowerCloud](https://flowercloud.net/cart.php)
  - [TAG Internet](https://tagss01.pro)
    - 154￥/年: 200G/年
  - [泡泡云PRO](https://ppy.buzz/)
    - 168￥/年: 1024G/月
    - 85￥/年: 256G/年
  - [泡泡Dog](https://www.paopao.dog)
    - 7.5￥/月: 70G/月
    - 30￥/年: 150G/年
    - 开业时间：2022.04；老板肉身：海外(确定)
  - [KuLi云-IEPL](https://cyuuu.co)
    - 180￥/年: 200G/月
  - https://ikuuu.club/

- 一元机场
  - https://github.com/yiyuanjichang/dizhi
  - [一元机场节点安全吗，不会是钓鱼吧 - V2EX](https://www.v2ex.com/t/913781)

- git最近更新了socks5的语法，去掉了引号，git config --global http.proxy socks5://127.0.0.1:10808配合V2RayN可用
  - #只对github.com
    - git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
  - https://gist.github.com/laispace/666dd7b27e9116faece6

- [npm设置socks5代理](https://www.lihuacats.com/archives/npm%E8%AE%BE%E7%BD%AEsocks5%E4%BB%A3%E7%90%86)
  - npm install -g http-proxy-to-socks
  - hpts -s 127.0.0.1:1081 -p 8002
  - npm config set proxy http://127.0.0.1:8002
  - npm config set https-proxy http://127.0.0.1:8002
# law
- [中国执行信息公开网](http://zxgk.court.gov.cn/index.jsp)

- [中国裁判文书网](https://wenshu.court.gov.cn/website/wenshu/181029CR4M5A62CH/index.html)
# artman
- https://www.boyfriendtv.com/
  - 光头大叔
- https://www.gv2.mom/
  - 便利受
