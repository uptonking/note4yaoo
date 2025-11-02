---
title: devops-vps-community
tags: [community, vps]
created: 2024-11-16T10:52:39.113Z
modified: 2024-11-16T10:52:53.263Z
---

# devops-vps-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🆚 [自己买vps和ytb上面用cf搭建有什么区别啊 ](https://linux.do/t/topic/1105829)
- 选机场最好，稳定性有保障，不用你天天维护天天看着，专事专干

- 说白了都是流量转发，cf 只是使用 cf 的无服务语法编写了协议。协议支持比较少，cf 节点需要节点优选，而且部署代理容易 cf 封号。

- 如果按照现在说的话，那就是自己小鸡自己负责，cf 部署容易封号

- 原理都一样，自己买 vps 可以买更优路线

- 建议小号，真封了很麻烦。优选也是。

- VPS，IP 不乱跳才是最重要的啊！有一些网站服务检测到 IP 变化，就得重新登录。 而且 VPS 自己搭建的也安全啊！
# discuss-dns/domain
- ## 

- ## 

- ## Cloudflare的域名注册业务可以说是走自己的路让别人无路可走。我现在是能转尽转。别人根本没法竞争。
- https://x.com/PenngXiao/status/1982716318836220250
- 是便宜还是说集成生态方便呢？
  - 最具杀伤力的还是便宜，这个没的说。就域名注册而言，大家也没啥区别。反而CF家还有一些限制比如DNS必须用他家的。集成方便也是真的。

# discuss-vps-awesome
- resources
  - https://github.com/cloudcommunity/Cloud-Free-Tier-Comparison
    - Comparing the free tier offers of the major cloud providers like AWS, Azure, GCP, Oracle Cloud etc.

- ## 

- ## 

- ## 

- ## [Basic free VPS : r/VPS](https://www.reddit.com/r/VPS/comments/1mud4dp/basic_free_vps/)
- Cloudflare does not offer any VM services that I’m aware of. Workers is not a VPS.
  - GitHub has their code spaces, but they’re also not a VPS in the traditional sense, since they are intended to be used as coding apps in the cloud.
  - Oracle has the only “forever free” stuff, but as you said it’s complicated to set up.
  - On a side note, why would you go with a VPS if you already have compute at home? A VPS is just a computer hosted by someone else. It’s nothing special.

- Cloudflare doesn’t give you actual VMs, just edge functions and Workers with storage options. Oracle Free Tier does provide proper VPS instances, though the setup can feel clunky at first. GitHub Codespaces is another route but it’s more for dev work than a true always-on server.

- ## [Free VPS. low performance is fine : r/VPS](https://www.reddit.com/r/VPS/comments/1l05w5g/free_vps_low_performance_is_fine/)
- Yes, you can get a free VPS using Oracle Cloud or Google Cloud that offer a 'free forever' instance. Those do require a card, and I recommend using privacy.com to create a $1-2 limit card for verification just incase you don't get an unintended charge.

- There is no “free” VPS that is usable. I don’t like using Google Cloud, Oracle, and others because you have to use a card to sign up and risk being billed a ton of money accidentally.

- ## [Is this true? GCP provides e2-micro always free : r/googlecloud _202505](https://www.reddit.com/r/googlecloud/comments/1kjw4u7/is_this_true_gcp_provides_e2micro_always_free/)
  - Does this mean that GCP provides e2-micro one instance free every month for always even after 300USD credits gets over?

- If I create more than 1 VM and each VM usage does not exceed the limit - is it still Free?
  - Yes, you are charged on the basis of time not on instance. Your limit is 730 hours
  - Your Free Tier e2-micro instance limit is by time, not by instance. Each month, eligible use of all of your e2-micro instances is free until you have used a number of hours
  - Compute Engine free tier does not charge for an external IP address.

- I follow the above to create the VM Instance and I somehow still get charged
  - Turnoff scheduled snapshot, and delete all existing snapshots, then you won't be charged by compute engine.
- Thank you . It works now. Filtered by SDK and found that snapshot actually grouped under compute engine.

