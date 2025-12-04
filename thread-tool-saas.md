---
title: thread-tool-saas
tags: [saas, thread, tool]
created: 2023-05-07T18:35:34.827Z
modified: 2023-05-07T18:35:50.897Z
---

# thread-tool-saas

# guide

# discuss-stars
- ## 

- ## 

- ## Anna's Archive 可以视为 Zlibrary 的超集，拥有比 Zlibrary 更多的图书资源，不需要登录即可下载。
- https://twitter.com/OldPanda/status/1764871238282080549

- ## 🕷️ 有没有推荐的收费合理的url到html的crawl服务？能绕过一些机器检查，显示完整html内容的，尤其是各大新闻资讯网站。
- https://twitter.com/dotey/status/1765844546041049560
  - 可能和RSSHub还是不太一样，我要的是服务端请求一个特定URL的HTML而不是列表，要完整HTML，最好是能绕过防火墙限制。
  - 主要使用场景是在科技文章翻译GPT（https://chat.openai.com/g/g-uBhKUJJTl-ke-ji-wen-zhang-fan-yi）中，输入一个URL就能自动抓取翻译
- 如果量不大的话，我建议用浏览器扩展。技术上来讲，浏览器扩展的效果应该和用户浏览非常接近，不太容易命中 WAF。不过我也不太清楚有没有方便的框架。
  - 谢谢建议，这个我同意，因为浏览器插件能拿到真实用户能看到的任何数据，不用担心任何防火墙。只是使用场景的话，我是希望用户输入URL就直接可以开始生成内容，而不需要去安装插件。

- curl 命令行好像有一个伪装浏览器版本的
  - 我有写过一个无头浏览器版本的，但是很多防火墙绕不过去

- 可以用 PhantomJS 无头浏览器来抓取动态网站内容。如果不怕麻烦的话，也可以折腾下 Selenium。你这个需求场景我感觉应该不少，我都想做个收费的。边缘节点用 cloudflare 白嫖，它自带缓存，运营成本应该不高。

- 听上去你需要的是代理ip？
  - 我就是想用在GPT中，能稳定的抓取和翻译网页内容，无所谓是不是IP

- Apify有不少Actors，可以满足需求，很好用，我经常使用，但需要付费。我们用于商业目的的，这点费用就没多大关系了。

- 现在一部分用了cloudflare的也很难绕过了吧，之前试过playwright，结果频率高一点就被cf暴击
- 如今想绕过 Cloudflare 验证可不容易

- 自己做吧。。。做好调度系统，其他的交给puppeteer，cookie处理好就行了

- ## Cloudflare 禁止自助服务（包括 Cloudflare Pages）用于图床和视频床。
- https://twitter.com/isukkaw/status/1763415242330235088
  - 只要有别有用心的人对着这个域名的图片刷 100 TiB 流量，Cloudflare 就会派销售提醒你需要掏钱上 Business Plan 否则就会 Suspend 你的域名。
- 我能理解有 100TiB 的免费流量吗？
  - Cloudflare 免费客户的 DDoS 防护基本形同虚设、阈值设的非常高的。一旦流量被刷到域名 Suspend，就意味着只要你不交钱升级，你这个域名终身不能继续薅 Cloudflare。
  - 所以我自己托管在 Cloudflare 上的服务都上 Cloudflare 配了一堆 WAF 规则避免被刷流量。
  - 配置 WAF 需要绑自己的域名，免费套餐可以配简单的自定义规则（Cloudflare Managed WAF 需要额外加钱）和简单的 Rate Limit。
  - 我的建议还是注册个单独的 Cloudflare 账号、单独的域名做这件事。这样即使不幸被 Cloudflare 清退，也不过损失一个域名、一个账号而已。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## [Favorite Self-Hosted Tools in 2025 (Looking for More Suggestions!) : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/1pdui2u/favorite_selfhosted_tools_in_2025_looking_for/)

- [What’s one tool you self-hosted that completely replaced a SaaS subscription for you? : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/1pdwbvl/whats_one_tool_you_selfhosted_that_completely/)

