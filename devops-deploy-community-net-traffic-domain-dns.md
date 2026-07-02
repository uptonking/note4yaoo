---
title: devops-deploy-community-net-traffic-domain-dns
tags: [devops, dns, network, traffic]
created: 2026-06-17T05:42:42.014Z
modified: 2026-06-17T07:27:04.608Z
---

# devops-deploy-community-net-traffic-domain-dns

# guide

- tips
  - 先想用途， 商业化项目/开源项目/玩具
  - 业务地区， ~~要国内的~~ ，还是国外的， 国内买域名后需要备案/超管帐号
  - 比较各平台的续费价格, 注意小平台不支持国内支付方式
  - 不必纠结，大多是 .net/.org 都是 $12/year
# domain
- comparison
  - [tld-list ](https://tld-list.com/)
  - [TLD List - 域名比价 ](https://tld-list.com/zh-hans)
  - 可按续费价格排序
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-free/awesome
- ## 

- ## 

- ## 

- ## [深度分析各地区App Store 订阅价格 - LINUX DO _202604](https://linux.do/t/topic/1947655)
  - 土耳其以 1400 条拿下榜首，而且相对美区均值仅 32.9%（深度折扣）——既量大又便宜，典型"货币贬值红利"地区。
  - 尼日利亚 38.2%、印度 37.0% 并列最凶猛折扣梯队，但印度上榜的 app 总量少（138 个）。
  - 巴基斯坦、加拿大、韩国 虽然上榜次数也接近千条，但相对美区均值都在 85% 左右——往往是"并列最低价"（多国按同一美元价定价）造成的统计增量，折扣深度有限。
  - 想省钱，土耳其区（TR）最值得开小号——量最多、折扣最深。其次是尼日利亚（NG）

- ## [App Store 各区 App 订阅价格速查对比在线表格 自动更新 - V2EX _202505](https://global.v2ex.co/t/1132573)
  - 之前因为付款方式限制的原因，很多应用/服务都需要本地付款方式，导致目前有不少都迁移到了 App Store 内购（ IAP ）的方式，主要在美国、土耳其、印度等区域。用 Google Sheets 建了一个在线的价格动态表格，一方面方便跟踪（因为定价经常会变，汇率一直变，订阅套餐不时也会调整），方便查看（过滤、排序等），协同而且可以自动更新，也方便共享给需要的人。
  - Apple 不提供能查询 App 内购项目和价格的公开 API ，这里是通过 IMPORTXML 加 XPath 从网页抓取数据。按照 Google 的文档，刷新时间应该是 1 小时
  - App Store 区域代码按照 ISO 3166 ，区域货币代码按照 ISO 4217 ，通过区域正式英文名查询，数据来自 https://datahub.io/core/country-codes
  - https://docs.google.com/spreadsheets/d/1G6HGCfYW6CBAQmf6UC0EVBD6l79EyLWcIvNbkTsXEAo/edit?hl=en_US&pli=1&gid=1144211665#gid=1144211665

- 这应用也太少了，能不能把怎么搭建的分享出来，我们自己搭建呢？
  - 有需要的应用可以列出来我加在这个表里，或者你也可以利用里面的公式另外做个表抓数据。不用搭建什么，所有东西都在 Google Sheets 里面，也都是可以看到的，“重用及增强”和“内部实现”里面也有说明。

- ## [账号，除了美区、土区，还有哪些区值得持有 _202408](https://www.nodeseek.com/post-151409-1)
- google one 2T最便宜就是土区和埃及，土区399首年/499续费，埃及一样。不过土区和埃及都锁卡了，走apple土区内购599。
  - 剩下便宜的区域就是印度、菲律宾、乌克兰；记得尼区和奈区比印度贵点。
  - 另外ytb和one 各区价格不是成正比的。

- 土记得涨了啊，看看尼日利亚吧
# discuss-payment
- ## 

- ## 

- ## 

- ## [想问下netcup购买可以使用国区PayPal吗（已解决，可以使用，付款需要全局走代理，不然卡验证） _202606](https://www.nodeseek.com/post-771854-1)
- 可以，我就是国区支付的

- 挂t了吗？如果挂了开全局试试看
  - 全局好了，我以为是和注册时候一样不挂t，谢了

- 我就记得pp有些域名直连已经g了，得全局或者写进规则里面。很多默认规则都没更新

- [netcup用paypal付款突然抽风了？ _202606](https://www.nodeseek.com/post-765283-1)
- 工行的问题, 工行银联卡现在也付不了googleplay了

- [（已解决）paypal支付netcup问题求解 _202605](https://www.nodeseek.com/post-735622-1)
  - PayPal绑定的工商储蓄卡，11号都可以支付的，突然今天支付提示：请先检查您在发卡机构持有的账户，然后再使用此卡重试。 换了张建设卡绑定成功付款了
- 我是建行app银行卡里面有个管理境外交易，有开通时间（最多一年）和限额，两个之一满足了就会限制境外消费，需要重新开通

- ## [买鸡买到银行卡被冻结怎么办？ _202606](https://www.nodeseek.com/post-785761-1)
- 你直接使用银行卡付款吗？太勇了，银行卡充到余额宝，加密货币、买鸡等都用余额付款，这是基本操作啊

- 买鸡不会 自己干了其他什么事 应该清楚
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-traffic/bandwidth
- ## 

- ## 

- ## 

- ## 

- ## [有什么好的刷下行流量的开源程序推荐？ - LINUX DO _202605](https://linux.do/t/topic/2198204)
  - 为了应对运营商对上行流量的审查，必须保持在单位时间内下行流量大于上行流量。个人没有PCDN 设备，但是因为有用 PT 且 NAS 保持24小时开机，所以有时也会意外走不少上行流量。
  - 一直以来都是根据 qBittorrent 的流量统计，手工进行补偿性下载来平衡上下行流量，但是这会造成硬盘的写入损耗。
  - 记得之前看到过一个纯前端实现的刷下载流量的网站，页面预设了几种可供下载的文件选择，忘记是哪个网址了, 但最好是能根据路由器的流量监控智能动态调节并发下载数量来实现下载补偿。

- 下行但是不写入硬盘内存，获取后直接丢弃，倒是比较简单，爬取整个互联网就行了。

- 直接搞到 /dev/null 里呗

- 现在ai这么方便，直接手动vibe一个就行了，监测当前路由上传量，然后根据上传量去找个开源镜像链接刷下载，刷到大于上传就暂停

- 需要的是这个吗？ https:// db.laomoe.com 
  - 流量消耗器 The most straightforward way to waste all of your data.

- 家宽吸血+保种即可，想刷留的话开盒子，这样能让效益最大化，时间和硬件都是成本的。没必要拿家宽和硬件损耗去刷那低价值的流量

- 这个我熟悉，直接vibe就行，你拉的时候最好是在晚高峰的时段，5点-晚11-12点拉，不能停，也不用特别快，保持速度就行了，其他的时间段拉有时候不管用（看运营商）。或者是你直接限制下pt的机器在晚高峰时间段不要上传，晚高峰计费跨省流量

- 没用的，真抓不看比例直接封。真的怕可以直接关了upnp保种就行了，偶尔有公网的连上了上传一点也没事
# discuss-domain-free
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-domain-paid
- ## 

- ## 

- ## 

- ## 

- ## [10 元/年 .com 域名，到期续费不涨价 - LINUX DO _202607](https://linux.do/t/topic/2510730)
  - 注册 google workspace
  - 公司名称、姓名、邮箱什么的随便填，但区域一定要选择“土耳其”
  - 选择获取新的自定义域名
  - 填入土耳其真实地址，这里的电话号可以随便填写，后面登陆 google 的时候可以绑定国内手机号
  - 之后会跳转到登陆页面，输入密码、绑定国内手机号（绑定手机号的时候需要 ip 干净，否则可能会被风控）
  - 然后就是添加付款方式，自测招商visa可以支付。(域名是一年有效期，过期会自动续费，我的账单已经出来了，第二年还是 75 土耳其里拉，现在的汇率约等于10 RMB)
  - 之后可以把域名绑定到 cloud flare， 改一下dns服务商就行了，我就是改到cf上了
  - 还可以无服务器拥有自己的域名邮箱
- 不用勾，付款之后还要马上去取消 workspace 订阅，只需要保留域名注册订阅就好。
  - 进去后可以取消这个订阅，刚测试成功
- 下面可以点，选择新手版的，14天免费试用，注册完之后将试用取消就行

- 汇率越来越好了，以前好像是14块钱。现在只需要10块，太划算了 

- 刚上午用招行万事达薅了，很顺利
- 交通银行万事达卡已经注册成功了
- 浦发visa成功了

- 实测，没有visa卡使用u卡也能付款

- 取消google workspace订阅之后域名能正常续费吗
  - 评论里有佬第二年续费成功了

- 这种域名能转出吗？转入要是也能支持就牛了
  - 不能转
- 只能转入，转入你的续费就和谷歌没关系了，实操过？

- 注册的时候需要的IP地址是土耳其的吗？
  - 不需要，只要能访问google就行

- 非英文的网站域名，显示时会变成Punycode编码， 第一次申请时不知道，整了个土耳其文域名，丑的不行，后面号注销重建了一个

- 工信部备案系统只认可国内持有域名注册资质的服务商（阿里云、腾讯云、华为云、新网等），Google Domains 属于境外注册机构
- 备案必须把域名转入国内服务商
- 工信部备案系统只认可国内持有域名注册资质的服务商（阿里云、腾讯云、华为云、新网等），Google Domains 属于境外注册机构，不在工信部备案白名单内，系统无法读取、核验域名实名信息，直接驳回备案申请。

- 绑定手机的时候提示“此电话号码用于验证的次数过多。请换个电话号码重试。”，家人的也不行，估计以前绑定太多了
  - 可能是你 ip 不干净 换一个试试

- bitget 卡失败
  - 要ip加宽就不会出现这样的情况，或者是现在风控咯
- 跟账号环境关系很大，我直接升级当前账号，招商银行 VISA 也会报这个错误。但如果是新建账户，就不会报。
- 不要用fiat24之类的虚拟卡 会风控 让你提供证明材料 用蓝狮子这类港卡 还是很丝滑的 我这破ip都没管 就正常通过了

- 提醒一下大家：测试域名的过程中，Safari浏览器回退可能导致BUG，后续注册完成后变成了“使用现有网域进行设置”，也就是非购买，后续账号和域名（至少14天）都费了。

- ## [【教程】NetCuP域名托管至Cloudflare _202508](https://www.nodeseek.com/post-434359-1)
  - 根据邮件内容登录管理主页后➡️在左侧区域点击Domains➡️点击Domains Name前方的放大镜
  - 选择DNS➡️往下滑动页面-出现Netcup Name Server➡️点开选择 own name server
  - 点击add name server➡️在 hostname中填写你CF提供的两个NS，其他留空 ➡️点击 save name server 进行保存

- [Netcup 域名 DNS 托管到 Cloudflare：新手也能照做的完整教程 - Netcup 中文网 _202511](https://netcupzw.com/netcup-domain-cloudflare-dns/)
  - Netcup 自己的 DNS 服务器解析时间长，添加或修改完成后并不能在短时间内容生效，所以很多人更喜欢将域名的解析服务托管到 Cloudflare。
  - 把选项从 netcup name server 切换到 own name server。
  - + Add additional name server, 点两次，因为 Cloudflare 一共会给你两条名称服务器。
  - 点了这个按钮，修改才会提交。
  - 几分钟内 Cloudflare 就能检测到, 完全生效可能要 5～30 分钟不等, 最多不超过 24 小时（极少情况）
  - Cloudflare 检测到后，你就可以在 Cloudflare 里添加 A 记录、CNAME、MX 等解析了。

- ## [netcup domain kyc是不是多个域名，需要提交多次验证。 _202605 ](https://www.nodeseek.com/post-740178-1)
  - 去年我在netcup买了两个域名，前天收到domain kyc, 昨天提交了银行月结单进行kyc, 晚上收到netcup的回复： Based on the documents provided, the domain verification has been successfully completed. 然后今天又收到netcup发过来的domain kyc, 两次是不一样的工单号，我需要再次提交银行月结单进行kyc吗？请问下是不是有多少个域名，就要提交多少次kyc，虽然是同一份月结单。
- 看起来像这样的

- ## [netcup的de域名kyc通过 _202605](https://www.nodeseek.com/post-735677-1)
  - 其实蛮简单的，我从众安下载月结单，下载后是PDF格式，让Claude将地址信息改成英文后(或者你提供写好的英文地址)重新生成PDF。
  - 到netcup ccp后台将地址信息改成跟月结单上的一致，然后就可以提交这份PDF了。

- 我当时是随便填美国的一个免税州的信息就过了

- 分两步，第一步是你提交到netcup，netcup内部会初审，此时是第一封邮件。netcup内部觉得没问题，他们会提交到外部，此时你收到第二封邮件。两封之间基本上2个工作日

- 你ccp里master data里的数据跟你提供的要一致

- ## [我推荐个.de域名注册商, 转入续费¥14/年 _202605](https://www.nodeseek.com/post-728664-1)
  - 注册是 ¥19.77 CNY，续费和转入是 ¥14.87 CNY
  - 顺便一提，他的.com转入也很便宜: ¥56
- 还是netcup搞活动最便宜，但这家好处是不用等

- ## [netcup kyc过了 _202605](https://www.nodeseek.com/post-736164-1)
  - 工商银行信用卡对账单，改成英文提交就过了，名字是乱写的，国内有姓fo的吗？

- netcup填的名字和账单名字不一样也能过吗
  - 能，我的就不一致，账单名字它不管的
  - netcup里面masterdata页面，你的信息要和对账单中一致，别的无所谓，随便搞

- [坏了 netcup的de域名收到kyc了 _202606](https://www.nodeseek.com/post-727694-3)
  - 就WPS文档翻译，会员的那个功能，然后就会给你输出一个原格式的英文版本，你不要直接交中文原件，netcup不收

- ## [spaceship 买的 .de 域名被封了  - LINUX DO _202606](https://linux.do/t/topic/2285288)
  - .de 域名是我当时推荐他买的，图省事直接在 spaceship 上买了，宇宙飞船现在检测这么严格了吗？
  - 域名也没有乱搞吧，托管在 cf 上，搭了一个博客和2fa的项目，用的子域名，一共用了也没两个月。

- de域名风控挺大的，会触发kyc认证的，而且你注册的时候提示就会提示你了，需要kyc，大概率是你的注册信息存疑，我是完全用德国真实信息注册的，没被封过也没触发kyc

- de域名才会，老传统了，他们会定期对域名注册信息审核，有些一看乱填的百分百触发kyc，需要证明你是德国人才解封。

- 不需要是德国人，只要你提供的文件跟你购买域名的身份对得上就行，我半个月前刚过验证，用的是国内的银行账单
- netcup真实信息的，两三年的de域名都没啥事

- 前两天de的DNSSEC爆炸了，de管理局除了修DNSSEC，也开始使用bot审查whois记录，先拿那些假的离谱的开刀，会要求验证地址

- ## [如果你有.de的域名的话，可能会遇到KYC - LINUX DO _202605](https://linux.do/t/topic/2205831)
  - 这两天收到域名KYC的人应该不少，de现在大面积发邮件，好像ru也有
  - 建议这种可能要KYC的国别后缀，尽量填真实信息，尤其是姓名，地址最好是真的，以防KYC的时候，你需要用英文的银行卡账单之类的核对，地址要对得上
  - 再补充一个，如果你是netcup上买的，没有及时续费会产生滞纳金，同时30天内不做KYC，netcup会直接停掉域名
  - 有缓冲期，30天内，只要别卡死最后几天做应该能通过，会存在部分审核卡住的情况，正常工作日1天能审核通过，如果超过3天可能有点问题了

- 啥意思，de域名托管到cf触发kyc吗，还是托管到哪里。是netcup还是托管机构让kyc
  - 托管，不一定是cf，有概率会触发，kyc是注册局要求的，nc只是执行注册局的政策，目前还不知道具体触发规则是什么，有的什么都没干就收到，有的刚注册就要求，不想要kyc的话就别动他了，延缓触发kyc
  - 国内的地址也行，和银行对账单上的地址一样就可以

- 其实很好过，我拿宇将军的身份证都过了

- ## [0.11€的.de域名！netcup复活节活动限时返场了！附PayPal国区-国际号与netcup的注册事项 - LINUX DO _202504](https://linux.do/t/topic/594811)
  - 支持：PayPal国区 - 国际号
  - 如果你是netcup第一次买，下单需要填入地址信息之类的，尽量填真实的中国地址信息，相对详细一点，地区选中国，名字拼音。全部信息使用英文填写。中国直连，不要开代理下单。
  - 中国地区免税
  - netcup人工审核注册信息，比较严格，假信息容易被拒单。

- ## 💡 [[教程] NetCup注册一次过教程 & 常见问题 & 当前活动：世界杯促销活动 - DE 域名 0.11 欧 / 月 - 教程 - IDC Flare _202601](https://idcflare.com/t/topic/55040)
- 由于NetCup的风控机制严格，下单后可能会发邮件告诉你订单可疑而被取消（也就是注册失败）。 必须下单的同时才能注册。
- 关闭所有代理，打开浏览器无痕模式，进入NetCup官网。
- 填入地址信息（关键）
  - 先去IP2Location查询下当前IP的归属城市。注意：查询显示的城市不一定是你实际所在的城市，以查询结果为准。
  - 然后去高德地图在该城市中随便找一个地点（如酒店），最好是xx路xx号的形式如：崇文门西大街1号。同时搜索得到该地点的邮编为：100005。
  - 最后让翻译软件翻译成英语：No. 1 Chongwenmen West Street。注意路需要翻译成Street而不是拼音。
  - 确认订单金额，优惠券都无误后，点击提交订单，进入人工审核。
  - 一般 1 小时内，审核通过，会给你发一堆邮件。 在Identity Verification required这封邮件中点击链接进行身份验证。
  - 可通过PayPal或者银行卡支付订单。
  - 注册完成后，以后登录对ip还有限制吗？没有，之后随便登录，不会风控。

- ## 💡 [从注册到免税和合约，netcup个人注册图文记录（附注意事项与全年促销总结，补充本次0.11欧每月的de域名注册记录） - LINUX DO _202506](https://linux.do/t/topic/743845)
  - Netcup 是欧洲著名的云服务器大厂，稳定度和信誉有保证。
  - 但到国内的线路无优化，普通线路，高峰期会拥堵，属于不好也不差的线路。
  - IP质量不会高，对此请降低期待。
  - 德国合同法视合同为持久协议，终止的责任在于客户。厂商注重契约精神，取消合约需要用户手动去取消。 允许在合同签订后的14天内无理由撤销合同 。
  - 可选择Direct Debit (直接借记)、Bank Transfer (银行转账) 、PayPal (支持国内paypal)、Credit Card (外币信用卡，支持虚拟卡)
  - netcup 会人工审核注册信息，且审核较为严格，假信息可能容易被取消订单。因此建议直连访问，不要开代理下单。
  - 早些时期netcup的注册身份认证需要上传个人资料，现在放宽，可以通过预付款来身份验证，而不需要上传资料，本贴使用的也是预付款验证的方法，注意操作时不要选错。

- netcup本身不提供域名隐私代理服务，WHOIS的展示主要依据相关注册局的规定。
  - 对于de，在德国的域名注册局 DENIC（对个人隐私保护很看重）的规定下，姓名、地址、电话、邮箱等隐私信息在 WHOIS 中会被隐藏。
  - 对于eu，由欧盟指定的注册局 EURid 运营，遵守 GDPR（ 欧盟通用数据保护条例），姓名、地址和电话会被隐藏，会显示邮箱地址和“通信首选语言”。
  - 此外按EURid规定也可以向注册商（netcup）提供一个可用的替代邮箱用于公开显示

- ## [1.32欧/年！netcup de域名活动限时返场 - LINUX DO _202606](https://linux.do/t/topic/2379981)
  - 每月0.11欧，年付1.32欧，首次购买额外一次性收取1.68欧。即首年3欧，续费1.32欧/年，折合人民币首年23.4元，续费13.1元/年
- 前段时间费了个 de，要求 KYC，很麻烦，有护照还好一点，否则非要英文版证件，沟通了一个星期放弃了，果断丢弃
  - 还有网杯需要邮件沟通，没有在线客服，一般都是第二天回邮件，建议避雷

- 前段时间刚买完，没几天就要求KYC，没理他给我封了

- 我也使用快一年了，就前段时间突然要求让我 KYC，不是注册时要求 KYC。
  - 大概意思是：您的域名存储的联系方式已被负责的注册机构归类为可疑或高风险，必须进行验证，以便您的域名保持在线。
  - 我注册信息都真实的，这个邮件沟通是真费劲，每次都是第二天回复你，烦得很，很多域名注册商是有在线客服的，沟通很顺畅的
- 邮件沟通麻烦费劲我老早就吃过了，那确实，一天一次，要等对方上班回复。德国人上午上班是我们这北京时间下午16点，你就自己算吧，你经常会可能在晚上或者凌晨收到邮件。还好，客服还是很耐心的回复邮件内容和帮忙。

- 我也是绑了一些服务，突然发现绑定的服务都不可用才发现的，建议de只做备用，说不定哪天抽到，我上传的身份证，他们不认，要官方翻译版，官方英文版身份证我是闻所未闻，咱也没这个渠道。上传的驾照他们不认，只有护照有全部英文标识，我没有，但能不能用也是未知，他们还甩给我一个欧盟成员国合法身份证明的教程。 反正沟通来沟通去我自己都烦了，让他们直接删除我的域名，账号和留存的所有信息，不和他们玩了，把服务都转移到其他域名了

- ## [netcup的域名活动又来了 .de域名 0.11欧一个月 首次注册3欧一年。续费1.32欧一年 - LINUX DO _202606](https://linux.do/t/topic/2414229)
- .de不建议冲，有概率触发KYC，我有两个域名都碰到了挺麻烦的，想要域名不如去spaceship买
  - KYC直接用护照和中国地址也能过的

- 我的全部域名都是在spaceship 感觉目前spaceship就是最好的选择 还可以alipay

- [netcup Domain verification 流程分享 - LINUX DO _202605](https://linux.do/t/topic/2155012)
  - 5.7 收到了netcup的Domain verification 邮件，要求上传地址信息进行验证，否则会删除域名。
  - 搜了一下好像没人遇到。。。就提供上传了信用卡账单
  - 5.8 收到了netcup的回复，告知账单地址和Matser Data 信息对不上
  - 账单是PDF；Master Data就是CCP 的个人信息

- [netcup家2026年世界杯域名活动开始了！de域名1.32€每年续费原价！几十个后缀都在搞活动  - 教程 - IDC Flare _202606](https://idcflare.com/t/topic/97799/15)
  - 原则就是真实不伪造任何环境ip
  - 最好使用中国ip打开下面的购买链接
  - 这家是先给产品然后账单过一两天随之而来
  - 友情提示：这家的域名活动一般时间都不太久真的想玩的赶紧了
- 付款之后没有在控制台的域名那里看到东西，是要等一会才能出来吗？
  - 是的，都是人工审核的

- [netcup域名续费了，1.32€ - LINUX DO _202606](https://linux.do/t/topic/2237918/8)
  - 去年跟着佬们凑热闹也注册了一个1.68+1.32欧, 最近提示续费了, 今天又花了1.32欧续了一年
- kyc是要德国籍才行吗
  - 真实资料就行，应该是注册局的要求

- [netcup的de域名怎么续费呀，要到期了 - LINUX DO _202606](https://linux.do/t/topic/1929883/15)
- 应该会有邮件发账单的，我之前没注意到邮件账单，还有类似滞纳金的东西，比域名还贵，亏大了
- 留意注册邮箱的邮件提醒，账单会有提示，如果你在网站绑定了支付方式比如说信用卡，到期会自动扣费续期。

- 别急 netcup 算是域名注册中比较特殊的一家了 如果不要域名了需要提前通知的 续费那更不用急了 等账单就好

- ## [极其抽象的域名续费思路之迁移续费 - LINUX DO _202606](https://linux.do/t/topic/841921/2)
  - 在两个域名注册商之间反复横跳，有时候是低成本续费域名的好馊主意（当然存在一些限制）
  - 以这个普通的.art域名为例，其在Spaceship上的注册价格最低，仅$1.99，而 Cosmotown 提供了最低的续费价格，$13.37，与注册和续费价格基本一致。我们可以轻松计算得到如下成本：
  - Spaceship 注册+续费9年，总价为 1.99+(20.88)*9=$189.91
  - Cosmotown 注册+续费9年，总价为 13.10+(13.37)*9=$133.43
  - Spaceship 注册+迁移Cosmotown+续费8年，总价为 1.99+13.37+(13.37)*8=$122.32
  - 最后一种方法看似精妙，但仍然不是最低成本的方法（只要你玩得转且喜欢折腾）
  - 不难注意到，Dotology和Spaceship分别提供了$10.17和$9.88的迁移优惠价，那么只要： 在Spaceship上注册域名并等待60天冷却之后迁移到Dotology之后等待60天冷却之后迁移到Spaceship之后等待60天冷却之后迁移到Dotology之后等待60天冷却之后迁移到Spaceship之后等待60天冷却之后迁移到Dotology之后等待60天冷却之后迁移到Spaceship之后等待60天冷却之后迁移到Dotology之后
  - 由于迁移与上次注册/续费/迁移之间有60天的冷却期，完成此操作的时间成本大概是……540天（在你定好闹钟的前提下）
  - 该域名注册策略在绝大多数情况下仅供图一乐。要实现文中方法，你需要熟悉多个不同的注册商的平台规则，记好域名所在的注册商和下一步操作的时间，同时可能承担平台定价和迁移策略变更、部分平台莫名其妙风控等风险。总而言之就是，操作极其复杂，收益相对有限。

- ## [域名购买平台namecheap、namesilo、porkbun、cloudflare对比 - LINUX DO _202412](https://linux.do/t/topic/282622)
  - 打算购买com域名，我对比了namecheap、namesilo、porkbun、cloudflare, 其中首年namecheap最便宜，其次porkbun, 最贵cloudflare; 
  - 但是续费就是namecheap最贵了，大概17美金多一年，比另外两个贵很多！只要续费一次，就比porkbun的11多美金、cloudflare的10.44美金都贵不少了。还有其它namesilo也是续费贵，不适合购买
  - 从支付上，porkbub支持支付宝，cloudflare支持信用卡和PayPal
  - 总结，确定只买一年可以从namecheap上买，如果是2-3年则porkbub和cloudflare上都可以，越久cloudflare上越合算

- ## [国内注册商的可备案域名续费好贵，有没有便宜推荐 - LINUX DO _202606](https://linux.do/t/topic/2104137)
- 国内服务器好像只能绑备案域名，不然80和443会被拦截
- 国内别想了，cnnic 神人操作一堆，而且不备案锁你 HTTP/HTTPS 端口。
- 国内对于每种网站都有极其细致的备案要求，个人博客还分有可评论和不可评论两种，更别提论坛还要给管局提供超管账号。

- 个性域名都这样，首年便宜，续费贵死，而且容易 serverHold，我的 .top 就被封过一次。
- top域名早期很多诈骗网站使用，所以三大运营商都或多或少的对top后缀有所针对

- .top 的阿里云首年 1 元，续费十几块。

- [购买域名 有无续费便宜的域名 - LINUX DO _202605](https://linux.do/t/topic/2118542)
- 纯数字6-9位的.xyz域名，在Spaceship这个服务商注册价格和续费价格都最低，可以做到4块钱左右一年，续费同价，国内服务商一般6块钱左右一年，续费同价。
- 免费域名我是从来都不推荐大家去使用的，因为共用的人太多，会有很多人做违规网站，导致所有子域名都会跟着报毒。

- 续费价格比较便宜的域名，排除纯数字6-9位的.xyz域名以外，常规后缀我推荐.cn和.top。.cn和.top续费一般都是38块钱左右一年。

- netcup 搞特价的时候，.de 域名 0.11 欧每月，续费同价，按年付

- ## [请问现在想买个便宜的域名，各位老友有什么推荐的网站吗？ - LINUX DO _202605](https://linux.do/t/topic/2268522)
- 可以买xyz的，记得好像十年才几十？
- 可以看看spaceship，我有一个十年的六位数字xyz和一个org一个com在上面。org和com一年续费总共20刀

- 临时用可以买别人卖的临期域名，几块钱各种后缀都有
  - 长期用我自己买的top域名，10年好像是188，阿里买的

- 按年的花，想要续费便宜的话，cf 大善人可以，每年都是一个价。国内云基本第二年就翻高了。

- 得看你用什么后缀，一般上https://tld-list.com/ 或者米情局，如果有那种特别优惠的，像是飞船的xyz确实是注册很优惠，但是如果是续费的话就不一定，想要低价就买之前扫一眼

- 狗爹贵成那狗样，首年0.01的很多，然后限3年起购，后面每年来个49.99的太多了

- 最便宜的肯定是数字xyz。可以选择6-9位的数字.xyz域名，首年0.99美元续费同价。可以在这里查询想要的有没有被注册 https://gen.xyz/number
  - 其次呢就是.top。不过要注意下这个TLD由国人运营
  - 如果这两个都没有的话可以考虑下. OVH
  - 还有一个比较灵车的选择就是.kg
  - .edu.kg一年也就三四十的样子
  - 在买之前可以看看 https://tld-list.com要注意首年的价格，续费的价格，还有隐私保护收不收费。
  - 如果不习惯Cloudflare生态的话我比较推荐namesilo。但这家前后端的界面比较割裂（笑）。不过隐私保护什么的不用额外收费还是不错的。

- ## [求小众域名推荐 - LINUX DO _202605](https://linux.do/t/topic/2148661)
  - 之前有买.su的域名，但现在续费不了了
- 👷 实测小众的.space域名续费非常贵
- 现在 .ru .su还有几个俄罗斯域名都要实名很麻烦，关键不是俄罗斯人还不知道好不好搞，反正我没看懂应该怎么填
  - 好像只需要填写护照号，不需要上传任何图片吧？

- 现在2字母的国别后缀都挺贵的，除了cn和cc价格在你的预算范围内，好像其他都飞天了，但是如果前缀只有4位，估计cn和cc也已经被人注册了

- ## [喜欢短域名的来撸  _202511](https://idcflare.com/t/topic/37656)
  - 发现个网站，注册.uy域名只要10美元
  - 支持两位字母注册和续费这个价格可不多, 续费14美元
  - 记得地址填美国哈，不然有增值税

- [263个仍可注册的便宜2字母域名  _202511](https://idcflare.com/t/topic/37658)
  - aj.uy
# discuss-dns
- ## 

- ## 

- ## 

- ## 

- ## Cloudflare的域名注册业务可以说是走自己的路让别人无路可走。我现在是能转尽转。别人根本没法竞争。
- https://x.com/PenngXiao/status/1982716318836220250
- 是便宜还是说集成生态方便呢？
  - 最具杀伤力的还是便宜，这个没的说。就域名注册而言，大家也没啥区别。反而CF家还有一些限制比如DNS必须用他家的。集成方便也是真的。

# discuss-cloudflare-awesome
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [cloudflare免费版大概能用到什么程度会被要求升级？ _202606](https://www.nodeseek.com/post-783209-1)
  - 2个域名一个是自建S3存储一个是图床。
  - 图床全缓存，网盘只回源不缓存，主要作用是只藏IP/并保证更好的回源线路。
  - 图床和网盘下载的流量估计28或37开，每个月可能5-10T流量，会被封号或者要求升级吗。
  - 如果被升级的话$20的可以吗。还是一定要企业版？

- 别怕，每天7T还是活的好好的

- 只有不违规，流量随便造
  - 比如优选ip，流量大了会封号。缓存文件多确实可能会要求升级，但你5-10T流量的量应该是远远达不到的。

- ## The Cloudflare $5/mo plan is honestly absurd
- https://x.com/fayazara/status/2053774461934191032
Workers - 10M requests
D1 - 25B reads, 50M writes
KV - 10M reads, 1M writes
R2 - 10 GB storage, zero egress
Email - $0.35 for 1000 emails. I think first 3000 emails are included in the $5.
Browser - 10 hours per month
You also get
Durable Objects, Queues, Workflows - included, Unlimited Hyperdrive queries, Vectors.

- The absurd part is the point. Cloudflare isn't pricing a product, it's pricing the developer's first instinct. Whoever owns where you bash-deploy at 2am owns the decade after

- Big cloudflare fan use it for everything minus docker which I use railway

- It always comes down to the same reason: Vendor lock in. If that's a thing for you, walk along. If you don't care, there's nothing better than CF.

- ## Cloudflare 最强技术栈总结
- https://x.com/realchendahuang/status/2066514264656097571

Cloudflare Pages适合托管静态站等前端项目。也可以配 Pages Functions 做轻量后端逻辑。

Workers 是 Cloudflare 的核心 Serverless 运行时。可以理解为一段按需跑的 Node JS 函数。搭配 Hono框架可以实现基本完整的 API 后端。

Cloudflare DNS 可以用来管理域名记录，可以配置缓存这些东西。

Durable Objects，理解为可以持久存储的状态对象。适合处理强一致的小范围状态。比如聊天室、协同编辑、实时连接、用户会话、房间状态、AI Agent 状态、WebSocket 协调。

Containers，可以理解为 Docker 容器。用来跑各种各样的 Docker。但是它是按时间收费的。适合跑一些重型的任务。批量音频处理、复杂爬取、PDF/图片批处理、Agent 沙箱。

Queues 是消息队列，用来把请求和后台任务解耦。用来跑一些异步任务消息。

Workflows 是 Durable Execution，也就是可恢复、可重试、可持续几分钟到几周的多步骤任务。

R2 是 Cloudflare 的对象存储，类似 S3，用来放图片、音频、视频片段、备份、日志、数据集、模型文件、静态资源等。把它理解成一个很强大的网盘，免费用户有 10 个 G。

D1 是 Cloudflare 的 serverless SQL 数据库，把它理解成一个免费的 SQLite，免费用户有 5 个 G。

KV 是全球低延迟 key-value 存储。把它理解为免费的 Redis。

Hyperdrive，把它理解为自己托管的 数据库的免费连接池，可以加快自己数据库的连接，不需要每次每次请求都创建连接。在边缘端维护一个连接池。

Pipelines 负责把流式数据摄入、转换、写入 R2，可以写成 Parquet 或 Apache Iceberg 表。

R2 SQL 是 Cloudflare 对 R2 Data Catalog 里 Iceberg 表的 serverless 分析查询引擎。

Workers AI 是 Cloudflare 的 serverless GPU 推理平台，可以在 Workers、Pages 或 API 中调用模型。

Models 是 Cloudflare 的模型目录，包含 Workers AI 托管模型，也包含通过 AI Gateway 访问的外部 provider。

AI Gateway，是一个免费的 大模型 API 网关。可以把它官方的，包括你自己的一些模型的供应商聚合在一起。一起调用还有一，很强大的监测功能。

Vectorize 是 Cloudflare 的向量数据库，可以从 Workers 直接做 embedding 检索。

AI Search 是 Cloudflare 新的托管搜索/RAG 能力，可以连接网站、R2、上传文档，并支持自然语言搜索、混合搜索、metadata filtering。

Cloudflare Agents 是基于 Workers、Durable Objects 等能力的 Agent 开发框架，支持聊天、语音、邮件、Slack、webhooks、工具调用、持久身份、本地 SQL 状态、实时连接和可恢复执行。

Browser Run，是 Cloudflare 的浏览器自动化能力，可以跑 headless Chrome。

Cloudflare Images 可以在边缘动态 resize、优化、转换图片，避免你为每个尺寸存多份图片。

Stream 是 Cloudflare 的视频平台，负责上传、存储、编码、播放直播和点播视频。

Realtime 是 Cloudflare 的 WebRTC 相关产品，包括 RealtimeKit、Realtime SFU、TURN Service，用于音视频通话、实时互动、数据通道等。

Turnstile 是 Cloudflare 的验证码替代方案，可以保护表单、登录、注册、评论、API。

WAF 用于保护网站和 API，支持自定义规则、托管规则、Rate Limiting、安全事件分析。

Access 和 Tunnel 适合保护后台、数据库面板、内部服务、MinIO、监控面板、Admin。如果你自己部署的一些东西，你通过它，你就不用额外的再去做健全了。直接用自己的邮箱登录注册就行。

这些东西要么都非常便宜，要么有非常慷慨的免费额度。好好的利用 Cloudflare，基本上每个月都不怎么有服务器花费，这是在 AI 时代，我们每一个想开发产品的人省钱的利器。

关键是你别看现在这些功能这么多，你用 Codex 结合 Cloudflare 的插件，可以全自动的，按照你自己的需求。

帮你搭配好最佳实践，不需要你去操心，你只需要用豆包输入法口喷出来你的需求就行。

具体的执行由 Codex 来做。

但这一切的前提是你需要知道有这些东西。你要知道有了 Cloudflare，有这些东西才能让 Codex 去做。

所以在 AI 时代，知道 know how 也是一种很强大的技能。

- ## [[开源自荐] CF-Server-Monitor 部署在Cloudflare Workers的免费探针 - LINUX DO _202606](https://linux.do/t/topic/2391991)
  - 一个基于 Cloudflare Workers + D1 的多服务器监控探针系统，支持实时监控、历史数据查看、延迟追踪、地图展示等功能。兼容主流Linux系统，Alpine Linux，Windows系统。
  - https://github.com/huilang-me/CF-Server-Monitor /MIT/202606/js/vue
  - https://tz.dashdeep.dpdns.org/
  - 实时监控：CPU、内存、磁盘、网络、进程数、连接数、负载均衡
- 实测可用，现在可以把哪吒卸载了。

# discuss-netspeed
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [这个是什么工具，找了一圈也找到半点踪迹 _202606](https://www.nodeseek.com/post-782556-1)
- [Impart公益测速Bot已上线 免费为你的订阅测速 同时招后端  _202505](https://www.nodeseek.com/post-350094-1)
  - https://t.me/Impart_Chat
  - [Miaoko ](https://www.miaoko.net/)
  - 一个自动化测试节点连通性的机器人，并会自动生成连通报告以方便使用者运维。

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
