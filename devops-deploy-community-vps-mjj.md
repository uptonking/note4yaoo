---
title: devops-deploy-community-vps-mjj
tags: [deploy, devops, mjj, vps]
created: 2026-06-17T05:42:26.194Z
modified: 2026-06-19T06:15:35.007Z
---

# devops-deploy-community-vps-mjj

# guide

- tips
  - 分析需求: 想要更强的CPU、更大的RAM、更多的流量、CN线路优化、升降配置
  - 公开与分享的需求不强时，没必要上顶级vps
  - 可以先月付便宜的vps，等到活动或论坛有人抛售时再获取长期vps
  - dedirock性价比高，但口碑不好
  - 是否能多次免费更换ip
  - 支持7天无理由退款的很方便

- comparison
  - [VPS值得买！ 产品库存状态 ](https://stock.vpszdm.com/)
  - [Cheap VPS Deals ](https://serverdeals.cc/)
  - [PoorVPS - VPS 导航 ](https://poorvps.com/)
    - [HostDzire CN | HostDzire Deals Monitor ](https://hostdzire.cn/)
    - [RackNerd Plus | RackNerd Deals Monitor ](https://racknerd.plus/)

- resources
  - https://github.com/cloudcommunity/Cloud-Free-Tier-Comparison
    - Comparing the free tier offers of the major cloud providers like AWS, Azure, GCP, Oracle Cloud etc.

- forums
  - [LowEndTalk – Web Hosting Forum & Community ](https://lowendtalk.com/discussions)
# vps-xp
- 如何隐藏服务器ip

- usecases
  - opengraph
  - blogs
  - new-api, sub2api
  - download proxy
  - vpn
  - frp, tunnel
  - 图床
  - 网盘/文件服务器
  - webdav
  - 密码管理器: vaultwarden
  - git自托管仓库
  - sync notes/settings
  - remote control
  - plex, jellyfin
  - 抽奖， 将吃灰的小鸡也抽了
- saas
  - ai-chat
  - rustdesk/远程桌面
- 定时任务
  - 系统/平台 的 探针/健康监控
  - 自动签到
- server-underrated
  - email server
  - text search
# vps-vendors

## dartnode

- [DartNode - Affordable Cloud Hosting, Dedicated Servers & VPS Solutions ](https://dartnode.com/warehouse-deals)
  - vps规格多， 主要是美区，美东/美西都有
  - ✨ 
    - No bandwidth caps or overage fees. Use as much as you need within fair use policy.
    - Full Root Access: Install anything, configure everything. 
    - Optional enterprise-grade DDoS Protection
    - Custom ISO Support: Upload your own ISO images. Run any OS, any configuration. 
    - Automated Backups: Optional daily backups stored off-site.
  - [DartNode 无限流量 vps 注册申请教程 ](https://www.hicairo.com/post/71.html)
  - DartNode 成立于 2023年，总部位于休斯顿技术中心的中心地带，是 Snaju® Inc. 的一个部门，在 NASA 约翰逊航天中心附近运营着一个 24/7/365 网络运营中心。
  - 提供带宽  1 Gb/s 不限流量的 vps 套餐，其中 VPS-1 Plan 每月仅需 2 美元，对于经常看 Netflix、youtube 或需要大量下载的小伙伴，终于不用担心流量用超的问题了。

- [How to Create, Restore, and Delete Snapshots (Backups)](https://help.dartnode.com/cloud-compute/cloud-compute/manage-snapshots-backups)
  - View your current snapshot count, total slots (3 free, or 30 with the premium addon), and auto-schedule status.
  - Warning: Restoring a snapshot overwrites your current server state and reboots the server.
  - Premium Backups ($4.95/month): Upgrade from 3 to 30 snapshot slots with auto-scheduling by enabling the backup addon.

- [How to Grow a Partition on Ubuntu](https://help.dartnode.com/how-to/linux/how-to-grow-a-partition-on-ubuntu)
  - If your Ubuntu server was installed using a default partition layout, and it's not using the full capacity of the physical disk, you can manually expand the partition and filesystem to utilize all available space.
  - This guide will walk you through the process using common tools like lsblk, growpart, and resize2fs or xfs_growfs, depending on your file system.

- docs
  - [Does DartNode block ports?](https://help.dartnode.com/faq/does-dartnode-block-ports)
    - By default, DartNode does not block any ports — you're free to use any port you need. However, we do monitor for abuse and maintain protections to ensure network health. Our filter list is updated every hour, automatically.
  - [Difference Between VPS, VDS, and Dedicated Servers](https://help.dartnode.com/faq/what-is-the-difference-between-vps-vds-and-dedicated-servers)
    - A VPS(Virtual Private Server) is a virtual machine that runs on shared physical hardware, giving you dedicated slices of CPU, memory, and disk space — but the underlying infrastructure is shared.
    - A VDS(Virtual Dedicated Server) is a step up from VPS. While still virtualized, it provides guaranteed CPU cores and RAM, offering near-dedicated performance.
    - A Dedicated Server gives you control over an entire physical machine — 100% of the hardware is yours, with no sharing.
  - [How to Reinstall the Operating System](https://help.dartnode.com/cloud-compute/reinstall-os)

- pricing
  - [Can I Transfer a Service to Another User?](https://help.dartnode.com/faq/can-i-transfer-a-service-to-another-user)
    - Yes! DartNode allows you to transfer services to another user — completely free of charge
    - Open a support ticket with our Accounting department.

## popular

- [DediRock ](https://billing.dedirock.com/index.php/store/promo-vp)
  - 美西、美东 价格不同

- [Hosteroid ](https://www.hosteroid.uk/store/special-deals)
  - 2c4g - $20.9/year
  - 可选: London, New Jersey(US), Amsterdam, 很多欧区
  - [Hosteroid美国新泽西KVM VPS：1核2G/25GB NVMe/1.5TB月流量/14欧元/年 ](https://www.vpsjyz.com/5790.html)
  - 上线美国新泽西机房，依然是赠送双倍流量，仅限新订单，不得转让。旧套餐不得更改为此套餐。
  - 成立于2018年的英国IDC商家，主营英国伦敦、美国新泽西、罗马尼亚布加勒斯特、奥地利维也纳机房的虚拟主机、VPS、专用服务器业务。
  - [Hosteroid是不是灵车？ _202411](https://www.nodeseek.com/post-188592-1)
    - 还不错，闲置了半年了，很稳，老板人也很好说话。
  - [【测评+已出勿念】hosteroid 闪购鸡7.24欧1年 2C4G50G ](https://www.nodeseek.com/post-246683-1)
    - cpu和RN的差不多。内存给的很大。硬盘性能非常不错，基本上第一梯队了吧。ip质量不错，解锁啥的也很全。网络10g口。结合这个价格，性价比没得说。为啥出：鸡太多从买来到现在一直吃灰。

- [HostDZire :: Premium And Affordable Web Hosting Solutions ](https://hostdzire.com/billing/index.php?rp=/store/usa-cloud-vps-services)
  - [HostDzire CN | HostDzire Deals Monitor ](https://hostdzire.cn/)
  - [LAX-USA Cloud VPS #1 ( Triennially-Special )](https://hostdzire.com/billing/cart.php?a=confproduct&i=3)
    - 4c6g - $64/3year, $21.3/year
    - 100 GB NVMe
    - Bandwidth :- 25TB/mon
    - Ip :- 1 IPv4
    - No Refunds | No Replacement | No Transfer Policy
  - [HostDzire 闪购活动，最低至 $66 三年付 - 情报 - IDC Flare _202511](https://idcflare.com/t/topic/37061)
    - Leaseweb 是 1997 年成立的，只卖给大户，分销商 HostDzire 也卖了十年了
    - 有代理需求的佬友退让了，这家到国内线路基本不可用，跑服务和网站还行
    - 这家是建站和服务用，没有任何优化，大部分都绕路
    - No Refunds这条有点硬，三年付万一中途出问题就只能认了
    - 这价格九月就有了
    - 我有个洛杉矶的，搭了节点网速不行，ip进不了gpt，能进奈飞。 晚上有时候谷歌都打不开，youtue限速。 iperf3测速，tcp到国内最高70兆，udp能跑满500兆，但是我搭hy2的udp节点只能跑到50兆不知道为什么。 说实话我不是很想要这个vps了。
  - [求教，hostdzire的用家，可以升級內存 - IDC Flare _202606](https://idcflare.com/t/topic/91112/3)
    - 不可以，因为是分销上游的，上游不支持

- [GreenCloud ](https://greencloudvps.com/billing/store/budget-kvm-sale)
  - 1c2g - $15
  - 2c4g - $25
  - CA, NY, UT, Phoenix, Canada
  - [绿云12周年 _202510](https://www.nodeseek.com/post-482135-1)
    - 闪购——独家生日 VPS 套餐
    - 预购开放地区：荷兰阿姆斯特丹和德国法兰克福
    - 即将推出：悉尼、犹他州和纽约的新机架！
  - [说下我对绿云的认知（主要是缺点） _202512](https://www.nodeseek.com/post-538290-1)
    - 优点：工单回复快。 长期运营。
    - 配置只能看不能用（cpu限制30%）。
    - tos条款免责声明特别多，并且商家可以随时更改。
    - 和绿云客服打过几次交道，想退款是不可能的，基本也不存在人性化处理。
    - 目前性价比套餐，没有任何线路保障，目前优化能用的线路或许只有澳大利亚的au（我没有）。
    - 很容易被封号的（相对而言）
    - 绿云真没那么垃圾，很多人一看30%直接开喷，问题是咋不看价格，咱们能不能花了多少钱再去要求多少钱的服务啊，而且那30%说白了就是个免责声明，我现在就能跑100%占用超过一小时我机子也不会停信吗
    - 绿云感觉是亚太线路中比较有性价比的。而你说的不管是不让退款，还是限制CPU，都是因为成本在那（好多闪购都是亏本的）。
    - 垃圾玩意，那么高配置，装个编译的软件，结果给我关机，然后还不会自动开机。
    - 除了优化线路，不要指望任何线路能长期使用
    - 闪购蹲到的话很不错，但是动不动三年的话就难顶了
  - [绿云日本软银两款有什么区别呢？ - 求助 - IDC Flare _202510](https://idcflare.com/t/topic/34243/6)
    - 线路和带宽一样，2222用的ZEN4，内存少2g但能三年付最低叠到60，Bucket用的ZEN3，内存多2G但只能年付25，其他一样，说是2222性价比更高
    - 绿云所有机器都没有中国优化，只有日本软银和iij这两个能直连的勉强能用，其他全都是纯纯的落地或建站机

## more-vps

- [Chunkserve - LET VM Special ](https://billing.chunkserve.com/index.php?rp=/store/let-vm-special)
  - 1c3g - $9/year
  - 3c3g - $12/year
  - 2c4g - $15/year
  - 欧区 荷兰/波兰
  - [chunkserve：便宜荷兰VPS，低至$1.3/月，1G内存/1核/15gNVMe/2T流量/1Gbps带宽 ](https://www.zhujiceping.com/75476.html)
    - 2022年成立的荷兰公司， 自有网络AS214481，当前主要运作荷兰和波兰数据中心的VPS、独立服务器、设备托管… 这里介绍下荷兰vps，低至$1.3/月，采用E5-2690v4、DDR4、NVMe SSD阵列，1-10Gbps带宽、CPU、内存、硬盘、IP在下单的时候都是可以自由定制和扩展的…官方支持PayPal、Stripe、加密货币、支付宝、Apple pay等。
    - KVM虚拟，NVMe SSD阵列，1Gbps-10Gbps带宽，自带一个IPv4
  - [[Chunkserve] Payment done, server not delivered, no support response — LowEndTalk _202606](https://lowendtalk.com/discussion/218301/chunkserve-payment-done-server-not-delivered-no-support-response)
    - Chunkserve's stuff is on vacation now please come back in September or October, in October is better. Thank you for your support and patience.
  - [ChunkServe 争议退款了，这也太灵了... _202606](https://www.nodeseek.com/post-757933-1)
    - 刚买就失联，5/15开始又失联
    - 工单是不回的，virtualizor面板是用不了的，discord都是催工单的
    - 4h差点没单核高 大部分正常服务器都是单核1k
  - [chunkserve，买过最离谱的灵车 _202601](https://www.nodeseek.com/post-588520-1)
    - 欧元美元英镑都是一个价
    - 买鸡即失联，每一小时可以正常连接ssh十分钟，体验真正的速度与激情。
    - 四核GB5狂跑1000分！氪星石头盘。
    - 一星期了还没回工单，按let论坛说法下次回工单应该得2月中旬了。
  - [chunkserve 这家VPS服务商有什么黑历史吗，它家咋样？ _202511](https://www.nodeseek.com/post-506641-1)
    - 站里一搜就有，机器长期离线，工单不处理
    - 价格实惠，线路不行，晚高峰经常断联。
    - 已经失联好几天了，一个月总有几天掉线，工单一个月处理一次，垃圾中的战斗机

- [HostBrr ](https://my.hostbrr.com/order/main/packages/anniversary/?group_id=59)
  - 1c4g - $36/year
  - Location: Frankfurt, Germany

- [Layer7 Networks GmbH ](https://login.layer7.net/index.php?rp=/store/cloud-server-germany-fra1)
  - 需要等活动
  - Location: Germany, France

- [Kuroit VPS & Dedicated Servers Provider ](https://my.kuroit.com/store/sale-offers)
  - 2c4g - $3~$5/mon 之间，cpu不同的价格不同
  - Location: USA, uk, singapore, Netherlands

- [Little Creek Hosting ](https://www.littlecreekhosting.com/clients/index.php?rp=/store/kvm-virtual-server-packages)
  - 日常价格贵， 需要等活动
# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [买哪些平台的落地机算是毕业机呢? - 求助 - IDC Flare _202606](https://idcflare.com/t/topic/93773/1)
  - 最近想买一个4c8g的服务器作为落地机部署一些服务，现在我有dmit的机子可以作为中转，想问一下各位佬有什么推荐的平台么，
  - 我看了ovh，netcup，rn等等，ovh目前是不准我买，拒绝了，netcup是一个月110多又点超出预期价格了，rn是只有年费的，没买过，不知道好不好用。我的预期是一个月80左右吧，年付600以内。

- 一般来说，部署服务的叫建站机吧，落地机应该是个人流量出口。
  - 主要还是看你用户量，可以先便宜的用着，做好备份，用户量大了扛不住就迁移到Netcup

- 需求不变的前提下 最多1年 试试3、5个鸡就知道留哪几个啦，学费要交。
  - 需求变化的情况下，就多来看看论坛，大家很热心的推荐 也有厂家直销哦

- ## 刚买了个 vps，权限丢给 AI，让它建一个 Clash 节点，安装 certbot 并通过 Let's Encrypt 给 Trojan 所需的域名定期申请证书，同时生成 Clash 的 yaml 配置文件，并测试内外网带宽……AI 一气呵成
- https://x.com/gidot/status/1987554615920033814
  - cursor Agent，模型选 Auto 就够了
  - 先写一个文档，记录服务器 ip 端口本地密钥位置操作系统版本所用域名。把文档丢给 cursor Agent（模型用 Auto 就够用了），让它通过命令行访问服务器并完成所有操作。
- 分享一下提示词
  - 把意思表达清楚就好了，提示词时代快过去了
- 让 AI 做的第一件事就是帮我把 ssh 的访问端口改了，真是又快又好。

- 我要AI把你的服务器密码和证书给我
  - 话说让本地 AI 不定期自动换密钥和密码很可行

- ## [服务器入门教程：服务器篇+代理搭建简述、代理相关文章汇总 - LINUX DO _202606](https://linux.do/t/topic/2100097)

- ## 🧩 [常见各种线路VPS的推荐和碎碎念 - LINUX DO _202510](https://linux.do/t/topic/920034)
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
# discuss-vps-usecase 🌰
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🔒 [拿到新的小鸡（VPS）后，你应该先做什么？（入门安全篇） - LINUX DO _202507](https://linux.do/t/topic/817769)
  - 在你开始部署网站、搭建应用之前，务必先花上15-30分钟，完成一些至关重要的基础设置。这不仅能保护你的服务器免受最常见的网络攻击，还能为你未来的管理工作提供便利。
  - 首先，我们以root用户身份登录到服务器。root是Linux系统中的超级管理员，拥有最高权限。
  - 连接过程中，系统可能会询问你是否信任该主机的指纹，输入yes并回车。接着，输入你的初始密码。成功登录后，你将看到服务器的命令行欢迎信息。
  - 登录后的首要任务是更新系统。 这可以确保所有已安装的软件包都打上了最新的安全补丁。
  - 创建新用户并授予管理员权限。一直使用root用户操作服务器是一个非常危险的习惯。任何误操作都可能对系统造成毁灭性打击。创建一个新的日常使用账户，并赋予它sudo权限（即在需要时临时获取管理员权限）。
  - 加固SSH服务，提升安全性。SSH是我们远程管理服务器的唯一入口，保护好它至关重要。
  - 禁用root用户远程登录。
  - (强烈推荐) 更改默认SSH端口: SSH默认使用22端口，这使得它成为自动化扫描和攻击的首要目标。
  - 配置基础防火墙。 防火墙是服务器的第一道防线。UFW (Uncomplicated Firewall) 是一个非常易于使用的防火墙管理工具，使用系统底层的iptables进行设置。
  - 安装Fail2ban防御工具，Fail2ban，顾名思义是防止后台暴力扫描的软件，通过分析系统日志中的异常行为（如多次登录失败），自动封禁可疑 IP 地址，有效抵御暴力破解攻击。
  - 将系统时间设置为北京时间，推荐使用 timedatectl 命令。
- 新手小白建议使用 Ubuntu 系统，默认配置比较完全，软件包更新也还算及时，只要你的 VPS 配置不至于比 1C1G（1 个虚拟核心，1GB 内存）还低，如果再低就换 Debian 吧，如果 Debian 还卡那就得用 Alpine 了，不过这个大多数人不太用得来，它太精简了

- fail2ban 不太推荐用默认的 ufw 来屏蔽恶意扫描，IP 太多了影响 ufw 自己，推荐用 iptables+ipset 的方式（nftables 我就不清楚了，不会用）
# discuss-free/awesome
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

- ## [坛里这么多注册机，有甲骨云的注册机么 - LINUX DO _202603](https://linux.do/t/topic/1812619)
- 有, 但是最好别用, 因为甲骨文除了ABC还有后封
  - 服务器又不像GPT, 封了大不了换个号继续用, 反正聊天记录在本地
  - 服务器被封了我还得花时间迁移…

- 有肯定是有的, 只不过有这个的都发财去了，之前有过一阵子突然冒出一堆甲骨文新号，还是域名邮箱的，只是别人一个号卖3位数的没理由给你开源的

- 已经试过了，注册了一星期毛都没有，反而卡里被冻了十几新币

- 自己让AI + 浏览器MCP，写个扩展辅助填写不就行了。

- IP库和卡台才是关键的

- 别想了，手动都是abc，还注册机
- 手动注册每天坚持abc呀，之前注册机跑域名邮箱，跑了两千多个号，没一个成功的，卡里被冻了那么多，不知道还会不会退回来，就停了

- ## [hf开始封滥用的帐号了 - LINUX DO _202603](https://linux.do/t/topic/1801888)
  - huggingface有免费的高配docker容器可以白嫖，当然之前一部分项目会触发滥用规则，其实就是各种2api，爬虫之类的项目，但是今天，我部署了2个2api项目，其实就是顺带测试一下看看hf的出口ip，马上干掉了我的space，还把我的账号封掉了，并且原因就是滥用space。各位佬注意咯，不要中招了。其实cf也有类似的规则，但是还算友好，只是封你的项目，不会干掉你的账号。
- hf 一直是在封各种 2api，青龙啥的

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
# discuss-paid-ww
- ## 

- ## 

- ## 

- ## 

- ## [海外服务器购买，有哪些推荐，以及哪些坑需要注意？ - V2EX _202606](https://v2ex.com/t/1196279)
- 稳定且性价比高选 Netcup 、便宜大碗选 racknerd

- 如果你要稳定性、又要性价比，因为 KYC 莫名其妙被封号的，排除 Hetzner （ KYC 严格、涨价、贵）、OVH （ KYC 严格，不欢迎中国人、涨价、贵）。
  - 可以看看 Netcup

- ## [dartnode过排队思路 _202606](https://www.nodeseek.com/post-781010-1)
  - 判断了这个参数是claim就弹出抢购页面，但是我没有claim_url怎么办？
  - 灵机一动，去排队另外两台月付几十刀的，人很少，一下就拍到了，抓到返回参数把商品id换成173
  - 实际抢购地址：https://dartnode.com/wh-session/173/claim

- 这是后端鉴权吧，哪有把逻辑放前端的, 肯定过不了

- ## [Dartnode 13.99 休士頓 _202606](https://www.nodeseek.com/post-781019-1)
一、 核心短板：CPU 性能较弱
配置：Intel Xeon Gold 6148 (2.40GHz)，分配了 2 核 2 线程。

表现：Geekbench 5 的单核得分 612，多核得分 1021。这个分数在目前的服务器市场中属于偏低水平。

影响：不适合用来跑重度计算、大型游戏服务端、复杂的实时视频转码，或者高并发的大型动态网站。如果负载过高，这颗 CPU 会成为明显的系统瓶颈。

二、 绝对亮点：极其优异的硬盘 I/O
配置：100GB 容量，测试显示大概率为 NVMe 固态硬盘。

表现：顺序读取（SEQ1M）高达 ~2585 MB/s，顺序写入高达 ~2900 MB/s。更关键的 4K 随机读写（RND4K）也有 50+ MB/s 和 13k+ 的 IOPS。

影响：这是这台机器最拉分的地方（击败了大部分同类检测库里的硬盘）。这意味着极快的系统启动速度、极其丝滑的系统重装与恢复过程，以及非常优秀的数据库（如 MySQL/PostgreSQL）读写响应。它在处理海量小文件时会非常从容。

三、 中规中矩：内存与网络设施
内存：总容量约 4GB（实际可用 3.8GB）。对于运行 Debian 12 来说非常充裕。配合 100GB 的硬盘，用来跑 Docker 容器、搭建几个中小型网站环境、或者作为测试节点是完全绰绰有余的。

底层架构：KVM 虚拟化，并且支持 VT-x 和 AES-NI 指令集。这意味着如果你需要在里面跑一些需要加密解密的代理服务，或者进行轻量级的嵌套虚拟化测试，底层是完全支持的。

- ## [求推荐服务器，大带宽无限流量每月 200-300 美元左右，最高可到 3K/月以内 - IDC Flare _202606](https://idcflare.com/t/topic/98226)
- RN这两款带宽最大1Gbps，流量不够直接+70刀/月买100T流量，或者可以+199刀/月升级为无限流量。缺点是带宽无法升级，优点是流量可以加，CPU也不错，同时工单很快。
  - HostDzire优点是带宽大，缺点是无法加流量，也没有无限制流量选项，CPU也略差

- ## [DartNode这个7刀年付貌似也没啥性价比啊 _202606](https://www.nodeseek.com/post-782223-1)
- 一般，除了无限流量，我为什么不选dedirock呢? 还是1h2g 30G的硬盘，虽然流量只有4T，但是正常建站玩机也足够了吧
- 如果是洛杉矶放货的话肯定很快就被抢光。

- 不如dedirock, 人dedirock工单回的也快，服务态度没的说
  - dartnode买了一天都没部署好，工单隔了老久回了一下，但也就是回了一下，啥问题没解决

- [DartNode的美南7刀鸡没人买吗？ _202606](https://www.nodeseek.com/post-782192-1)
- 买了美中了，可惜没抢到美西
- 库存多，放了115台，另外很多人都在等美西放货。

- ## [Let's discuss their service attitude. dartnode.com — LowEndTalk _202408](https://lowendtalk.com/discussion/196839/lets-discuss-their-service-attitude-dartnode-com)
  - dartnode.com They offered a very tempting price, and I don’t doubt the quality of their servers.
  - But as for their service quality, have any of you experienced something similar to what I have?
  - When you submit a support ticket, they hardly ever respond. They’re extremely lazy.

- I can't reach them from anywhere right now. If any of you know them, please help me find them. My server has been unreachable for several days, and there is very important data on it. This damn server is disrupting my work. I’ll say it again, I don’t want to damage their reputation, but if they see my post, please contact me as soon as possible.

- ## [做中转站推荐用哪个机？目前知晓以下4个鸡 - LINUX DO _202605](https://linux.do/t/topic/2238660)
- 看你用户数量，一般推荐HostDZire，但是有缺点，就是三年付绑定太长了，而且由于是分销商，所以无法更换ip，如果ip出问题了很难换，不过性能肯定是最强的，
  - 然后是绿云，绿云的问题的硬盘小，核心有30%限制，
  - 然后是Chicago，这家和ccs是一家，超售大王，可能会遇到容易关机的问题
  - 但是买HostDZire要考虑周期问题，三年付太长了，而且ip出问题了很难换ip，不过还是最推荐HostDZire，因为中转站并发肯定很多，所以绿云肯定不适合，因为有30%核限制，长时间超过就停机，所以这就是为什么我把绿云在排最后的原因，有核限制，无法程度并发高的任务
- 推荐HostDZire，个人目前在用HostDZire做开发鸡，rn和ccs的3c4g都持有但是这俩基本都因为有超售存在容易重启，HostDZire目前没有遇到问题

- HostDZire 作为落地还好，套CF，直连都不适合作为中转使用，我目前也是用的HostDZire 只能说凑合用，晚高峰丢包还是挺严重的

- hostdzire性价比不错，建站套CF就行，就是需要三年付要考虑一下，像VPS的G口带宽一般都是共享的吧，商家不可能允许长时间占满带宽
- 之前我站就是hostdzire，4c6g sfo月付，说实话不好用，cpu性能不好，超售了

- ## [大佬们总结聊聊稳的、值得推荐的VPS运营商 _202605](https://www.nodeseek.com/post-745439-1)
- 线路机就那么几家吧，亚太龙系和小秘书，大妈好像也可以，美国就瓦工大妈还有小秘书
  - 建站机除了大厂就nc吧，hd是三哥开的不太敢用，rn和ccs还有cc稳定性还是差了点

- 越来越多人直接用 AWS、Oracle 这些大厂了，虽然不一定便宜，但稳定性和生态确实舒服。

- netcup应该算很稳的建站了，然后就是一些大厂，腾讯云、阿里云、甲骨文、aws、azure、digitalocean，最近看到的DigitalFyre也不错，性价比也极高也很稳定。

- ## [DartNode, 这是在干嘛？我都排到51，结果给我重新顺延到127位，不抢了 _202606](https://www.nodeseek.com/post-780901-1)
- 我13.9的，跑到了第7，然后没了哈哈哈，7刀的跑到了第4没了
- 不要刷新，不要点其他的抢购，否则排名会重置。PS: 可以同时开不同的浏览器抢不同的产品，可以抢到后下单时再登录。

- [dartnode 核心发现：你排到了也没用！ _202606](https://www.nodeseek.com/post-780849-1)
- 排到是有用的，我是排到的。看样子是等前一个退单了才排到的，到了第一名还排队了1个多小时。。
- 界面显示还有五六台美西时，我就排到1了，等了十几分钟，然后还是没有
- 我排到了，然后告诉我没货蚌埠住了
- 每次排到#50就自动重排恢复#160了，非常逆天的商家

- 隔壁LET也有人说了，有个哥们排到第7名，然后莫名其妙掉到57名，还有一个人排了两个小时，纹丝不动，只能说难以绷住

- 我刚才点进去试了一下其实是 left 0 但是还让你排队

- ## [最近一直在看vps相关的，一些小心得体会 - LINUX DO _202606](https://linux.do/t/topic/2313988)
  - 看站里的测评啊，还有猫猫整理的资料什么的，发现这种像走流量的机子，除去涨价RN（已经变成了20刀了），大多都是10-15刀之间，甚至有的还会8刀（按年算）。这种都是1c1g。（我看的都是便宜的，不看超级优化线路的，那种略过 ）
  - 然后一些可能配置稍微好点的，低价的，大多都是美东，像CCS 这些。20-25刀应该就能拿下至少2c2g的，稍微贵点的像rn（总觉得涨的有点离谱）36刀也能拿下同配置。
  - 结果：像我这种一个月都用不了100G流量的，最近部署docker服务什么的都少很多，真的是放在那吃灰，而且像2c2g的说实话也运行不了什么龙虾呀什么的，折腾半天回过头发现自己竟然没那么多需求，基本都是用别人现成的服务。

- 去年在dedirock上 买了一个一年7刀的，感觉对我来说挺够用的了。

- 还是得有自己的稳定机子，甲骨文杀龟太突然了，没办法部署一些需要长时间稳定的

- hostdirze是36刀年付 4c6g（有同配置三年70刀的）
- CCS洛杉矶3c4g 年付22刀也还行

- ## [想找个年费100以内的大盘鸡 - LINUX DO _202606](https://linux.do/t/topic/2400758)
- 现在硬盘这么贵大盘鸡1个t的少说也要六七十刀（这还是几年前有活动的价格）

- dedirock客服挺积极的，我在他家买了两台，一台1.5T HDD一台2.5T HDD，有时候会出问题但是发工单回复很及时，他家好像隔段时间就发邮件说维护一次，具体冷备份的话应该无影响就是断线一小会而已，感觉性价比还是很不错 

- 最后买了Interserver的2.4刀月付试试咸淡，是钻石盘，Fio只有我绿云2T的十分之一，不过这个价格确实也没办法，我绿云2T年付要80刀。。。

- ## [佬们，有没有便宜的服务器链式代理webshare家宽 - LINUX DO _202606](https://linux.do/t/topic/2406011)
- 我现在用的dedirock，感觉现在便宜机器基本要被dedirock dedione两个替代了，我就是用的dedirock链式的webshare
- DediOne是不是最便宜12.99刀一年？dedirock好像我看着一年$9
  - 差不多，dedirock我黑五买的$7, 现在应该也是差不多$10，一个月还是断过两次，一个小时都能恢复，不过考虑这个价格也就还好

- ## [dedirock 是灵车吗 - IDC Flare _202511](https://idcflare.com/t/topic/37735)
- 他们家客服做的很好，去这个贴子下留言还能流量翻倍+IPv6
- IP烂完了，但是好在速度可以，7刀只希望能用的久点跑得晚点 

- 这家去年就在了，至少开了一年了吧，应该不是灵车……（就7-8刀要什么自行车……

- 老板在LET上高频互动, 工单回复也比较及时. 但是他的这个后台不显示IPv6, VNC无法连接, 工单一顿回最后也没解决, 无所谓了, 小玩具.

- 用一年不亏，两年血赚，三年他还不跑的话可以考虑传家了

- 问一下这种机器一般用来做什么？
  - 探针

- 他家的 IP 质量很一般， IP 风险完全看运气开出来的。

- 
- 
- 

- ## [🍀平替Racknerd美西！【5月10日售罄】CCS洛杉矶补货了，可能是目前美西最便宜的机器了，CCS低价机，不是优化线路，备用机优选美西 - 测评 - IDC Flare _202604](https://idcflare.com/t/topic/77833)
- 中国大陆到美国的优化线路或者无优化线路，几乎都是走洛杉矶，物理延迟低，买其他地方的也要经过洛杉矶，例如去美东的纽约，水牛城，美中的亚特兰大，芝加哥，都要经过洛杉矶。 目前确实是最便宜的，量也是最大，服务也稳定。其他品牌的不清楚，但ccs是十几年的牌子，跑路概率不大。

- 狐蒂云难民来了, 便宜一时爽，跑路火葬场
  - 我推aff也是看商家下菜，看起来不靠谱的都不敢推
  - 现在ccs算是最便宜的靠谱机器了，无优化，无优化，无优化，会玩的佬友都玩的很溜

- 开了台纽约的4c8g玩。不过这个开机真的好久啊。
  - 他们老外下班了就不上班的，一般下午或者晚上买开机会快一点
- 我半夜买的买完就开机了，纽约的2+2。虽然说听松弛，但是我之前中午找他们换IP啥的回复也挺快的

- ## [RN闪购建站鸡平替 2C4G100G 仅需13.99/y - IDC Flare _202606](https://idcflare.com/t/topic/99797)
  - 两家最大区别
  - RN 服务售后好
  - DN IP原生 解锁好，售后服务响应慢 支持PP支付
  - 我特意标注了pp，遇事不决上pp，敢上pp还是有点实力的

- 会有跑路风险吗
  - 我用了两年，就是售后慢，其他与这个价格匹配，跑路应该不至于，let上他们认过

- ## [日经贴, 小白求推荐个建站小鸡 - IDC Flare _202603](https://idcflare.com/t/topic/72945)
- hostdare 和 hostdzire 不是一家，后者是 leaseweb 的十多年的分销商，而 leaseweb 是始建于 1999 年的老牌厂商

- ## 国内的云服务器快到期了，不打算续了。准备全部搞到海外服务器，但又不想用aws，调研一番，
- https://x.com/wsygc/status/1856623132087558565
  - 似乎digital ocean + dokploy是个不错的选择，兼具了便捷与可定制化。 有实战经验的推友分享下吗？
- 刚实战完，dokploy 非常好用
- 我看dokploy官方视频演示的就是 Hetzner ，算是官推首选了，有点介意的是“德国”产品，会不会延迟比较高

- 然后你的域名还需要转移出去，否则没法用，因为海外没法备案，然后你把域名从国内转移到国外会发现有多麻烦。 而国外域名往国内转就有想收个验证码的事儿

- ## [有哪些性价比高的高配美国服务器 强调cpu和内存 线路似乎无所谓? - LINUX DO _202603](https://linux.do/t/topic/1792158)
  - 仔细计算 此帖应该终结了 我决定自己组建一台128gx86 或者直接mac, 这边问题是国内上行宽带升级一下 还有做好代理就好
- 
- 还有高配到底是啥高配，CPU单核强的，还是核数多的？还是内存大的，还是硬盘大的，还是带宽大流量足的，还是全都要？

- 直接干独服

- 我觉得最大预算会花在国内上行上

- 套cf只能不挑IP吧，带宽不够，访问速度一样上不来啊
# discuss-paid-cn
- ## 

- ## 

- ## 

- ## [亚洲优化线路感觉100%被通信运营商人为控制在高价位 _202606](https://www.nodeseek.com/post-786732-1)
  - 最近用了几个亚洲落地鸡，国际互联都非常优秀，而且价格都很便宜。由此让我对亚洲优化线路机器的售价远远超过美西优化线路鸡这种现象产生了深深的质疑。抛开最近由于硬件涨价导致亚洲优化线路机器一机难求。以香港举例，国际互联优秀的机器并不贵，但是内地优化线路机器比非优化线路贵很多倍。硬件、空间占用、电力、IP等资源这些两种机器应该是没太大区别，那么溢价就出在香港到内地的优化通信线路。而香港到深圳，不过隔了一条河，可以说建设跨境通信线路远远低于美西海底光缆。成本更低，卖得还更贵？还是说内地人就应该花高价用这么贵的线路？应该感恩？
- 建一堵墙，然后在墙上开几个洞，守在洞口收钱就可以赚大钱。

- ## 🆚 [一文看懂: 阿里云轻量与ECS服务器区别：价格、使用、网络及限制对比 - 知乎 _202604](https://zhuanlan.zhihu.com/p/2030928067451994982)
- 轻量服务器
  - 自动创建VPC网络资源，实例创建完成后默认配置了一个公网IP地址，不支持更换公网IP地址。
  - 带宽为套餐内指定，不支持自定义调整带宽。
  - 不支持安装虚拟化软件和二次虚拟化。
  - 不支持声卡应用。
  - 内网连通性上存在一定限制。
  - 仅支持挂载一个数据盘，且数据盘只能在创建轻量应用服务器时挂载。
  - 不支持部署集、资源编排、弹性伸缩、标签和资源组等ECS支持的高级功能。
  - 不支持配置IPv6地址。
  - 灵活变配支持升级为更高配置的套餐；也支持将服务器数据平滑迁移至ECS实例
  - 简便运维提供基础的运维操作，包括远程登录、服务器监控、简单的防火墙配置、数据备份与迁移、应用管理 、操作日志等。

- ECS
  - 支持自行规划和维护网络，通过专有网络、交换机等功能自行规划私网。通过安全组、网络ACL等功能自行控制流量。
  - 仅弹性裸金属服务器和超级计算集群支持二次虚拟化，其他规格族不支持安装虚拟化软件和二次虚拟化。
  - 不支持声卡应用。
  - 可以根据不同场景灵活变配。
  - 提供弹性扩容能力，实例与带宽均可随时升降配，云盘可扩容。
  - 提供丰富的OpenAPI。

- ECS公网带宽是独享的，购买云服务器ECS选择带宽的话会分配独立公网IP地址，轻量应用服务器公网IP也是独享的。
  - 目前阿里云轻量应用服务器升级到200Mbps峰值带宽，200M带宽是指该实例在公网出方向和入方向所能达到的瞬时最大带宽上限为200 Mbps，但该带宽值不作为业务承诺指标，啥意思？就是虽然标的是200M，但是实际达不到的意思。
  - ECS的固定200M带宽有区别，ECS固定带宽就是固定独享的，即便是网络高峰时段也不会出现丢包的现象，ECS的固定带宽是有保障的，轻量不承诺无保障，以实际为准。

- 出于安全考虑，阿里云服务器ECS和轻量应用服务器默认只开放了22和3389端口，其他的如网站所需的80、443端口，数据库3306端口等都需要手动设置开启。云服务器ECS是通过安全组来管理的，而轻量应用服务器是通过防火墙来操作的。

- ## [国内长期服务器求推荐 ](https://linux.do/t/topic/1350199)
  - 起因是题主2年前买的服务器最近快到期了，续费价格突然从一年400暴涨到2000+，转了一圈下来发现国内大厂都是这个策略，前期低价使用，后期高价续费。
  - 2年下来想迁移各类服务也蛮烦的，所以想请教下各位佬，有没有国内长期价格稳定的厂商，年付300-500，用途主要是建站+国内中转。续费刺客太吓人了
  - tips：因为手里还有境外的线路机，所以目前的想法是把一些网络环境需求不高的服务，比如博客，工具站、导航等等一些都放到境外的服务器上。但一些类似FRP和虚拟组网的服务就难办了。 

- 国内全这样，新人首单便宜，续费就是刺客~
  - 每年一换吧，VPS和域名都要备案，不备案就骚扰你，还有可能真的被封~所以真累了~
  - 腾讯流量刺客，超出后要付费，而且无法超出后自动实时停止。
  - 华为云方向很模糊，域名整个部门都不玩了，让人很担心~对了，白嫖华为代金券不错，而且华为这一点很赞，常年有各种活动，可以白嫖代金券
  - 其他的不是一线梯队大厂，不敢尝试~

- 不仅是VPS，国内域名也有续费刺客。。

- 阿里云99一年，可以续费三年，但是带宽有点子小3MB

- ## 现在阿里云服务器也这么贵了吗··· 4GB内存的低配，一年都要1000多，大家现在在哪买服务器...
- https://x.com/caiyue5/status/2051159488548450540
- 国内的服务器没有便宜的 海外的话过 cf 的话买啥都行

- 2核4g的服务器，企业实名认证的情况下，第一台一年只需要199，而且每年续费都是199，促销活动页里，是一个长期活动。
- 阿里云还是挺优惠的，双核4G ECS 199年，开通自动续费每年都是199。不过只能薅一台。不限地域。
  - ECS要流浪费吧

- digital ocean 也算小厂了吗
  - do是流氓厂，网上搞ddos攻击，无时不刻乱扫端口试图碰撞破解的，7成以上都是do的机器

- 搜轻量云服务器就得了，足够用了。你这个 ECS 是做主站分发用的，不适合你

- @Vultr这个可以，我用了六年了，最低2.5$一个月的美国节点，纯净IP

- 之前朋友找了一家香港的云服务，4核8g一年300多点，不定期断网、故障、联系不到人、设备数据丢失。

- 我穷，只买racknerd，配置tailscale，保证安全又节省了梯子

- greencloudvps性价比高，但是你要自己做安全防护。

- 我推荐几个，都是自己在用，比较稳定的服务器厂商，非常适合出海产品/外贸独立站：
  1. NetCup 这家我给很多做欧美的客户部署系统用的，非常经济实惠，可以买VDS，性能嘎嘎好，真正的独享资源；
  2. Ovh 超级划算的独服务，挺适合存储需求大的场景；
  3. Heztner 这个和ovh有点接近，我最近用的少了
  - Vultr / Digital Ocean 等这种算是云厂商里比较出名的，就是比较贵，对我来说使用没有感觉有什么优势，可能对非技术人员来说操作简单一些。

- nube.sh/invite/897602750V27SC 我最近用这家还可以，1cpu 2gRAM 3usd左右，关键是AMD 服务器zen3 CPU，现在VPS市场5usd以下套餐基本都是用10年前的inter服务器 CPU
# discuss-deprecated/shutdown
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [狐蒂云倒闭了，，，好牛批啊，连吃带拿 - LINUX DO _202605](https://linux.do/t/topic/2135602)
- 付费取数据也太不要脸了吧，吃相这么难看
- 无敌了，自己跑路，客户受到了损失还要付费才能取出原本自己的数据吗？

- 这一波跑路，其他厂家涨价太厉害了。简直牛逼啊

- 让我想起了前司的竞对公司的操作，也是业务到期了，然后甲方选了前司，竞对公司也是摆明了不打算干了，直接服务器拉闸了，用户数据直接锁死
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [刚学会用小鸡搭节点，玩了几天ip就被谷歌送中了 - IDC Flare _202603](https://idcflare.com/t/topic/63964)
  - 突然对mjj有了兴趣，搞了个很便宜的DediRock的小鸡，学习搭建节点、面板、探针，玩的不亦乐乎，今天突然发现ip被谷歌送中了, 有什么方法可以尽量避免ip被送中呀
- 怎么发现ip被送中的
  - 访问gemini的时候提示该地区不提供服务，前几天用的时候还没问题
  - YouTube, Google 搜索，未绑定账单的 Google Play 商店，都能很明显的体会到 “节点被 Google 送中” 了
- Android 手机的话记得关闭 GPS，因为只要手机有 GMS 服务且登录了 Google 账号的话，Google 就是会静默检查 GPS
可以尝试使用 WARP+ 往回拉一拉，或者如果是家宽的话可以直接向 Google 申述 IP 所对应的地理位置不对，当然如果能直接换个 IP 那肯定是最好的了

- IP 被 Google 送中的时候，YouTube App 也能打开并显示视频内容，无法使用可能的是代理没代理上

- 这算什么，好歹还玩了几天，我买的一台机子，刚开机就是送中IP
- 一般几天就回来了

- 先套warp，然后xui配置成vless+tls，优选IP，这样挺稳的