- ## 一款专注于哔哩哔哩直播切片和投稿的工具：BiliBili ShadowReplay。
- https://x.com/GitHub_Daily/status/1895323043079299561
  - 支持直播缓存、历史回放、实时切片投稿，提供多直播间管理和多账号支持。
  - https://github.com/Xinrea/bili-shadowreplay

- ## .io存世量很大，应该不会直接删除，可能会停止新注册。 别怕苏联解体这么多年不见了， .su 也还在呢
- https://x.com/hixiaoji/status/1845312320525959235
- spring官网就是
- http://socket.io 丸辣

- 主要是之前南斯拉夫解体，出来一堆克罗地亚，黑山国家都在争吵继承.yu域名，IANA就改规则，国家没了域名也要删除。
  - 不过io域名由于使用广泛，很可能会被IANA收回转为com，net一样的通用域名。
- 大惊小怪，su 域名现在都能注册，苏联都解体几十年了。

- ## 推荐一个最近发现的邮件发送服务商 Brevo（http://brevo.com），他的免费套餐非常良心，
- https://x.com/interjc/status/1840917391120691463
  - 包含每天 300 封邮件的额度，并且还有免费 WhatsApp 推送、网页在线客服等服务，是一个一站式解决方案
  - 之前使用的 Sendgrid 莫名其妙就把我风控了，于是才重新调研找了这家，也算是一种机缘
  - 需要验证域名
  - 这个只是提供 api，调用以后发邮件。嵌入到哪里的软件应该没有区别。不过纯国内似乎也可以使用 aliyun 的 mail
THREAD
- ## Another day when I miss that cloud disk storages (S3, Google Drive, Dropbox, iCloud etc.) didn't implement atomic compare-and-swap.
- https://x.com/Horusiath/status/1791335631823712266

- ## 在找一些网页版绘图工具时看到 Sumopaint，很简约，但是同时还有一个不需要登录就能使用的 AI 绘图 / inpaint 工具，太菩萨了
- https://x.com/zQwQs/status/1791434868133666984

- ## 做了一个在浏览器里「视频转 GIF 」的工具。
- https://twitter.com/zQwQs/status/1779465415217066204
  - 使用 WebCodec 解码视频，转换速度还是有保障的。而且还可以自定义颜色、抖动等参数，提高转换效果
  - https://lyonbot.github.io/video-to-gif/

- ## 💡 七牛现在提供的 CDN HTTPS 免费证书只有 90d 的版本了 
- https://twitter.com/alswl/status/1768924198372794718
- 90天是之前Google的倡议 然后各大CA厂商不断跟进的 trustasia官方也减少为90天了
- 都一样，阿里云的也是，周五刚发现线上服务的过期了
- dnspod 免费证书一年有效

- 从它某一年突然取消默认提供的域名，必须要绑定一个备案后的域名才能访问存储中的内容时，我就没再用过它了
  - 中国特色，内容会污染域名。

- https://twitter.com/alswl/status/1769321792693530996
  - 研究了原因和解决方案，我的结论是： 免费证书都是 90d 了，只能使用自动化机制。 使用 http://acme.sh 可以对接多种 CA + DNS Provider + CDN 厂商。
  - 最终方案：使用 http://acme.sh 申请 ZeroSSL，通过 DNS Domain 认证（CF + DNSPod），使用 Qiniu API 自动上传证书并部署 CDN。

- ## oh-my-rime，不喜欢输入法联网的朋友可以试试。
- https://twitter.com/iamcheyan/status/1767761177004961926
- rime双拼的问题一直没有好的解决方案
- 这似乎不是输入法，就是一套 Rime 配置，大量借鉴了雾凇拼音，不太确定和雾凇拼音相比有什么差异或优势。但是网站和教程比雾凇拼音更新手友好一点。

- ## http://SchemaStore.org now serves 1.6 TB of data every single day, and that number just keeps going up. 
- https://twitter.com/mkristensen/status/1766232046349984046
  - Pretty much all modern IDEs and editors consume it for both JSON, YAML, and TOML schemas. It's mind-blowing to me.
  - Thank you, Microsoft, for sponsoring the massive amount of traffic