- [Free VPS really exist ? : r/selfhosted](https://www.reddit.com/r/selfhosted/comments/14p8qq9/free_vps_really_exist/)
  - they wont accept my credit card, just like oracle
  - it says only 1gb outbound/ month?

- ## [有没有比较好的免费云服务器推荐？ - 知乎](https://www.zhihu.com/question/638923115/answers/updated)
- aws里面有一款2核2g的免费套餐，可以用一年

- 免费套餐：阿里云提供了“飞天加速计划”，针对学生和开发者提供免费的云服务资源，包括ECS云服务器、对象存储OSS等。这些资源通常有一定的使用期限和资源限制。

- ## [常见各种线路VPS的推荐和碎碎念 - 开发调优 - LINUX DO _202510](https://linux.do/t/topic/920034)
- 搬瓦工
  - 美西线路两大巨头之一，主营三网优化线路，特点是性价比高，稳定性好，老牌商家，缺点是 ip 较差，CPU 不可长期占用，长期占用会限制单核性能，近期 DC1 超售较为严重，常有断流的反馈。
  - 换 ip 10 刀 / 次我记得。
  - 这家的 aff 比率很高 (22% 返利)，所以有很多 affman 推荐，导致哪里都是这家的推广，当然产品本身质量也是相当不错的。
  - 瓦工有相当友好的退款策略，30 天内流量不超过一定限度，即使 ip 被 q 也可退款，可以放心购买。
  - 性价比高的套餐为
  - BiggerBox-Pro 年费 36.36 刀: 1c1g 21gdisk 1T双向/月 电信联通CN2GIA移动CMIN2
  - MegaboxPro 年费 45.68 刀: 2C2G 40gdisk 2T双向/月 电信联通CN2GIA移动CMIN2
  - MINIBOX 年费 27.04 刀: 1c0.5g 10gdisk 0.5T双向/月 三网CN2GIA, 最适合个人使用的小鸡，年付超低价，电信联通和Megabox相同，移动走的是CN2GIA而非CMIN2。 这个套餐还可以补差价升级为1T/2T流量，但不推荐，因为这个套餐的核心是小，加了钱性价比反而不如MegaboxPro/BiggerBox-Pro
  - 这家的正价产品性价比就很一般了，不如 DMIT，上面都是活动款，性价比爆炸的，有需要的佬友可以等待补货。

- DMIT
  - 美西线路另外一个巨头，瓦工上游，性价比也很不错 (比瓦工低点)，线路稳定，ip 比瓦工要好很多，而且可以免费换 ip，他家还有带防御的机器 
  - 这家有三网优化也有国际互联机器，优化鸡自带国际互联优秀。
  - 这家的套餐线就比较清晰，无非就是价格配置区别。
  - LAX. EB. WEE 年费 39.9 USD: 1C1G 20g 1T双向/月 电信联通9929移动CMIN2
  - LAX. Pro. Wee 年费 39.9 USD: 1C1G 20g 0.5T双向/月 三网CN2GIA
  - 有人对比了一下发现好像瓦工 megabox 性价比薄纱 DMIT，emmmm，从线路上来看是这样的，体感还是有些区别，这也是个很复杂的话题，双方都吵了很久了，各有支持者，我个人体验下来是感觉 DMIT 是有 EB 产品线比较特殊，联通快乐鸡，瓦工就没有，但是大部分情况下二者体验没什么差异，所以我个人还是推荐瓦工多点，DMIT 省事吧，选个好 ip 能省个 ip

- RackNerd/Cloudcone
  - 其实美西看了瓦工和 DMIT 就够了，其他任何一家都远远弱于他俩，没有资格能站在一起比较的，
  - 所以再推两家玩具鸡，常年弄出推销活动，10 刀左右 / 年的售价，无线路优化无性能，什么都不突出，就是便宜能当个玩具鸡，多少人的第一台小鸡呢？
  - 如果是一个小白，我推荐是先玩玩这两家的玩具鸡，玩明白了再换瓦工 / DMIT。线路本身相当爆炸，连上就是胜利

- 小秘书 (V. PS)
  - 特色：极致三网优化产品，美西最强线路
  - 一个主打优化线路服务商，早期相当多性价比不错的产品，但后续商家策略转为面向大户，基本不做散户生意，所以散户产品性价比相当低，但是他家有大口子的三网各自顶级优化产品，所以有不差钱的佬友可以上
  - 相当昂贵的价格，换来的是最为极致的美西线路，也是三网各自顶级优化中少见的 G 口小鸡，除了贵没有什么缺点。

- VMISS
  - 最新推出的 US - LosAngeles - TRI 系列，是非常推荐美西三网各自顶级优化产品，强烈推荐没有 DMIT / 瓦工的佬友购买此鸡作为临时替代
  - 特色：性价比很好的三网优化产品

- zorocloud
  - 特色：性价比不错的优化线路 + 伪家宽 ip
  - 主打优化线路 + 伪家宽的服务商，前段时间盲盒大卖，褒贬不一，我是觉得性价比还不错的，是这么多线路鸡里 ip 不错性价比很高的小鸡，还是十分推荐的，cogent/GTT 的 ip+9929 线路只要 25.8r / 月，实在是没什么毛病。当然这家有点超售严重，网络稳定性一般，可以算个不错的补充线路。

- 不推荐的服务商
  - zgo kurun 机房，稳定性一塌糊涂，是被上游坑害的服务商，谁买谁知道，买了差不多就是买个活爹。
  - lightlayer 优化线路正价性价比低，活动款抢不到要溢价收没必要，经反馈佬友提醒说这家还有台 29.9 刀 / 年的 9929/CMIN2 机器，这款流通性一般，我已经买了，测试一段时间后再做决定是否推荐。
  - hostdare 天天在 LET 上稿活动的咖喱商家，稳定性相当一般，ip 质量相当恶劣，三网优化线路超售严重，口子小 (100Mbps 以下)，原本性价比还不错的，但是被最近出的 VMISS 爆杀，故不再推荐
  - 三 A 家的 (ACCK/AKI/AKKO) 槽点太多，总结为性价比低
  - Bytevirt 美国优化上游是 DMIT，卖的还比 DMIT 贵，性价比低，不知道产品定位是什么
  - lisa 史，ip 线路和 zoro 同款，比别人贵一倍，有人说他家线路就是跑的比 zorocloud 快，emmmm，值翻倍的钱吗？

- HK 地区的低价非常难做，性价比高必定挨打，必定被薅，最后清退，HK 低价鸡大致结局如此，claw 已经清退，Y 系挨打最后限速。作为整个亚太的核心中转地区，性价比高的小鸡基本是存量，没有什么增量了，所以大量的 MJJ 在从直连转向专线 (IEPL/IPLC/IXP)，专线又有点通报严重，直连目前基本上也只剩下正价了，所以 HK 推荐是专线为主，直连为辅。对于预算不高不想折腾的佬来说，美西才是归宿。

- 亚太最昂贵的区域，JP 地区的最佳建议就是：能玩专线别玩直连。基本上所有线路晚高峰都是爆炸的，太拥挤了。如果还是选择直连，很难推荐出一款完美的产品，只能说性价比不错，各有千秋。
# discuss-vpn-awesome
- ## 

- ## 

- ## 

- ## 

- ## [求各位佬推荐靠谱的机场 _202510](https://linux.do/t/topic/1071814)
- 可以考虑 $3 买台落地 VPS 自建，套 cloudflarecn2 提速
- cf 在国内不是很慢吗？
  - 所以要优选啊，有些 cf 节点是香港新加坡的 cn2 线路，或者找反代了 cf 的 IP

- 如果佬对梯子都要求不高，低价机场就可以满足

- 便宜的有一元机场或者油管不良林的直播有免费公益的，贵的有奶昔等一线机场，也可以自建。

- 用的一元机场马马虎虎，可以尝试一些免费的一些节点网址 [免费节点 - v2rayShare](https://v2rayshare.net/f/freenode)

- 要求不高的话，宝可梦免费的应该就够
  - 这两个都是大机场，谷歌一下就能搜到，价格会比较高

- ## [关于机场节点多年使用以及深度测试的一点经验 _202509](https://linux.do/t/topic/967981)
- 作为一个机场重度应用者，一些经验与看法跟大家聊一聊。
  - 1 市场上至少有不下于 100 家节点机场我有试用过。
  - 2 软件除了 V2R 不怎么使用其它的主流都有日常使用.
  - 3 基于热爱，每天还会去搜集各种节点，包括开源公益网站。

- 如果对于机场要求不是很高，平时搜集一些公益节点足够使用。如果每天需要用来工作，至少要购买两家节点以上。一家常态化使用。一家长期流量备用。特殊时期容易出问题，就比如最近。节点不要买太长时间，如果试用过稳定的时间。最多一次性买一年。不熟悉的节点先买一个月试用，跑路节点多不胜数，一定要选择全员在外落地的机场。

- 本人最近收集的节点比较多，但昨天来了一个大暴击，可能是城墙又厚了。发现之前好多优秀的节点不经打。最后蓦然回首，发现之前自己买的订阅坚挺得很。

- 机场才是最终的归宿，一二线机场一般都不会出问题

- 另外还有一点补充，选机场的时候就看机场的导出订阅。是不是有多协议可选？如果只有一个通用订阅那一般是个人搭的小机场没实力。

- 我试过二三十家机场，后来发现还是一线机场牛逼，贵就是好
  - 毕竟花了钱人家才会花大精力去维护。正向循环，但真的购买时间不要太长，太多跑路的了。
# discuss
- ## 

- ## 

- ## 

- ## [有什么提供免费主机的idc服务商 - 茶馆 - IDC Flare _202509](https://idcflare.com/t/topic/5602)
  - oracle
  - vercel/netlify
  - webhostmost 虚拟主机

- Netlify支持Function，所以也能部署动态网站，看你会不会写
- Vercel 也能跑后端，不过是类似云函数，需要对已有的程序做一点改造。额度其实也不算多，放个 demo 差不多吧

- 有意思，第一次听说wasm，好像是可以把PHP解释器 + SQLite数据库整个打包编译成Wasm，并放到了用户的浏览器里运行的方式，这也算是动态的吧

- 我提一个，mofh，只要自己有域名，就能自己当admin，就是文档有点旧
- infinityfree送的二级域名容易出问题，有时候整个域名要停几个月。还有就是数据库好像有点问题，经常动不动数据库无法访问，连接什么都没改，但过几个小时就又正常了，就很迷 

- 老生常谈，都不好搞了

- 托管这块可以增加一些老生常谈的容器化部署平台？ koyeb render 这些 还有railway(这个好像取消免费了但是老用户可以删除账号重新注册 每个月 5USD) fly.io

- 建议玩gcp, 一直续杯就行

- ## 对比不同平台 serverless 的结论出来了，有点出乎意料。同样 hono 写后端，开发部署速度、性能、成本最优都是 AWS Lambda。
- https://x.com/zhdsuperman/status/1904070505583563070
  - AWS 的方案是一开始最不愿意用的，结果用 CDK 编排技术栈上线速度超快，控制台都不用打开域名、证书、DNS 解析都自动配完了。
  - 使用 CDK 前提要熟悉 AWS 各种服务。

- lambda 性价比这么高吗？
  - vercel 的函数计算背后就是 aws lambda。

- 也应该是对比AWS GCP Azure. 过来人经验，不要被cdk拴死，直接上terraform

- ## 国内的云服务器快到期了，不打算续了。准备全部搞到海外服务器，但又不想用aws，调研一番，
- https://x.com/wsygc/status/1856623132087558565
  - 似乎digital ocean + dokploy是个不错的选择，兼具了便捷与可定制化。 有实战经验的推友分享下吗？
- 刚实战完，dokploy 非常好用
- 我看dokploy官方视频演示的就是 Hetzner ，算是官推首选了，有点介意的是“德国”产品，会不会延迟比较高

- 然后你的域名还需要转移出去，否则没法用，因为海外没法备案，然后你把域名从国内转移到国外会发现有多麻烦。 而国外域名往国内转就有想收个验证码的事儿
