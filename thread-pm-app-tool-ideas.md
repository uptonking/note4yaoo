---
title: thread-pm-app-tool-ideas
tags: [app, ideas, products, thread]
created: 2022-11-07T10:02:52.517Z
modified: 2022-11-07T10:58:24.512Z
---

# thread-pm-app-tool-ideas

# guide

- goals
  - 优质的内容、优质的数据

- 产品的入口形式
  - 浏览器，需要用户培养习惯，优点是方便跨端
  - 系统级组件如spotlight，优点是与系统是深度集成、操作方便，缺点是通用性不强

- 某一类数据源聚合的产品
  - 搜索多个app-store，如flathub/snap

- inspirations
  - https://github.com/open-source-ideas/ideas
# ideas
- 数据碎片搜集
  - pc, mobile, browser ext
    - list-pin
    - 复制列表/表格数据
    - 表格行列数统计

- 大而全的产品如google/notion使用方便，但特定场景的解决方案仍然有生存空间
  - linear，挑战jira
  - zendesk，客户帮助平台
  - roadmap/feedback, canny

- 如果你做独立开发，没任何用户感知和判断力，建议多逛逛这个subreddit，https://reddit.com/r/SideProject/

- 解决版权问题的内容管理平台
  - 思路1: 类似 hacker-news 只放链接

- 链接整合平台
  - 类似 hacker-news 只放链接
  - 针对音乐，放视听地址、B站地址

- 给热门产品做周边或工具
  - ai/ide/卖课 + collab

- 技术大会的分享
  - cs会议论文总结

- 技术文档
  - 公开的文档会自动收录
  - 私有或个人的技术文档需付费收录
  - 独立开发者博客链接，不放具体内容

- 文字动画、代码动画
  - 局部放大
  - 倍速播放，设置速度

- ai + bi图表/报表 是否有市场机会

- 
- 
- 
- 

# datable/数据整理
- 高质量数据 + AI ( + 技术文档 )
  - wikipedia
  - hackernews
  - reddit-tech
  - stackoverflow

- 技术文档 + AI
  - mdn
  - languages apis

- 学术相关数据
  - 论文一条龙: arxiv/paper, huggingface-data, github-code
  - 中科院PubScholar公益学术平台