- Mostly immutable data - what’s the cache policy? Could this have been done by a CDN?

- ## 我的密码管理最佳实践
- https://twitter.com/kinokoameme/status/1765950237515141363
  - 这么多年用过许多类似1password这样的密码管理工具后，但最终的最佳实践是抛弃所有工具，也不需要记录，回归到最原始的脑记。
  - 我实践了好几年了，不敢说是绝对的最佳方案，但很适合我自己。在这里分享一些密码原则和规则给推友。
1. 不同服务使用不同密码
2. 所有密码具有一样的规则，并且满足常见复杂度要求。
3. 规则举例如下：
3.1 以特殊符号开头，比如 #
3.2 # 号之后跟着三个字符，分别是数字、小写字母和大写字母，可以跟自己熟悉的事物比如名字之类的产生关联，也可以随便确定一个。比如拿蔡徐坤为例，C是字母表第三个字母，于是可以设置为3xK。
3.3 之后再加上具体服务的最一般的名称，则蔡徐坤的常见服务的密码如下。
推特：#3xKtwitter
微信：#3xKwechat
支付宝：#3xKalipay
1. 【重要】设置随服务名不同而变化的魔数。再制定一条可以简单心算的规则，比如服务名的字母对应9键键盘的数字之类的（可以选取一部分，比如前两个后两个之类的）。

- 依照上述规则制定的密码有如下好处。
1. 规则固定简单，只需脑记即可，无需任何工具劳神，也不存在忘记的可能。
2. 每个服务的密码均不同，泄露个别服务的密码也不会影响其他。
3. 如果不幸被人从你多条密码中看出魔数以外的简单规则，因为魔数的存在，仍然很难被完全破解。

