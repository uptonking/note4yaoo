---
title: devops-deploy-community-vps-mjj
tags: [deploy, devops, mjj, vps]
created: 2026-06-17T05:42:26.194Z
modified: 2026-06-19T06:15:35.007Z
---

# devops-deploy-community-vps-mjj

# guide

- tips
  - 分析需求: 想要更强的CPU、更大的RAM、更多的流量、CN线路优化、可升降配置
  - 公开与分享的需求不强时，没必要上顶级vps
  - 可以先月付便宜的vps，等到活动或论坛有人抛售时再获取长期vps
  - dedirock性价比高，但口碑不好
  - 是否能多次免费更换ip
  - 支持7天无理由退款的很方便
  - 一号一鸡容易转手

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
- ports
  - nginx不常用端口 33777

- 如何隐藏服务器ip
# vps-vpn
- vendor的内网策略
  - [【已出】剩余价值-5 RakSmart 2核心，2G内存，50G HDD，大陆优化 VIP，带宽5G/3T流量 _202609](https://www.nodeseek.com/post-908183-1) 
    - 因为要组内网所以重新买在同一个账号下了 ，这个号的这台机器出了
    - 同一个账号下 同一个区域的机器 可以组内网 流量算单向
# tips
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

## colocrossing

- [Can I change the location of my VPS? - ColoCrossing Cloud ](https://cloud.colocrossing.com/index.php?rp=/knowledgebase/2/Can-I-change-the-location-of-my-VPS.html)
  - $3 for swap ip
  - ColoCrossing allows location changes on Cloud VPS plans purchased at standard pricing from our website
  - Your VPS qualifies for a location change if: It was purchased at standard pricing directly from colocrossing.com
  - Location changes are not available for: Special order VPS plans

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

- ## 🧩 [ [小白入门科普]服务器行业黑话大全 - 知乎 _202412](https://zhuanlan.zhihu.com/p/15029600004)
- 小鸡
vps，虚拟服务器，指由独立服务器虚拟出来的小型服务器。

- 母鸡
指独立服务器。因为vps都是拿独立服务器虚拟出来的（其实就是独服开了一堆虚拟机），所以小vps叫小鸡，生出小vps来的独服叫母鸡。

- 杜甫、毒妇
独服，独立服务器的意思。

- 落地鸡是网络不好，但是解锁啥的比较好，做落地
  - 落地机 则指的是VPS实际运行的服务器。当用户购买VPS时，实际上是购买了一段虚拟资源（CPU、内存、硬盘空间、带宽等），并在实际的物理服务器上运行。这个物理服务器就是落地机。当用户访问VPS时，实际上是在使用在落地机上运行的虚拟机进行操作。落地机的性能和稳定性对于VPS的使用效果非常重要，用户在选购VPS时也需要关注落地机的配置情况和托管商对于落地机的维护和管理情况。

- 中转鸡一般指线路优秀，或者国内沿海城市的中转服务器。其实都是袋里
  - 中转机指的是一个中间服务器，将用户的请求转发到目标服务器上。在使用VPS的时候，也常常会通过中转机进行访问。例如，用户在国内使用VPS搭建了一个网站，但由于网络限制等问题，国外用户无法直接访问该网站。这时，用户可以在国外租用一台VPS作为中转机，然后将中转机和国内的VPS连接起来，通过中转机实现访问。在此过程中，用户的请求会先到达中转机，再由中转机将请求转发到国内的VPS上，最后再将响应返回给用户。中转机也可以增加一些额外的安全性和隐私保护措施，保护用户的数据和隐私。

- NAT鸡指的是共享ipv4的鸡。用法就是多一层端口转发。虚拟机的NAT模式，运营商的公网地址(NAT上网)

- MJJ
小鸡是vps，母鸡是独立服务器，而购买他们的人就是买鸡鸡的人，简称MJJ，另含有没jiji的意思。

- 灵车
其实就是字面意思，比如你买了个vps或者其他服务，但是具体能用多久看卖家良心了，有可能今天买了明天就用不了，或者服务商跑路了，就是不确定买了能用多久（看运气随缘），多指那种新开没几年的，或者突然冒出来的新商家。

- 石头盘、钻石盘
指一些IO极低的服务器的硬盘，钻石盘（0~30M/S）是比石头盘（30~100M/S）更低IO的硬盘。

- DD
就是换系统，用非平台提供的方式来安装自己需要的新系统。
- 玉米
域名
- oneman
只有一个人经营的idc服务商，随时会跑路。

- 晚高峰
北京时间晚上7点~12点，上国外网站造成极高的丢包、延迟卡顿的现象。因为北上广三地负责出国线路的交换机容量不足，电信还限制普通用户的优先级，人为制造卡顿。

- CN2 GIA
GIA是Global Internet Access的缩写，CN2 GIA自然也是CN2线路的一种，并且是CN2线路中的高端产品，在CN2里的等级最高，全程和回程全部走59.43高速节点，CN2(AS4809)。CN2 GIA线路一般比较稳定，速度较快，丢包率低。

- CN2
分为CN2 GT和GIA，是电信的精品线路。普通用户是163（和网易无关）。GT是回程CN2，去程163，GIA是双向CN2，土豪专属。路由跟踪出现59.43开头的IP则代表经过了CN2线路。三网CN2是指其他运营商也走电信节点出去。

- 4837
指回国前一两跳及国外前一两跳经过AS编号为4837节点的线路。 由于线路负载相对较低，表现比普通的更好，比的CN2 GIA/9929等线路价格更为便宜，是一款性价比较高的线路，因此近两年成为热门选择。

- 9929/10099
联通的精品线路，数字来自于联通的ASN，而普通用户的线路是AS4837。

- 163
传统163骨干网，最常见也是最普通的线路，也叫ChinaNet(AS4134)，没有针对电信用户优化的线路，一般走的就是这个承载网络类型（全程202.97节点），因为用的人多，线路也没有优化，所以在晚高峰会出现线路卡顿，以及丢包率高的情况。

- CMI
中国移动国际公司，位于香港，移动的精品线路。

- 传家宝
指一些性价比极高且稀少的服务器，往往伴随着极高的溢价

- 三毛、五毛
俄罗斯服务器ruvds出售的超便宜服务器，如三毛便是因其30卢布（约2.7元）的价格且是毛子（俄罗斯）的服务器而得名。

- CFT
AWS亚马逊云永久免费CDN服务，每月免费1T出站（流量从vps到cft不计费，cft到你的电脑计入免费1T流量），但是因为超出1T将按要求收费，建站被打就是一晚一套房，绑自己卡怕是会被跨国讨债，所以mjj只敢月抛薅羊毛。

- 伯力：指服务商http://gcorelabs.com 新西伯利亚机房的VPS

老伯力配置：1c 512m 10G 1TB 500mbps，88rubles/m
新伯力配置：1c 512m 10G 500G 100mbps

- 胖子：由于MJJ错把RN老板当成了VirMach老板，所以曾经用"胖子"指代过VirMach老板。
- 瘦猴/麻杆：经资深MJJ深入挖掘出VirMach真实老板的FB/INS/LINKIN/TWITTER等社交媒体账号后发现，VirMach老板比较瘦，现在MJJ们通常用"瘦猴"或"麻杆"指代VirMach老板。

- bandwagon（搬瓦工）：一家供应商，提供优质CN2线路的鸡。在2014-2015年左右，其在售的年付3.99、4.99、5.99刀OpenVZ小鸡廉价鸡被炒火熟知，之后逐渐没落后沦为经典传家宝。

spartanhost（斯巴达）：因其高防VPS线路又便宜，在硬件上CPU和硬盘性能内存也不错，线路改版后走cera4837线路，10G口，速度上仅次于GIA，后因其4837线路的不稳定，海缆故障，线路体验不佳，被MJJ戏称为斯巴拉

wikihost （微基）：据mjj了解老板名就叫屌鸡，又是卖鸡的，所以简称鸡总。

V.ps（五折云）：因为经常搞五折年付（三年、五年等）被mjj戏称为五折云。

Greencloud (绿云)：这么多称号就因为名字带了个”绿“字，还被mjj戏称贾乃亮云，不得不佩服mjj冠名的能力！懂得都懂

- 四大金刚 （CC、RN、VIR、PR）
这是四家VPS供应商，主打美国VPS，算是灵车，争议比较多，但是便宜。

CC指Cloudcone，我自己也在用他家的VPS，似乎有一些超售现象，晚高峰那个MULTACOM机房有时波动，会掉线。
RN是racknerd，比较便宜，但是性能不怎么高。
VIR是virmach，很便宜，日本vps线路不错，据说是联通快乐鸡，但是老板经常删号坑人，什么信誉不佳之类的，封号不退款。灵车不要碰。
PR是PacificRack，删鸡删号不退款。辱骂客户，人人喊打。

- 缩写：az、pr、od、a1、a1p、pp、tg、gv、ion、cc、rn
az：Microsoft Azure；
pr：垃圾服务商pacificrack；
od：Microsoft Onedrive；
a1：Microsoft Office 365 A1 订阅；
a1p：Microsoft Office 365 A1P 订阅；
pp：支付方法 paypal；
tg：即时通讯软件 telegram；
gv: Google Voice，提供免费的美国手机号，可以免费给美国/加拿大号码发短信、打电话，可以接验证码。是网络电话，断网就无法使用（而且是必须能上Google的网）。匿名注册一些服务。比较难申请，我有幸在不严格的时候成功自选了喜欢的号码。
ion：服务商ion Cloud；
cc：cloudcone
rn：racknerd

- 套路云、良心云、凉心云
套路云：指因活动、优惠、计价等套路深的阿里云（对应良心云，太套路了）
良心云：指活动力度较大的腾讯云。（某一年腾讯云送了2000元无门槛代金券，之后也送点小额代金券，太良心了）
凉心云：指多次以很大活动力度吸引大批量MJJ们上车后，开始大规模封杀存在挖矿和跳板行为账号的腾讯云。

- v2、酸酸、酸酸乳、hy（歇斯底里）
v2：v2ray；
酸酸：ss，指shadowsocks；
酸酸乳：ssr，指shadowsocksR。
hy：hysteria（又歇斯底里）是一个功能丰富的，专为恶劣网络环境进行优化的网络工具（双边加速），比如卫星网络、拥挤的公共Wi-Fi、在中国连接国外服务器等。 基于修改版的QUIC 协议。

- 3欧（3O）、5欧（5O）
3O：指服务商http://online.net的3欧独立服务器传家宝

5O：OneProvider OP 5o独立服务器

- 总裁/烈马/剑皇/127
总裁/烈马： 人名，黑帽seo技术人才或团队，起因是一个名为 “总裁” “烈马” 利用墙外规则，要求灰黑常，电影网站缴纳保护费投放他家的菠菜和瑟情广告，不给就假墙了你的站点，让你的站点打不开降权。（就是利用高墙混饭吃的人）
剑皇：鉴黄谐音，指维护青少年的身心健康发展，自我组织的鉴定黄色作品。并进行大流量访问导致其服务器或者钱包不受负荷放弃迫害青少年的一种行动。据传一个黄播人士他的站作死用了阿里oss，流量费高达0.75r/gb，然后他的黄播付了钱不给看mjj愤怒几十台（也可能是几百台）g口鸡鸡刷了好久最后被迫删了文件，但是按照阿里云计费起码六位数以上（简而言之就是利用脚本刷流量）
127： 127.0.0.1 你的网站无法打开

- PT/盒子
pt：（PrivateTracker）下载其实也是BT下载的一种，和BT下载有两个最明显的不同，即私密的小范围下载和进行流量统计。PT下载是一种小范围的BT下载，通过禁用DHT，有要求地选择并控制用户数量。这样，在有限的范围内，下载的用户基本都可以达到自己带宽的上限。
盒子：这里盒子包括但不限于专业盒子运营商提供的盒子，IDC服务商提供的VPS、独立服务器，以及其他可用于pt下载、上传的网络服务设备。（mjj通常喜欢用hz、netcup、廉价的几O独服、G口流量大的大盘鸡）

- 北岸
备案的和谐版，因为那里有关键词过滤，有些词语应该是打不出来

- DMCA
《数字千年版权法》(DMCA) 是一项美国版权法，规定线上服务提供商，如果在网站内容方面接到版权所有者或其指定代理方涉嫌侵权的通知后，迅速删除不当内容，即可免除版权侵权责任。 U. S. A. 如版权所有者认为，其版权作品在未经同意下被侵权，则须向AMD提供以下信息。

- 补充：
1、你不用猜测，移动东南亚无敌的水平，拳打163，脚踢4837，如果是hk，甚至能和gia龙虎斗。
2、至于电信的话，其实电信跑东京iij很不错，速度快，延迟低
3、另外，天海人（沪国）家用9929跑vir的iij线路是软银过去，但是gc的iij不是，无论是大阪还是东京都不是。
4、现在（不考虑软银被打的情况）软银依旧是三网通吃，移动联通电信都可以跑，日本延迟也优秀
5、移动跑软银和iij的差距极小，甚至延迟和速度都相差不多，因为两条线路都是走的hk

- ## [常见落地VPS的推荐和碎碎念 - LINUX DO _202601](https://linux.do/t/topic/930977)
  - 注意：这里推荐的产品除了有特殊说明，网络都是没有面向 CN 优化的，直连速度稳定性都很一般，为纯粹的落地产品。
  - 其实落地就那几家，bagevm/DMIT/RFC，这三个用的最多，其他都没啥特点

- ## [虽然四级，但我真的不懂什么是线路鸡和落地鸡；于是我专门学习了下 _202507](https://www.nodeseek.com/post-380732-1)
- 在服务器网络架构中，“线路鸡”和“落地鸡”是两种功能定位完全不同的服务器类型，主要区别在于它们在网络链路中的角色、性能特点和部署目标。以下是两者的核心差异解析：
- 线路鸡（中转鸡）：
  - 位于用户和落地服务器之间，承担流量转发职责。它不直接处理最终请求，而是优化链路质量，将用户数据高效转发至落地服务器。相当于网络传输中的“中转站”。
  - 因需优质线路和带宽，成本较高（例如CN2 GIA线路服务器）。性能重点在转发效率和稳定性。
- 落地鸡：
  - 是代理链路的最终出口节点，直接访问目标服务（如流媒体、网站），并返回数据给用户。它提供实际的服务功能和IP地址（如解锁地区限制内容）。
  - 因不要求优质线路，价格较低（如廉价VPS）。性能重点在功能支持（如流媒体解锁、大带宽存储）。

- 测试脚本啊，另外多逛逛论坛就知道。这个没有绝对。

例如bage，cnfast，rfc这些，通常大家都说是落地，但是对于移动或者联通来说，也是直连快乐鸡。

yxvm vol这种，大家都拿来当线路鸡用，毛子ip不好。但是他家接入jinx，解锁也很好的。

- [什么叫落地鸡 _202602](https://www.nodeseek.com/post-603493-3)
- 就是最终ip 的机子 也就是帮你访问网站的机子

- 这个属于机场术语了，正经术语叫做出口节点（exit node），也就是多层代理中的最后一层，面对终点网站的节点。拿航空做比喻就是起飞用一架飞机，中途转机，落地用另一架飞机。
  - 用落地鸡的目的一般是：直连的节点IP质量不好，或者节点的地理位置看不了某些电视（锁区），于是再套一层节点。直连这个出口节点的话又太慢/连不上。

- ## [关于传家宝，有那些比较不错的传家宝嘛 _202606](https://www.nodeseek.com/post-754514-1)
- 缺钱啥都是传家宝，不缺钱啥都不是

- 直接在交易区找溢价高的()
大妈 瓦工 v.ps活动款 越炒越高
claw jp/sg 两/三网直
ovh 0.97和其他抽奖鸡
gomami/neburst 折扣款
evoxt my 半价翻倍和炒鸡多流量款
穷鬼云 转盘

暂时只能想起来这点, 还有一些小商家的不算了

- [看看大伙真正的传家宝（神机） _202507](https://www.nodeseek.com/post-385981-1)
1、斯巴达西雅图48刀/年、36刀/年
2、bage 7刀/年 香港

- 说实话绿云也没什么传家宝 最近那个74刀直接背刺一堆老用户

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

- ## 🔒 ¡[After spinning up way too many VPS servers, this is the checklist I now run every single time : r/selfhosted _202603](https://www.reddit.com/r/selfhosted/comments/1rob0cj/after_spinning_up_way_too_many_vps_servers_this/)
  - 类似参考 [新 VPS 上线前 10 分钟安全加固指南 ](https://www.ssdnodes.com/learn/lang/zh-hans/new-vps-first-10-minutes)
- After setting up dozens of servers over the years (for projects, game servers, infrastructure, etc.) I realized many beginners skip some really basic things in the first minutes.
- First thing I always do: Update the system.
  - apt update && apt upgrade -y
- Then I go through the basics:
• disable root login
• disable password authentication
• create a normal user with sudo
• enable a firewall (usually ufw)
• install fail2ban
• enable automatic security updates
• set up basic logging
One thing that surprised me when I first started running public servers:

SSH brute-force attempts often start within minutes of a fresh server going online.

Sometimes literally 2-3 minutes after deployment.

Since then I always assume a server is being scanned immediately after it gets an IP.

- I left things like ipset/conntrack out mostly because I wanted to keep the checklist beginner friendly. For the first hour on a fresh VPS I usually focus on SSH hardening + basic firewall. But once a server runs something public facing for longer, ipset / rate limiting definitely become useful additions.

- Why not create an ansible playbook that does this for you programmatically so you don't have to "check" each item off a list. You run once (or 100 times) and you always get the same results.
- Or Terraform script so that one can run it and have fresh VPS to standard set
  - Terraform will only provision the VM. Ideally, you'd be doing that and then a cloud-init config to make most of those changes, but an ansible playbook would be a drop in replacement for typing those commands manually.

- True. If you're provisioning servers regularly, Ansible or cloud-init is definitely the cleaner approach.
  - The checklist is more how I mentally structure the first steps on a fresh machine as a beginner guide for people doing that not such often. Once the setup becomes repeatable or you need to do it regulary it makes sense to turn it into automation.

- Cloud-init script? Should be supported on most mainstream VPS providers. Hetzner, Linone, Digital Ocean.
  - Yes, it is supported by Hetzner. Together with Terraform and a Terraform Cloud-init template passed to a Hetzner server resource, it is pretty straightforward to create a flexible server boilerplate. 
  - Cloud-Init is just a pain to debug. As Hetzner saves the Cloud-Init config as metadata, secrets need to be provisioned separately via, Terraform provisioners (or Ansible), but this is still very manageable.

- This looks like a promising cloud-init script: https://gist.github.com/NatElkins/20880368b797470f3bc6926e3563cb26

- This looks like an interesting bash script to check out: https://github.com/buildplan/du_setup

- If you aren't using an incommon SSH port + fail2ban + ufw on all your servers, you are playing with fire. This is the bare minimum you can do on any server.

- I’m very new to all this but is fail2ban and turning off password sshing mostly redundant? I do both but was curious how fail2ban works with key based sshing
  - Yeah, that’s basically it. Disabling password SSH removes the main attack surface, and fail2ban just adds another layer by blocking IPs that behave suspiciously. Even if they can't log in, it still helps reduce noise and scanning attempts. So it's less about redundancy and more about defense in depth.
- Fail2ban monitors login attempts, no matter what method, and blocks IPs if some threshold is passed. It would also protect against someone trying to brute force an SSH key (which is practically impossible but just making a point. Defense in depth is a good strategy. 

- Monitoring is really important too. Something like Beszel can be really useful. I've tossed around the idea of centralized logging but without an idea of a service to go through the logs, haven't bothered yet. 

- I do the same, but I also change the SSH port, set the timezone, and install some essentials like Docker, etc. Automate with Ansible.

- ## [保护你的小鸡! VPS 安全探讨分享 _202309](https://www.nodeseek.com/post-25170-1)
- 系统更新
- SSH 务必配置密钥登陆, 避免使用密码登陆, 更不用说弱密码!

- Nginx 泄露源站证书, 导致源站暴露是相当常见问题了. 自 1.19.4 起, Nginx 支持 ssl_reject_handshake 参数, 设置为 on, 当客户端传过来的 SNI 与已配置的 server name 都不匹配时, 会拒绝 SSL 握手, 进而避免证书泄露.

- 不要设置 DNS 直接指向源站, 使用泛域名证书
  - 不要设置 DNS 直接指向源站! 就算后面改为 CNAME 到 CDN 的域名, DNS 记录是可以查历史的!
  - 其次, 子域名爆破是查源站常用方法了, 有个非常好用的查子域名的方法是 crt.sh, 原理是查 SSL 证书颁发记录, 所以, 推荐使用泛域名证书.
  - 还有 RDNS, 不过一般没人会将自己服务器 IP 的 RDNS 配置为自己的域名, 许多商家也没提供这个功能, 此处按下不表.

- Zerotier 组建虚拟内网, tailscale 等其他虚拟内网方案我没用过.
  - 为什么要虚拟内网? 原因很简单, 搭建非公开的服务, 如个人的 emby 媒体库服务只给认识的人用, 还有自己管理的服务器间通过 socks5 等非加密代理协议访问对方, 使用虚拟内网服务器无需暴露相应端口, 大大降低安全风险. 好处多多可以说了. 使用虚拟内网后, 服务器只需要暴露 9993 端口(zerotier), SSH 都不用暴露在公网, 除非 zerotier 出了致命零日漏洞, 否则安全的很.

- Cloudflare ZeroTrust 里面的 Tunnel 功能做到服务器不暴露 HTTPS 端口建站, 安全性 UP 一大截

- 尽量不要使用服务器面板, 尤其是宝塔这种不开源的, 分分钟爆 0day, 更不用说弱密码等. 嫌麻烦确实要用可以看看开源的使用 Go 编写的 1Panel, 风险低一点. 但也要切记设置强密码, 同时更改面板端口, 最好搭配虚拟内网使用.

- 没有安全组的服务器，当你用默认docker部署一个项目时如果有端口映射，它将会突破你的防火墙，无视你的规则直接把端口暴露在外。

- ## [VPS基本安全措施 - 开发调优 - LINUX DO _202607](https://linux.do/t/topic/267502)
- 加一个在登录 ssh 时候自动发通知到企业微信机器人，以防偷家不知道。 可以通过 PAM 模块在每次 ssh 登录时触发脚本来实现。
- 限定 SSH 登录 IP

- 隐藏公网 IP
  - 隐藏公网 IP 并不是所有 VPS 使用者的共同安全需求，有一个胡诌的针对未来（指 ipv6 广泛使用）的方案就是只暴露源站 v6 地址给 CDN 用，这样 Censys 这样强扫的工具耗时会很长，不过也还是要配白名单。
- 防止 SSL 证书泄露 IP
  - 注册并且登录 ZeroSSL
  - 配置证书并且设置禁止 IP 80/433 的 HTTP 访问

- 只能确保攻击者无法通过直接访问 ip 获取默认证书来推断域名信息。然而又没有规定说攻击者只能用这种方式获取 IP 与域名的对应关系。可以看出，前文的规则依赖于 server_name 的匹配。攻击者完全可以携带正确的 server_name 握遍所有可能的非已知 CDN 的 IP 段，记录正确响应的目标。下面是判断（不包含遍历）的简单实现

- Cloudflare 不仅提供 CDN 服务，还有一系列其他产品，比如 Workers 和 WARP。而这些服务有一些需要注意的特点： 能对外发出请求; 用的是 Cloudflare 的 IP 段
  - 虽然 Cloudflare 对于滥用肯定是限制的，但是为了以防万一，我们还可以再做点安全措施 —— 经过身份验证的源服务器拉取。
  - 必须确保 SSL/TLS 加密模式为完全或者完全（严格）

- 没必要用 ufw 来管理 docker 的端口开放，docker 会自己写入 iptables 规则用以管控端口

- 
- 

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
# discuss-vps-usecase 🌰
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [vps可以用来干什么 - LINUX DO _202607](https://linux.do/t/topic/2645317)
- 探针，节点
还有一些其他玩法？
sub2api/cpa/new api
matrix 私服
searxng，搜索，可以给 openclaw 当搜索用
openclaw/herness
订阅节点聚合（站内佬友的 sublink pro，非常好用）

- 游戏联机，游戏私服，爬虫，代理，注册机

- 你可以理解为端口映射，不过内网穿透这个说法确实是安全圈说的比较多，但是内网穿透一般是用类似 frp 这种软件搭建好隧道，并且流量可以根据需求的不同用不同的协议正常转发。

而端口映射只是把内网的端口通过路由或者光猫等网络设备映射成公网可以直接访问的状态

- ## [佬们在自己的网站/服务器上部署了什么有趣的服务（除了博客） - LINUX DO _202606](https://linux.do/t/topic/2451712)
  - https://awesome-selfhosted.net/

- frp 把nas的服务搞出来公网访问

- 我部署了一个可以查询任意 Chrome extension 信息的接口，传入插件 Id 就可以直接查询

- openlist、hermes，好像没了
# discuss-vps-落地
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [问大家一个问题：你们找落地机都要满足什么条件？ _202608](https://www.nodeseek.com/post-887896-1)
  - 是只需要他的IP好，比如是ISP住宅就行，还是有其他的附加条件
- 最起码，就是解锁好（广播ip，自带DNS解锁）< ip干净原生 < 双isp住宅ip <全都要。

- 最终还是选择动态家宽独享鸡

- 最好大厂，固定IP，国际互联不要太差

- 没有滥用标记就差不多了，伪家宽和机房区别不大情况，我个人更看重国际互联

- 真正的家宽很贵，一般只找一些nq看起来还可以的就行了
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
# discuss-paid-vps
- ## 

- ## 

- ## 

- ## 

- ## [海外服务器购买，有哪些推荐，以及哪些坑需要注意？ - V2EX _202606](https://v2ex.com/t/1196279)
- 稳定且性价比高选 Netcup 、便宜大碗选 racknerd

- 如果你要稳定性、又要性价比，因为 KYC 莫名其妙被封号的，排除 Hetzner （ KYC 严格、涨价、贵）、OVH （ KYC 严格，不欢迎中国人、涨价、贵）。
  - 可以看看 Netcup

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

- ## [🍀平替Racknerd美西！【5月10日售罄】CCS洛杉矶补货了，可能是目前美西最便宜的机器了，CCS低价机，不是优化线路，备用机优选美西 - 测评 - IDC Flare _202604](https://idcflare.com/t/topic/77833)
- 中国大陆到美国的优化线路或者无优化线路，几乎都是走洛杉矶，物理延迟低，买其他地方的也要经过洛杉矶，例如去美东的纽约，水牛城，美中的亚特兰大，芝加哥，都要经过洛杉矶。 目前确实是最便宜的，量也是最大，服务也稳定。其他品牌的不清楚，但ccs是十几年的牌子，跑路概率不大。

- 狐蒂云难民来了, 便宜一时爽，跑路火葬场
  - 我推aff也是看商家下菜，看起来不靠谱的都不敢推
  - 现在ccs算是最便宜的靠谱机器了，无优化，无优化，无优化，会玩的佬友都玩的很溜

- 开了台纽约的4c8g玩。不过这个开机真的好久啊。
  - 他们老外下班了就不上班的，一般下午或者晚上买开机会快一点
- 我半夜买的买完就开机了，纽约的2+2。虽然说听松弛，但是我之前中午找他们换IP啥的回复也挺快的

- ## dartnode [RN闪购建站鸡平替 2C4G100G 仅需13.99/y - IDC Flare _202606](https://idcflare.com/t/topic/99797)
  - 两家最大区别
  - RN 服务售后好
  - DN IP原生 解锁好，售后服务响应慢 支持PP支付
  - 我特意标注了pp，遇事不决上pp，敢上pp还是有点实力的

- 会有跑路风险吗
  - 我用了两年，就是售后慢，其他与这个价格匹配，跑路应该不至于，let上他们认过

- ## [HostDzire他没有push通道吗 _202609](https://www.nodeseek.com/post-913404-1)
- 不能push
- 还不能修改邮箱

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
# discuss-vps-vpn
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [【自建线路】cloudflare自选优选ip，sing-box搭建快速低延迟的vpn教程 - LINUX DO _202607](https://linux.do/t/topic/2639989)

# discuss-vendors
- resources

- cons
  - 

- ## 

- ## 

- ## 

- ## 

- ## [有没有硬盘IO比较好的鸡鸡啊？ _202608](https://www.nodeseek.com/post-864645-1)
- 可以 zRAM + zswap，这样可以往死里开并且还对 IO 不太敏感

- ## [有没有硬盘好的便宜鸡（首选亚太？） _202604](https://www.nodeseek.com/post-689923-1)
  - 鸡多了之后发现挂komari服务端的鸡io阻塞严重，websocket频繁断连，刷新一下也要等好久。准备换掉现在挂服务的阿里云鸡了

- 腾讯阿里的硬盘io都烂完了 腾讯和阿里的99年付鸡 甚至不如超开的狐蒂云
  - 大厂的存储是这样，分布式存储为了弹性狠狠牺牲性能？

- ## [为何大型云服务商的磁盘性能都很差？(aws/oracle等) _202404](https://www.nodeseek.com/post-92634-1)
- 测试了oracle和aws的服务器，磁盘性能都极差，就算把block storage的性能调整到最高，4K测试，连续读写的性能都很差。和那些小型的主机商性能都不是一个量级别，有谁知道原因吗？

我在aws开了100G的io2存储（性能最高的）IOPS调整了到50000（性能容量比最大是1:500），
fio disk speed测试下来4K性能大概也只有52MB/s(13.1K)，64K 122MB/s(1.9k)的性能水平，
oracle把block storge的性能调整到UHP(最高性能)，4K也是50-60MB/s的水平。

- 因为后端架构完全不一样。
大厂都是高可用虚拟机。后端有个高可用存储集群，通过网络挂载空间给虚拟机。这样子就算母鸡挂了，因为数据在后端集群上所以可以立马在其他地方起个虚拟机并且不丢失数据。做的好的话甚至可以母鸡挂了小鸡也不会掉线, 会被自动热转移到其他可用的母鸡上。
优点就是高可用很难丢数据。缺点就是非常昂贵，难以配置且有性能限制。硬件成本和管理人力成本都很高。

至于小主机商，硬盘直接用母鸡硬盘。自然速度非常快。但是母鸡挂了就指望商家比较良心有做备份或者冗余。无论如何小鸡都会挂一阵子。

- 我在aws开了100G的io2存储（性能最高的）IOPS调整了到50000（性能容量比最大是1:500），
fio disk speed测试下来4K性能大概也只有52MB/s(13.1K)，64K 122MB/s(1.9k)的性能水平，
oracle把block storge的性能调整到UHP(最高性能)，4K也是50-60MB/s的水平。

- 加钱。阿里可以上本地盘。要多快有多快

- OCI, AWS的磁盘性能是和硬盘大小相关的，OCI你把磁盘拉到1T性能比肩sata

- 很简单啊，你用大厂的本地盘服务器就知道了。
云盘用的硬件带宽，非网络带宽，nas才是网络带宽

- 大厂基本都是云盘，云盘小文件io比不过本地ssd的，想要性能好买baremetal啊

- azure的bare metal有1.2亿的IOPS

- ## [我觉得cloudnium 0.54/month 现今比 dedirock 6.45刀/year更有性价比。。。 _202607](https://www.nodeseek.com/post-844717-1)
- cloudnium配置2c2g 20gb 6.48$/year
dedirock配置1c2.5g 15gb 6.45$/year

我这里电信两者测速白天也能跑到400m左右，晚高峰在200m左右
价格差不多但是性能方面却有差，且现在dedirock push或者改邮需要5刀，cloudnium随便改邮

- 流量吧，dedirock有4t，另一个只有一半
- 我用超了也没有关机的

- 如果确定cpu是8168不会换就好了，重启有概率换cpu还是不太敢买
  - 客服有解释过，而且你被换了发工单他也会给你换回来且有补偿

- 别忘了，dedirock的tos是有对资源使用限制的，我记得是25%以上cpu使用率不得超过90秒。现在是不管，说不定什么时候就要用这个条款来杀鸡了

- dedirock服务态度很好

- [现在终于开始意识到了牛马云cloudnium的价值了吗。价格上涨就是最好的证明 _202608](https://www.nodeseek.com/post-853097-1)
  - cloudnium重启换u需要与客服battle才能换

- ## [Virmach到底怎么了？？？ _202607](https://www.nodeseek.com/post-840654-1)
- 之前的四大金刚之一。和Rn齐名，之前还在CCS机房的时候，服务非常的好，稳定性也不错。主要是有CCS机房的技术服务帮他擦屁股。
之后和CCS机房闹崩之后，瘦猴就整了一堆AMD3900、5900的机器。但是瘦猴贪图便宜，用了一堆消费级硬件，再加上超售，就导致母机不断宕机。M疯狂地投诉，Paypal争议。现在这家就是灵车驾驶状态，母机修不修全看运气。瘦猴的公司只有两个人

- 事情太久了，不记得是邮件还是LET上的帖子，猎杀mjj持续了半年多，创造了信誉不佳的经典梗，当时只要老板不开心，觉得你是中国用户，会直接说你信誉不加封号删机，所以才导致中国人几乎不玩vir了
- 主动切割mjj了，发过邮件的，大意是如果你是中国用户立即停止续费，否则会无条件删除

- 我提了一个工单 说我的实例从创建开始到现在都是pending 没任何回复 没任何人处理 直到现在十天了还在pending 没任何人回复

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

- ### [dartnode过排队思路 _202606](https://www.nodeseek.com/post-781010-1)
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

- ## [DediRock的稳定性怎么样？ _202601](https://www.nodeseek.com/post-599346-1)
- 灵车要啥稳定性， 一个月大半夜重启两次，每次半小时

- 非常差，我大盘都停了3次了 都是数据清零

- 我是美东水牛城的机房，感觉还可以啊。缺点是延迟高，客服一般吧。优点是稳定而且几乎0丢包。晚高峰体验比rn dc2好。

- ## [问一下ccs dedirock cloudnium _202608](https://www.nodeseek.com/post-885585-1)
- 机房一样线路一样 机器配置定价不同

- ## [盘一下cloudnium，mjj参考一下 _202607](https://www.nodeseek.com/post-804064-1)
  - cloudnium曾经是nextarray合伙人，nextarray有达拉斯自有机房，但是老板生了个病死掉了，合伙人接收就叫cloudnium了。早期nextarray机器迁移到了breezehost（就是杜甫盲盒那一家）
  - cloudnium开始就是做杜甫和托管生意的，从San Angelo的frontier机房起家，后来逐步拓展业务的
  - 后来frontier机房不作为，杜甫全迁移到了达拉斯，我就溢价把传家宝卖了。
  - 他家效率非常低，机器是不知道从哪儿淘来的硬件，迁移杜甫换了两台都没法装系统，都是硬件有毛病
  - 今天的活动款其实把老用户背刺得连裤衩子都不剩了，之前一直有1刀的配置，现在0.54刀
  - 目前cloudnium 达拉斯在tier.net机房，和曾经的nextarray没有关联，应该不属于左手倒右手

- 刚刚好这个价格就差不多是IP成本

- [cloudnium咋样？ _202312](https://www.nodeseek.com/post-50924-1)
- 成立時間太短，不建議放重要的數據。

- 无限流量真的挺好的 

- 偶尔给你失联两三天，目前是吃灰
- 平均每月断网一天。
# discuss-vendor-racknerd
- resources
  - [RackNerd | VPS Specials](https://www.racknerd.com/specials/)

- cons
  - 似乎不支持 backup: [How to Backup Your VPS: A Simple Guide to Getting Started — RackNerd _202409](https://blog.racknerd.com/how-to-backup-your-vps-a-simple-guide-to-getting-started/)

- ## 

- ## 

- ## 

- ## [RN 圣何塞和洛杉矶DC03哪个更好 _202510](https://www.nodeseek.com/post-488380-1)
- 自己拿测试ip去ping一下啊，不同地方，不同运营商的结果都是不一样的，要选适合自己的，而不是人家说什么就是什么

- 圣何塞电信用着很舒服 直接hy2速度也挺快 联通直接ping不通 移动没测过

- 对线路来说稳定性无非就是延迟，抖动，或者你问的就是机器，会不会宕机失联

- ## [对比测一下 RackNerd DC02 / DC03 / SJC - LINUX DO _202511](https://linux.do/t/topic/1150760)
  - 单纯作上网用途，其实没有必要盲目跟风购买，因为这三台机器都没有优化，晚高峰的表现可能令人失望。三网中联通直连效果最好，属于是矮子里拔高个儿。DC02 综合下来是三者中直连效果最好的。

- 如果买 DC02，可以选 cloudcone，同机房，而且活动款叠加储值优惠更加划算

- ## [在RackNerd买的小鸡，上传速度只有这么点？ - LINUX DO _202512](https://linux.do/t/topic/1275819)
  - 之前在 RackNerd 买了只小鸡，用起来感觉速度非常慢，浏览网页都很吃力，刚才测速发现它的上传速度只有 4Mbps？一定是哪里出了问题。
  - 位置在纽约

- 那这速度非常正常了，隔着一个太平洋 + 整个美国。美国鸡的话建议买洛杉矶的，对中国友好一点。

- 廉价鸡是这样的，质量纯是抽奖

- RN 虽然便宜，但是晚高峰卡
- RN 的机子除了价格，其他的优势一点都没啊，晚上高峰 ssh 连半天，连上一会儿也掉了

- 不差钱就 搬瓦工 CN2GIA 免费有谷歌云 甲骨文

- ## [racknerd买的服务器很卡 - LINUX DO _202608](https://linux.do/t/topic/2705444)
- rn 线路很差，我测下来我的延迟还行，丢包很多，一般都是套个 cf 建站用
  - 需要用跳板机，最好是线路优化的机器，连梯子代理也行

- 需要套 cf 的代理，然后走优化域名，且是联通宽带, 为了这个折腾很久，还换了联通号卡 情况好的时候能稳定 200ms 延迟 + 20MB/s ， 不套这些真的完全没法用 上个 google 都难丢包严重

- ssh，finalshell 加代理或者隧道就能解决，至于建站对外访问，或者搭建节点
建站直接套 cf
节点直接用 hy2 也能跑到 7 万（油管）
只能说没明确需求和不会玩而已

- RACKNERD 的主机 ssh 不会太好的，直连多少有延迟，RACKNERD 一般都是搞自建线路的，胜在便宜，在套上 cf 的优选 ip，不会输机场的，自用基本上都满足，可以看看 RACKNERD 配置 cf 自选优选 ip 搭建线路

- ## [RACKNERD 现在一般都溢价多少？ _202608](https://www.nodeseek.com/post-885356-1)
- 个别黑五活动款会有些溢价，比如去年黑五第三波的性能款，其他普通款基本没有甚至折价

- rn 的机子很脏，ip 被滥用的

- ## [【RackNerd】RN 2026年黑五历史所有特价机整理（常规套餐+性能建站AMD系列）【均可代申请流量翻倍】 _202604](https://www.nodeseek.com/post-673445-1)
2025年RN全部黑五套餐
1 GB 内存
1 CPU 核心
25 GB SSD 存储
2000 GB 月流量
$10.60 /年 (续费同价)
可选机房: 多机房
购买链接: https://my.racknerd.com/aff.php?aff=12854&pid=923&language=chinese

2.5 GB 内存 (热门款)
2 CPU 核心
45 GB SSD 存储
3000 GB 月流量
$18.66 /年 (续费同价)
可选机房: 多机房
购买链接: https://my.racknerd.com/aff.php?aff=12854&pid=924&language=chinese

4 GB 内存
3 CPU 核心
65 GB SSD 存储
6500 GB 月流量
$29.98 /年 (续费同价)
可选机房: 多机房
购买链接: https://my.racknerd.com/aff.php?aff=12854&pid=925&language=chinese

6 GB 内存
5 CPU 核心
100 GB SSD 存储
10, 000 GB 月流量
$44.98 /年 (续费同价)
可选机房: 多机房
购买链接: https://my.racknerd.com/aff.php?aff=12854&pid=926&language=chinese

8 GB 内存
6 CPU 核心
150 GB SSD 存储
20, 000 GB 月流量
$62.49 /年 (续费同价)
可选机房: 多机房
购买链接: https://my.racknerd.com/aff.php?aff=12854&pid=927&language=chinese

需要申请流量翻倍的，回复订单号/PM我订单号都可以(代申请)，一般1-2天即可完成翻倍。

- ## [从 RackNerd 换到搬瓦工再换回来 _202604](https://www.nodeseek.com/post-685159-1)
  - 两年前第一次买 VPS，在 nodeseek 看了一圈，入手了 RackNerd 洛杉矶的年付机器，$11.29，想着便宜先试试。后来又换过搬瓦工 CN2 GIA，最终又回到 RackNerd。过程踩了不少坑，记录一下。
- 第一阶段：RackNerd 年付 $11
  - 实际体验：白天 SSH 连上去操作完全没问题，延迟大概 180ms 左右，勉强能接受。博客访问也还行。 
  - 问题出在晚高峰，丢包率会明显上升，偶尔 SSH 卡几秒，网页加载变慢。普通 BGP 线路，高峰期就是这样，没什么好抱怨的，毕竟一年才 $11。
  - 稳定性倒是出乎意料得好，挂了快一年没遇到无故宕机，有一次机房维护提前发了邮件告知。
- 第二阶段：换搬瓦工 CN2 GIA，为了速度
  - 后来项目需要访问国内的一些 API，晚高峰的丢包让我受不了，咬牙换了搬瓦工 DC6 CN2 GIA-E，季付约 $50。
  - 效果是真的好。延迟稳定在 140ms 左右，晚高峰丢包几乎没有，下载速度能跑满本地带宽。DC6 机房对电信、联通、移动现在分别走 CN2 GIA、CUP、CMIN2，三网都有优化。
  - 但用了半年，我意识到自己的实际场景根本用不着这个线路质量——项目访问量很低，偶尔慢一下没什么影响，每季度 $50 花得不值。
- 第三阶段：现在的方案，两台机器分工
  - RackNerd 年付 $11：跑不重要的服务，脚本、博客、测试环境，挂着就行
  - 搬瓦工只在需要时用：需要稳定访问国内资源时再开
  - 说直白点：RackNerd 的线路够不够用，取决于你的实际用途。跑脚本、个人博客、境外业务，完全够；如果是面向国内用户的服务，或者对延迟敏感，搬瓦工 CN2 GIA 才值得价差。

- 落地鸡 + 线路鸡 + 活动鸡 等于性能线路性价比🐔

- ## [Racknerd洛杉矶dc-02的VPS要换机房了 - LINUX DO _202605](https://linux.do/t/topic/2202607)
- 曾经优质的 74 段 IP 以后再也没有了
  - cloudcone 还是 74 段的，不清楚会不会也这样搞
- 不要啊。我的 74 网段，直连没了。dc02 直连可以 150ms, 不知道 dc03 可以不。。。

- DC03 线路比 DC02 的延迟高多了，晚高峰速度也拉胯得多 

- 有人发了工单问了，不能退款，但是可以发工单选其他机房，比如圣何塞什么的

- DC02 完全可以直连，DC03 似乎一部分 IP 都被 google 打到香港去了，之前买了个 DC03，连不上 gemini，直接废弃了

- 经过对比测试，发现：

CPU 从 E5-2690 变成了 2697，但是单核 / 多核性能略有下降，没了嵌套虚拟化；
内存读写性能下降；
磁盘 4K 读写略有提升，顺序读写性能下降；
NAT 从 Full Cone 改成了 Port Restricted；
Gemini、Reddit 被拉黑；
电信延迟加重・・・

- ## [RackNerd 的 DC03 和 DC02 机房，到底有啥区别？老用户帮你扒明白 _202605](https://www.nodeseek.com/post-737628-1)
  - 这俩压根不是一家公司的机房。
  - DC03 的真身：ColoCrossing（CCS）
  - RackNerd 的 DC03，底层是 ColoCrossing（业内简称 CCS）洛杉矶机房。CCS 是北美知名的 IDC 批发商，旗下有大量"下游品牌"在卖它的资源，RackNerd 就是其中之一。所以你买的 DC03 机器，网络、硬件、上游线路全都来自 CCS，RackNerd 更像是一个"贴牌零售商"。
  - RackNerd 的 DC02，底层则是 Multacom 洛杉矶机房，和 DC03 完全是两套独立的网络与基础设施。同样用 Multacom 这个机房的，还有大家熟悉的 CloudCone。
  - DC03（CCS）的网络架构偏向北美本地与欧美互联，到国内的整体延迟普遍高于 DC02（Multacom）。
  - DC03（CCS） 与中国移动的互联较弱，移动用户经常出现绕路、丢包、晚高峰拥堵等问题。
  - DC02（Multacom） 对比DC03移动线路方向的对接相对友好，稳定性更好。

- 网络感觉差不多，但是DC02的IP确实干净一些。

- 建站套CF的话影响不大 科学用可以考虑不续了 DC02在白天 电信和联通和移动起码还是能用的

- [racknerd快讯，dc02 所有机器将物理迁移到 dc03 _202605](https://www.nodeseek.com/post-736588-1)
- dc2机房是属于mc的，mc被ec收购了，ec也收购了cc，现在cc和dc2都是一家，rn估计没续约找借口
# discuss-vendor-dartnode
- cons
  - backup restore 慢到不能忍

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [My Disappointing Experience with DartNode VPS: A Cautionary Tale — LowEndTalk _202510](https://lowendtalk.com/discussion/210302/my-disappointing-experience-with-dartnode-vps-a-cautionary-tale)
  - When I attempted to restore from backup, I discovered that none of my backups were functioning properly. Despite having three different backup points available, not a single one would boot successfully after restoration. The restore process would complete, but whatever was being restored simply wouldn't start.
  - The restoration process was painfully slow, and ultimately unsuccessful.
  - The fact that multiple backups failed to restore properly raises serious questions about their backup system's reliability. What good are backups if they don't work when you need them?

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
# discuss-attack
- ## 

- ## 

- ## 

- ## 

- ## [挑战：能不能黑进我的服务器 - LINUX DO _202607](https://linux.do/t/topic/2661600/6)
  - 有一个闲置的服务器，假设你们只知道我域名有没有什么办法能黑进我的服务器
- 你得先发誓这个是你的站，不是找个仇家的站就发过来
- 你怎么证明这个机器是你的

- free 根本不耐打，多 ip 打你跟没有一样， 除非设置严格的速率限制 WAF
# discuss-tips
- ## 

- ## 

- ## 

- ## 

- ## [各位收鸡，敢收Gmail原邮吗？ _202609](https://www.nodeseek.com/post-911582-1)
- 不敢，我之前出别人gmail原邮的rn，刚登上就风控
- 不敢 自己注册的gmail还好说 有可能申诉回来 买的那很难说了

- 不敢，现在风控太狠了，而且能卖的一般都是临时注册的或者买的养号可能没那么好，不像自己注册使用很多年的不怕被封

- 我谷歌飞了还没申诉回来，前几天刚注册的甲骨文啊啊啊，很难受。

- 买的我也申诉回来好几回了，感觉只要申诉就解封诶，我之前陆陆续续注册了八个Gemini邮箱
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [我发现其实硬盘才是对网站性能影响最大的 _202510](https://www.nodeseek.com/post-468057-1)
- 以前一直以为是CPU, 但是根据我发现, 
CPU型号一样, 一款2C8G的硬盘是NVME SSD, 
另一款8C8G 普通SSD, 
2核 NVME的居然比8核普通SSD的快80%以上

- 这不应该是典型的木桶效应的问题吗？你如果CPU两者差很多，那你换再好的硬盘，两者之间谁更快也犹未可知。只不过你当前的场景中，制约A和B两款服务器性能差异的恰好是硬盘。
而且你还有一个很明显的误区，认为8核就一定强于2核，多核只在并行任务时有优势，在单线程任务上就要看两个CPU的单核能力了，所以还是要看具体场景，并非核心多就一定在所有场景下都比少核心强。

- cpu只有在高并发时候才会体现优势

- 确实io很重要，古董机换上固态起飞就是例子

- 实际上感觉差不多，现在都有缓存，和界面压缩，我论坛采集了六万多个帖子，用cc的hdd建站的，打开也就花了两秒不到

- 我建站直接上memdisk了，毕竟内存够用，就让缓存去处理这些吧！内存读写总比硬盘快得多！

- 一般来说，不用太高吧。我网站放4k随机读写12mb和160mb。强制刷新缓存，我发现首页的图片加载速度都不差，秒出。除非是只有1. 几的垃圾盘吧

- 数据库读写还是吃cpu和硬盘读写的

- ## [大妈dmit都是优质机房ip吗，还是要随机 - IDC Flare _202608](https://idcflare.com/t/topic/122141)
- 只保证线路不保证 ip 的

- 是一个 ipv4 但是你们在一个网段里啊

- 机房 IP 都是会随着使用的人数增加纯净度越来越低的，是否优质取决于你的需求（例如更快过盾，AI，银行等）。一般认为贵一点的或者冷门地区的 ip（不管什么属性）可以规避买的人太多从而保持 ip 纯净度。

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