- 版权过期文档
  - [免费阅览全文！国图等6家联合发布古籍数字资源 - 资源分享 - FreeMdict Forum](https://forum.freemdict.com/t/topic/18274)
  - [Anna’s Archive: LibGen (Library Genesis), Sci-Hub, Z-Library in one place ](https://annas-archive.org/)
  - [文硕阁 – 公共版权电子书下载网站](https://www.wenshuoge.com/)
    - [传硕公版书](https://www.reddit.com/r/publicbook/)
  - 毛主席的文档版权即将过期

- pm-data
  - 类似企查查/天眼查的政府数据整合平台

- 政府数据
  - 各级统计局
  - 国外统计局
  - 统计年鉴
  - 中国裁判文书网
  - 政府公报/报告， 如 [资料下载 - 中华人民共和国教育部政府门户网站](http://www.moe.gov.cn/jyb_sjzl/ziliao/)
  - [国家数字图书馆](http://read.nlc.cn/)

- public dataset
  - imdb

- 经典数据集
  - 公开数据

- 高质量文档
  - 字典mdx
  - 书籍epub
  - wikipedia公开db, kiwix-zim
  - 统计年鉴
  - [中国百科网](https://www.zgbk.com/)
    - 拷贝功能暂未开放
  - [求闻百科](https://www.qiuwenbaike.cn/)
    - 据说是从维基百科中文版fork而来, 有前维基百科中文大陆编辑参与
  - [Introducing the Overflow Offline project - Stack Overflow _202210](https://stackoverflow.blog/2022/10/20/introducing-the-overflow-offline-project/)
    - [The Overflow Offline project | Hacker News _202210](https://news.ycombinator.com/item?id=33274186)
    - [WikiHow and StackExchange/StackOverflow now avalaible for download via Kiwix. : r/DataHoarder _202208](https://www.reddit.com/r/DataHoarder/comments/x1fltz/wikihow_and_stackexchangestackoverflow_now/)
  - 💡 针对经典书籍的playground
    - wikidata
    - 统计局

- 标准文档
  - 工业技术
  - 社科类: 
    - [通用规范汉字表 - 维基文库，自由的图书馆](https://zh.wikisource.org/wiki/%E9%80%9A%E7%94%A8%E8%A7%84%E8%8C%83%E6%B1%89%E5%AD%97%E8%A1%A8)

- 各大公司技术博客
  - mdn开发者文档，历史版本的作用不大，但可作为参考

- 公共数据的衍生产品
  - 地铁线路图上添加 租房价格/美食, 再提供给第三方社交平台如知乎/小红书
  - 租房地点，位置测评，交通指数、美食指数

- 网站数据整理/year/month/week
  - github trending
  - 微博热搜
  - openrouter top models/apps 排行

- 数据整理
  - [2023各平台年终报告](https://www.yuque.com/paidaxin/dkopg8/gqpfgysdw0wiqwmh)
# 国内替代/open-alternatives
- obsidian

- algolia
  - MeiliSearch
  - algolia是纯做SaaS服务的吧，跟es还是有定位上的区别

- 🖼️ comfyui-alternative
  - comfyui/unsloth 都是在技术社区里面寻找目标用户, 并主动提供工作流/微调模型来积累用户
  - 一直主动提供大公司/政府主导模型的技术支持
  - 支持魔搭社区的api/分享
  - 提供与其他主流工具的集成
  - 寻找产品机会: 
    - 比如 32B-70b 之间没有适合mac 32G的微调版, 因为Q6/Q8对VRAM的需求翻倍
    - 提供商业版如 medium/large 的社区版
# sync-setttins
- vscode-config
- greasyfork-scripts

- [Settings Sync · zed-industries/zed · Discussion _202302](https://github.com/zed-industries/zed/discussions/6569)
  - I really like the "settings repository" plugin for CLion. I point it to a git repo and it does the rest.
  - I appreciate the simplicity of the VScode sync, but it's also a bit shady(靠不住的; 不正当的) isn't it. (Yes, I'm aware of the JetBrains sync plugin that works similarly to VSCode as well).
  - The reason I prefer settings sync that's sort of built-in vs a third party is two parts, the first part is trust, the second part is support.
    - By trust I mean, I'm perhaps a paying customer of Zed and I can trust that the feature is implemented by the company and I'm trusting a single entity in this situation (I don't have to worry about a rogue update to the extension that starts to siphon off secrets from my computer).
    - By support I mean, since it's a tier 1 product feature and so will support sync'ing all relevant settings, extensions, and themes. I don't have to worry about it getting abandoned (like I worry about most of the Sublime ecosystem).
  - I would be happy even to be able to change the location of the settings json file to a shared folder (dropbox or google drive or apple cloud or whatever) to be able to keep the settings in sync between my two machines.
# sharing
- 版权过期书籍绘画的二创

- 规避版权问题的内容讨论平台
  - 科技分享，类似hacker-news
  - 产品讨论，类似product-hunt
  - 打分评论，类似豆瓣电影与音乐
  - 论坛圈子，类似贴吧/reddit，支持一个url在不同板块重复讨论、多次讨论
  - today i learned
  - 音乐平台规避版权问题的方式，切换音源，参考洛雪音乐平台

- 分享设备的dock栏

- 分享有设计感的网站、主页

- b站很多视频是带人读文章/公告、读论文
  - 评论图书, 类似豆瓣/goodreads

- sharing-ai
  - ai-model config
  - image workflow

- 类似 异步社区、图灵社区 的社科类书籍分享平台
# integrations
- search-filters

- ModelScope魔搭社区，主打中文的 AI 模型开源社区，
  - 魔搭社区经过半年左右的发展，拥有开发者数量超过160万，模型下载量超过2500万，但演示应用程序才41个，下载应用比例是百万分之一，严重不符合实际
  - 希望国内这种平台有朝一日可以互通，比如百度AIStudio和魔搭。
  - 类似的社区像百度飞浆社区早就办了好久了，也是公开了百度自己训练的文心大模型，还半免费供用户使用百度的GPU算力，类似谷歌colab的模式

- doscord message saver
  - [Discord Notebook](https://chrome.google.com/webstore/detail/discord-notebook/jeeilfacglnffgflhgmciaegglekjlod?hl=en)
  - the extension will save your messages locally in your browser storage.
  - 因为discord前端升级而不可用了，要等待作者更新
  - 可参考 betterdiscord 的 favorite media 插件
# saas
- Grammarly 只做英语市场，所以大部分人并不了解：从不起眼的语法检查起家，这家公司已有百亿美金级别的估值
  - [Neo Zhang on X: "Grammarly：生于技术曲线左侧" / X](https://x.com/neozhang/status/1828953389016945049)
# tools/productivity
- obsidian open source version

- office许可过期
  - https://github.com/infohost/infohost.github.io/blob/main/office-license-is-not-genuine.html
  - https://htmlpreview.github.io/?

- color-mode-converter
  - rgb-hsl-hsv/b-contrast
# devtools
- 以github作为插件/产物/模版仓库，支持自动统计更新时间/star数量

## sandbox

- 标准版 拖拽、低代码
- 专业版 codesandbox 在线打包
- 源码

## markdown-formatter

- [sumnow/markdown-formatter](https://github.com/sumnow/markdown-formatter)
- 代码块格式化时，开始3个\`会对齐到行首，末尾3个没对齐到行首，前面会有空格
  - 给代码块加上语言后，就可以自动对齐了
- link的圆括号内默认带有 `https://` ，这样粘贴url时就会重复这一段
- 带有空格的空行格式化时会单独占一行，浪费空间
- 格式化多个连续的转义字符时，斜杠会混乱
- 会自动在点号后，大写英文字母前加空格，这会破坏代码中的调用，如React. Component
# effect-playground
- 文字不可选择、不可复制
  - https://www.mingyantong.com/ju/5704496
# running
- 国内的跑步类app几乎都不支持导出数据
- 国内的gps工具类app几乎都将导出数据或批量数据操作作为付费功能
- 国外的运动、gps类app几乎都依赖google服务
- 跨国公司如nike砍掉了不盈利的nike run club网页版

> 结论是，如果要完全掌握数据，则需要选择支持导出gpx数据的硬件，不能是硬件不支持而必须在网页或app操作导出的那种产品

# study-room 自习室
- 量贩式，按小时

- 租期制，包月/季
# dormitory

# business-features

- 📱 针对 移动端 短视频/小程序 的nocode更符合国内市场需求

- 提供相同的功能，但
  - 需要点击更多的确认按钮
  - 非高级的动画效果

- links
  - 外链，显示链接或简化版文字可减少干扰，减少用户离开；支持付费自定义card样式

- open-graph
  - http://ogstudio.app, to dynamically generate Open Graph images with custom texts

- 内容页面都可公开访问，但页面中部分敏感数据或结论默认是隐藏或付费可见
  - 敏感内容不会被seo或泄露，但普通内容可正常访问

- 付费问答或咨询
  - 提问免费，提问可发起奖励，回答者可领取奖励
  - 奖励型问题可设置回答部分可见、二次付费可见

- ActionText

- offline/local
  - 本地大模型llm

- 规避版权问题的内容讨论平台
  - 科技分享，类似hacker-news, reddit
  - 论坛圈子，类似贴吧/reddit，支持一个url在不同板块重复讨论、多次讨论
  - 产品讨论，类似product-hunt
  - 打分评论，类似豆瓣电影与音乐
# discuss
- ## 

- ## 

- ## Build popular open source library, train own model on docs + examples (some private?), guarantee that model is updated with every release, sell as integration with user IDEs
- https://x.com/steveruizok/status/1908816804140511456
  - Let’s say @threejs went this route. The core product is free (wedge) but AI assisted coding environments sometimes trip over out of date versions or make poor choices based on bad examples in their training data.

- Best documentation is pair programming type thought process + checkpoints and changes

- ## 我真的好需要一个能按语义（而非单纯名称）搜索 emoji 的 app
- https://x.com/laike9m_/status/1865845517974216935
  - 现在的 app 都只能按名称检索。比如输入 "computer"，我希望找的是这几个 emoji 🧑‍💻👩‍💻，但它们根本不会出现，因为这些 emoji 的名称是 "programmer"

- Raycast 满足，mac app 可以绑定快捷键，全局触发，AI 搜索
- 为了这件事我都把 Alfred 换 Raycast 了，之前还写 workflow 搜来着
- 我需要一个能全局触发的 Mac app。网站不方便

- ## 我觉得带壳截图的春天来了
- https://x.com/CoffeeOrPasta/status/1797139043744104471
- 做一个专门用来给截图加灵动岛的 app，卖 30 块钱一个月
- 摆拍炫富发朋友圈用的呗，名贵一点的护肤品都有卖空瓶的
- 溢出屏幕的虚荣。。

- ## Wikipedia 运行了 24 年，内容最丰富的英文版 wiki，也才不到 800 万个词条。
- https://x.com/howie_serious/status/1796482192060846545
  - 豆包ai牛逼，一眨眼给你生成了1700 万条“知识”。

- 好像是把搜索引擎都扒了一遍，热搜都生成了一遍。或者干脆把用户生成的信息暴露在公网。

- 全行业大跃进

- ## 为猫开发的抓鱼游戏
- https://twitter.com/ShouldHaveCat/status/1768910153737277752

- ## 推荐一款语音识别 APP，Whisper Transcription，
- https://twitter.com/Barret_China/status/1730988938641449287
  - 这款软件基本属于对 Whisper 模型的本地套壳，附加了诸多体验优化和额外功能模块。看来在大模型时代只要肯动手，还是有很多机会的
  - 软件大小只有 10Mb，要支持语音识别，需要从远端将大模型下载到本地，官方 Whisper 提供了 tiny/base/small/medium/large 等不同 size 的模型，需要 large 版本（~1.5Gb）才支持多语言，这个软件竟然所有版本都支持，看来是经过了一次微调。我试了下 tiny 版本，基本可用，large 版本下载太慢了，还没测试。
- 这都能卖88，我搞了一个完全免费🆓的，看来我还是不太会做生意
- 不是的，本来小模型（tiny，small，medium）就是支持多语言的。另外，还有一套只支持英语的模型，从tiny到medium，速度更快且精度更高
  - 查了一下，是的，我记错了

- ## Any good tool to collect and organize important links from the internet?
- https://twitter.com/dobroslav_dev/status/1730985170138800213
  - Features: Make collections, see automatic link preview, etc.
- I recommend http://linkcollect.io 
- I made https://linkace.org (open source, self hosted, php)
- Use a Notion db
- Google keep