- ## Introducing http://git.new – a free GitHub link shortener.
- https://twitter.com/steventey/status/1765776978391789612
  - get world-class analytics – powered by @dubdotco
  - [Git.new – Free GitHub Link Shortener](https://dub.co/tools/github-link-shortener)

- ## 一个同事给文件命名的方式，是时间+文件名。
- https://twitter.com/biantaishabao/status/1762766840147894691
- 这种把时间在前的命名规范非常常见，比如大学、律所、文书机构等
  - 一是因为要处理大量来源的文件时，时间是唯一有意义的信息，用时间排序是很常用的操作，放后面没法排序了
  - 二是文件元数据在这些场合不可靠，这些场合文件很可能会被各种软件传送、压缩、修改格式很多次，元数据指不定就丢失了
- 我也经常这样命名的，更多是用在文件夹命名上。这样排列起来按时间顺序很整齐有条理。

- 照片是另一回事了，因为照片通常都是某一天拍了很多张，甚至都不需要给每张照片命名，只需要给文件夹命名就行；更进阶的做法是用专门的管理软件（lr、br、c1）等等填写关键词来管理。

- 和同事相处的第一原则：不要管别人是怎么做事的…

- ## [帮小忙，腾讯QQ浏览器在线工具箱平台](https://tool.browser.qq.com/)
- https://twitter.com/LuoSays/status/1762751711532478517
  - 今天才知道，原来腾讯做了一个在线工具箱，里面有非常多实用的小工具，而且还是免费的，也不需要登录。

- 部分功能还是得登陆，得VIP的
- 被夸克浏览器打得难受了，在QQ浏览器里加了入口，抄了夸克的在线工具路子想叫夸克无路可走，安装了一下，就给给了几个入口直接访问web那样，体验平顺度目前还落后夸克两条街吧.
- 腾讯应该留点活路给小开发者
  - 大厂做到这么细致的确实还挺让我吃惊的，小开发者的生存空间越来越小了。
- 我转pdf的文件，后台会留一份吗？

- ## 一名职业编程讲师录制视频所用到的6️⃣款工具
- https://twitter.com/cui_xiaorui/status/1763044309719556331
- 1. OBS - 视频录制/直播
- 2. Camtasia - 视频剪辑
- 3. iThoughtsX - 通过脑图绘制课程授课大纲
- 4. Excalidraw - 画图 
- 5. ScreenBrush - 屏幕画笔
- 6. keyCastr - 实时显示按键

- ## 有没有什么比较稳定的云GPU可以租用，要求是价格亲民。
- https://twitter.com/JXQNHZr1yUAj5Be/status/1758188952106762272
  - Colab虽然便宜，但是不稳定，重启以后啥数据都没有了。AutoDL在国内，数据集和模型比较难下载，需要搞网盘。虽然这两者都可以用某种手段绕过，但是目前不太想折腾。
- kaggle每周可以免费跑30小时p100，每个实例最长跑9小时

- Colab这个也不叫不稳定啊，它用的是云原生的容器解决方案，重启之后数据没了是这个方案的尿性。可以把数据集、模型之类的大文件挂载到到Google云盘，这样再重启就只需要下载和安装基础的开发环境，十分钟内就能启动了。

- ## 小红书对爬虫/RPA 的压制，已经到极致了
- https://twitter.com/huangyun_122/status/1755096457428803830
  - 在搭配 RPA + Fiddler Everywhere 之后，还是无法突破。只要一打开小红书，手机立马掉线，根本不给机会联网
  - 接下来只能尝试 Wireshark 和渗透注入了。

- app 上了 ssl pin ，mitm 要先给ssl pin 过了
- 这不只能反编译了？
  - 干掉ssl pin 就行
- 这个做不到吧，ssl服务器端可以选做客户端验证

- 国内厂商是这样，开放生态啥啥不管，可劲制作信息孤岛
  - 商业平台是这样的，国人的复刻功底，太强了

- 脚本爬虫显然很容易被检测到，客户端爬虫（定制的注入了脚本的正常应用）可能会有timing、属性污染等问题），MITM代理可能是个好办法，但是你需要手工去交互，即使这样，只要做到API接口动态修改schema你就忙不过来了
  - 现在发现已经半自动了，太费劲了

- 小红书 web 版说实话反爬虫做的一般般，他们也就判断那几个爬虫特征（变量）然后让接口返回错误，很好绕过。
  - 但东西少啊，内容没几个，爬一会儿就到顶了，哈哈哈哈哈

- 藏起来搞吧 不然人家加个策略就功亏一篑
  - 确实如此，难怪都说闷声发财

- 反编译app找到https相关验证函数，hook过去
  - 策略对极了，赞

- 将来的爬虫可能只有采用物理bot的方法了：机器人点击，屏幕截图、OCR识别布局和内容

- 用appium直接自动化搞啊。什么搞不下来？

- ## 🌰🐛 我想吐槽的 rsync 的问题
- https://twitter.com/LightQuantumhah/status/1754773199357968412
  1. text binary protocol 混用
  2. 握手只能握协议版本不能握功能 (比如说是否支持硬链接)
  3. 客户端用户给的命令行会被发到服务端进行 parse
  4. 非常灵车的 mux 但是只能用来 mux 数据和 log 流，完全没有并发传输更不能取消
  5. 协议设计根本不能随机访问
- 实现问题:
  1. 原版实现奇灵无比全局状态满天飞控制流混乱根本看不明白 (openrsync 组织成了状态机，实现干净很多)
  2. 失败文件得等所有文件下完了到下一个 stage 重传
  3. 协议要求两端的文件列表必须按某种顺序排序，但是一端给另一端发送这个列表的时候居然不保证是排好的

- 如果 rsync 能用，其实没什么动力让大家改用的.. 现在苦了的只有我这种重新实现协议的
  - 实现一个 rsync-ng 然后兼容之前的协议，名气打响，十年后用户就慢慢过度到新协议了

- 停止吐槽吧。如果它实际使用中没有问题，那就不用管什么协议设计的纯粹性，如果想要其他特性，看看有没有别的软件可以组合使用，最后看能不能修改代码实现

- 开源软件就像创业，很多时候确实是时机比技术重要，草台占领全世界

- 这种需要考虑兼容性的老代码，可以想象有多混乱，还有比如 Firefox, Samba

- ## 发现一个有趣的网站 https://endoflife.date ，呈现各个常见软件（供应链）的生命周期。
- https://twitter.com/alswl/status/1754053512877781012
  - [endoflife.date](https://endoflife.date/)
- Go 的强向后兼容性使得长期维护旧版本没太大意义，如果你愿意升级，完全可以升大版本。

- ## 我压缩图片经常会用到 https://tinypng.com 这个网站，我试过其他的网站和软件好像都没有这个好，它们功能非常简单，就是压缩图片，没别的。
- https://twitter.com/vikingmute/status/1753609198422937683
  - 今天我一查，发现它们的月流量是 400万，一年预估盈利是 720万美元（一个网站预估，不知道准不准），2013年成立，总共员工就 3 个人，将一个产品做到极致就是这个水平吧。
  - 它们也针对程序员卖 API，看了下 nodejs 的 SDK，点赞的人还挺多的。

- 图片压缩，我用ppduck， 最喜欢的地方：
  1. 可以一个文件夹拖拽进APP，自动压缩，非常方便。 
  2. 显示文件从oldsize 压缩到newsize, 非常直观的价值感 
- Mac：Optimage（https://optimage.app）
  1、压缩比强大，横测对比最强
  2、交互细节好
  3、对 Gif 支持友好
- 用了很久了 很好用。Mac app一个月限500张

- ## 最近想给一些网站的数据做个第三方看板，没找到什么合适的方案 主要是起个DB/服务太重
- https://twitter.com/fuergaosi/status/1747674668407153049
  - 整了一套 Notion + Grafana + N8N 的 Nocode 玩法（后两者我家里部署的都有现成的，也有免费的公有云方案）
  - 用 Notion  Database 做 DB 
  - 用 Grafana 做看板
  - 用 N8n 抓取数据, 抓低频数据非常方便

- 我用的CloudFlare定时脚本抓数据，存到GreptimeCloud，用 Grafana Cloud 做展示，全白嫖

- ## 发现「云闪付」App 最近新推出了个「一键查卡」的 beta 功能，
- https://twitter.com/luoleiorg/status/1738951627686789464
  - 支持看你有没有在国内近 496 家银行开过哪些卡，银联官方渠道，应该还算靠谱。大概用途可以查自己以前遗漏的卡，或者看有没有人冒充开卡？
- 这个只能查到带银联标的卡，非银联单标卡查不到
  - 美国运通也能查到
- 亲测查不到单币visa卡
- 支付宝也有，但是根本查不了
- 这并不是最近出的，有几年了
- 很早之前就有了，之前查过，需要等短信通知结果

- ## postman 竟然不是本地运行的？UI好慢好卡。有么有更好的替代品呀？
- https://twitter.com/river_leaves/status/1735646281488580659
- Insomnia

- ## I don’t know why anyone would willingly add “ctl” to the end of their CLI tool’s name
- https://twitter.com/jarredsumner/status/1735762522760978734
- How about people adding "d" to the end of their daemon's name?

- ## 微软 terminal 团队想给 windows 内置一款默认的 CLI 文本编辑器，跑来 github 上征询大家的意见，于是评论区各个编辑器又开始互掐。
- https://twitter.com/skywind3000/status/1734401495691600346
  - [Default CLI Editor - Feature Exploration! · microsoft/terminal](https://github.com/microsoft/terminal/discussions/16440)
- 在windows上使用命令行的一般都是写程序的，写程序的一般都使用git，安装完git后可以使用git的git-bash，当然git也带了vim，所以就直接使用vim了。

- ## 突然发现可以使用 Cloudflare 的 Redirect Rules 来做短链服务，天然使用 Cloudflare 自带的强大的 Analytics 功能！Cloudflare 太强了，哭死！
- https://twitter.com/yetone/status/1734139420801187931
- 但是免费版只有10个rules
  - 已经比很多短链服务的免费版多了

- 我感觉 Analytics 功能是要页面上内插的统计 JS 加载出来才会统计到的？
  - 有道理唉，它没有 HTTP request 统计吗？
- 据我所知，HTTP 请求统计好像不能精确到请求路径
- 可以自己写 worker 实现 rules 然后也可以加统计到 D1

- ## 学到两个读 arxiv PDF 论文的新技巧：
- https://twitter.com/Barret_China/status/1729867231344144414
  - 1）将域名中的 x 更换成 5，会跳转到 HTML 版本
  - 2）将域名中的 v 更换成 w，会跳转到一个 AI Chat with PDF 版本

- ## Live coding is hard to be perfect (I'm so good at typo), so why don't we automate it?
- https://twitter.com/antfu7/status/1505236765447458817
  - Take the snapshots for the changes(clicks), and then play it! Saves as plain text so you can edit it afterward and even commit to git
  - 基于编辑记录文件，在vscode播放代码编写的过程

- ## 一个视频处理库，提交记录12000多次，非常古早且强大
- https://twitter.com/chenbimo/status/1725213333991931992
  - 比如你的官网要放一个视频背景，该视频有几十M，你可以用这个软件，把它变成几M甚至几百K！
- https://github.com/HandBrake/HandBrake
  - open-source video transcoder available for Linux, Mac, and Windows

- ## 多次看到有人推荐，可以跳过付费墙直接免费查看各大网站内容的 Chrome 插件，把源码 down 下来研究了下，原来核心代码只有一句
- https://twitter.com/Barret_China/status/1724978017922093540
  - h++ps://webcache.googleusercontent.com/search?q=cache:${window.location.href}
  - 这些付费内容平台为了可以获得更多的流量，针对搜索引擎的爬虫是输出全文的，因此只需要通过 Google Cache Page 打开对应的网页，或者通过 Achieve 网站打开，就可以看到全文了。
- 大部分关掉 js 就可以了。
  - 有些服务端渲染的，根源上就不发给你
- 有一些是这样的。需要用到原文的技巧，走搜索引擎的 cache 或者搜索结果的跳转有时候也允许阅读全文。
- 还不如直接右键 源码，就可看到web里面的内容

- ## 刚发现 Syncthing 这个强大的跨平台文件同步工具，适用于 Mac/Win/Linux。
- https://twitter.com/hylarucoder/status/1722536795626471723
  - 自从使用 Stable Diffusion 后，越来越多的文件使得我的文件同步流程变得复杂。
- 它这个文件传输是通过什么做的呢，以及安全性如何
  - 点对点传输, 通信通过TLS加密。
  - 我的场景是: 局域网内的几台机器数据同步, 那就很安全. 如果走公网的话, 可以自己搭中继服务器

- ## Anna的档案馆称他们获得了读秀图书数据库，包含750万本、总计359TB的中文非小说书籍的收藏，这个数字超过Library Genesis （530万本）。
- https://twitter.com/xiaohuggg/status/1721532104998105264
  - 如果哪家大模型公司能给他们提供OCR和文本提取服务，将会获得Anna的档案馆一年的独家访问权。
  - [独家访问：全球最大的中文非虚构图书馆藏，仅限LLM公司使用 - Anna’s Blog](https://annas-blog.org/duxiu-exclusive-chinese.html)

- ## 阿里云难得良心一次，2C2G3M 配置每年只要 99，看活动时间优惠持续四年
- https://twitter.com/cosmtrek/status/1721484209968259487
  - 托管于中国内地服务器上的网站，如果网站没有绑定域名，直接通过IP地址对外提供服务也需要进行ICP备案。目前阿里云ICP代备案管理系统只支持域名备案，不支持IP备案。重要无论网站是通过IP地址还是通过域名对外提供服务，未备案成功前，均不允许开通网站访问。阿里云官方

- 这类 VPS 适合自用，不适合严肃的生产环境。 有好多用途，比如当跳板机、网络代理、部署 Web app、文件中转、Grafana 统计、学习 PHP
- 长期用还是得看国外，续费同价。国内的云服务器过几年就得找下家。
- 最多能买两年吧？我续到第三年就是原价了

- ## 还没用过 Whisper 语音转文字？ 这里有一个在线版本，
- https://twitter.com/finedtune/status/1721049768464667127
  - 可以直接输入 YouTube 链接，也支持自己上传音频文件，不需要安装和部署，速度比初版 Whisper 快 70 倍， 1 小时音频 1 分钟就转好，关键还免费
- 我确实还没用过，因为找不到合适的使用场景，比如现在用的语音输入，讯飞输入法用的语音转文字也还挺顺手。如果需要做实时会议转录成文字之类的，可能用得上。
- 长远看油管视频的语音转文字没必要做，现在的很多油管视频已经包含了文字，用油管自己的功能几秒就把文字复制出来了

- ## [My IP Address - BrowserLeaks](https://browserleaks.com/ip)
- https://twitter.com/RkMonoChrome_CN/status/1719747686679597141
  - 检测ip，还能检测dns，DNS Leak Test
  - 如果DNS服务器里有自己手机or宽带的运营商的话那么运营商就已经知道你在翻墙了

- ## Misgif：一款可以将你的脸放入你喜欢的GIF 表情包中的应用
- https://twitter.com/xiaohuggg/status/1719186332319416388
  - [misgif: ai powered memes](https://misgif.app/)
  - 可以免费使用三次。

- ## 扫地机器人最大的bug是会挑衅到狗，然后被狗翻过来
- https://twitter.com/syeerzy/status/1717518202027331904

- ## 备份方法
- https://twitter.com/Ruohai/status/1717178829612187852
  - 新手：移动硬盘冷备
  - 中级：买nas组raid
  - 高级：买多套nas做321备份和功能区分
  - 骨灰：旧电脑装debian用rsync和rclone
- 我用 nuc 挂了一堆硬盘，都是独立的。
- 就想知道旧电脑不考虑功耗的么？
- 可以裝Unraid

- ## 一个有趣的网站「12英尺」，http://12ft.io，一位外国程序员受不了互联网充满了付费高墙，他撸了一个 12 英尺的高梯来帮助读者们翻越各种付费围墙——Show me a 10ft paywall, I’ll show you a 12ft ladder.
- https://twitter.com/Barret_China/status/1711042013230256476
- The idea is pretty simple, news sites want Google to index their content so it shows up in search results. So **they don't show a paywall to the Google crawler**. We benefit from this because the Google crawler will cache a copy of the site every time it crawls it.
- 有个插件叫Bypass Paywalls，可以破解看各大新闻网站的付费内容，估计实现原理是一样的，那些付费网站的付费内容为了搜索流量给谷歌爬虫开白名单，允许抓取付费内容，谷歌就有了文章缓存，然后把网站链接的内容替换为谷歌的缓存内容，以此绕过付费

- ## Cloudflare 的验证码服务 Turnstile（图一），对所有人开放了。只要加入几行代码（图二），就能免费嵌入自己的网站
- https://twitter.com/ruanyf/status/1710661567552045077
  - 再不必费劲识别图片和字符，只要点击一下就识别是否机器人，我觉得用户体验很不错，而且只要不用企业版功能，就都是免费的。

- 可以用 Google recaptcha_v3 企业版，用户连点击都不用，每个月的免费额度很高，不过还要自己实现服务端接口麻烦一点。

- 在中国加载这个js文件似乎有点慢，再等等看

- ## [What are your most used self-hosted applications? | Hacker News_202205](https://news.ycombinator.com/item?id=31260061)

- ## 最近有给自己的 SaaS 接入日志监控的需求，考察了两个服务:
- https://twitter.com/novoreorx/status/1658323720140881927
- https://betterstack.com/logtail/pricing
  - 免费版 1GB 存储，保留3天。Linear 风格黑色主题。
- https://axiom.co/pricing
  - 免费版 0.5TB 存储，保留30天。清爽干净的白色主题。
- axiom 底层来看应该是 grafana loki，和以前使用来比太像了。而且换算一下，如果是 loki 这个存储成本完全可以 cover 住

- ## Yandex 竟然有个完全免费、没有流量限制的网站统计服务
- https://metrica.yandex.com/
  - All-Round Web Analytics
