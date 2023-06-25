---
title: tool-app-collection-saas-xp
tags: [app, saas, tool, xp]
created: 2020-07-12T15:27:22.003Z
modified: 2022-11-07T10:25:12.034Z
---

# tool-app-collection-saas-xp

# saas-xp
- https://github.com/iamadamdev/bypass-paywalls-chrome
  - help bypass paywalls for selected sites.
  - Bypass the following sites' paywalls: bloomberg, fortune, glassdoor, medium, national geographic, quora, vanity fair, vulture
# zhihu
- 有时候评论的内容比回答的内容更有意思

- [知乎违规记录](https://www.zhihu.com/community/reported)
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
# twitter
- search
  - 搜索关键词时，可加上'min_replies:1'的条件，筛选出被讨论过的质量更高的内容
  - https://github.com/igorbrigadir/twitter-advanced-search
  - 搜索转发的内容
    - [Use Twitter Advanced search to find retweets made by a single account? ](https://webapps.stackexchange.com/questions/92616)
    - from:@username include:nativeretweets filter:nativeretweets chrome

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
# 邮箱注册
- 不需要手机号的邮箱
  - mail.protonmail.com
  - ref
    - [请问现在有什么不用手机号可以注册的邮箱](https://v2ex.com/t/683308)
# 图片资源
- unsplash镜像战
  - https://unsplash.dogedoge.com/
# gfw/proxy
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

- git最近更新了socks5的语法，去掉了引号，git config --global http.proxy socks5://127.0.0.1:10808配合V2RayN可用
  - #只对github.com
    - git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
  - https://gist.github.com/laispace/666dd7b27e9116faece6

- [npm设置socks5代理](https://www.lihuacats.com/archives/npm%E8%AE%BE%E7%BD%AEsocks5%E4%BB%A3%E7%90%86)
  - npm install -g http-proxy-to-socks
  - hpts -s 127.0.0.1:1081 -p 8002
  - npm config set proxy http://127.0.0.1:8002
  - npm config set https-proxy http://127.0.0.1:8002
