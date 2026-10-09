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
    - 临时的需求可以用LDC在 ldstore 买一些proxy/vps
  - 公开与分享的需求不强时，没必要上顶级vps
  - 可以先月付便宜的vps，等到活动或论坛有人抛售时再获取长期vps
    - vpn也可以先找短期活动的, 再等一个长期适合的
  - dedirock性价比高，但口碑不好
  - 是否能多次免费更换ip
  - 支持7天无理由退款的很方便
  - 一号一鸡容易转手

- mjj-options
  - 偏线路? 偏性能?
  - ip能访问、 未送中, 打开google访问的不是 google.com.hk

- vps-vpn/落地
  - 可考虑 普通线路 + 优质落地 的组合， 就是要折腾下
  - 可考虑 拼车线路 + 自建落地

- [【汇总】剩余价值计算器，总有一款适合你 _202410](https://www.nodeseek.com/post-171213-1)
  - [VPS.ss - VPS 剩余价值计算器 - 服务器转让剩余价值/溢价在线计算 ](https://vps.ss/)
  - [xiangmingya - VPS剩余价值计算器 ](https://xiangmingya.github.io/vps_valuation/)
  - [VPS 剩余价值计算器2.0  ](https://jsq.211119.xyz/)
  - [DigVPS - 专注服务器测评，总有一款服务器适合您 ](https://digvps.com/calculator)

- comparison
  - [VPS值得买！ 产品库存状态 ](https://stock.vpszdm.com/)
    - [BWH 产品库存状态 ](https://stock.bwh91.com/)
    - [DMIT 产品库存状态 ](https://stock.dmitea.com/)
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

- ## 

- ## 

- ## 💡 [【教程】成功把送中的ip拉回日本，只用了一周时间 _202511](https://www.nodeseek.com/post-503481-1)
  - 前段时间绿云多个ip段被集体送中，我是其中之一，虽然是集体送中，但也拉回来了，下面是方法。
  - 第一，先去向谷歌报告IP问题
  - 第二，用插件改定位， 安装Location Guard https://github.com/mrfanii/Location-Guard-V3
  - 打开Location Guard插件，选择Fixed Location，在地图上点击你IP想要拉回去的位置，比如我的原本是日本，就找到日本东京，点击一下地图上的位置。
  - 来到Options选项，Default level默认设置改为Use fixed location
  - 打开Google地图 https://www.google.com/maps 点击右下角获取定位，此时就会定位到你刚才在插件里所点击的位置，说明成功了
  - Google随便搜索一下，滑到底部，点击 update location 来更新位置。
  - 之后每天用一下Google搜索和YouTube就行了，我是用了一周就成功了，集体送中的话，最好是人多力量大，发个贴让你那个ip段的人一起参与进来。

- https://github.com/anthonysgro/geospoof 
  - https://geospoof.com/
  - Browser extension and iOS app that spoofs your gps, geolocation & timezone, and auto-syncs to your VPN. Firefox, Chrome, Edge, Brave & Safari.

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
# discuss-vps-中转+落地
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 🆚 [【流量转发该选哪个？】𝕏𝕣𝕒𝕪任意门，realm，gost，socat，iptable/nftable 的技术性区别 _202512](https://www.nodeseek.com/post-545073-1)
- 底层架构与工作原理分级
在理解区别之前，必须先将它们分为两个流派：内核态 NAT 与 用户态代理。

- 没看懂拥塞控制对比的意义何在。
BBR 或者其他拥塞控制算法本来就是端到端的情况，理论情况下一边支持就可以，中间设备透明转发就行了……
现在中间设备还得处理 TCP 层的东西……？

- 一直用gost转发，无高并发的情况下，不会有很大的占用，当然，gost内存泄漏是老问题了

- 确实，realm没有面板。iptables更没有了。gost有哆啦A梦，xray有x-ui的dokodemo door.

- ## [高手进阶：详解“IX上云 + 大厂前置”上网方案 - Type My Life _202610](https://www.typemylife.com/advanced-ix-vps-setup-for-stable-connectivity/)
- IX（Internet Exchange）或 IXP（Internet Exchange Point），中文全称是“互联网交换中心”。
  - 你可以把它想象成一个巨大的“网络握手广场”。各大网络运营商（如电信、联通）和互联网巨头（如阿里、腾讯）都在这个广场上有一个摊位。当它们需要互相传递数据时，可以直接在广场上“当面交易”，而不需要派人绕远路去对方公司。
- 为什么现在IX火了？ 这得益于两个趋势：
  - 大厂入局：如今，我们日常使用的绝大部分服务都托管在云上。而阿里云、腾讯云、华为云这些国内巨头，以及它们在海外的节点，都纷纷加入了全球各地的IXP。
  - 新型IXP出现：以深圳“前海IX”为代表的新型互联网交换中心在国内建立，几乎所有国内主流云厂商和运营商都是其成员。
  - 这就创造了一个机会：如果我们能接入某个IXP，理论上就能与同在该IXP的各大云厂商建立一条“高速内路”（类似一个大的内网，甚至可以规避掉近来愈演愈烈的跨省/跨网QoS问题）。
- 为什么要这么折腾IX上云，而不选“优化线路”的VPS直连出海？
  - 估计很多人也有这个困惑：IX和“优化线路”VPS（所谓“线路机/鸡”）有啥区别？
  - 其实没有说谁更好的问题，看你的取舍。
  - 比如说优化机的明显问题就是贵（尤其是号称三网优化的那种机器），万一被和谐IP，换IP成本也不低。举个栗子，以MJJ们都很推崇的高端商家DMIT为例（普遍评价是除了贵没有其它缺点），他们家提供国内访问优化线路，比如日本方向的，有一款TYO. AS3. Pro. TINY，线路优化为三网CN2 GIA，月付21.9美金，500GB流量。这价格，一般人真承受不起啊。。。但是IX组合妥当的话，成本并不高，稳定性算可以，就是相对折腾。

- 实战操作：如何搭建你的专属通路
搭建这套系统需要三台机器：前置VPS、IX机器、落地机。核心逻辑是端口转发。
准备工作
购买IX专线服务：这是成本较高的部分。由于价格不菲，很多人选择“拼车”合租。好消息是，最近也有不少服务商提供了相对低价的IX产品，月付几十元或者年付两三百元甚至两百元以内的那种，降低了门槛，比如TapHip家的CNIX系列产品。或者是YT. NET云途的产品。
购买前置VPS：关键一步！ 务必向IX服务商或者“车主”确认，哪些云厂商的哪个地区的VPS可以作为前置。
例如，阿里云深圳可用，但广州节点可能就不行。买错前置，全盘作废。
购买落地机VPS：所谓落地机，就是你用来访问Google或者解锁流媒体的那台机器。请在这台落地机上提前安装好魔法程序。
注：有少数IX服务，提供双端专用IP（入口+出口都是独立IP），那理论上你直接在这种IX机器上安装魔法程序，用他们家的出口IX直接冲浪也未尝不可。但大部分IX都是NAT机器，共享对外的出口IP，所以一般还是建议用户自备落地机。

- 
- 

- ## [NodePass 搭建教程给有需要的小伙伴参考（GPT优化） _202511](https://www.nodeseek.com/post-506209-2)
过去一直使用 realm 做 TCP/UDP 转发，但现实痛点包括：

所有节点都需要手工 SSH 登录修改配置，运维复杂
缺乏端口/实例级别的流量与连接监控，仅能看到机器级别监控
转发链路拓扑难以可视化
因此开始寻找可观测性更强、运维自动化程度更高的转发方案。

市面上开源的两个主流转发面板是：

✔ NodePass
https://github.com/yosebyte/nodepass

优点：
转发组件由纯 Go 实现，依赖极少，部署轻量
前后端分离，易于自定义面板 / 自托管
支持 Docker / 二进制混合部署
架构灵活，server-client 模型可实现中转链路/内网穿透
更新维护稳定、社区活跃

缺点：
目前不支持多用户

✔ 哆啦A梦转发面板
https://github.com/bqlpfy/flux-panel

优点：
原生支持多用户

缺点：
作者曾删库，维护稳定性存在疑问
依赖 go-gost / go-gost/x（链路复杂度高）
后台为 Java + MySQL，部署较重
综合对比后，最终选择 NodePass。

由于我的节点都可以互相访问，不需要 server-client 链式代理，全部使用 client 模式即可完成中转。
如果需要：
负载均衡
多节点 relay（A → B → C）
内网穿透
则需要合理组合 server-client，但不是本教程范围。

NodePass 结构清晰、轻量、易于扩展。
通过 Master + Dash，可以把所有节点的转发配置集中化管理，解决：
手写转发配置
手工 SSH 部署
端口/流量不可观测
节点分散运维

- 也可试试我的河马面板，是支持链式转发的。安装也很方便。我现在使用的是百度-HK IX -HK -SG 。因为我要看netflix。所以多拉一点

- ## [请教大家用前置vps 拉落地机的问题 _202610](https://www.nodeseek.com/post-965592-1)
- 链式本来就会增加一层握手延迟
直接端口转发吧

- ## [链式代理和中转 有什么区别 _202601](https://www.nodeseek.com/post-589350-1)
- 链式代理需要中转机和落地机均搭建梯，适合✈️场这种没有中转机权限的情况，优势就是可以利用✈️的专线规避GFW，但是本质上其实就是用✈️场套了个自己的落地。如果中转是自己的机器转发就行。

- 链式多一层解析的延迟吧，中转基本都是本地的服务器，延迟低

- 先讲性能，使用过iptable防火墙类和xray singbox之类的自由门做中转，理论上防火墙更稳定和效率更高，链式代理需要多次加解密有性能上损耗效率相对较低，但是实测上差距不明显。
再讲灵活性，中转就像一条隧道，只能点到点，缺乏灵活性；链式代理可以实现分流，举个例子：HK的小鸡，不能使用AI，那就可以分流到其他地方使用AI，平时上网就使用HK做出口。

- 链式会多0.5-3ms延迟，有加解密损耗。
中转几乎没有损耗

- ## [中转 _202511](https://www.nodeseek.com/post-517908-1)
  - 中转是如何搭建的。 比如我有一台美西落地鸡，有一台香港机器，如何搭建中转。 我理解是 美西搭建一个3x-ui面板， 香港也搭建一个3x-ui面板，香港如何连美西，香港生成vless给大陆用户使用？ 是这么个流程吗
- 推荐油管一瓶奶油，256m的机器都能搭中转，3xui都太麻烦，233一键脚本v2ary，简单好用

- 你用了任意门，就是，美国到香港再香港到你家的延迟了。如果香港到你家绕路到美国的话，延迟会增加。

- 任意门或者转发面板比如哆啦A梦，链式损耗大点

- 最简单的 生成两个节点 然后代理工具里面使用代理链

- 哆啦A梦要最少三台小鸡而且配置要求有点高，我分享给你的那个256m的小鸡都可以，而且只需要两台小鸡就可以，一台转发一台落地

- ## [不懂就问 谁能教教我如何中转 _202512](https://www.nodeseek.com/post-546766-1)

1、3x-ui 隧道转发
2、3x-ui 配置出站
3、s-ui 配置出站
4、realm转发
目前就想到这几个

- 直接xui就能转发啊，再轻量realm也可以转发，这些脚本不如自己配置下
- 最简单就是xui任意门，如果要流量控制就在面板里面做一下分流规则

- 3x-ui吧 省事

- 中转机上直接用3x-ui
在入站出站那边设置一下

- 我都怀疑3x-ui有毒，用xui的时候同样的协议，同样的内容，ip没被墙，用了3xui就被墙了，两个vps（不同地区）都是，我至今不理解，换掉3xui后，半年多了，ip没被墙过...

- https://github.com/arloor/iptablesUtils
落地机搭Reality，中转机IPTABLES一键脚本转发即可，简单方便
在墙眼里，是你的中转机在跑Reality, 所以用端口转发落地机千万别用SS之类容易封的协议

- realm
gost(哆啦A梦yyds)
任意门
这3种都可以都可以
链式代理也可以

- realm，gost，iptables，不喜欢用面板

- 整个哆啦a梦面板吧，多台机，多个落地鸡，整起来方便

- ## [我->中转->落地怎么接？ _202601](https://www.nodeseek.com/post-580773-2)
- 中转机->落地机 我是直接Socks转发全部流量

- 最简单的端口转发，只需要在落地机用vless+reality即可。

- 落地鸡搭vless+reality，中转机直接端口转发到落地鸡就行了

- 落地鸡搭vless+reality，中转机用realm端口转发tcp/udp

- 我是wireguard+swgp-go+mimic到中转线路鸡，中转鸡的swgp-go直接把wireguard转发给落地鸡，很简陋小众奇葩，但我一般也不转发不用落地鸡，中转鸡的ip就够好了，只有个别问题网站得用落地鸡
一般简单的转发用iptables或nftables就能实现，我是看swgp-go有这功能就懒得折腾了。还有其他不少用户态的软件能转发，但我都没试过

- 我都是落地机Reality，中转机直接IPTABLES端口转发，方便快捷不影响中转机其他用途

- 区别在于链式能用机场中转, 又便宜线路又多

- ## [中转机和落地机之间用什么协议比较好？ _202510](https://www.nodeseek.com/post-492188-1)
  - 我现在用的socks5转发，测的真连接延迟不高但是进网页明显卡，感觉实际上1+1>2，大伙都用什么转发的？

- 中转机不需要协议直接端口转发，落地机用reality

- ## [中转和落地分别用什么协议？ _202511](https://www.nodeseek.com/post-516210-1)
  - 我之前一直以为中转用realm, 落地用vless刚才看别人说落地用ss，这样的话中转用什么？难道是链式代理？
- 不链式就 中转Vless+落地SS，或者使用Gost隧道端口转发

- 落地reality，中转iptables最方便

- 落地reality有点扯，落地当然是怎么快怎么来，直接裸vless或者ss就完事了

- 中转用机场，机场提供的协议中找个开销最少的加密协议
落地用ss chacha20-ietf，同样开销小

- 链式代理的话，如果是机场专线随便用啥都行，自己搭就用reality，被墙概率低

- 落地想用ss，如果中转机在墙外就必须链式，中转机在国内就用遂道加密，落地用能过墙的协议，那中转就有很多选择了。

- 中转用reality，落地用ss的话两个是怎么连接起来的，链式代理？

- 中转用机场，落地用任意一个带加密的协议都可以，我用ss，起协议方便

- ## [中转是否应该和落地同样的协议比较快？ _202601](https://www.nodeseek.com/post-570949-1)
  - 举例： vless+snell不如vless+vless ？
- vless + vless和vless + snell本质一样，中转鸡接收到vless的流量，解密出来，再按照vless/snell的协议加密给落地鸡，落地鸡再解密
使用realm/iptables等转发（其实就是端口映射）。落地鸡开放了vless的12345接口，中转鸡配置11111端口转发到落地鸡12345的端口，这样发送到中转鸡11111端口的所有流量都会原封不动发送到落地鸡12345端口，整个过程只需要落地鸡解密一次就行了。

- （1）中转：vless，落地：ss2022
  - (2）中转：realm端口转发，落地：vless

- 中转鸡直接realm啊，直接转发不比你解密再加密快？

- 落地用vless+reality，然后直接端口转发最好用

- 那就落地vless，中转端口转发

- 中转到落地什么都行
通常tcp连接（quic也是一样）到中转就中止了，后面是另一个连接
简单地说，后半段ss就挺好的

- 最快当然内核防火墙直接转发。不过有些协议不支持。tcp大部分没问题。

- ## [线路鸡如何拉落地鸡，用哪种方案比较好 _202512](https://www.nodeseek.com/post-538001-1)
落地鸡用的是s-ui配置是vless+reality
方案一：线路鸡该用s-ui在配置一个vless+reality，然后中转到落地鸡vless+reality吗？（clash配置，线路鸡的ip+端口+线路鸡vless配置）
方案二：线路鸡用x-ui，端口转发dokodemo-door协议转发（clash配置，线路鸡的IP+端口+落地鸡的vless配置）
方案一，方案二，目前都能正常访问。
疑问：
方案一，两次vless+reality延时会不会比方案二高，是否有必要，两次vless是不是更安全
方案二，线路鸡直接流量转发到落地鸡，延时会不会更低，会不会不安全
安全指的是哪个更容易被gfw封ip

- 我是链式代理或者wg

- 我是落地搭reality，线路用gost转发

- 我是落地ss2022+中转realm

- 直接端口转发，两次加解密纯多余，落地机加解密就够

- reality中转shadowsock-rust落地，没必要2次reality

- 你落地机配置好后端程序
然后中转鸡只需要装个realm或者gost 当然iptables也可以
最无脑的还是整个转发面板搭建隧道

- ## [哪位大佬可以给个搭建中转和落地鸡的教程！ _202501](https://www.nodeseek.com/post-254412-1)
- 3xui dokodemo-door
落地机正常搭建节点，然后在中转机上使用dokodemo-door转发一下端口，最后客户端的IP和端口换为中转IP和端口即可

- ## [[分享]小白的通过第一次自我摸索已经AI帮助，解决的中转落地转发的问题，特此记录。 _202505](https://www.nodeseek.com/post-343703-1)
  - 落地机 协议： vless+ Xhttp+reality. 导入V2ray可以正常连接。
  - 中转机 协议： 哆啦A梦-door

- ## [萌新问一下，为什么需要中转机+落地机 _202411](https://www.nodeseek.com/post-197987-1)
- 落地鸡用来解锁特殊服务。中转用来提升特殊服务速度的。

- 用来中转的机器到国内线路好 直连快 但是可能解锁不好 或者国际互联不好
用来落地的机器 到国内线路不好 直连不行 但是解锁很好或者国际互联很好 两个一结合......

- 大部分线路机器的IP都很脏, 比如claw

- 就是因为国际出口带宽不够 所以需要选择线路好的进行中转
# discuss-vps-落地
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [大家嫌弃的Racknerd作为落地鸡流媒体解锁和IP还行的啊 _202503](https://www.nodeseek.com/post-281849-1)
- RN 除了没 v6，性价比和服务基本完美。

- 我的圣何塞解锁也是全绿，无奈欺诈也几乎全满

- DC02 不错，就是一直没货

- [大家嫌弃的Racknerd作为落地鸡流媒体解锁和IP还行 补充版【DC02 74.48号段】 _202503](https://www.nodeseek.com/post-281874-1)

- ## [落地鸡解锁对比 BAGEVM LA vs LegendVPS NYC _202606](https://www.nodeseek.com/post-366752-1)
- LA跟NYC没啥可比性
延迟差一大截

- ## [【已出】25r 出wap的US原6刀年付 _202603](https://www.nodeseek.com/post-657365-1)
- 现在12u年付？
  - 是的

- ## [求推荐原生ip且干净的美国落地机 _202501](https://www.nodeseek.com/post-237574-1)
  - 之前听说zgo的ip质量不错，结果收了一个测了一下发现定位甚至都不在美国，也不是原生ip。还有其他高质量ip的美国落地机推荐吗？用来当dmit落地的

- RN黑五的机子, 感觉还凑合, 可以试试圣何塞, 主要是便宜$10.99一年, 续费同价

- lightlayer 的美西。9.9刀/年的VS/VG

- ## [求推荐个美国落地 _202603](https://www.nodeseek.com/post-642533-1)
  - 要求解锁ai的，gemini、chatgpt。之前看到一个qqpw，但是我看坛友出的都是nat鸡呢？nat质量能行吗？
- 其实有解的，你觉得NAT不行，就上VDS，35U。确定的是IP只有你自己用。

- nat不是很推荐，首先nat会屏蔽弱协议（也能用，可以落地加密，中转转发的方式），其次nat很多人用同一个ip容易送中。最大的优势的是便宜，便宜能用的前提是不超售，否则体验也一般。
然后就是搞个美国的落地也挺便宜，可以收个rn或者cc的74开头的ip，一年也不贵。

- wap 年付6刀 ，bytevirt 年付8刀
目前自己在用的俩落地

- ## [美西极低配落地机（解AI），完全不需要回国优化，预算50内 _202604](https://www.nodeseek.com/post-683843-1)
已有日本机做前置中转，现在纯收一台美西（洛杉矶/西雅图/圣何塞均可）机器当落地。

核心需求：

只要 IP 够干净： 必须能稳定且无感地正常使用 AI（包括 Gemini, NotebookLM, ChatGPT 等），其它流媒体能不能解无所谓。

完全无视直连网络： 直连中国大陆的延迟多高、丢包多严重都无所谓（最好是那种没人拿来翻墙的灵车线路），只要它在美国本土和到日本的互联正常就行。

只要能跑 3x-ui 就行： 对 CPU、内存、硬盘、流量没有任何要求，哪怕是 1核 256M 的纯玩具机也没问题。

接受的机器类型（满足其一即可）：

首选： 纯 IPv6 小鸡

次选： 便宜的 NAT（带干净的独立 IPv6，或 IPv4 端口均可）

备选： 极低配的美西双 ISP / 住宅原生 IP

明盘预算：
年付 50 RMB 以内（或 5 刀左右的传家宝）。好的机器可以考虑合理溢价，一切都可以谈

手里有吃灰探针机的大佬请私信，带上价格和大模型解锁脚本的截图。最好能带原邮或者支持 Push 出，谢谢！

- ## [便宜好用的美家宽落地鸡有什么便宜的，推荐一下大佬们 _202609](https://www.nodeseek.com/post-939063-1)
- 便宜，好用，家宽
符合要求的只有nat吧
- 是真家宽就不便宜，伪家宽十几到几十块吧，但也是 socks5 的小鸡鸡，要么就是 nat 鸡

- 伪家宽可以看看我前面发的帖子，正在出Panstar的NTT伪家宽

- novix的cox，20cad不到100块钱

- ae的attv6，伪家宽和机房可能区别不大
- ae家的v6家宽，或者去独角鲸/Shill的托管看看

- ## [美西落地怎么选：taipei、breadcloud、aethercloud、haruka、sakura、bage？ _202610](https://www.nodeseek.com/post-923793-1)
- sakura，bage 的互联好吧，taipei 的互联比较一般， breadcloud 的主要是单线 gsl，有可能没有路由互联绕港，haruka 没听说过

- 面包云还不错，主要是价格便宜
  - 但是面包的老板不是要去掉v6 att了吗，我都不知道以后还会做什么调整，感觉不稳定

- 我cloud、gpt和gemini都走面包落地了，不过采用了一周，目前还好
  - 你是走面包的v4还是v6落地呀？这么勇吗，其实gpt和gemini我倒是不担心，但很怕claude被封。其实性价比最高就是他家了，但是他的老板我很担心，随随便便就改这个改那个，我担心的是哪天突然用不了导致我要换ip又增加被封的风险。我现在只想找一家能稳定长期用ai的
- 直接走机房IP了，没指定V4还是V6

- ## [问大家一个问题：你们找落地机都要满足什么条件？ _202608](https://www.nodeseek.com/post-887896-1)
  - 是只需要他的IP好，比如是ISP住宅就行，还是有其他的附加条件
- 最起码，就是解锁好（广播ip，自带DNS解锁）< ip干净原生 < 双isp住宅ip <全都要。

- 最终还是选择动态家宽独享鸡

- 最好大厂，固定IP，国际互联不要太差

- 没有滥用标记就差不多了，伪家宽和机房区别不大情况，我个人更看重国际互联

- 真正的家宽很贵，一般只找一些nq看起来还可以的就行了

- ## [常见落地VPS的推荐和碎碎念 - LINUX DO _202509](https://linux.do/t/topic/930977)
  - 注意：这里推荐的产品除了有特殊说明，网络都是没有面向 CN 优化的，直连速度稳定性都很一般，为纯粹的落地产品。
  - ip 质量 / 国际互联 / 流媒体解锁 不是一个东西，流媒体解锁≠ip 质量好。
  - 其实落地就那几家，bagevm/DMIT/RFC，这三个用的最多，其他都没啥特点
- 某个挺好用的 N 开头的脚本不能发。:thinking: 平常除了融合怪外我用的很多它。知道不能发就行，这是规则，没有为什么。
zgocloud 盲盒抽奖，保底是原生的 IP 质量不错，运气好就抽到线路优化
bagevm 盐湖的 IP 不错，不过一点也没有线路优化，需要中转。我直接用瓦工拉了。
cloudcone/racknerd 这两我印象好像是 IP 机房类型的，质量一般般，线路也没有任何优化，纯纯建站
legendvps，胜在便宜的灵车。2.5 刀月付（现在 25 刀年付）的那款 Evo-SIP，原生 IP 很干净，解锁很好。现在缺货想买也买不到。前天我记得 Evo-SIP 炸了几小时，灵车是这样的没稳定性保证，补偿了一个月 0.5$ 款我测了一下 IP 质量很差。。
偏远地区的话我想到之前 HostDZire 促销。我买最低档的，IP 居然是原生的，质量还凑合还不错。当然没有线路优化，我用港鸡拉。
欧洲那边，苦于没有好的线路鸡，每次想买新鸡都退却了。其实我知道哪几款线路鸡，要么是价格太贵，要么是延迟问题我看一下到欧洲到广东 170ms、180ms 左右再加上不稳定的波动，好像也没差多大了我直连 netcup 德鸡延迟才 220ms，线路优化了寂寞。（可能只有上京德专线 130ms 才能救了但太贵了。。 :tieba_087:）
就这样，再加上家宽车，东亚主流我都点亮线路和落地了，基本好像没啥玩了没动力买新鸡了。

- ## 📌 [常见地区(SG/US/欧洲/少数地区)线路/落地/家宽 VPS的推荐与介绍 _202601](https://www.nodeseek.com/post-582305-1)
  - 线路机器：拥有CN大陆方向的优化线路机器，延时低稳定性高
  - 落地机器：国际互连优秀/流媒体解锁优秀的机器，注意：落地适合与否和ip质量并无关系
  - 家宽机器：IP质量优秀的机器，不容易被风控

- ### [常见地区(HK/JP/TW)线路/落地/家宽 VPS的推荐与介绍 _202601](https://www.nodeseek.com/post-578682-1)
# discuss-vps-vpn
- tips
  - 2种方案: 
    - 高质量小鸡 dmit/bw
    - 便宜小鸡 + 落地家宽, 在小鸡上开全局代理
  - 成本过高时要考虑替代: 订阅费 + 网络费

- ## 

- ## 

- ## 

- ## [问一下大家，广播IP 的原生IP 有啥区别？ _202610](https://www.nodeseek.com/post-969120-1)
  - 哪个好点，刚看了面包云日本的IP是广播其他的哪里都好，在纠结呢，要不要下手呢

- 原生ip就是注册的时候就是那个国家，然后使用也是这个国家的。就是注册和使用是同一个国家
广播ip就是注册的是国家A，使用是国家B。然后广播一下，说我现在把这个ip在国家B使用了。
一般来说的话，肯定是原生ip最好了。但是日本的原生ip比较少可能，大部分鸡都是广播ip，各种地方广播过来的。
你要说差很多那也不至于，就是心里作用比较强。主要还是看具体使用起来，cf盾人机验证啥的多不多。如果滥用的多了，原生ip也不好使的

- 主要看解锁吧，如果你不怎么看流媒体，可以不用关注原生 IP，看纯净度就行

- 没影响。无论是ip纯净度还是解锁能力，跟原生/广播都一点关系没有

- 运营 TK 的话，要原生 IP。看的话不清除，可以看看 NQ 测试，TK 解锁了应该没啥

- 各大数据库的ip风险值以及各种服务能否解锁才是更重要的
买原生ip的商家：广播ip不行
买广播ip的商家：ip是不是原生无所谓 

- 日常用基本没区别，特殊软件还有电商直播，会用到原生ip

- ## [现在美西4837有推荐的吗？ _202610](https://www.nodeseek.com/post-971006-1)
- 那就云悠跟伤心 伤心的上游是云悠 机器都一样的买哪个都行

- 可以看看bytevirt的signature，akari的sjc出口4837，也带去程优化，7c13的u，就是价格不便宜，在4837里算贵的了

- ## [收ByteVirt LA4837 8刀鸡 _202604](https://www.nodeseek.com/post-676167-1)
- 除了这个，貌似最便宜的4837就是白丝了吧

- lxc性能差可玩性差，他的4837线路也不好，很多人都不续费了

- 以前还行，现在延迟很高，但是还是不舍得扔。

- ## [我不同的服务器，用了后都出现ip评分和cf评分降低 · Issue · hotyue/IP-Sentinel _202606](https://github.com/hotyue/IP-Sentinel/issues/94)
  - 现象就是人机比变好了。但是ip评分变低了
  - ippure和iplark看评分都变低了。看了下每个机器降得都不一样，有个甚至cf风险都91%了
- +1 cloudflare人机比例上来了。

- [增加bot流量比 · Issue · hotyue/IP-Sentinel _202609](https://github.com/hotyue/IP-Sentinel/issues/114)
  - 使用过后IP送中拉回来了，但是会增加人机的流量导致访问谷歌跳人机认证，这个要怎么解决？

- ## [“Google位置纠偏”只是访问 /maps/search/...？“IP净化”只是 curl 白名单网站？——浅看 IP-Sentinel 源码：AI Slop 如何唬住 LLM 和真人 _202605](https://www.nodeseek.com/post-746631-1)
  - tldr: 这个脚本仅仅只是crontab+curl的融合产物，定时curl一些地区性的官网门户网站对于“IP信用净化”有没有用暂且不表，所谓“Google位置纠偏”也只是在通过curl在Google Map上搜索随机坐标的信息，种种迷惑操作自欺欺人的.sh和README.md的诡异遣词造句，其介绍帖居然还能拿下论坛的精品帖子，实在让人摸不着头脑
- 脚本其中一个功能是“Google位置纠偏”，其核心实现文件是 core/mod_google.sh，脚本先加载配置和两个数据文件：UA列表、区域关键词列表。代码要求存在 data/user_agents.txt 和 data/keywords/kw_${REGION_CODE}.txt，然后 mapfile 读入数组。
- 再看"IP信用净化"，其实只是通过curl访问一些区域性的官方网站，或者Wikipedia、Apple、Microsoft？
- 包装得如此高大上、强技术力的脚本，功能的真正实现却如此草台，令人哑然失笑
- curl headless 行为可能更像自动化流量，定时定点curl一些网站更是越描越黑
- IP-Sentinel 最吊诡的地方在于它把一套非常浅层的 HTTP 请求包装成了“Google 位置纠偏”和“IP 信用净化”的高技术力的脚本。
- 真正的位置上报依赖设备、浏览器、系统定位、Google 服务、账号会话和长期一致的行为信号；真正的IP信誉恢复依赖停止滥用、等待记录衰减、申诉、解除黑名单，或者更换更干净的网络来源。反观这个项目，随机 UA、随机关键词、随机坐标、定时curl白名单网站，这些动作看起来热闹，实际却没什么用。

- 可是他给我的送中ip拉回来了是真的
- 但是确实拉回来了，实践是检验真理的唯一标准。我看不懂lz写的，但我支持脚本作者。

- 笔者？这是哪个AI写的

- 这个时候我要说: 你行你怎么不上啊？白嫖还嫖出优越感了？

我从这个插件发布初期就安装了，这段时间更新了多少次我是能真真切切看到的。从此处可以看出插件作者是花了一些时间和精力来做这个事情的。

虽然我不去研究/解读他的代码，但是从描述和功能以及对应的一些命令命名上，也能大概猜出来这是一个玩具，但是:

我鼓励作者的行为，认同作者的付出
我就把它当一个开心的小玩具
这个东西没有太大危害
白白拿出来给你用，又不找你要钱，又没逼你用，客观评价/解读一下人家的劳动成果也就罢了

你写那么多主观且语气不敬的词语作甚？？？？

- 看到它只干了这么简单的事，我反而放心了。

不把它当灵丹妙药就行了呗。

反正我开着location guard每天自己到Google上搜餐厅和天气上报IP位置之类的都不管用。

那就丢个脚本跑着呗，不然也没别的办法了。

- 我也以为是‘开发者抓包分析了Google的定位能力，或者干脆实现模拟一个设备来上报位置’，原来是给小鸡增加了一堆bot流量。我都舍不得这么整小鸡啊

- 已经用了快一个月了
我的结论：对 ip 质量卵用没有，对送终有点微弱作用
我之前看这个项目 readme 还以为是什么跑个 chrome 模拟用户行为

- ## [4837优化线路是什么，不是普通直连吗 _202606](https://www.nodeseek.com/post-797274-1)
  - 看到有商家标4837优化线路，问问佬们4837优化线路是4837吗，还是说像163pp一样，联通也有一个介于4837和9929之间的线路。4837虽然体验挺好，但也就是普通直连吧。

- 4837优化只是国际10999国内4837，和全程4837相比路由上面有优势，10999-4837是直连，全程4837可能要绕路，晚高峰国内段4837也是有QOS的，别听某些人乱吹，这东西最多也就和163PP接近，和CN2完全不能比，如果你还是跨网用，那更加糟糕

- 似乎圣何塞机房的4837要稳定的多，虽然都叫4837，但延迟和丢包率要比洛杉矶好得多
- 好像是SJC那边4837的带宽冗余更多，所以表现较好，最开始指的4837好像也是指SJC的4837，而不是现在到处都有的LAX4837

- 10099-4837
  - 这个并不好，当然也可能是商家优化的问题，vmr-L2的10099-4837丢包率非常高

- 4837是普通线路
- 一坨，所有10099到4837从晚上七点到十二点都是不可用的状态。而且有时候会全天拥堵（tcp全黄），纯看运气
- 其实无优化线路是国际带宽，任何能直连大陆的网络，都可以叫优化网络。
  - 在三大运营商国际那里确实就这样分的，只要直连，别管好不好使，都属于优化线路。
- 大概是分为普通（非直连）-优化（直连）-精品（cn2gia/9929/cmin2）?

- 都是4837，为什么会差很多，主要是什么因素造成的
  - 我暂时也不清楚，但我手里用的比较好的是白丝4837/flawless node的4837。
  - 听别人说斯巴达的也好用，但我没用过。白丝在圣何塞，flawless在洛杉矶，但两者丢包率都非常低。
我甚至觉得可能是商家签订的带宽比较充裕。

- 根据玩法不同会有这几种意思：
三网强制4837：虽然4837跟9929比质量要低一些，但比起电信4134直连的表现还是要更好的，这样宣传的商家有raksmart的COV

精选T1直连4837：并不是所有的T1 ISP都有充足的4837 peer带宽，甚至绝大多数T1跟三大运营商的peer带宽都不是很充足。 不充足怎么办？ QOS丢包、绕路呗，这也是上面说的4134、4837体验不佳的最主要原因。(你们不会真以为联通骨干网连接国内联通的质量会很差吧？)
这时候就考研IDC商家对于路由的把控了，舍得花钱的，那就优选T1-4837, 不舍得花钱的，那就普通T1、T2-4837，都是4837，这里面的每兆成本差可以差到一倍甚至更多，那人家真多花了钱，确实质量相对优化了，打出大陆优化我觉得没问题，这样宣传的商家有RFCHOST的部分CO

白名单4837：这是非常特殊的玩法，我们之前有过。
你要理解，丢包、绕路归根结底是给三大的保护费不够，QOS的等级不高，所以在高峰期时三大的路由没空理你的数据包就给你丢了。 那么这个方案就是给三大交保护费，一大笔保护费。具体中间的流程你别管，效果就是这个IP不管路由垃圾到了绕地球多少多少圈，它就是不丢包还跑得快。
这个玩法非常的极端，需要巨量的大陆带宽需求才能回本，除了我们目前没见哪家IDC这么玩

transit 4837: 哦~这玩意在国内IDC中应该就更罕见了。
我可以告诉你的是，香港4837 IP Transit的费用大约在50~70USD/Mbps/月，9929则在此基础上x1.5
(4837: 你不会以为我是什么廉价货吧)
因为太罕见了所以忽略。

以上。
你要说这些玩法对比CN2等精品网的延迟与稳定性，那肯定是精品网更好。
但你要说到带宽大小以及晚高峰带宽性价比，那精品网绝大部分情况下比不上优化了的普通公网
这就看各家IDC对自己套餐的把控了

- 根据观察: 亚太的9929 ipt > 其余区域的9929 ipt = 9929家宽接国际运营商 > 10099-4837/纯4837 >> 4837家宽直连国际运营商。
有些商家会把"10099-4837/纯4837"叫做"4837优化"。
声明: 以上内容仅为本人经验判断。如有差错，欢迎指出

- ## 💡 [【教程】成功把送中的ip拉回日本，只用了一周时间 _202511](https://www.nodeseek.com/post-503481-1)
  - 前段时间绿云多个ip段被集体送中，我是其中之一，虽然是集体送中，但也拉回来了，下面是方法。
  - 第一，先去向谷歌报告IP问题
  - 第二，用插件改定位， 安装Location Guard https://github.com/mrfanii/Location-Guard-V3
  - 打开Location Guard插件，选择Fixed Location，在地图上点击你IP想要拉回去的位置，比如我的原本是日本，就找到日本东京，点击一下地图上的位置。
  - 来到Options选项，Default level默认设置改为Use fixed location
  - 打开Google地图 https://www.google.com/maps 点击右下角获取定位，此时就会定位到你刚才在插件里所点击的位置，说明成功了
  - Google随便搜索一下，滑到底部，点击 update location 来更新位置。
  - 之后每天用一下Google搜索和YouTube就行了，我是用了一周就成功了，集体送中的话，最好是人多力量大，发个贴让你那个ip段的人一起参与进来。

- https://github.com/anthonysgro/geospoof 
  - https://geospoof.com/
  - Browser extension and iOS app that spoofs your gps, geolocation & timezone, and auto-syncs to your VPN. Firefox, Chrome, Edge, Brave & Safari.

- ## [大佬们推荐一下性价比高的美西线路鸡 _202610](https://www.nodeseek.com/post-964307-1)
- 不溢价就只有lightlayer 4.9，超出你预算了

- ## [有没有用DMIT的？Claude的封号情况怎么样？ - LINUX DO _202607](https://linux.do/t/topic/2544132?tl=en)
- 封号和 dmit 无关，机房 ip 不是封号的主要原因。用家宽的照样有被封的..

- 如果你在 VPS 上用 Claude，那么风险分 - 20，如果是连到 VPS 的代理然后本地跑 CC，那么风险分 + 20，如果本地 CC 之前封过账号，那么风险分 + 40。

- 我是在 vps 上布置 cc，然后远程桌面 ssh 登陆用，目前还比较稳
  - 我在甲骨文机器上装的 cc, 目前用的没问题
  - 你想美国程序员租用机房 vps 远程开发也是正常用途吧，注册账号可以用家宽 IP，但远程用甲骨文 cc 没问题啊

- 感觉 DMIT IP 段对于 A\ 来说很脏，之前忽然在 IOS 上一直登录不进去，后面发现是有一个 cdn 走了默认的 dmit ip，把这个 cdn 加到家宽以后就能进了，应该最近的 dmit 被机场滥用了导致的

- 我的洛杉矶 dmit 的节点给 5x 用，一直都很稳，反而我的 vircs 的家宽容易封号。感觉这事情非常玄学

- ## [你们 Claude 用的什么 IP？qqpw 这种够了不？ _202608](https://www.nodeseek.com/post-853850-1)
- 感觉ip不是最主要因素，我用cogent伪家宽也没事。
而且感觉是否独享比是否真家款要重要

- ovh的机房IP照样用

- 獨享 活半年了， 不一定要家寬

- 独享比真家宽重要

- ## [求推荐跑Claude code的服务器ip _202607](https://www.nodeseek.com/post-849453-1)
  - 最近被封麻了，准备系统改英文、时区改海外、再部署个🪜独立干净ip来跑Claude code。有推荐的服务器吗老铁们。

- 连坐了

- 套sock5家宽，服务器本身IP无所谓

- 感觉通过苹果订阅安全系数稍微高点
可能我是最低级的20美元订阅，不值得他封，普通的vps美西，一直用没遇到过被封

- Claude针对中国用户，不但追踪邮件、记录系统时间、默认语言、甚至github 登陆的账号都会被记录，被封过后即使伪装的再好，还是有办法封你。除非换全新设备并且更换github仓库。

我觉得IP不是最主要的原因。一旦被封后你的很多特征都被记录，下次使用还是会追踪到你。

- ## [vmiss的IP干净吗？ _202608](https://www.nodeseek.com/post-887100-1)
- 担心这些就去找落地机用，线路机的IP质量只是摆设

- 没有一直干净的ip 你不搞事情，不代表你的邻居不搞事情，所以没啥意义，勤换落地

- gpt随随便便解锁，线路机ip也就那样，gpt不会因为ip封号，但会有降智问题。claude那边貌似对ip质量比较敏感，可能会因此封

- ## [vmiss的ip也是捞完了 _202608](https://www.nodeseek.com/post-882343-1)
  - 38 207 216都一样
- 线路鸡需要搭配落地鸡。不仅对vmiss，所有厂家都一样。

- 请问有啥落地鸡推荐的吗？感觉便宜的都又时候会送中
  - 我用的面包云 然后他的ipv6是家宽 分流给ai使用

- 任何需要ip纯净度的时候，首先就别想着线路机
  - 只要是线路机器，1个月必被人蹬得风险度拉满

- ## [求推荐三网优化大陆 _202605](https://www.nodeseek.com/post-707621-1)
有没有三网优化的 晚高峰不丢包的
现在用的白丝云的圣何塞大陆优化BGP
但是硬盘太小了才10G
有推荐吗
月5刀 更便宜更好

- 你买的白丝云 4837 这款嘛？ 晚高峰用起来怎么样？ 我也想入手这个。
  - 挺不错的 晚高峰不丢包 直连很爽 就是硬盘太小了 问了客服也不能付费加硬盘

- DMIT 搬瓦工 VMISS VMRack 哪个能买到就去买哪个

- ## [三网精品vps比较 _202402](https://www.nodeseek.com/post-70417-1)
- 你列的有几个可以归类到一起
Kurun系：Kurun、怪兽云、ZGO、图安云、Akile（Lax premium）

1、kurun系列：怪兽云，图安云三网精品、akile(Lax premium) 三网双程优化，单线程限制150mbps左右，测速去程变普通线路
2、v.ps系列：三网精品 三网双程优化
3、dmit系列： 三网gia 回程优化
4、Nearoute：wap usp（1刀款单线程限制50mbps）回程优化
5、艾云系列：艾云 akile（lax pro）回程优化

- kurun1.5更便宜但50的口子。ak119也不错 流量少

- 没用过其他的，如果不缺预算，首先排除kurun系的

- 大部分三网精品出自kurun

- ## [三网优化有什么推荐的🐔吗 _202405](https://www.nodeseek.com/post-110514-1)
- 第一梯队: 搬瓦工36刀CN2GIA、DMIT37刀CN2GIA、39刀cmin2
  - 二梯队: 年付159白丝云、咸鱼云的洛杉矶4837
  - 三梯队: 穷人套餐BYTEVIRT、WAWO、AKILE的4837一年五六十块
  - RN CC的洛杉矶机房也不错，能搭梯还能放点应用

- ## [除了vmiss，还有什么其他低价的三网优化？ _202610](https://www.nodeseek.com/post-962328-1)
- 有电信就要上cn2

- 价格和他差不多的，没他稳，价格比他高的，除了口子，不见得比他稳。被炒起来也不是没有道理，现在变成物以稀为贵了。

- isvoro，vmrack，lightlayer，光锥云
- 三网灵车有 isvoro, shandun，Matrixidc, lamhosting，双网的话推荐Lightlayer，只是这鸡联通有些残疾
- isvoro 22块一个月，200m，500g，三网优化
- 白丝159

- 光锥云在我这有点差，我发过避雷贴。

- TY云有一个三网优化的机器10元一个月，50Mbps的口子，我体验下来除了加载稍微慢点其他的和我的大妈没区别，关键无限流量就很爽

- shandun的三网优化和tri一样的配置我记得好像4刀一个月

- 上游netlab的那几家三网优化还算便宜

- 线路机器就是直连用的，IP方面可以直出，也可以拉起来一些线路不是很好的机器。比如我用vmiss 9929中转 aitr的att机器，延迟网速都不错。

- 可以看看nosla家的圣何塞，三网优化，或者洛杉矶电联9929移动cmin2。现在国庆特惠价格还不错

- ## [有没有美国三网优化或者CN2的灵车， 不怕灵就怕你不够便宜， _202610](https://www.nodeseek.com/post-961556-1)
- raksmart $3.99 1G带宽 1T流量，其实这家算老商家了，硬说也算不上灵吧，就是bug很多，然后ip质量很烂
- raksmart $2.99 4837做出口 $3.99 CN2做入口
单程CN2又不是不能用

- nosla家的国庆特惠，339 三网优化，可以看看

- ## 📌 [替我家小鸡问一下佬们，关于各家对更换IP的政策 _202410](https://www.nodeseek.com/post-175828-1)
1、🌹 DMIT dmit.io 每15天可以免费换一次ip，立即更换5刀一次，工单申请
2、CLAW claw.cloud IP被墙不能更换，花钱也不行，官方有回复的，只能等墙把你放出来
3、🌹 绿云 greencloudvps.com 3刀一次，工单申请
4、狐蒂云 szhdy.com 更换一次ip10元，工单申请
5、🌹 CCS colocrossing.com 交换IP地址需要一次性支付3美元。请注意，我们不保证被替换的IP在这种情况下会处于更可用的状态，工单申请
6、糖果 sugarhosts.com 更换一次90元，工单申请
7、JTTI jtti.cc 免费，工单申请
8、搬瓦工 bwh81.net 8刀一次，工单申请
9、🌹 Cloudcone cloudcone.com 2刀一次，工单申请
10、deluxhost.net 工单询问是否可以更换及费用，回复：NO
11、🌹 Racknerd.com 第一次免费，后面的3刀，工单申请
12、massivegrid.com 免费, 工单申请
13、Vmiss.com 购买5CAD的IP Replace订单，然后工单要求更换
14、yxvm.com 更换一次也是5刀

- ## [除了龟壳还有那些服务商可以免费换IP? _202501](https://www.nodeseek.com/post-246228-1)
- AWS GCP AZ Oracle 这些大厂都可以随便换没有限制
二线我知道的是DMIT wikihost 可以免费换，但是都有一些限制，比如DMIT是15天可以免费换一次IP（必须要完全被q） wiki是60天可以免费换次IP，但是这家已经如跑了

- ## [各位大佬，你们在用什么鸡能在晚高峰4K畅爽 _202607](https://www.nodeseek.com/post-810019-1)
- MEAGABOX、RN HY2 4K也能跑

- 4k有啥难的，随便啥烂线路用hy2都能看啊
- ipv6 + hy2 基本都可以应该

- 我是个新人，个人需求就是ai和偶尔看看油管。跟着论坛和大家学习，一路买了不少机子。现在大大小小有15个了。zgo和akko，都能畅跑。14.99的cloudcone我也能畅看4k油管。至于softshell和greecloud的机子，晚高峰，点个视频等3-5秒，也就可以4k畅看了。除了zgo和akko是三网优化，其余都是普通的。前段时间当云也可以，现在限速了。等dmit放货了，我也买个看看，为啥呼声那么高，实际使用体验差异化到底在哪里。

- neburst、光帆、vmiss

- ## 🤔 [DMIT 大佬们都用啥协议 _202511](https://www.nodeseek.com/post-499226-1)
个人使用，以前用bwg时一年ip正常，是 vmess+reality。
然后用Nat专线 就直接转发，然后落地ss

不知道大家在 dmit malibu 上用啥协议？ 又快又稳？

另外，大家手机上一般选择哪个客户端？

- vless+reality, 截至目前没有任何一台机器用这个协议被 ban 过

- 直接v6+ss，反正dmit的v6有优化

- SS 千万别，即便换IP也是15天一次，而且还污染邻居，损人不利己的事不要做。

- ## [为了防止封号，请教Claude code cli是部署在Dmit还是Azure的VPS上更好呢？ - 开发调优 - LINUX DO _202608](https://linux.do/t/topic/2770302)
  - 基本不跑项目，只是处理下文案类的工作

- DMIT 不知道，我只知道我美区 Azure 的 IP 连 L 站都进不来……

- 已这样用了一个半月，但最终没逃过 A\ 的刀，还是被封。全程代码都在服务器上，只 ssh 远程终端编码。

- aws，老美不少开个 aws 搞开发的，如果支付纯净，理论上和美国人没区别

- 我用 DMIT，没啥大问题，没有封号，没有遇到什么问题

- 用美西的 VPS 装 cc 跑了三四天了，没有问题，应该很稳！

- ## [【快讯】DMIT已支持自助升级为154IP _202609](https://www.nodeseek.com/post-952889-1)
- 154的质量到底好在哪里
  - 原生而且全部解锁都是us

- 179的偶尔会飘巴西去，但如果解锁稳定的话不用折腾154
- 我刚换的179, 怎么全解锁, 原生ip, 没什么风险, iplark邻居也是全绿...
- 现在最大的问题是跳盾，我179段的ip绿得很，但是cf跳盾是看机器人流量的

- 只要用的人多了，154照样被人送中

- ## [晚高峰的移动，非CMIN2的小鸡完全没法用了，单线程全部低于20Mbps _202411](https://www.nodeseek.com/post-195648-1)
周五晚上9点-10点，感觉移动家宽卡得不行，测了下单线程（使用iperf3+非docker版librespeed测了两遍）
发现手上所有的非CMIN2小鸡都被限速到港日单线程20Mbps了，美西8Mbps了，东部移动

涵盖以下线路机：
hk：瓦工hk85、claw hk、cera hk
jp：瓦工软银、几个jpp、绿云iij
美西：dmit gia

大家有没有什么非CMIN2速度正常的机子？
反观上海电信和上海联通就没如此离谱，哪怕hk85这种三网cmi回程机，都能跑到单线程100，个别还有单线程500的
应该不是瓦工的问题，是移动的锅，所有的线路机都不行
我CMIN2的香港小鸡是唯一速度能上百的了

- ## [晚高峰一般指的是几点到几点 _202508](https://www.nodeseek.com/post-421133-1)
- 下班到半夜

- 看波动就知道了。工作日是晚上10点半到凌晨1点。有时候前后半小时误差。还有就是节假日和周五周六晚上不一样。

- 6:00 pm - 0:00 am， 使用上的感觉是这样的
- 晚上10点半到12点半。有些线路这个时间段都会严重丢包。

- 也和商家的用户量、口大小有关，有的小鸡商的高峰是中午12点到凌晨7点....

- ## [晚高峰与非晚高峰普通线路各协议速度简单对比 _202512](https://www.nodeseek.com/post-551926-1)
  - Hostdzire SFO机+F佬的一键脚本

- 晚高峰不是好线路都Q，不如hy2直接力大砖飞

- 我的垃圾鸡今晚换hy2后，直接复活，移动都q不了

- ## [晚高峰优秀的商家有哪些推荐下呢？ _202609](https://www.nodeseek.com/post-934926-1)
- 狗妈奶爸龙系的晚高峰现在还行性价比应该算可以了，大妈会贵一点，要是绝对优秀感觉还是gn2如Riven这些了

- 我点开看了一下 狗妈奶爸都太贵了吧 动辄二三十刀一个月
  - 亚太就是这个狗屎价

- ## [vps 晚高峰推荐（接受 400 元/年） - V2EX _202401](https://www.v2ex.com/t/1009872)
- 请问下瓦工 49 和 dmit 36.9 哪个好点？
  - dmit 性价比更高，瓦工可以切 DC6 CN2 GIA-E 、DC9 CN2GIA 、日本软银、荷兰 EUNL_9 9929 等 14 个机房，瓦工的硬件配置拉胯
- 体验差不多，但是 dmit 有 ipv6

- rn 是洛杉矶 dc2 机房吗？我电信晚上用着还行啊。

要稳只能加钱 cn2 了，便宜的有搬瓦工年付 46 刀，dmit 年付 37 刀，不过上货就被抢光，要等着抢。现货有 akkocloud 的 299 年付圣何塞 cn2 。

差一点的有日本的软银和 iij ，绿云最便宜的年付 22 刀。最好找官方的 looking glass 自己测测高峰速度和回程路由。

- racknerd 的话可以用 hysteria2 ，速度很快，延迟可能一般，但是看视频这种场景很够。

- ## [vps: 求推荐一些晚高峰不卡顿的 vps - V2EX _202505](https://global.v2ex.com/t/1130777)
  - 自己手上的一款 RN vps ，到了晚上，卡到飞起。 套了 cf 也完全不好使， 不知道啥 cdn 可以提速，但总觉得即便提速了，晚上也不可用。

- 联通的话 Oracle 新加坡可以跑 300m
  - 联通到甲骨文新加坡线路本身不直连（ TCP 去回程都绕美日），得靠手段来解决。 但，怎么说呢，不直连的线路都不快乐。因为要解决速度和延迟问题，同时要付出一些额外的精力和成本，以及一些些潜在的代价。

- RN vps 有 ipv6 没？ 推荐使用基于 ipv6 的 hysteria2 协议 我目前在使用的是 netcup 家的无限流量的 vps 一年换算下来应该是 80 元多点 晚高峰也能稳定 10M/s+ 不过只能跑 ipv6 的 hysteria2 协议 其他的协议都跑不快 只有几百 k 的样子
建议先在 RN vps 上试试 hysteria2 协议
另外推荐免费的甲骨文云新加坡地区（使用自己的外币信用卡就能注册 注册时不要挂梯子 剩下的就交给运气。。。） 联通的体验很不错

- 联通还可以选东京或者新加坡的 AWS Lightsail

- 虽然不能一概而论，但一般认为联通的国际连通性是比电信要好的。你现在用的 RN 大概率在美西？联通直连美西无优化线路是基本能用的，换了电信可能就真不太能用了……另外山东联通的话，明年底联通在青岛的国际出口就要启用了，还有梦可以做（
$50/年这个预算的话，BWH 和 DMIT 洛杉矶都有对国内连接优化的年付 $40 、年付 $50 的特价机，几乎可以说是标准答案了，不着急用的话可以蹲一下他们不定期补货。亚太地区的机器价位要比美西高一大截，一般上网也不在乎那点延迟。

- 联通
- 一、选 4837 可以直连的线路。
  - RN 的话，你要选 DC02 机房，基本直连，不过今年晚高峰都不行
  - 继续，你可以选 AWS lightsail ipv6 的机器一年 42 刀，ipv4 的 60 （你可以先试用 3 个月），EC2 可以试用 1 年，这可以说是联通的最佳选择（新加坡或日本机房）。你可以等一些亚洲 aws 的分销商的促销活动，可以低价拿下上面的 lightsail 。
  - 继续，考虑日本软银线路的机器，比如绿云的软银线路
  - 甲骨文云可遇不可求，试一试吧。即便注册上了，对于联通也没有优化线路。甲骨文亚洲线路只有移动可以用，移动快乐鸡
- 二、实在不行，就上优化线路
  - 美西 9929 ，选项不多，就那几家口碑好的
  - CN2 ，选项不多，同上

- ## [大妈环境注册的Claude被封好几次了，有啥IP推荐 _202603](https://www.nodeseek.com/post-644910-1)
- 大妈套个落地就解决ip质量问题了

- x 上看到有家宽也被封的，可能是彻底的玄学

- ## [【求推荐】找一台 IP 干净的 VPS，用来搭 Claude Code 中转 - 求助 - IDC Flare _202603](https://idcflare.com/t/topic/66645/4)
- 存粹玄学，我个人是 zgo 落地用 claude pro 好几个月了比较稳定
有的群友用搬瓦工的机器也没问题，也有用 racknerd 的
个人经验就是固定 ip+apple pay

- ## [想用claude，求vps推荐 _202606](https://www.nodeseek.com/post-778226-1)
- 我用免费的甲骨文新加坡，v2rayn打开系统代理就可以用了。我通常是开全局模式。

- 我现在就在跑claude。建议：帮瓦工和大妈，完全没问题。问题得独享。

- 感觉这一套下来使用成本比Codex贵太多了

- ## [求推荐使用claude的vps，在vps上使用  - LINUX DO _202608](https://linux.do/t/topic/2798476)
- 我第二个被封的号就是这么做的。
我是独立的 mini 主机，6 核，32GB，sing-box 代理开全局 tun，走的美国家宽 sixtynet。
就是我第二个被封的号，找人代开，1 小时被封。

我完全独立的主机，放在家里，和你一样。
但昨天 1 小时就被封

- 我用非常纯净的家宽订阅，仍然被封了。没什么用。
你就直接 vps 用 cc 就是了，然后 ssh 隧道过去，但是这个方案用来开发还是挺麻烦的，vps 性能本来就弱，测试结果全是盲盒全靠 ai 一张嘴自己说，你自己上手测试又得配其他工作。

- 有没有可能封号不是 IP 问题，而是充值渠道或账号问题？
我节点也是万人骑，甚至美国、日本开会切。
Claude 账号用了好几年，升级 pro 也 3 个多月了。自己用 Google Pay 支付。

- 还有个主要原因，同一账号不要多个设备同时使用。使用设备越少越好

- 目前跑在 Ovh 上，感觉挺丝滑的。月 18.9 欧。
我账号是 ca 区，用的法国 ip 的机子。
我觉得这个不用非得美国 ip，因为美国人远程开发也不一定用本国的机子。

必须在服务器上跑哈。
因为这个防封原理就是，随便让 cc 拿本地数据，反正服务器是合法境外机器。
拿来搭梯子是没有意义的。

- 我全程在美国 vps 上使用 + 美国时区 + 极度纯净的美国家宽 IP（开了 Tun 并覆写了 DNS） + 没订阅过 claude 的美国实体信用卡 + 全程英文对话。
试了几个测试项目对话并观察了一天也没出问题。但跑自己的项目两轮对话后秒封，也就 20 几分钟。

- 最低配置 2c4g, 4c8g 才比较流畅。但是 vps ip 会被风控，比如稳定要 kyc。所以还需要处理 ip 问题

- ## [【纯测评/晚高峰实测】自用近一年的RN黑五老神机：RackNerd 洛杉矶 DC02 2核/2.5G/近6T流量 性能与 22:30 晚高峰实测 _202608](https://www.nodeseek.com/post-902453-2)
- 我的IP突然就被送中了，害得损失了一个Claude账号。

- ## [想问一下各位能用claude不封号的大神，都买的什么VPS？ _202607](https://www.nodeseek.com/post-842944-1)
- 我一直都中文沟通，机场vps都用过也换ip登录过，正常分流 电脑环境也都是中文环境。用到现在一直没问题。充过几次pro和max。搞不懂a/的封号逻辑

- 甲骨文

- 我主用的vmrack，有时候vmr挂了就用racknerd，有时候用esim 换来换去也没封号
可能用的时间不长，有次vmr炸了换racknerd用了一两个小时差不多

- ## using domain like verge.aichorage.de added the overhead of dns.  do you think it is a good idea to use the direct IP 198.46.xx.xx?
- Hysteria 2 operates over QUIC (UDP). Once the initial UDP connection is established:
  - Clash Meta caches DNS in memory, so repeated DNS queries do not occur for every request.
  - All proxied HTTP/TCP streams are multiplexed inside the single established QUIC tunnel.
  - Therefore, throughput, bandwidth, and streaming performance are identical, but cold-start connection handshake is ~15–20 ms faster with Direct IP.
- Where Direct IP is More Reliable:
  - No DNS Query Exposure: Your local ISP won't see DNS queries looking up
- Where Domain is More Reliable:
  - Resilience to VPS Migration / IP Changes

- Why they can't meaningfully differ: both variants dial the exact same server, port, password, and SNI — the QUIC connection that carries all your traffic is byte-for-byte identical. The only difference is at connect/redial time: the domain variant does one DNS lookup (cached afterward, served by fast domestic resolvers 119.29.29.29/223.5.5.5), the IP variant skips it. That saves a few milliseconds once per connection establishment, on a persistent multiplexed connection — invisible in real use.
- Neither is more private: both still send `sni: verge*.aichorage.de` in the QUIC handshake, so the domain is on the wire either way.
  - SNI = Server Name Indication — a field in the TLS handshake where the client announces, in plaintext, which hostname it's trying to reach, before any encryption is negotiated.
  - Why it exists: TLS encrypts the connection, but the handshake has a chicken-and-egg problem: the server must present its certificate before encryption exists, and a single server hosting many sites (one IP, many domains) owns many certificates. SNI is how the client says "I want verge.aichorage.de" so the server picks the right cert to present. Without it, every HTTPS site would need its own IP address.
  - Hysteria2 runs over QUIC, which is TLS 1.3 inside UDP. QUIC encrypts handshake frames after the ClientHello, but the ClientHello itself — SNI included — is still visible on the wire. That's what I meant: whether your config says server: verge.aichorage.de or server: 198.46.182.199, the packet going out contains the same string verge.aichorage.de in the ClientHello, because your config sets sni: verge.aichorage.de and the client needs it to validate the Let's Encrypt cert. The IP variant only removes the DNS query leak (see previous discussion), not the SNI one.
  - Encrypted Client Hello (ECH) is a newer TLS extension that encrypts the sensitive part of the ClientHello — SNI included — using a public key the client fetches from the site's DNS records. Cloudflare supports it for normal HTTPS browsing. Hysteria2/mihomo don't use ECH for proxy handshakes

- ## [Clash Verge怎么用yml文件配置Hysteria 2？求教程 - LINUX DO _202505](https://linux.do/t/topic/641154)
- 
- 

```yaml
- name: JP
    server: xxxxx
    port: 3121
    sni: bing.com
    up: 0
    down: 0
    skip-cert-verify: true
    type: hysteria2
    password: xxxxxx
```

- ## [国外vps被封？使用Cloudflare + Nginx + V2Ray，代理服务搭建 - 教程 - IDC Flare _202609](https://idcflare.com/t/topic/127101)
  - 本文记录一套使用 Cloudflare 橙云代理、Nginx 和 V2Ray 的部署方法：客户端通过域名访问 Cloudflare，由 Cloudflare 通过 HTTPS 回源到 VPS，再由 Nginx 将 WebSocket 请求转交给本机 V2Ray。
  - 除了安装配置，文章也整理了本次实际遇到的两个问题：TUN 模式下的 DNS 解析异常，以及客户端误用 TCP、未开启 TLS 导致连接失败。

- 
- 

- ## [【自建线路】cloudflare自选优选ip，sing-box搭建快速低延迟的vpn教程 - LINUX DO _202607](https://linux.do/t/topic/2639989)

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
# discuss-vps-trading
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [VPS交易避坑指南：原油、改邮、PUSH与交易所模式深度解析 (含搬瓦工/DMIT/NetCup实战) _202601](https://www.nodeseek.com/post-577764-1)
本文将为您详细拆解这四种模式（原邮、改邮、官方 PUSH、交易所），并结合 搬瓦工、DMIT、NetCup、RackNerd 等代表性商家进行分析。

第一种：原邮
定义：
“原邮”（圈内常称“原油”）指的是用户在 VPS 商家注册账号时第一次使用的邮箱账户。通常是 Outlook、Gmail 或自建邮局账号。

特征：邮箱内通常保留着商家发送的第一封“Welcome”欢迎邮件。
风险：交易时涉及移交邮箱账号本身，因此必须考虑邮箱被找回的风险。
1. Outlook 邮箱的安全清洗
如果是 Outlook 邮箱，在接收账号后必须进行彻底的防找回设置。我之前专门写过一篇教程：

文章地址：拒绝被找回！MJJ必修课：Outlook邮箱交易后的“防回手”安全设置全攻略

2. 代表商家：搬瓦工 (BandwagonHost)
搬瓦工的交易一般分成两种，分为“原油”和“改邮”两种，这两个在交易的时候容易价格方面差距明显：

带原邮：最安全，价格最高。没有找回的风险，也是交易的时候最受欢迎的。
改邮：有很高的风险。因为搬瓦工的机器账户可以通过“原始邮箱”和“支付凭证”进行申诉找回。如果买到的是没有原始邮箱的改邮账号，很有可能被第一任号主，也就是原始邮箱的拥有者 “毁号”或“找回”的风险，因为有的搬瓦工账户被交易了很多次，追踪第一任号主有的时候是一件很麻烦的事情。

第二种：改邮（修改绑定邮箱）
定义：
“改邮”是指在 VPS 商家后台将账户绑定的邮箱地址更改为买家的新邮箱。这通常意味着账户归属权的变更。

与搬瓦工不同，对于大多数支持改邮的商家，只要官方允许修改，交易通常是安全的。

1. 代表商家一：DMIT
DMIT 可以通过后台修改邮箱界面完成账户邮箱的修改。
需要注意的是：新注册的账户或新购买的机器自带 10天冷却期。在此期间无法修改邮箱或转移机器（这是我曾在交易新机时踩过的坑）。
安全建议：DMIT 改邮后基本无找回风险，具体操作可参考我的另一篇文章。
2. 代表商家二：RackNerd
RackNerd 除了部分特定的闪购套餐（Flash Sale）会限制修改邮箱，大多数套餐的账户都可以通过发工单的方式申请修改绑定的邮箱，但是一般只能修改一次，如果次数过多可能要求，使用官方的PUSH（需要收费，一次8美元)。

第三种：官方 PUSH（最稳妥）
定义：
官方 PUSH 是指通过商家提供的平台功能，将账号内的某一台特定机器转移（Push）到买家的账号下。

优势：只涉及机器转移，不涉及账号、密码和原始邮箱的交接。这是三种方式中最稳妥、最方便的。
1. 代表商家一：NetCup
NetCup 提供了非常成熟的过户机制，这家的交易我想大家都应该很熟悉了，通过转移码完成机器的过户操作。

费用：免费。
条件：必须付清当前季度的账单。
操作：卖家在后台生成转移码，买家输入即可接收，怕大家不知道，我这里加上了我以前写的教学文章。
2. 代表商家二：RackNerd
费用：RackNerd 的 Push 费用是 $8，通过提交工单的方式完成机器的过户。
需要注意的：RN 的 Push 费用是按次数（工单）收费，而不是按台数收费。如果你一次性 Push 多台机器给同一个账号，只需要支付一次 $8，所以如果一次性转移多台机器到另一个账户还是很划算的，转移的时候需要提供对方账户的邮箱地址。

第四种：交易所交易
定义：
这是一种相对少见的模式，等于把你的机器放在商家内部的交易平台上。

操作：卖家设置好机器信息和价格，买家购买。也可以私下商定好价格，通过交易所指定 ID 或时间锁定机器完成交易。
特点：官方的交易平台，还是有保障的，但是比较坑的是，部分商家可能会收取手续费，且卖出的资金不能立即到账，需要先提现到余额，然后再提现到你的对应支付宝或者微信账户，等待周期长提现时间不可控，还可能收取多笔手续费，很不划算。
代表商家（仅作知识扩展）
Akile
狐蒂云
注：这里不是打广告，仅为了告诉小白一种比较少的交易形式。

总结与建议
追求相对安全：首选 官方 PUSH 因为官方提供的PUSH服务是有保障的，不会出现邮箱找回，或者账户被找回，泄露自己账户信息（很多原油交易的账户还绑定了银行卡或者PayPal的自动续费，给自己和他人造成麻烦）。 交易的原油的时候，记得解绑自己的交易信息，防止被无故扣钱。
有原油要原油：比如搬瓦工这类的商家，能有原油交易肯定是 原邮，因为不容易出现问题，你下次交易也方便，不会留下隐患，下次交易也可以直接给别人邮箱账户，让他自己完成解绑你也方便。
改邮不是不可用需要看清楚：改邮 通常也是安全的，但是需要分清楚商家，也要注意商家的修改邮箱的规则，比如DMIT不是随时都可以修改，有10天的冷静期，自己在频繁交易的时候注意账户安全和平台限制。

- 狐蒂云的交易所已经取消了

- RN 按台收费，不是按次。客服说每个 $8
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
# discuss-vendors
- resources

- cons

- ## 

- ## 

- ## 

- ## 

- ## [能不能把家人云bitsflow清退出本论坛啊。。。。。 _202603](https://www.nodeseek.com/post-663250-1)
- 清退德国，但是可以退款和退余额，但是这不是耍人玩么，大家浪费的时间精力怎么算。。。
- 你自己算算你这个事情发生几次了，清退，迁移
你非要我帮你想，我觉得你别做这个项目了，你不适合。

- 自从去年12月份过后，除了DE-FRA-GOLD之外，我没有主动迁移过，只有一次是NUE上线之后我告知FRA的老用户可以免费升级
  - 我认为作为商家，清退确实是很不体面的，但是话说回来，但凡有一点可能，谁愿意去清退呢？况且历史无清退的商家凤毛麟角，强如DMIT也终止过服务，也退款了，我只是向榜样学习。

- 你是卖东西的，你自己售前不考虑好，来问我？开玩笑。。。。。。
而且我的态度就是这个帖子已经说了，希望管理员把你清出这个论坛

- 低信誉只对商家有效，家人云是oneman并非商家无法选中

- 家人这波操作给我看得目瞪口呆

7刀卖爆没记错的话至今可能也就一个月

- 因为母鸡是租的首月试用机，所以，如果买的人多就续费，如果买的人不多，就流浪。由于名气早就臭了，所以，基本上全是流浪。
不过对他无所谓，因为退余额嘛，钱已经到手锁定了。

- ## [2025-2026年可能还是国内最丑陋的IDC-家人云bitsflow.cloud---续集 _202512](https://www.nodeseek.com/post-548619-1)
- 官方账号 BitsflowCloud 被ns论坛封禁

- 迁移余额还打折
- 还有那啥的IP疗养费

- 谁能把bitsflow从5月到12月的折腾历史整理一遍，绝对的波澜壮阔 

- ## [家人云发布新站点 nosla.cloud, US-SJC三网精品, 上游xTOM _202511](https://www.nodeseek.com/post-501212-1)
  - 我们已经上架了新SJC-Premium的预售, 并且启用了新的站点-NoSLA Cloud， 此站点隶属于我们, 此后我们的优化线路产品将全部转移到该站点下独立运营.
- 跟国外的那个delux学的，以后每波新产品都搞预售，钱收够了再去买母鸡，属于是学到老外delux精髓了， 钱收齐、买母鸡、超售卖给韭菜，没收齐钱就原路退给你，0成本割韭菜，一茬又一茬啊，割不完

- 这招不错
我忘了之前是哪家好像也这样
我估计下一步是旧站点清退机子（或者已经清退了），给你退到余额
然后新站点与老站点余额不互通
变相“____” （自评，我什么也没说）

- 我只记得香港带宽不够那回商家论坛回帖说永不涉足优化线路，到现在已经言而无信了
- 我第一次在站里看到他宣传的时候，他说之前是服务机场主的，现在开始做散户，然后一口一个我司的，现在都绝口不提了

- 它这个预售机制太搞了，自己就算清退也不能亏一点，合着就是tmd把客户当非洲人搞

- 为旧站点清退铺路呢吧
- 换个名字再招一波家人

- xTom是瓦工荷兰三网精品的供应商, 吊打Netlab

- ## [nobrand卖的是ix还是iplc _202607](https://www.nodeseek.com/post-835889-1)
  - 在论坛里搜了半天没看懂，感觉大家都把ix和iplc混起来说，nobrand也是，标的是iplc，卖的是ix，所以这个究竟是iplc还是ix，还是这两个是同一个东西

- 👷: 整个沪日产品线都是IPLC专线，只是分成了两个入口类型，IX入口和移动入口。
IX入口只通IX、移动款含两个ix入口和上海移动入口。买我们移动款就不需要前置了。
不想麻烦的直接买移动款就行了。

- 有没有一种可能ix的跨境传输段也是iepl/iplc，这里的ix只是一种接入方式的称呼

- iplc，分为ix入口和移动入口，移动入口的套餐需要kyc（包含移动+ix两个入口）

- ## [nobrand也是火起来了 _202608](https://www.nodeseek.com/post-896578-1)
- d哥已经d过一轮大的了
主要缺点老板玩的太花了 每天都能产生新的sku，绷不住每天看群

- 他家好像并非oneman 员工挺多的 也有公司注册

- 👷 欢迎和我们6位员工交流

- ## [lightlayer是国人oneman吗，亚太地区稳定性怎么样 _202610](https://www.nodeseek.com/post-968581-1)
- Megalayer的子品牌吧，稳定性可以的，一直在用他家的hk反代，目前稳定在线300+天

- 他家亚太小水管很好用

- ## [gen2和zouter，十倍的差价，体验差几倍？ _202608](https://www.nodeseek.com/post-863385-1)
  - zouter一年168，绿云gen2一个月25刀，基本就是十倍的差价了，它们在体验上差多少呢？如果兜里没啥钱，有没有价格和线路介于两者间的机器？

- zouter 一个月 2T
绿云 500G 除非你再掏钱组他那个丢包丢成傻逼的内网 1T

zouter 已经属于中间档位了，移动和联通都属于是能用。

兜里没钱，就选这些联通快乐鸡、移动快乐鸡，体验不顶尖但是能用。
兜里有钱，再上这些三网精品吧。
不存在便宜+高质量的产品，存在的话也会被mjj冲烂

- 这没有任何可比性吧。不可能再有比zouter更有性价比的选择了，如果有那按照mjj定律，只有两种结果，一个是挨打被打，一个是被冲烂。zouter之前不就被打了好长一段时间吗。

- 差3倍，gen2是三网顶尖，zouter是1网都不顶尖

- 非晚高峰差别还好，Zouter JP上游是SkyLine，用的软银+IIJ

- 不是晚高峰用不出来区别

- 其实兜里没钱真可以考虑美西，k系我用下来除了延迟是gen2的一倍其他基本没有什么区别，美国的落地还好找

- skyline最近移动也一般，联通好点

- ## [shandun的LA三网优化差在哪呢？ _202609](https://www.nodeseek.com/post-952256-1)
  - 感觉shandun价格也只比vmiss高一点点，同样也是三网优化。而且现在随便买，vmiss为什么会有这么高的溢价呢？shandun差在哪里？
- 我用下来vmiss9929和tri差不多，哈哈哈
  - 我也是9929 core，这个月流量用光了买了一个shandun的4$机器，感觉都挺好，我用来当线路机的。

- 上游不一样，回程速度也不一样，VMISS虽然写的200M口，但是回程速度能跑到600多Mbps，而shandun无论去程还是回程都超不过200M，而富强往往重要的就是回程速度
- 我是一台vmiss9929core + shandun 4$机器，看探针数据shandun的机器确实要好很多。

- 差在炒鸡老看不上 

- 不都差不多的，够用了，他家机器性能还可以，跑脚本比很多都要快，不过估计新商家用的人少

- ## [shandun有没有可以媲美vmiss tri的us节点？ _202609](https://www.nodeseek.com/post-918636-1)
  - shandun有没有可以媲美vmiss tri的us节点？ de感觉还挺稳定
- 之前美国出大流量套餐还行，一个月4刀，现在貌似还可以用折扣，cogent 伪加宽，之前出过一个

- shandun有个三网优化的，八折，4每月，200mbps，500G

- ## [晚上才上来，看见shandun解散了！ _202608](https://www.nodeseek.com/post-892096-1)
  - 其实我也用了这家的de 9929，速度确实还可以，也相对便宜。
  - 但是炸鸡、送中等问题确实存在，实话都不让说了。
- 格局太小了，我估计很多人10月份四折或者5折不会续费，主要没啥价格优势，别家也做得到

- [Shandun闭群，我来捋一捋 _202608](https://www.nodeseek.com/post-891780-1)
- 没必要开群聊，有问题有工单系统就行，开群聊的都是闲着没事的商家，还得找人管理

- ## [【ShanDun Network 新商家入驻】德国 AS9929 上线｜40% OFF +40% OFF 首月低至💲1.01｜抽奖送 30 台 VPS _202608](https://www.nodeseek.com/post-863994-1)
  - ShanDun Network 主要提供云服务器、物理服务器等服务。本次为大家带来德国 AS9929 云服务器，并准备了 30 台 VPS 作为新商家入驻福利，欢迎大家参与体验。

- ## [全面总结cloudcone，不算垃圾也不算好吧，一般而已，上位替很多 _202408](https://www.nodeseek.com/post-143962-1)
- cloudcone有什么可以争的，cc的技术是有一点，人家自己开发面板的，但机器一般般，除了几个远古款没必要买
cloudcone的竞品
rn
单从性价比来讲，rn完全碾压cloudcone，cpu性能伯仲之间，io吊打
cloudcone的经典款如879还有稍微比较一下的能力，其他就没必要比了

crunchbits
天上地下，crunchbits真的能赚钱吗，似乎勉强不亏钱

其他欧洲机
有很多，netcup等，或者那个忍者，还有些想不出来了反正很多

cloudcone的io水准的数值不会说谎，真要搞个东西，部署个数据库，性能差别一下子就出来了
为什么有时候hdd的io数值可以
cloudcone的io是ssd cached，刚开始是往ssd缓存写，之后是往hdd硬盘写。
这就导致跑分和实际用的性能差别

cloudcone到底买不买
远古879，9.xx高性价比款，溢价不离谱，可买
老款hdd普通款，纯冤种，谁买谁sb，不如rn，不如crunchbits/layer
新款13刀ssd，io性能差，建议观望，或者买隔壁rn妥妥的
花30刀买个垃圾io机器的，看乐子

- rn的ip好像很烂，谷歌一直跳验证

- rn和clonecone的ip上游是一个，没差
这种机房ip跳验证正常，套warp或者登录谷歌账号可以缓解

- rn洛杉矶以外的上游是colocrossing这里的ip更烂
洛杉矶74开头的还可以

- crunchbits 独服托管应该还是在赚的 只是VPS不咋赚
- 独服托管一般都是赚的，vps可能是为了增加名气

- 13刀，内存才1g，硬盘才20G，明显瘸腿，而且cpu很差，等超售多了更差，单核跑分200多我都见过

主要是affman在硬推，管理员又不理

- 买的人多了，cpu分就降了，超售大王

- ## 👀 [还在用 CloudCone 的 随时做好准备吧 _202605](https://www.nodeseek.com/post-752561-1)
- 这篇文章主要报道了洛杉矶知名数据中心和基础设施提供商 Multacom 因为拖欠房租而被起诉的新闻，并分析了该事件对下游主机厂商和用户可能带来的潜在影响。
由于 Multacom 主要是作为“上游批发商”，很多大家熟知的便宜 VPS 商家都是租用它的机房。这次事件牵扯到了几家热门厂商：

RackNerd（闪购王）：
时间线非常微妙。RackNerd 最近刚刚完成了大动作，把大量设备从 Multacom 洛杉矶机房（DC-02）整体迁移到了新的 West 7 Center 机房（DC-03）。其 CEO 曾含糊地表示“由于一些无法控制的建筑/大楼因素，继续留在原地已经不是长久之计”。现在看来，RackNerd 可能是提前听到了风声，为了避免重蹈 QuadraNet 的覆辙，提前帮客户避了雷。

CloudCone：
CloudCone 在 2024 年被 Edge Centres 收购，而 Edge Centres 在 2023 年也收购了 Multacom，这意味着 CloudCone 和 Multacom 目前属于同一家母公司。近期 CloudCone 正在通知客户进行大规模的 IPv4 改号（Renumbering）。虽然不一定意味着他们要搬走，但在母公司深陷官司的背景下，IP 变动加上近期有用户抱怨其联盟营销（Affiliate）佣金提现延迟，让部分网友猜测其资金链是否存在压力。

HostNamaste（来自评论区商家补充）：
该商家表示，他们在今年 3 月就收到 Multacom 的通知，称其计划将基础设施从 Aon Center（707 威尔希尔）重组搬迁到附近的另一个机房（600 W. 7th Street）。HostNamaste 已经主动完成了迁移，目前没有生产环境留在那栋涉及纠纷的大楼里。

文章最后提醒广大垃圾机（LowEndBox）爱好者：虽然不能证明 Multacom 会马上倒闭，但这笔 40 多万美元的欠款绝非小数目。如果你有海外 VPS 或服务器在 Multacom 的洛杉矶机房（或者不确定上游是谁），现在是检查并做好数据备份（Backup）的最佳时机。

- ## [cloudnium可以直接改成按年续费码 _202608](https://www.nodeseek.com/post-871470-1)
  - 按月怕忘记续费

- 工单改年付客服涨价
- 我也有一台改成年付客服居然说要9.9刀，我直接月付算了，应该可以提前手动出账单付款吧

- 可以，改成年付就要9.9$

- 直接充值余额，让系统自动扣就完了

- 以前可以5.88年付 现在貌似不给改了

- 可以提前支付订单，我一次付三个月的，应该也能一次付一年

- 可以直接手动点击续费，付款12次不就一年了
  - 进服务器详情有个 Manual Service Renew

- ## [【已破解满0.5刀才能支付宝】cloudnium这家支付宝不能支付了？ _202607](https://www.nodeseek.com/post-832542-1)
  - 续费点支付宝没反应，我是一个人吗？

- 0.49的吗 得大于0.5才能支付宝
- 0.5以上才能支付，0.49充值余额要10刀，收的话收0.54月付比较方便

- ## [感觉cloudnium这波账算不过来啊 _202607](https://www.nodeseek.com/post-808589-1)
  - cloudnium这波给独立ipv4，只要0.54，据说用信用卡支付可以0.49。即使完全不考虑机器和人工的费用，一个ip费用一个月我看也要0.5刀的成本吧。他卖这么便宜怎么办到的，账算不过来啊
  - 好吧，看了大家的回复我自己也查了下，现在ipv4成本价格降了，大概就0.2-0.3刀一个月左右，那账还是算的过来的
- 这家23年就有了

- 0.49是一开始的价格，因为第三方通道最低0.5起，所以就改成了0.54，并不是使用信用卡才是0.49
  - 这家开了蛮久了，会不会跑路不好说，反正月付吧

- 自有数据中心，与其吃灰，不如发挥一下价值。
- 机器成本我觉得超兽下可以完全不考虑了，但是ip成本是实打实的，每台机器都要有的，还能这么便宜就很神奇

- 海创还0.39呢
  - 海创配置可比这个低, 而且还涨价了, 现在也得0.5

- 人家都拿的B段吧 0.2-0.3刀 有的赚

- ## [CLAW限速越来越变态了 _202505](https://www.nodeseek.com/post-331171-1)
  - 我自己同步数据已经把速度控制到50M了，这也是偶尔一次跑大流量。还没跑一小时给我限速到2M.......

- 8刀4刀4.2刀，几刀的机器都限速。赶紧弃坑保平安。

- 限10M才得行

- 一小时还算好，我啥也没干。。。。晚上直接限速本以为是qos没想到机里就1m 

- 你一说claw限速，就有人进来冷嘲热讽，不得不说阿里母公司公关这一块儿还是到位啊。

- 你在NS LOC说都没有用的~
它们只怕在老外那边被人喷！建议大家都去lowendtalk围剿无良IDC

- ## [netcup老1o的价值在哪？有啥优点吗？我看好多人溢价收 _202603](https://www.nodeseek.com/post-652710-1)
- 便宜稳定，可开25端口
- 大厂稳定可靠

- 1欧一个月带ipv4

- 其实就是便宜 一年10欧 + 无限流量

- 大厂，稳定，可以开邮局，无限流量，以后要涨价了

- ## [netcup老1o鸡怎么样 _202608](https://www.nodeseek.com/post-884221-1)
- 流量？老1欧我记得没流量限制来着，不少人拿来刷pt

- 流量无限，但是会限速，24小时平均每小时超过100Mbps，会限速到100Mbps

- ## [收到了一台netcup 老1o 无比开心 _202609](https://www.nodeseek.com/post-915795-1)
- 大厂里的便宜鸡，而且开放了 25 端口出
- 探针鸡

- 快乐就好，这鸡太鸡肋了，不然溢价也不会这么点

- ## [netcup新老1o的区别是什么 _202609](https://www.nodeseek.com/post-916765-1)
- 新1o比老1o贵
老的1o原价就带v4 新的默认只有v6 要v4得加0.5o

- 新1o不带v4是1.04o，带v4是1.54o；老1o带v4是0.99o

- 新1o好像是1.2o老的价格就不清楚了，好像是0.84o？

- [nc的新1o/2o和老款什么区别 _202608](https://www.nodeseek.com/post-861558-1)
- 怎么可能不涨价，合约到期都涨的
- 之前是0.84，五月涨到0.99，后面还会不会涨不知道

- ## [这下应该很多人对netlab有清楚的认识了吧 _202602](https://www.nodeseek.com/post-622748-1)
  - geelinx新商家
价格确实便宜，比之前家人云同样的价格便宜了一半，流量还多。
但是着线路我看是真不如软银，就在刚刚软银联通刚刚轻松破300mbs，netlab也就不到200。虽然老板说是线路没调好
电信晚上会比发疯的软银强一点。
昨天晚上给我看傻了，我本就是准备买台搭个面板，那么多人抢。1g的搭flux总报错，开swap都不行。
不是说这家不好，我也买了台，但是这么疯狂还上脚本真是太夸张了。

- 感觉也还好吧，一个月十块钱出头，电信比claw好，联通比claw差
主要是突然意识到亚太要上就干脆极致一点，半吊子的亚太不如上美西，所以才出掉了

- 不拉不睬，我这边晚上确实比软银好，晚上9.25的结果

- 只用过netlab美西4837，拉中之拉。不过亚洲利好联通移动用户

- ## [netlab就是垃圾 _202610](https://www.nodeseek.com/post-962824-1)
  - 偶尔小炸一次，然后每个月准时憋个大的 
- 远离netlab，上游是netlab的都不买，太垃圾了

- 圣何塞已经稳了2个多月了，没人打肯定不炸

- ## [xtom有大陆优化的套餐卖吗？ _202603](https://www.nodeseek.com/post-661470-1)
- v.ps即可 xtom不直接面向散客

- ## [有人科普 v.ps 和 xTom 老板郭秀峰的瓜吗? 好奇 竟然能引起千人众怒 我记得老板也在 v2 就是 smms ipsb 的作者 - V2EX _202305](https://www.v2ex.com/t/939029)
看评论区总结了下

主要歧视中国人
1. 移民澳洲 不承认是中国人 并且不允许别人叫他中文名字 因现在有了英文名字
2. 黑五清退了所有中国用户, 发现中国 IP 注册就封号
3. Paypal 过 6 个月争议期再要求 KYC 实名认证水电单, 不提供则封号
4. 不能说 v.ps 不好, 否则拉黑封号
5. 言而无信, 多人证据实锤

- 简单总结下主线剧情：V. PS TG 群里一个管理做事不按章法，想起啥就做啥，平时语气有点得罪人，群里精神股东也比较多，败路人缘。前两天又封了几个典型虚假信息的账号（按他家 AUP 规定），此为导火索。争议点在于不是一开始注册的时候就封，而是过了几个月了想起这回事就顺手封掉，导致了一波节奏，昨晚开始补救但为时已晚，节奏已经起来了，开始翻旧账挖黑料，愈演愈烈，现在矛头逐渐指向老板兽兽进行攻击，所以能看到如此“盛况”。

至于图中的内容有事实，也有张口就来的。现在隔壁有几个人在一直发帖带大节奏，有些路人看到后感觉自己正义感爆发，强行把自己代入进去跟着喷，他们只是想爽一下。现在的形势是只要不跟着喷就会被打成舔狗，一般人也懒得吭声，毕竟现在 Hostloc 没人管理，想干啥都行。

- ## [【Dmit PK 搬瓦工特价机】-chatgpt _202604](https://www.nodeseek.com/post-687304-1)
机型	官方价	溢价	实际成本
MegaBox-Pro	$45.6	+900	❗极高
CORONA	$49.9	+260	✔较低
PowerBox	$41.9	+350	中等
BiggerBox-Pro	$36.3	+900	❗极高
MALIBU	$49.9	+350	中等

- DMIT 美西特价机一年至少补货四次，MJJ们就这么等不及吗？还是一堆炒鸡佬自导自演？

- ## [目前搬瓦工和DMIT的主要业务是什么？ _202607](https://www.nodeseek.com/post-830079-1)
  - mjj占比大吗？如果占比较大的话，那么gfw岂不是盯着dmit和瓦工封就行了？

- 搬瓦工老板主业卖软件的

- 三网直签，能没点背景才怪，特殊时期随机封点当当绩效，完后直接放出来。

- 据我所知，这两家散户占比都是很高的，那些大户下游与其说是“大户”，不如说是合租。
精品合同肯定是合规的，三大本来就是睁一只眼闭一只眼。不过合规和ip是否被墙也没什么关系（这两家的ip段确实是被重点关注的），因为gfw和三大不属于同一个部门，甚至在我眼里它们之间有点“敌对”的关系，只不过明面上不能翻脸而已。

- 运营商知道你干什么，甚至提前通知你。本质都是为了挣钱，除非上面真的要施压了，才会有点收敛
- 一句话来说就是：三大想卖海外精品，但是又顾忌相关部门的合规性检查，所以专门成立海外这些分公司（CTG、CUG、CMI），让idc与分公司签合同，绕过集团繁复的审批，满足原先的“灰色交易”的需求

- ## [瓦工和dmit谁会先跑路 _202603](https://www.nodeseek.com/post-668740-1)
- 搬瓦工自己就是上游。。。也购买了DMIT/V. PS的带宽，比如

HK85 / USCA_9 / 加拿大DC6 / 荷兰DC1 / 东京CMI，自己拉的线。

荷兰9929 / 澳洲9929 / 新加坡CN2GIA 上游是 V. PS

东京CN2GIA / 香港CN2GIA / 洛杉矶DC1 上游是 DMIT

大阪软银电信去程 CN2 上游是 DMIT，回程上游是 V. PS

再说详细点，洛杉矶DC9移动方向和国际方向上游是 DMIT，电信联通是自己的。

洛杉矶DC6，中国方向上游是DMIT，但国际方向又是自己的。

非中国优化线路机房暂不讨论，搬瓦工自己本身就是规模非常大的上游。

但在 NS，搬瓦工 完全当了 DMIT 下游，所以 DMIT 很高贵，亚太地区动不动溢价四位数。一群自导自演的炒鸡客而已

- 跑路大妈的成本更高，极少数vps商家自建线路，除了大妈几乎没有，都是租用包括大名鼎鼎的瓦工，所以你宁可相信所有vps商家都跑路也别信大妈会跑路，大妈是自建线路所以成本更低，经常活动，并且活动鸡量大管饱，但跑路代价太大了，跑了他建的线路我可以全盘接手

- ## [听说大妈dmit是瓦工的上游？ _202505](https://www.nodeseek.com/post-329370-1)
- 美西dc1机房的线路是的，其他美西机房大部分是瓦子自己的
在行业竞争激烈的idc业务中，合作和竞争是同时存在的，不必大惊小怪

- 瓦工从dmit接了香港和东京，从xtom接了圣何塞，阿姆斯特丹和大阪, 没啥好奇怪的。

- ## 🆚 [拒绝踩坑：DMIT 与 搬瓦工 (BWH) 全方位对比——服务、政策与套餐选购指南 _202601](https://www.nodeseek.com/post-589739-1)
一、 退款政策区别
1. DMIT 退款政策
根据服务协议，DMIT 提供 3 天内全额退款 或 30 天内剩余价值退款，退款通常是无理由的。

全额退款条件：

服务购买不超过 3 天；
使用的传输流量不超过 30GB；
符合其他基础退款规则。
退款处理时效：
通常在 48 小时内处理退款请求，高峰期可能会有所延迟。

2. BWH（搬瓦工）退款政策
退款地址： https://bwh81.net/refund.php

搬瓦工支持 30天内退款，但需同时满足以下所有条件：

账户创建时间在 30 天或以内；
账户信誉良好（无逾期欠款），且未违反服务条款；
VPS 每月数据传输使用量低于配额的 10%；
全额退还自账户创建之日起的付款（注意： 更换 IP 的费用不退）；

二、 更换 IP 方式
1. DMIT 更换 IP
IP 地址是有限资源，DMIT 提供有限制的更换服务。

免费更换政策 (适用于 Pro & EB 系列)：
需同时满足以下条件：

实例至少已购买 7 天（第 8 天起符合条件）；
距离上一次请求更换 IP（含付费）至少已过去 15 天（若有多个 IP，按最后一次更换时间计算）；
当前 IP 的 ICMP 和 TCP 所有端口均已被封禁；
服务剩余有效期不少于 7 天。
不满足免费条件时，可随时付费 5 美元 请求更换，每次间隔不少于 7 天。

2. BWH（搬瓦工）更换 IP
更换地址： https://bwh81.net/ipchange.php

更换流程：
更换一个新 IP 的费用为 8.79 美元。访问更换地址，可以自动提交工单，然后付款等待IP更换。

共同点
都提供了美国、日本、香港的优化线路，都属于很高的水准。
两家的机器都支持免费的快照。
都是三网优化线路，都很稳定，不同的套餐优化线路不一样，具体要看套餐说明。
注：搬瓦工DC1 机房的CN2上游其实就是DMIT。

DMIT 的优势
如果被封锁IP，套餐可以免费更换IP（具体套餐需要看官网，不是所有的套餐都支持。有15天的间隔）。
每次出问题公告及时，基本上每次都有补偿，虽然不是每次都满意但是至少有补偿。
给的硬件性能更高。 如果是正价款都是最新的硬件特价款硬件回落后一代，但是也比搬瓦工的硬件跑分更高，虽然不一定用得上，但是冗余的性能也是好的。
每次优惠活动，限时不限量都是敞开卖的，好几次DMIT官网都被冲烂了，去年圣诞节都加入了排队机制，但是还是出现了开机异常的BUG。

BWH（搬瓦工）的优势
客服响应快（是相对的DMIT的也不慢，但是很多BWH的工单和处理都是自动化不需要那么多人工干预）。
欧洲优化线路，其他套餐可以更换多机房。
优惠套餐，一样的价格配置和流量搬瓦工给的更足，价格方面更有性价比。
活动频率一年当中BWH的活动还是很高的，还有文章奖励、抽奖、优化机器活动。
注：虽然现在有了邀请码的机制，个人认为还是比较膈应人的，DMIT一般就元旦和春节前后会有活动，其他时候很少举办活动。

- ## [DMIT和BWH-传家宝科普 _202505](https://www.nodeseek.com/post-336754-1)
- DMIT，被各位俗称大妈，官网：https://www.dmit.io/。因其出色的主机和线路，几乎是商业IDC行业天花板的存在。下面列出的是官网目前看不到，热炒于市场的各个传家宝

- LAX. EB. CORONA
  - 1 vCPU	1 GB	20G SSD	2Gbps	2000	49.9
- LAX. Pro. WEE
  - 1 vCPU	1 GB	20G SSD	500Mbps	550	39.9
- LAX. EB. WEE
  - 1 vCPU	1 GB	20G SSD	500Mbps	500	49.9
- LAX. Pro. MALIBU（老）
  - 1 vCPU	1 GB	10G SSD	1Gbps	1100	49.9
- LAX. Pro. MALIBU（新）
  - 1 vCPU	1 GB	10G SSD	1Gbps	1000	49.9

- 日本：TYO. Pro. Shinagawa(品川)
  - 1 vCPU	2 GB	60G SSD	500Mbps	500	199.99
- 香港：HKG. Pro. Victoria(维多利亚)、HKG. Pro. MongKok（旺角）、HKG. Pro. Nathan（弥敦道）、HKG. Pro. Lokmachau(落马洲)、HKG. Pro. TsuenWan(荃湾)
  - 298.88

- 搬瓦工是老牌主机厂，对大陆线路有优化

- 香港：THE PLAN，可更换18个机房，可用香港机房是选他最大的理由！HK85，CN2GIA
- THE PLAN(V1)	2 vCPU	2 GB	40G SSD	2.5Gbps	1T	99
- THE PLAN(V2)	2 vCPU	2 GB	40G SSD	2.5Gbps	2T	119

- NODESEEK-MINIBOX	1 vCPU	512 MB	10 GB RAID-10	1Gbps	500 GB	29
- NODESEEK-BIGGERBOX-PRO	1 vCPU	1 GB	20G SSD	2.5Gbps	1000 GB	39
- NODESEEK-MEGABOX-PRO	2x AMD	2 GB	40 GB RAID-10	2.5Gbps	2000 GB	45.68

- BWG 这个辣鸡CPU啊，3核当人家单核跑还限速（40%），服了。。。。

- dmit普遍是 amd epyc 的处理器。而瓦工大多是intel的老旧低性能处理器，单核性能跑分远不如 amd 的 epyc。不过爬墙一般对 cpu 没啥要求（除非是要跑出几百mbps的大带宽），确实 dmit 跟 瓦工两家任选就是了

- ## [为什么很少看到讨论使用AWS lightsail当飞机的呢？是线路不好吗？还是别的原因？ _202609](https://www.nodeseek.com/post-907440-1)
- 一个是动态路由，晚高峰拉胯，Claw啥的完蛋之后蹬的人多了现在JP和SG不是晚高峰也拉胯了
另一个是以前锁流量的时候还没这个问题，现在超流量之后收费，不额外操心被人恶意刷了或者偷来当优选CDN直接一夜刷没一套房

- 大厂！没有讨论意义！流量少！超了巨贵

- 线路没啥特点，然后贵。

- 贵啊 而且线路拉胯 不如买nat

- ## [lightsail是不是只计算出站流量 _202609](https://www.nodeseek.com/post-921071-1)
- 以前也有人和你的想法一样，嘎嘎用，用超了100多G，十几刀，实际上就是套餐内双向，超出套餐单向，当然你要不信邪那就超出后接着用，等下个月账单

- 套餐内双向，超了额外扣你钱的才是单向

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
# discuss-vendor-lightlayer
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [搜vmrack 、lightlayer美西干净落地 _202605](https://www.nodeseek.com/post-715537-1)
- lightlayer的建议收。理由
  - 1. 随时可以跑满 即便高峰期。
  - 2. 用jp的拉lightlayer落地机 一样可以达到gsl级别的延迟和速度。
  - 我实测用claw jp拉lightlayer的落地。可到700+延迟可以做到175上下（川）

# discuss-vendor-面包云
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [【面包云5折放货了】Breadcloud US 5折 12刀 有货了 _202607](https://www.nodeseek.com/post-815348-1)
- 前阵子被D了，涨价到了2刀/月。这是5折 12刀年付。
一个月6块8毛的落地 美国原生IP 全绿解锁 互联优秀 G口跑满， 可走JP GSL，延时105ms。
套大妈瓦工美西也可以，IP锁区 不送中。6块8，还要什么自行车。

- 不被打还是顶尖的 以前玩过jp，iperf3拉满3g口

- ## [新商家【面包云】的瓜，我看明白了，总结就是鸡圈不大，创造神话 _202604](https://www.nodeseek.com/post-691784-1)
  - 新商家销售策略没搞好，18刀一年定价，然后没几天出了36刀三年；
  - 买的人少，只能在加力度，上优惠。难免会触动老玩家权益

- ## [面包云的国际互联重传这么高还是落地好鸡？ _202608](https://www.nodeseek.com/post-870296-1)
- 落地好只是因为满血GSL把，这两天烂完了

- 不算好鸡，时不时维护和重启挺难受的，就这段时间就已经很多次了。

- 之前TCP优化一下就行，能个位数重传。但是他家不稳定，有时候就是拉不上去

- 重传高就是国际互联丢包严重吧？就是和线路机直连传输丢包严重的意思吧？

- ## [面包云疑似彻底陨落了 _202609](https://www.nodeseek.com/post-924696-1)
  - 继减配，涨价，升级母鸡把数据搞丢后，面包云老板再把原本的attv6给砍了，现在出了个抽象的attv6套餐，感觉是马上要跑路了
- nat小鸡从不靠谱，本来就是偷偷搞的，一查就封
- nat默认灵车吧

- push还要2刀，就是故意不让人活的，就当花钱买教训，他这样就算v4再干净我也不敢用来落地ai了
  - 貌似要先冲$10才能有资格$2去push

- 还有个aether不知道什么时候也这样
  - 那个我在用。。至少现在看来老板还算靠谱。。。只是清退了完全赔钱的hk。。至少现在看下去是真的想搞下去

- ## [现在的面包云的attv6什么情况了 _202609](https://www.nodeseek.com/post-931879-1)
  - attv6还能用吗，怎么出了一个att的套餐，之前的不给用了吗，100g的流量？
- 之前的被砍了
- 就是纯att流量单独作为一个产品，然后美国的小鸡取消了免费att

- 吞了，现在要单独买

- ## [面包云US的ATT IPv6是要另外申请的吗？ _202608](https://www.nodeseek.com/post-879835-1)
- 脚本申请，自动审核，等个几十分钟就行了

- ## [有人用面包云的att吗 _202610](https://www.nodeseek.com/post-969042-1)
  - 12刀纯ipv6 100g流量款，不懂落地用ai行不行，原来买的us bite款IP变得太脏了
  - 原来12刀的彻底废了，老板说换IP感觉也是画饼

- ## [面包云做落地机房属性影响大吗 _202606](https://www.nodeseek.com/post-780864-1)
- 还有比Breadcloud JP CPU 内存 硬盘更猛的鸡吗？IP还干净，国际互联跑满5Gbps，这种落地机堪称完美啊。 拿家宽比的，最起码家宽速度比不过，硬件配置差。

# discuss-vendor-raksmart
- ## 

- ## 

- ## 

- ## 

- ## [【慢讯】raksmart 已添加对 breadcloud 的线路支持 _202609](https://www.nodeseek.com/post-915034-1)
Bread → Raksmart	Bread → GTT/nLayer → PCCW → Raksmart
Raksmart → Bread	Raksmart → Twelve99 → Cogent → Bread

- 有人问了客服 结果第二天rak这边主动加了线路支持
  - 之前居然要饶港

- ## [[NQ]Raksmart活动2刀硅谷SV 国际bgp和大陆优化vip对比 _202608](https://www.nodeseek.com/post-852834-1)
  - 当时买了bgp尝鲜，后面中奖选了大陆优化vip
  - 同样的2刀，大陆优化放货好像更少点
  - 大陆优化vip好像好点，国际bgp测nq时失联了两次 

- ## [raksmart灵不灵 _202609](https://www.nodeseek.com/post-912907-1)
- 有波动 值这个价反正
40刀年付 280都不到的价格 k系299一共500g双向流量 dmit得50刀 这价40刀没啥好说的 便宜就完事了 线路也还行吧 有波动但是不大 体感不出来 口子跑不满不管是打流还是测速都跑不满 大概就是800多和lightlayer的sjc差不多 但是我说实话这个价格真的没啥好说的 就是便宜啊 但是我不推荐你年付 还是买个月付玩玩好了 万一别家做活动了也好快速解套 这家只能说目前性价比 但是确实挺一般

- 精品CN2是单程的CN2，国内除了移动去程CMIN2，其他俩都是普通线路。上传超级慢，5-10M，根本跑不动
但是他40刀一年，便宜一半线路也砍半，那很正常。。。

- 灵，不敢买，不过性价比确实高，3刀3T流量的4837，4刀1T流量的cn2gia
- 这家老商家，我觉得他和灵可能不太沾边
但是机器体验，还有站点后台管理连灵车oneman都比不了
最近也就4837表现比较抢眼开始有点讨论热度

- 不想说了 一堆问题没解决呢
广播风暴也还没解决 https://www.nodeseek.com/post-908432-1
内网网卡流量也在计费 https://www.nodeseek.com/post-911341-1

感觉他们的技术好像很烂 客服也只是传话筒 ，只会说帮忙反馈
还有很蠢的一点是 他家的用量统计 24小时才更新一次 。。。。

也就线路还不错 性价比高

- 这个问题都存在几年了都没解决 也别指望会解决了

- 你说他灵吧2011年成立的，可能灵15年了

- 这家烂, 但是不灵. 哈哈

- 我群里很多小伙伴买了目前都满意，虽然以前口碑有点问题ns所以风评不好，抛开一切不谈，一群友反馈，目前真实体验很好

- 月付就完了，随时跳车
- 建议月付，反正便宜，拿手里等大妈瓦工放特价就行

- ## [【已出】总价6r出 raksmart SV 圣何塞 大陆优化 VIP 5G口+1T流量 一只被低估的4837 高峰跑满500M _202609](https://www.nodeseek.com/post-906499-1)
  - SV （圣何塞）1核心，1G内存，50G HDD，大陆优化 VIP，带宽5G，1T流量；秒杀价：$ 1.99
  - 这鸡是真不错，但商家我不评论，论坛里全部是不太好的评价，但鸡是真不错，不管是nq、tq，还是日常使用，那都是妥妥的一线4837，高峰实际使用随便跑满500口子，这价格月付才1.99，十来块钱，我是鸡太多才出的

- 这家是不是只有sjc能用？第一次看到5g口的4837

- 同款，但是，送中太恶心了，拉回一次送一次。

- ## [结论：raksmart是国人且oneman 但是性价比很高 闲着无聊的可以试试 _202511](https://www.nodeseek.com/post-503430-1)
Intel的CPU 1核心1G内存50G硬盘
财务是魔方财务 之前的netjett也是魔方财务
财务这方面 我可以一眼丁真 0.1秒就可以识别是什么财务
所以99.9999%是国人开的
主控也一定是魔方云 （因为没有人会sb到用魔方财务+非魔方云主控，配合简直是狗屎中的狗屎）
其实用魔方系列产品没什么问题 但是从财务的选择上
魔方V10还是魔方财务 就可以看出商家的实力
比如物语云/Zouter.io 用的就是魔方V10魔改版 没点实力改不了
然后看RAKsmart 用的都是魔方财务 其实也改了，改了个首页 鼠标点三下就可以了

然后看产品
1.88刀一年大部分人是1刀一年， 线路和IO都对得起价格
只要看在线率 有99%的SLA都可以

- 财务不是一眼WHMCS...billing.raksmart.com/whmcs/clientarea.php
  - 不是whmcs vps控制界面是魔方财务 可能就是官网注册+付款结算是WHMCS 但是控制vps的页面绝对是魔方财务

- 这家搞了很多年了 没用过vps 以前用过杜甫 网络一塌糊涂 ping的线路跟tcp线路不一样

- 这家干挺久了 应该也不是oneman了
但是垃圾是真的垃圾

- ## [raksmart的cn2能上吗 _202609](https://www.nodeseek.com/post-942729-1)
- 月付呗，反正不贵。出问题丢了就是

- 半程CN2，去程是163普通，看你需求吧。然后价格也是双程的一半

- 4837用着咋样啊，移动电信高峰期爽用吗？，我用的cn2，西南延迟太高了200多ms，听说4837直一点
  - 一般，除了量大便宜

- ## [raksmart 137.175段 送中 _202609](https://www.nodeseek.com/post-951929-1)
  - 只能打开google.com.hk
  - 我现在在往回拉看看能不能拉回
- 我的4837上周刚拉回来，结果这周又被送中了，麻了

- 我的是Gemini送了，google没送，好像每个段的邻居习惯是不一样的

- 我下午买的2.99刀和3.99刀，整好4837转发CN2，一看给我送中了

- [Raksmart CN2 晚高峰再测 _202609](https://www.nodeseek.com/post-943119-1)
  - 这🐔别说还真可以，就是前段时候送中，这两天才拉回来。
- 回程速度的确不错，就是去程是163

- ## [【TQ】晚高峰 raksmart 4837 2c4g 1.99刀 _202609](https://www.nodeseek.com/post-955764-1)
- 浙江电信延迟这么低

- 这广东是真快乐啊。。最近好像看起来还挺稳的

- 月付款1.99，年付没优惠呢？
  - 年付 $19.9

- ## [【已收】raksmart 4837 2C4G 1.99 _202609](https://www.nodeseek.com/post-954503-1)
  - 溢价30元收一台，真有大家说的那么好吗，收一台摸一摸
- 这只是4837线路，你不会是要拿去碰瓷顶级线路吧

- 用来放claude code
  - 那可以，不过是机械硬盘，而且ip很脏。你最好配个落地

- 直接收2.99还有3T流量

- ## [很想了解下Raksmart这家产商 为啥不受MJJ待见 _202310](https://www.nodeseek.com/post-27202-1)
- 性能炒鸡拉垮 超兽严重
就这样买过一次，贼垃圾而且价格也没什么性价比，比如RN，吊打他

- icmp优化大师：ICMP走CN2，其它都是普通线路（现在大家都知道了也就没这么搞了
网络糟糕：100mbps在高峰期经常5mbps都跑不到。

- 那cn2就是骗小白的，就只有icmp流量走cn2，tcp啥的全是垃圾路线

- ## [Raksmart能够长期用么，黑五会有更性价比的三网优化么，TQ留档 _202609](https://www.nodeseek.com/post-925987-1)

- 现在都已经超售成灰了
- 超售到影响带宽，还买吗

- 超兽 半程cn2

- 超售之王，一半价格，线路也是只给了一半，去程都是普通线路。

- 目前我的之前能200m，现在只能50m了带宽，这不如4837的啥了快
  - 我也是，用ai帮我看了下，说是超售的问题，口子是G口没问题
- 我口子开始可以跑1g，现在对打la的机子只有500，然后代理测速只有50了

- 这家不太稳定，长期用的话还是换一家吧

- 4837那个1.99的可以玩玩

- 到期跑吧，超售到影响性能的商家也是很少见了。尤其4837的机器，cn2还在一直卖也快了

- ## [raksmart这家线路是最近优化过了吗 _202609](https://www.nodeseek.com/post-908857-1)
  - 他家大陆优化线路（4837）以前那个丢包平峰期都高到不堪入目，刚才看论坛里的晚高峰nq丢包现在能到0
  - 可能是以前去程有问题，我是一个月前直接挂itdog上测的，现在去程也不怎么丢包了
- 目前使用情况比我小秘书sjc还要好

- 4837并非优化，直连而已，联通的优化是10099/9929

- 对了，这家疑似和CSTSERVER也有关系，cst和这家的好多服务器测试ip都一样， 卖的线路高度重合

- ## [使用Raksmart 2天不到，遇到的7个问题 _202609](https://www.nodeseek.com/post-911449-1)
工单技术说，无法添加内网，必须在创建订单的时候勾选，只能退款重新下单，属于技术难题；
刚下单，遇到这个问题，没1分钟，退款到余额重新下单，还扣手续费？？？(下单才几分钟，由于他们技术原因，我不得不退款重新买，还扣这钱。太没格局)
工单技术说只有物理机能加v6，加不了v6, 销售说 是大陆优化就能加v6.？？？听谁的？
后台流量统计太迟滞，一天一更新；
管理后台，一言难尽，特别在手机上。。。
网站明确说内网不计费，但是流量双向计费。。。
工单技术不太聪明的样子，沟通困难。。。
更多问题，敬请期待。。。
我说我用的是内网 内网 内网 一台入站 40GB 通过内网从另一台出站。流量统计不太对。内网不应该统计。客服跟我鬼扯，不知所云。说后台统计显示80GB正常的。

后面如果 切线路 丢数据 也不意外了

- 👷: 首先，感谢你反馈的问题，我也在积极协调去优化解决，包括IPv6应用的VPS产品上，流量统计更新频率，以及组内网的问题；你反馈的问题也真实存在，但是退款到账户余额是没有手续费的，其他渠道会有接口费，也不是我们收的，望理解，有问题反馈，我也会积极推进解决。

- 商家居然还在论坛里呢？想问问你们，现在看到有些群里传小道消息，说后期你们会切线路，就是3.99月付那一款，现在论坛里的坛友们都购买了很多，看到群里说也都买了不少，希望你们后期别将CN2的线路给切换成普通线路，要不然我们都是月付购买的，后续切换成普通线路那我们可就全都不续费了哈！ 说句实在话，你们这次3.99月付CN2 1T流量的这个现在来说性价比很高，因为其他的三网优化的线路，现在都溢价，很贵，希望你们能稳住，后期不切线路，客服态度好，线路也稳定，这样你们商家的口碑自然会上来，不用你们打广告，我们都会帮你们打，如果不稳定，那再便宜，再优惠，论坛里很多人都喷你们，那最终也是会丢失掉一大批客户。
  - 👷: 这都是哪来的消息啊？我目前没收到你所说的切换线路的消息。精品CN2是新上的的线路，整体性价比还可以，值钱只开放带宽计费，现在是按流量计费，只要流量能限制住，不纯在切换线路的情况。
- 不会吧，那年付的不得血亏，月付的可以直接跑，如果这么搞，以后谁敢买他家的线路机。
- 给你搞成大小包，到时候mmp

- 他家后台流量使用量 需要一天多才更新

- 口碑差岂是浪得虚名

- 这家运维很灾难，我也就留个4837玩玩了
yysy，4837口子真的大，轻松跑满本地

- 哈哈 客服只能处理 退款和更换ip这种简单问题
一遇到难的问题就会说 帮忙反馈 然后没后续了

- ## 🤔 [【总结】raksmart月付还剩1个多礼拜，总结下问题请坛友自行判别是否续费。 _202609](https://www.nodeseek.com/post-941603-1)
已解决：
1. 有些机器开起来会有bug：比如ssh连不上 ，电信全部ping不通，github拉取不了，貌似是ip问题 发工单更换新ip就能解决。
2. ARP泛洪问题：持续收到大量的入站背景流量（约 60 KB/s），网络数据包密度高达 900 ~ 1000 pps。
3. 内网计费的问题：现在我的后台内网已经不计费了， 2026.9.29官方已经明确修复了
4. 官网的用量统计：之前为24小时更新一次。现在并非24小时才更新一次了 ，但是问官方说还在优化中，我也不清楚多久更新一次。
5. CPU跑分很低，超售问题：当前已恢复正常水平，详情看下面坛友晚高峰NQ。
6. 有坛友说到的 内网网卡貌似跑不满1G口子 发工单找客服已解决。

正在解决：
1. 说是之后会优化开完机之后也能开启内网功能。

总结：
内网计费和用量统计时间的问题：虽然后台已经有所修复，但是客服还不能给出解决问题的答复，只是说还在持续优化中。

最划算的玩法应该是 2.99的4837和3.99的CN2组内网玩法：
3.99 1T流量的CN2线路和2.99 3T流量的4837内网之间不计费，相当于你将获得2T CN2双向流量+2T 4837双向流量。
！！！记得购买的时候要勾选内网选项，当前购买之后无法再添加内网网卡。

他家的CN2比瓦工和大妈的延迟高10来ms
但是晚高峰速度没差 所以我也不在意

- 商家还是有在正面解决问题的，月付足以，现在4837性价比比他高的没几家
  - 如果只用CN2的确这样更便宜 ，只是1.99只有1T流量 加一美刀就有3T流量 ，所以我选择加一美刀

- 做个线路机还行吧
- 就当个线路机用，价格还好

- 5g带宽1g流量，我认为这是性价比最高的4837
- 4837很可以，用来爽看emby

- ip实在太脏了，IP2Location 99，IPQS 95，CF都要跳盾
  - 我会说我的瓦工和大妈 也这么脏 本身就是线路机 不在乎ip干净程度

- 说实话 我买了好几家4837用不出差距（云悠 matrix raksmart bestvm） 反正没啥差距 所以就留了一台性价比最高的。
至于论坛一直在炒的白丝， 溢价那么高 有这溢价的钱我不如去买CN2。。。
而且 299一年的续费价格。。。还是那句话 这么贵的4837我不如去买CN2

- 1.99刀的BGP是3T流量
  - 那是国际的 ，流量用不到。多余2T纯吃灰。这个多余2T的 4837至少还能跑的起来。

- 最划算的玩法应该是 1.99的BGP或4837和3.99的CN2组内网玩法

- 当前不代表未来，未来翻车的确实挺多例子了。当前溢价，未来打折的例子太多了。

- 2026.9.29工单 官方已经明确修复 内网流量统计问题了
至于流量统计更新还在优化中 依旧24小时更新

- ## [【NodeSeek福利】SV（硅谷）2核心，4G内存 大陆优化 VIP 秒杀$1.99，限量20台/周，抢完即止！ _202609](https://www.nodeseek.com/post-943813-1)
  - 经典款（每周一更新库存） SV（硅谷）2核心，4G内存，50G HDD，大陆优化 VIP，带宽5G，1T流量；续费同价，秒杀价：$1.99 
  - 每周一10点左右开放库存，自己留意一下，不用私信我，为了公平性，我也不会私信给大家具体时间。
  - 10点我开的库存，抢完了，我真没招了。这个机器价格我不能大量放库存。
  - 量小，只能等下周一开库存了。

- 别卖4837了.. 最近质量跟屎一样
  - 我真是没办法弄了，大家都想要这款低价，性价比高的产品，我争取到了一些，结果又不行了。

- ## [【NodeSeek福利】爆款云机，BGP 5G口/3T $1.99超低价限量秒杀，续费同价！！！ _202608](https://www.nodeseek.com/post-878338-1)
  - SV （圣何塞）1核心，1G内存，50G HDD，国际BGP，带宽5G，3T流量； 秒杀价：$ 1.99 
  - SV （圣何塞）1核心，1G内存，50G HDD，大陆优化 VIP，带宽5G，1T流量；秒杀价：$ 1.99

- 挺便宜的感觉跟dedirock差不多 这两家客服都挺快 但是这家很难说话

- [RakSmart特惠：新用户送$300代金券，全场65折，2核心，4G内存，大陆优化VIP/BGP 5G带宽，$1.99限量抢购！！！ _202607](https://www.nodeseek.com/post-843914-1)
  - 2核心 4G 50G HDD 大陆优化VIP 5G，1TB流量， $1.99
  - 2核心 4G 50G HDD 国际BGP 5G， 10TB流量， $1.99
  - SV （硅谷）VPS产品套餐：$1.99限量秒杀，每天限量20台，抢完即止

- [【NodeSeek福利】SV 2核心 4G内存，大陆优化/BGP 5G带宽 $1.99限量秒杀，续费同价！！！ _202607](https://www.nodeseek.com/post-831564-1)
  - SV （硅谷）2核心，4G内存，50G HDD，国际BGP，带宽5G，10T流量；续费同价，秒杀价：1.99
  - SV（硅谷）2核心，4G内存，50G HDD，大陆优化 VIP，带宽5G，1T流量；续费同价，秒杀价：1.99 

- ## 🚀 [RakSmart：新用户免费试用，全场65折，爆款云机$2.99秒杀！！ _202606](https://www.nodeseek.com/post-789397-1)
  - 如果机器存在问题，您可以工单反馈，我也可以第一时间解决。
- 啥新商家啊 这个都多少年了 ， 超兽怪， cpu 负载 长期40-100 ， 自己玩去吧 ssh都上不了

- 2011年的商家了 hostloc以前时不时都能看到 现在才跑来NS推广交商家订阅费 

- 之前开的一台，哪里都是拒绝连接，浪费钱，避雷
# discuss-vendor-hostdzire
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [近期最差服务商体验：HostDZire 两次沦陷、甩锅用户与毫无底线的私自停机 _202609](https://www.nodeseek.com/post-937638-1)
  - 此前我在评测他们自营印度机房的 AMD 7K62 机器时，就曾明确提醒过大家：*「此次的印度属于 HostDZire 自运营的，和 Leaseweb 无关，稳定性存疑……此外机器的虚拟化是VMware。
  - 从 8 月初宿主机集群全量被勒索导致数据彻底灭失，到 9 月 8 日自营 VPS 再次大面积失守被黑客植入 Xboard 节点与 root 后门并全盘甩锅客户，再到 9 月 19 日无视通知内容、无预警私自拔线停机，甚至暴露出了 **「疑似私下使用控制台明文密码试探登录用户虚拟机」** 的行业大忌问题。
  - 我从来不认为价格和免责条款是商家无底线的理由
  - [近期最差服务商体验（续）：HostDZire 官方自认草台运维、TG群甩锅与光速踢人封口 _202609](https://www.nodeseek.com/post-938769-1)

- 盲猜到商家最后又会拿出销量说：只要价格低，总会有人买单

- 8月印度机房重建之后，我的机器一直被组播风暴灌流量进去，一个月能跑1000多G，反馈了一个多月到现在还没修复

- ## [HostDZire这是被黑了啊 _202608](https://www.nodeseek.com/post-858093-1)
  - 很抱歉通知您，我们的基础设施遭受了勒索软件攻击，影响了多个虚拟化节点。因此，一些VPS和独立服务器服务目前无法使用。

- 三哥租的上游leaseweb很稳，除了超售没有其他的缺点。三哥自营的咖喱鸡最近这几个月掉线频率相对较高。
- 阿三在美国没有自营业务，都是租的leaseweb。

- 卧槽。三哥这个国家不行。老是被黑进去。还能安全点吗。

- 小鸡访问不了了，得亏我昨天部署了一个tolaria 做了一套总结同步
# discuss-vendor-racknerd
- resources
  - [RackNerd | VPS Specials](https://www.racknerd.com/specials/)

- cons
  - 似乎不支持 backup: [How to Backup Your VPS: A Simple Guide to Getting Started — RackNerd _202409](https://blog.racknerd.com/how-to-backup-your-vps-a-simple-guide-to-getting-started/)

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [对比一下 RackNerd DC02 / DC03 / SJC | 晚高峰测速 | 国际互联 | 洛杉矶 / 圣何塞 | RN 详测 _202511](https://www.nodeseek.com/post-499338-1)
- CC家的DC1就跟RN的DC2一样.. 基本是一样的
CC的DC2就跟RN的DC3一样..

- dc03到上移我看到几个版本，有arelion，有cogent ，有lumen
  - 应该是动态路由 

- 只能说DC02联通用还行，但是晚高峰也还是会丢包跳ping，速度一般；而电信移动晚高峰很大概率用都用不了。纯代理用途建议买优化，比如DMIT LAX. EB. WEE或者搬瓦工什么的，三十几刀贵了点但是能保障晚高峰体验。

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

- ## [怀疑 DartNode 服务商侧初始密码泄露——我的两台 VPS 被挖矿了 _20260930](https://www.nodeseek.com/post-955971-1)
  - 我在 DartNode 两台美国的小鸡，一台 2 核 4G 拿来跑点服务，一台 1 核 1G 当落地出口，都是 Debian 12。前天开始，那台 1G 的面板 CPU 一直顶在 100%。
  - 登上去一看，有个进程占了 85% 的 CPU，命令行伪装成系统自带的登录服务（systemd-logind），但那文件有 8.2MB——正常才 281KB。不用想了，被换成门罗币挖矿程序（XMRig）了。挖矿配置藏在类似 .cache 的目录里伪装成缓存，矿池是 supportxmr。为了让程序反复复活，它还在 systemd 目录下面塞了个假的设备管理服务，开机自启、杀掉自动重拉。
  - 除了挖矿，这哥们还装了 Docker，跑了三个卖带宽的挂机容器（bitping、traffmonetizer、peer2profit），容器名全起了系统进程的名字。操作历史也被清掉了。
  - 两台机用的都是 16 位随机密码，字母数字混的，爆破不可能。但我把 SSH 日志翻了一遍，压根没有任何 Failed 记录——攻击者第一次连上来，密码直接就对了。更离谱的是两台是"连着"被登的：某天 14:23 进了 B 机，25 秒后（14:24）又从同一个 IP 进了 A 机。
  - 所以基本能断定，问题不在我这：DartNode 那边把账户下的机器清单和对应的 root 初始密码泄了（平台被拖库、面板被撞、或者收开通信的邮箱被入手，都有可能）。两台机的密码都是它开通时下发的。
- 入侵来源 IP：
  - 185.121.108.3（乌克兰，AS43815 Nash Prostir LLC）
  - 103.29.127.12（孟加拉，AS38067 Radiant Communications）
  - 108.165.12.55（与受害机同机房的内网段）
  - 104.28.205.19 / 104.28.237.19（Cloudflare WARP 共享出口，仅作参考）

- 离谱，挖矿还偷偷挂机，系统直接重装得了

- 
- 
- 
- 
- 
- 
- 
- 
- 

- ## [My Disappointing Experience with DartNode VPS: A Cautionary Tale — LowEndTalk _202510](https://lowendtalk.com/discussion/210302/my-disappointing-experience-with-dartnode-vps-a-cautionary-tale)
  - When I attempted to restore from backup, I discovered that none of my backups were functioning properly. Despite having three different backup points available, not a single one would boot successfully after restoration. The restore process would complete, but whatever was being restored simply wouldn't start.
  - The restoration process was painfully slow, and ultimately unsuccessful.
  - The fact that multiple backups failed to restore properly raises serious questions about their backup system's reliability. What good are backups if they don't work when you need them?

# discuss-vendor-zgo
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [🔥ZgoCloud 上新洛杉矶三网精品线路机（CN2GIA CMIN2 9929）AMD EPYC 7002+ 美国原生 IP + NVMe SSD 测评 _202604](https://www.nodeseek.com/post-671000-1)
- zgo没有udp，买个便宜的落地还行

- 这家对CPU的限制相当严厉，我在群里见过一个老哥说，装个宝塔会触发限制自动关机。

- 不如vmiss，一样的小口子少流量，但至少vmiss上游好一点

- 我去，是netlab，我们完蛋了

- ## [ZgoCloud LA三网优化机器测评：IP质量不错，但性价较低，网络质量堪忧 _202602](https://www.nodeseek.com/post-618765-1)
  - AMD VPS-Specials-Starter 产品，定位为中国优化线路+性能机器，实测下来表现比较糟糕，断流较为严重。先说说网络方面，电信9929，联通则是按照地区不同走9929/CMIN2/4837不等，移动走CMIN2，因为注意到上游为kurun机房，所以特地分了闲时和晚高峰进行测试，晚高峰会比闲时普遍增加30ms左右的延时，且去程丢包比较严重，电信部分地区丢包到无法使用的程度，联通部分地区轻微丢包，移动地区大部分地区轻微丢包
- 它家的hy2跑不动的，不用想了，限制udp

- zgo比较少看到溢价的

- 我之前还挺想买，但感觉二手市场都不太行
  - 你还挺精的，凡是二手市场都不认可的鸡肯定有些地方不尽人意。目前还持有这家的鸡，等哪天不用了再评价，其实多翻翻老帖都说过

- 这家很垃圾，Kurun系列的，都很垃圾

- 后悔没早看到，垃圾的很
# discuss-vendor-vmrack
- ## 

- ## 

- ## 

- ## 

- ## [vmrack 的L3机子和大妈 搬瓦工的vps对比如何? _202604](https://www.nodeseek.com/post-696808-1)
  - 先说结论，VMRack机器的IP质量和解锁都挺好，线路的话只建议买L3级别产品，落地的话只建议L2、L1（其中L1只能拿来做落地用，直连有点费劲）

- IP和硬件比搬瓦工好，其他不如瓦工。VMRack是500Mbps的口子，瓦工DC99是1Gbps，DC1/6/9是2.5Gbps的口子。DC99是CN2GIA+CMIN2，VMRack是三网各自优化，而且瓦工大妈现在买不到，短期内补货希望也不大，只有VMRack能每周都能买到。

- 没法比，差不多同等价格瓦工和大妈的流量都是vmrack的2倍以上。品牌的口碑也没法比。有这俩的特价款没其它厂商的事。

- 一品牌口碑
二稳定情况
三长期持有
三方面来对比 VMRack还得考察

- ## [【测评/避雷？】Vmrack L2. VPS.1C1G. Base 三网优化 _202603](https://www.nodeseek.com/post-635859-1)
  - 今天看见Vmrack，刚好缺个流量稍大的有点线路的机子做反代，看见有个所谓三网回程10099的三网优化款，但是在论坛里找不到一个完全一点的测试，因为毕竟已经是低信誉商家了。想了想还是购入了，因为以前用过他家三网精品，感觉质量还可以，但是这次确实是踩雷了，就发个稍微完全点的测试说明下避雷。原先预想可能稍微差点，20~30Mbps晚高峰我也能接受，结果……
  - 本帖仅说明避雷Vmrack三网优化系列 即所谓去程163/10099/CMI 三网回程10099款，小包10099，大包隐藏，实际不知
  - 实测晚高峰期间三网TCP可用率极低，且有断流现象发生，说实话感觉不如国际T1，而且性能表现也一般不惊艳
  - 后记：甚至感觉不如RN和CC，感觉相差也不大了。想你了，家人云，为什么在我买后20分钟出了20刀Netlab，想上灵车了
  - 看他们退款政策，好像只支持退款到余额，还要扣除支付网关费用那些的...

- 我和楼主一模一样，精品4刀持有中，200M可跑满
想买个优化来反代
结果上海联通晚上单线程50Mbps
RN都能200Mbps单线程

- 楼主你这款好像不是三网回程精品款，像是他们家的三网回程优化款，全走4837
  - 对的对的，我标了是L2，三网优化款。美国版的软银，白天猛晚上拉

- 国际线路10099，过关进国内4837，不是9929，那丢包率不敢想，还不如家人云frm效果。

- 他家刚出的时候，我买了L2，当时晚高峰酷酷的能轻松跑满200Mbps，而且基本三网平。后来半个月不到，就“维护”了一次，三网不直了，且偶有断联，但速度也轻松能上100Mbps。

现在L2看起来是彻底的拉了。

另外冷知识，bwg的dc9好像晚上比白天更好一些，justmysocks的hk cmi套餐也是晚上更好用。

- ## [📍都在说VMRack好，我来看看怎么个事 | 测评 L1 L2 L3三条线路机器，果然L3机器确实很赞，没什么库存，购买靠抢（文末有抢机器的方法） _202604](https://www.nodeseek.com/post-695952-1)
- 今年高企的硬件价格，让搬瓦工/DMIT都不再投入资源，守着现金；再加上国内环境变化，海外IDC厂家各个都惜售手里的产品，小厂家也借机推出自己的产品，个个都卖爆了
- 先说结论，VMRack机器的IP质量和解锁都挺好，线路的话只建议买L3级别产品，落地的话只建议L2、L1（其中L1只能拿来做落地用，直连有点费劲）
- 3个级别分别是L3三网精品 L2三网优化 L1美国原生
  - L3三网精品是优化线路机器，三网各自优化，IPv4-电信CN2GIA 联通9929 移动CMIN2 无IPv6
  - L2三网优化是没有优化完全的机器，IPv4-电信163 联通10099 移动CMI 无IPv6
  - L1美国原生，无优化线路，IPv4-普通线路 无IPv6
- 最后说一下，值得买的是L3，特价款最值得买了，但经常缺货
引用论坛某位资深大佬的话是，vmrack每周一早上9点-10点会小批量放货，放货之前登录账号，点击购买，多点几次支付就能抢到
另外，根据祖训，大家抢特价机之前，一定要注册好账号，务必做到一号一机！ 
可千万不要一号多机，玩够了难以出手。一号一机非常容易出手。按现在的硬件趋势，未来这个特价机还会溢价，买到L3低配特价机就是赚到

- 更正一下，不是每周一，是最后一个周一了，这个月底活动结束

- 线路再好也不上低信誉商家
# discuss-vendor-白丝云/咸鱼云/akko/moe
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [4837的鸡只有白丝云和其他？ _202610](https://www.nodeseek.com/post-967235-1)
  - 4837的鸡只有白丝云和其他，我咋就这么不信呢，曾经用过一个月，停机三次，延迟确实比我瓦工的4837低10ms，但是丢包比瓦工要高，难道是利于炒鸡才这样讲的？
- 再强他也就只是个4837啊
- 4837终究是4837 只是比其他的4837好那么一些

- 没用过，想体验也难体验。看到去程是精品线，这确实在大流量里很独一份，做直播可能适合，或者上传数据多。

- 河南电信 日用 感受不到和vmiss tri的区别 下载东西的时候比tri快 晚高峰更快

- 没用过白丝4837。但我感觉他不管怎么优化，物理线路的限制摆在那啊。。
4837可能闲时大口子和瞬时峰值都比9929等更高，但丢包抖动、qos等依然是9929更稳。

- ## [呜呜, 仔细看了下白丝对比我的咸鱼 _202606](https://www.nodeseek.com/post-756572-1)
  - 好爽啊 白丝的160一年 性价比拉满了啊
  - 9929的也才240 呜呜呜呜呜
  - 好想买一台 本来都准备上床了的 给我整应激了
- 白丝160不是9929，240才是，主要是很难买到，而且闲鱼流量大口子大啊，翻倍了

- 不是这样比的啊 你也要看配置和流量多少啊

- k系不扩容，卖完了就是卖完了

- 这两款我都有，160的是三网各自精品去程，三网4837回程，但这个4837很顶
高峰期只有延迟明显增加，丢包基本与精品类似，比某vm的L2强的离谱

- akko他家最近带宽升级了1gbps。不过综合来看还是咸鱼云更好，工单更快

- 主要闲鱼的美西86刀真有点富贵了，这个价格都赶上咱们刘总的jp了（虽然小刘拉了）

- vmiss说实话只有tri值得买，9929感觉现在有点超兽，之前买了一台还算稳，不过有大小包问题
- vmiss口子小，挨打容易断流。不过他家段比较多，不一定都会顾及所有段。他家的tri还是不错的。

- ## [akko和咸鱼云的德国优化线路是不是同一上游的？ _202604](https://www.nodeseek.com/post-677547-1)
- akko那方面不行？
机器跑分
稳定性
售后服务
都不如咸鱼

- 咸鱼比其它的都贵 但是确实非常牛

- ## [akko 与 moe 是不是同一商家，产品安排策略很诡异 _202610](https://www.nodeseek.com/post-967614-1)
akko 500g 299；
moe 500g 349r；
akko 800g 449r；
moe 1000g 509r。
akko 1200g 699r；

- 不一定是同一家 但母鸡可能是同一台 

- 几乎可能就是一个老板，都是oneman，工单都慢的要死

- ## [akko官网恢复了 _202608](https://www.nodeseek.com/post-875653-1)
- 官网掉线是被ddos了吧，群组禁烟是因为被ddos群里就会有些不和谐的声音

- 群没解散，只是清空历史消息+禁言
官网每次被打都会炸

- 经历过面包云的各种操作，国人oneman idc的各种操作我都习惯了 

- ## [Akko是真的好用啊家人们 _202412](https://www.nodeseek.com/post-223938-1)
  - 咸鱼云的流量虽然多但是带宽略微小了点，买来用有点浪费了，又用不上那么多流量，发现Akko家流量减少了些，但是对我来说刚好够用，季付也特别省钱划算，据说商家也是老二刺猿了，这下不得不买了。

- 这家服务是kirino三家里最拉跨的了
- kirino三家你就认准咸鱼吧 贵点贵点 售后及时
  - 其实咸鱼反而是最便宜的 因为有活动款 白丝和akko都没有那种活动款

- 咸鱼服务好一点
白丝和akko都感觉很佛系

- 白丝和akko貌似是一个人开的两个站 (网关都用的同一个) 从去年基本都不怎么管了，回工单都是随机看心情回，有时候几个小时，有时候得几天。估计就是业余看一下的状态，平时的注意力不在做这个上面。 咸鱼老板是真的好，做什么事态度都很正式很负责，我有个机器好几年了，一直用的很舒心

- akko是国人oneman吗
  - 是的吧，国外也没这么垃圾的了
- 老板比较佛系哈哈，我用过，机子还算稳，服务一般

- 这同线路的就咸鱼云服务好
- 是的，咸鱼云白丝云akko三个德鸡好像是同一个上游，但是白丝云和akko都很多人说工单慢

- 記得前年買過，那時都是自動開通的，老闆日常在 TG 群潛水（玩游戲），佛性處理工單

- 论松弛感，还得是欧洲，我之前葡萄牙小鸡的工单居然一年后才回复

- 
- 
- 

- ## [akko口碑到底怎么样 _202609](https://www.nodeseek.com/post-908959-1)
  - 年付+不予退款，如果是当自用鸡鸡怎么样
  - 主要是用购前工单咨询过客服，问个换ip的事情拖了4h才回，有没有自用的mjj说一下
- 只说机器本身的话，它家德国 Mini (299) 挺好，推荐～
工单这个就不好说了，那是跟不上 GreenCloud、VMISS、DMIT 这些。

- 工单比较慢 其他k系四个都差不多

- 想起来akko好像是以前 昱格云 的员工，昱格云 因为合伙纠纷倒闭了，akko离开后另立门户。
19年 20年的事情了吧。当时我在 昱格云 还有好几个小鸡。

- 他家没什么太大问题，反正中规中矩吧。但记得跟 ACCK区分。

- kirino几个下游线路表现都差不多的，要炸一起炸，补偿一起补偿

- K系四兄弟
咸鱼
AKKO
MOE
白丝

个人体感是 咸鱼>AKKO>白丝>MOE

目前持有AKKO SJC和白丝4837 都算好鸡
不挨打 线路不抽风的时候 体验都算美西第一梯队 非常好

- 老商家+kirino的线路，目前看着没什么问题，是个不错的选择

- 他家的SJC目前是我认为最厉害的线路之一。起步速度100Mbits

- ## [绿云，白丝云，咸鱼云，zouter， 这几家有哪些强项优化线路？ _202604](https://www.nodeseek.com/post-677230-1)
- 白丝，咸鱼任意款都是同级强项

- 绿云的日本gen2强
咸鱼和白丝感觉是美西和欧洲方向
zouter是移动快乐机吧 

- 白丝和咸鱼的线路都很好，晚高峰杠杠的 

- ## [白丝云cloudsilk家的美西圣何塞是9929好用还是用4837？ _202403](https://www.nodeseek.com/post-79476-1)
  - 白丝云的美西9929是不是比4837更屌更好用？

- 那肯定是9929，本身9929就是联通vip线路，4837只算优化

- 都是在收 9929 的，4837 收的人少

- 经常大宽带下载选斯巴达的西雅图4837，稳定，带宽足，其它商家的4837多少有点毛病。9929 都差不多，带宽不够大，超兽的多。

- ## [白丝云 cloudsilk很顶吗，4837的 _202608](https://www.nodeseek.com/post-888121-1)
- 这也是没想到的，居然现在美西4837都有人抢 放以前都没人要吧
  - 不一定，阿里的hk也是163 4837，但是顶尖
- 美西和hk不能这样比吧

- 去程精品，回程4837

- 4837其实不差。主要是看商家是不是给超售太多了。一般这个线路就比CN2延迟高30-50ms，普通用户基本感觉不出来

- 年付299款普遍溢价50r左右，159款溢价基本80+

- 年付127.99的现在多少钱啊：美国-大陆优化BGP-套餐A，美国圣何塞-大陆优化BGP（4837）流量800G
  - 128款溢价都到天上去了，159款的还稍微好收一点，159的年付和128的套餐是一样的，然后159款的溢价是大概100r左右。128r的不好收不知道多少钱了，可能两三百起步

- ## [口子小的三网优化可能真不如白丝云4837 _202610](https://www.nodeseek.com/post-960405-1)
  - 年付128 月800g流量 性价比不比vmiss差啊
  - 我是河南电信 晚高峰也有200多
  - 我的8折vmiss tri basic感觉可以卖了
- 晚上再试，现在不拥挤

- 能跑，晚上延迟比其他两家飘得高而已，但依然不丢包

- 4837 永远不可能和9929或者三网优化坐一桌

- 丢包率和延迟比我之前的大妈还低, 18天内平均丢包率不到0.1%, 延迟几乎没波动, 晚高峰也一样.

- ## [白丝云这个能冲？回程4837 _202609](https://www.nodeseek.com/post-955392-1)
  - 回程三网4837，去程三网各自精品
- 去程精品没卵用，实际体验还是回程决定
- 关键看回程 你在国内下载吃的是回程 4837晚高峰基本都掉速 标的2560M别当真
去程精品只管上传和ping好看 所以买之前找他要测试ip 晚上8-11点用你自己宽带跑个单线程下载+mtr看回程丢包
899一年买的主要是8T流量 流量用不到这么多的话不如找回程也是9929/cmin2的

- 单ip配极大流量，跑不了多少流量就被嫱了，无论什么协议

- 上海选择性比较多，内地距离远，线路拥堵，体验还是有很大差距

- ## [详测及评价白丝云美西 SJC圣何塞（4837） _202606](https://www.nodeseek.com/post-761655-1)
  - 不错的备用机。去程各自精品，回程三网4837，在机荒年代算是不错的备用的选择吧。但指望晚高峰比各自优化强 纯有点扯了
  - 我这台IP纯净度及解锁尚佳但抽奖，目前我已有机器分185.148 和38.59段，后者会漂亮一些。这款机型老板原话是不打算在扩容了且挣不到啥钱。还是那句话，花多少钱就只能买到多少体验，商家tg群也以重新开放了，有问题可以直接找老板，

- ## [CloudSilk白丝云 美国圣何塞9929产品测评：三网表现都很不错 _202605](https://www.nodeseek.com/post-735685-1)
  - 美国圣何塞9929， 本次测评白丝云的精品大陆优化BGP产品，定位是三网优化线路机。
  - IP质量较差，广播IP，部分常规流媒体(Disney+/Netflix/Reddit)掉了，属于是典型的线路机IP质量，有相关IP需求可以套个落地

- ## [白丝云和咸鱼云4837一个上游吗 _202403](https://www.nodeseek.com/post-76406-1)
- 一个上游，咸鱼多回程一跳，这两天对比，白丝电信丢包高点0.3%，移动0.1%, 咸鱼联通0.1%，其他0。白丝最近偶尔会断流，高峰期延迟波动大些，电信移动飙到230，咸鱼好些飙200，平时180-190左右

- ## [白丝云和咸鱼云的上游是不是一家的 _202604](https://www.nodeseek.com/post-677808-1)
- 是吧，好像还有akko和moe

- 咸鱼云的de顶级

- 那欧洲咸鱼云与小秘书相比哪个更好呢，看着价钱都差不多
  - 咸鱼云
- 移动的话 v.ps 吧，便宜点。联通咸鱼好

- 开年费的话，好像咸鱼云9929好像更便宜一点
# discuss-vendor-vmiss
- ## 

- ## 

- ## 

- ## 

- ## [vmiss US LA TRI和TRI DC2有什么区别 _202610](https://www.nodeseek.com/post-964992-1)
- tri上游是zont，tri dc2上游是netlab，不过老板说后续dc2可能也会搬去zont
- DC2 是kurun，流量比DC1少100G，老板自己调的，目前感觉在使用上木有什么差别

- 上游不同 流量dc2少100G

- netlab 最近老挨打

- dc2 电信容易跳163

- ## [VMISS LA. TRI. Basic 是不是也属于传家宝了 _202608](https://www.nodeseek.com/post-892670-1)
  - 一年45cad折合人民币218元, 溢价150左右
  - 500g双向 200兆带宽，个人不追求极致，应该也可以归属于传家宝档位了吧

- 总有人喜欢拿限速200Mbps说事。对于绝大多数人来说了，这个带宽日常使用够用且能保证非常好的体验了。

其实，实际体验上，很多省份运营商们美西的单线程带宽上限给到的也就是200Mbps。而且这家IPv6也是优化线路。

然后，不到30刀一年。

我不知道还有哪家可以在同样的价格下提供接近的体验。

除了早期6折和8折的机器。机器的存量还是很大的，以后估计也是常有货。

这机器的存在不是为了当传家宝，但会让某些所谓的传家宝显得有点没那么传家宝了。

当然了，你要说给收藏家提供情绪价值，那某些传家宝还是有的。这点比不了。

- 算起来并不便宜，500G双向一年两百多，还限速200。

- 它得以后都不再放这样的货才能当传家宝，不过按照这个趋势也是有可能的，老板涨价后就再也没有4.5的价格了是真的。
- 才放货没几天的东西传什么家

- 这个鸡，我看探针下来，比dmit还要稳定。

- 去年前年 那时候 活动🐔多 价格也划算 眼下这个节骨眼 没办法 确实找不到 比vmiss更有性价比的🐔了

- 给200Mbps目的之一就是防止机场、测速党和拼车党进来搞坏个人用户的体验的。用心良苦。

- ## [vmiss的tri和cn2有什么区别？ _202610](https://www.nodeseek.com/post-961951-1)
  - 我看tri三网优化反而便宜了呢？cn2贵了的同时流量还少了？

- 三网各自和三网cn2
- cn2电信优化 tri三网优化

三网cn2gia
三网优化cn2gia 9929 cmin2

gia线路贵所以三网Cn2的机器比三网优化贵

- 三网更优，cn2 路由应该没差异

- 三网cn2gia绝对比三网各自优化贵，但实际体验三网cn2跨网拉得一逼，移动几乎不能用，电信的坑非要去踩哪只能说你小白活该被坑，就跟大妈的pro一样，移动联通还得用v6，流量也少了一半，仅仅多出一个cn2就得去为电信买单，毫无性价比，cn2线路太贵了，又被mjj吹得太神了，说三网cn2吊打三网各自优化的傻逼真的不在少数，移动联通走电信cn2专线你又没交过路费能上你好过吗？想想都不可能，三网除了4837兼容性较好，9929和cn2三网都是垃圾，说白了vmiss的三网cn2体验，还不如白丝的三网4837，vmiss只有电信顶尖，而白丝的三网综合体验会更好

- ## [VMISS的US. LA. TRI系列，洛杉矶两款三网优化的简易对比评测 _202512](https://www.nodeseek.com/post-532141-1)
  - 首先，我们把不带DC标记的称为DC1，以便于与DC2进行区分。
  - 我个人推荐是选择DC1，因为流量更多，更看好国际互联的GSL（当然也可能会更炸，压力都给到GSL了）。

- dc2的问题是上海（江苏）联通走的是4837，我也是这个原因换成了9929那款

- ## [话说 VMISS LAX TRI 两个机房的线路似乎差别还挺大 _202605](https://www.nodeseek.com/post-750257-1)
  - 感觉DC02的电信线路似乎要稳的多啊

- 应该是好点。要不然，不至于流量打了八折，价格和DC01一样。

- 上游不一样，tri是zont，dc2是kurun
- dc2是kurun
这个机房的兄弟有福了
跟netlab一桌的烂货

不过好像vmiss自己额外调试了

- dc1是zont，电信容量接近满载了，大概从一周前开始丢包持续在6%以上
dc2是kurun，老板自己调的，流量少100g

老板的tri-dc1扩容在等电信落地，扩容前估计电信都不好用

- 他们家dc2自己调的，应该比别的断流王好很多。不是所有netlab和kurun都断流，很多是商家超兽太多了

- > 著名超售上游，Zgo口碑差有一大半的原因出在kurun这，ip质量会出现几条家宽，三网延迟看着也不错，小白被坑二选一的经典产品
netlab和kurun 再怎么优化，上限摆在那里，谈不上优选, 
其实直接对照晚高峰的波动就明白了 dmit bwg稳如防御塔, 
其他的跳disco, 
这才是体现线路实力的真实表现

- 并不完全是真实情况其实。
这事取决于多方面:
商家实际找上游买了多少带宽, 
Kurun那边跑不起来其实不是带宽不足导致的，而是默认防火墙策略误杀严重，商家没有去找上游特调。
.....
有一说一很多事并不能完全怪上游，你可以在很多帖子里看到客户评价，我们家的netlab和kurun的网络基本是没有什么问题的。平心而论，在钱给够的情况下，kurun我先不好评价，但是netlab在我眼里算是服务和质量都很好的上游了的。

DC1的电信 上游那确实是带宽不足了，所以每天有时候带宽被占满的时候会出现问题，但不算太久。 上游一直在和电信进行扩容处理中，但是中国电信那边推进缓慢，一直在处理。 这事群里基本都知道，您可以加入我们的组群，关注下最新动态。 移动和联通没啥问题。
所以我们的DC1一直都没有再放货很久了，避免更多的客户对此造成误解。等中国电信扩容后才会放货。

- ## [VMISS 美国LAX-TRI产品 复测：性能+IP质量+三网优化 = 个人轻量单品 - LINUX DO _202607](https://linux.do/t/topic/2665086)
  - LAX TRI 产品，定位是三网优化线路机器
  - IPV4 三网双程各自顶级优化 (CN2GIA、9929、CMIN2)，IPV6 电信 [[163]] 联通 9929 移动 CMIN2 优化，比较可惜的是电信 IPV6 没有走 9929，优化并不算完整 (电信 IPV6 是没有事实上的 CN2GIA 的，所以一般走 9929 就是最好的选择了)，建议电信用户使用 IPV4 连接，联通移动用户可以选择 IPV4/IPV6 使用，优先使用 IPV4 连接。这里提一嘴教育网的情况，教育网不是很直，延时多在 230ms 左右，不过不丢包，对于教育网用户而言就是能用但不极致，推荐教育网用户去玩 HKIX。
- 为什么大多数人愿意溢价买 bwg 和 dmit 都不愿意便宜买 vmiss
  - 因为一直没货，就这么简单， 现在 basic 已经溢价 3 倍了
- vmiss 两年前一直在用，就是因为不稳，才弃了
- 去年买了一个，前几天放货想再买一台，结果限制单账号同类型只能一台

- vmiss 的美西确实可以，但是香港只能说是能用。不过人家也就那个价，没啥好说的。一直苦于找不到高性价比的香港优化

- 往年 DMIT 年黑五年付 50 刀，是比这个更高一些（性价比），但是今年机荒，不一定有什么好的优惠，也不一定能不能抢得到

- 东京美西都是好鸡，结果都完全买不到

- ## [有一说一vmiss晚高峰的时候比vmrack稳太多了 _202605](https://www.nodeseek.com/post-744220-1)
  - 同样是三网优化鸡

- vmrack基本每周炸，难绷。

- vmrack有点拉的 还好当时没有溢价收

- 是不是看地区，一线城市挺稳定

- ## [VMISS la tri 晚高峰怎么样 _202608](https://www.nodeseek.com/post-885142-1)
- 我的油管只能5w-10W DMIT也只能这个数

- 我的dmit也是只能10w以内

- 9929移动可以跑到16万以上 200端口 晚高峰

- 电信，西南10多W没问题

- ## [溢价135收vmiss US. LA. TRI. Basic _202606](https://www.nodeseek.com/post-767693-1)
- 八九折一个月只差2块钱，溢价60没必要

- 现在vmiss都是瓦工大妈的第一平替了，热度还没那么大不容易被重点关注。估计没人出，特别是basic都在自用吧，毕竟性价比那么高

- ## [我有个vmiss和dmit。这两个有啥区别啊。没感觉出来呢 _202609](https://www.nodeseek.com/post-906735-1)
  - vmiss溢价30收的，年付45刀。dmit溢价600多收的，年付40刀
- vmiss 年付不是45刀，是45加元，大概30刀吧

- vmiss流量少, 但是有时候下载感觉比dmit快, vmiss能跑到20兆每秒, dmit10兆左右
但是dmit流量超了 会有5兆的小水管
流量用的不多 vmiss感觉就够了
但是我现在主用dmit, 毕竟贵啊

- ## [美西线路机vmiss, dmit比较 _202608](https://www.nodeseek.com/post-888825-1)
- vmiss用户觉得它们差不多，dmit用户觉得它们差的远

- 抛开联通不讲，个人感觉vmiss还不如lightlayer，更别说与dmit相比了，谨记别买小秘书
- 电移，个人感觉，vmiss不如lightlayer

- 两台我都有，高峰期我觉得大妈稳一点，不过一台大妈能买两台tri了这点差距我能自适应

- 一个1G带宽，一个200M吧

- ## [VMISS的Tri Basic和DMIT的EB WEE简单对比 _202609](https://www.nodeseek.com/post-904034-1)
  - 这么看VMISS的Tri. Basic和DMIT的EB. Wee确实差不多，性价比挺高的，就是流量稍微少点，口子小点，简单对比一下，看个乐呵
  - 其他服务方面DMIT还是强很多的（服务，超量规则，换IP，不送中，V6优化等），VMISS长久稳定性有待验证，毕竟DMIT已经有口皆碑了，希望有更多的好商家好机子出现

- 还是不一样的，DMIT不会送中，ip墙了免费换

- ## [买🐔请教：DMIT EB 和 VMISS 9929 之类的实际差别大吗？ _202607](https://www.nodeseek.com/post-830592-1)
看双向路由都一样，联通走 9929、移动走 CMIN2，但价格差不少。

想问下差别主要在哪：晚高峰、丢包、速度、稳定性，还是 IP 质量和售后？实际体感明显吗？

还是说日常打开网页、刷视频、连接 SSH 时，体感其实差不多？

主要是联通使用，也会兼顾移动

- 浙江电信 用eb 和 pro感觉都一样，体感没啥差别

- 我建议先买vmiss用到黑五，大妈就算没有以往的折扣，他较之前贵个10刀，15刀总要做活动吧

vmiss我用过 jp的tr，晚高峰速度拉不起来，比不上大妈的pro和eb。拉不到10w

- 可能我这地方不太好，vm的会丢包，eb不丢，所以我就留了eb

- ## [美西Dmit和Vmiss到底差别在哪里 _202608](https://www.nodeseek.com/post-877064-1)
- 品牌影响力
配置
售后
稳定性
支付支持
退款政策

- Dmit确实大，有2Gbps

- 个人自用应该没什么区别，绝大多数人根本用不上美西的G口

1、国内很多地方去美西单线程就200Mbps限死的。你今天去浙江，明天去河南。用DMIT体验上相比vmiss没有任何优越性。vmiss就给了200Mbps的口子，刚好卡了这个点。
2、vmiss的v6也是优化线路
3、被打，去年底DMIT被干出屎的时候，vmiss正常用。
4、DMIT和BWG的IP段都是“很有知名度”的，所以，被干的时候也事先死。
看懂了上面这些。你再看看价格。

- 我感觉，除了口子，最大的区别是稳定性，两个都用过，vmiss的稳定性差点意思

- ## [错怪 DMIT 了，之前还说 DMIT 和 vmiss 没啥区别 _202610](https://www.nodeseek.com/post-956438-1)
  - 以前 VMISS 9929 不提供 IPv6，DMIT 默认会有一个 IPv6，迁移 xray 的时候忘记关闭 ipv6 出口了，导致重传率＞5% 了，关闭了以后小于 0.2% 了

- 关了干啥，大妈v6有eb优化啊

- DMIT v6 不是 cn2gia 优化，xray 在 IPv4/ipv6 都有的时候会尝试 IPv6 能不能访问，能访问就用了 IPv6，我是电信优化，ipv6 相当于非优化线路

- ## [Vmiss的 tri 比 dmit 的美西优化更好么，还是说大妈的更好 _202609](https://www.nodeseek.com/post-951741-1)
- tri basic只有500g双向 200mbps，不过也有更高规格的就是了

- Pro是电信鸡，三网cn2跨网拉得一比，VMISS TR是三网各自优化，三网优化要公平对比你的得拿大妈的eb来对比，pro跨了两网肯定拉跨，大妈的pro v6之所以能胜是因为他走了eb线路两网各自优化了，三网优化选大妈的eb除了9929偶尔炸一下，几乎是无敌的纯在，瓦工都比比了，因为瓦工移动瘸腿都快半年了，始终未修复

- ## [简单说明一下 避免很多后了解我们的顾客对我们有过多误解 _202609](https://www.nodeseek.com/post-948366-1)
  - 感谢近期Nodeseek用户对我们的捧场，导致我们的新用户数量有了很高的增长，所以很多新加入的朋友对我们以前的这些小彩蛋不是很了解，因此容易造成一些误解。 一些节日的折扣券和放货都确实是限量且数量不多的，但是通常都是群内提前给了提示了的，主打一个随缘和彩蛋。
  - 我们所有的机器皆为自行采购并托管，当前硬件价格飙升的行情大家也是知道的，我们以前单台三万的母鸡现在成本大约为七八万。因此我们无法做到像以前那样肆无忌惮地随意采购，但也尽力在做了，但当前没库存也是真的。

- ## [vmiss 有没有可能成为继搬瓦工和 DMIT 之后的传家宝？ _202608](https://www.nodeseek.com/post-898372-1)
- 涨价了包溢价飞升的。20 块钱一个月 2 0 0 mbps 的三网优化上哪找去。溢价应该会到两三百

- 不太可能，正价和折扣价差距不大，除非正价涨价了

- 自用可以，口子注定了溢价不会超 500
- 顶级自用甜点鸡， 200m的口子导致机场也不会买，这反而是好事
- 有正常溢价，传家宝估计难。口子太小了然后别的服务对比T0厂商也差了一些。

- 首先你要知道大妈能溢价那么多是因为免费换IP并且能无限薅流量

- 传啥宝哟，配置太低了，放货又过多，最多自用，干点其他的这口子和流量都不行，传不了家

- 还没用多久 ip 已经被封了。。。。。

- panster 这种新 oneman 商家价格低又怎样，稳不稳 还 有目共睹 ，但 vmiss 是老牌商家。
# discuss-vendor-dmit
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [DMIT套落地鸡请教 _202610](https://www.nodeseek.com/post-967191-1)
  - 请问DMIT套什么落地鸡性价比高啊？以及多个鸡可以套一个落地鸡吗？
  - 主要就是网站老跳验证有点烦

- 你要看你自己什么需求，是要解锁流媒体，还是稳定用ai减少风控可能性

- 先想清楚套落地是为了啥。dmit美西本身就是原生ip 看网页刷油管跑gpt直接用就行 没必要再套 套了反而多一跳延迟。
  - 需要落地一般是两种：要家宽ip跑claude这类风控严的 或者要特定国家的ip解锁流媒体。
  - 多台入口共用一个落地完全可以 落地开一个入站 每台入口建一个出站指过去就行 或者入口上直接用realm转发到落地端口。只有落地自己的带宽和流量要够大家一起用。

- 看你落地干嘛吧 流媒体解锁本身很够用了 ip本身也不算脏 质量要求再高点就家宽落地咯

- ## [DMIT现在的IP段里，哪个段最干净？ _202610](https://www.nodeseek.com/post-967172-1)
179.255
179.253
69.63
64.186
154
131

- 接个落地最干净

- 线路鸡没哪个段干净
- 线路鸡，都是千人骑的，没啥干净的。

- 154的还行 179的还在其他区域

- ## [[结案]DMIT不支持seek.li邮箱 _202607](https://www.nodeseek.com/post-808594-1)
  - 我看坛内dmit热门机都（炒到）1000+了。想拥有一台属于自己的美西，但是中介费5%有点不舍得。不走中介又怕被骗，贪小便宜吃大亏。尤其是0级1级号出机的......
  - 我想到这个方案（表达不一定流畅，方法可能有争议，轻点喷）：卖家创立新seekli，用seekli邮箱在dmit改邮, 买家用seekli账号登陆dmit，确认机器

- 想法很好 但是DMIT不支持seek.li邮箱
- .org 和 .li都不支持

- ## [🎄DMIT大妈修改邮箱（过户）保姆级教程 _202512](https://www.nodeseek.com/post-557276-1)
  - DMIT大妈的账户是可以很方便的过户的，只需要更改账户邮箱即可，简单快捷。
  - 但这也提出更高的要求，必须是一个账号，一台机器 （MJJ祖训：一号一机）
  - 一号双鸡或者多机不仅没有溢价，反而会折价
  - 新的邮箱（接收方邮箱）需要未注册过DMIT；
  - 距离上次修改邮箱大于10天。

- ## [求科普：收大妈必须是没有注册过DMIT账号的邮箱吗？ _202608](https://www.nodeseek.com/post-897381-1)
  - 是不是如果注册过DMIT账号对方就无法push过来？
- 不要理解成push，大妈是改邮箱账号

- 是的，DMIT是改游注册，不是push服务

- 新邮箱改邮。注册过，就被占用了啊

- [买 dmit， 注册过的邮箱还能作为改邮邮箱吗？ _202608](https://www.nodeseek.com/post-897269-1)
  - 要改绑的邮箱不能有绑定的 dmit 账号，不然怎么改绑

- ## [请问DMIT改邮出掉产品后，原邮箱还能重新注册吗？ _202610](https://www.nodeseek.com/post-957269-1)
  - 我这个邮箱改邮出掉产品了，未来从别人手里收的时候是否可以让对方改到这个曾经注册过的邮箱

- 可以重新注册，改邮前注意是否绑定信用卡那些的，避免一起转移到新邮箱

- ## [请教，DMIT更换为付费ip有什么优点吗？ _202610](https://www.nodeseek.com/post-960957-1)
  - 目前是179.255可以升级为付费ip，是更换到154吗？付费升级了有什么优点？求问

- 污染程度更低
154段是大妈租用的，现在上游涨价了每月多一刀，理论上表现更好，解锁更全面

- 154就是原来的段，没啥特别的，就是cognet涨价了

- 得不到的永远在骚动, 其实没啥用. 我换到免费 ip 有1个月了, 各种服务访问下来没有区别

- ## [大妈的CORONA究竟哪点不如megabox pro，真有必要溢价那么高吗 _202601](https://www.nodeseek.com/post-565213-1)
- 瓦工是三网各自优化，dmit pro和eb一个电信一个移动联通

- LAX EB 其实电信差不到哪去，年初的时候晚高峰是有点渣，但真的就还好。后来好像电信也改到9929了吧，比CMIN2好很多了。收台测测呗。

- 加强某工的饥饿营销＋邀请机制，利好炒鸡。而Dmit量大管饱，你所说的各自优化，根本就是营销手段，

- ## [DMIT的升级 _202610](https://www.nodeseek.com/post-959846-1)
- 没有升级的入口，你只有购买其他套餐的机器。如果流量不够用，就花钱重置。或者使用重置卡。

- 大妈没有升级机制，天王老子来了都没得升，只能重买

- 你可以发工单可以升级年费的，他家不缺机器，如果你缺流量或者配置，他家有很多机器套餐正价的。他都说明了，如果你缺流量，要么花钱重置，要么有重置卡。

- ## [dmit 老款eb。wee 现在什么价了 _202610](https://www.nodeseek.com/post-957755-1)
  - 1.15t 那个 当时溢价 890 收的 现在还能平出不，我能预出我就回血了 不能平出我就纠结纠结 

- 老款可以平出的
新款650~750差不多

- 老款和新款差距是不是就是便宜三美元呀
  - 多150g

- ## [DMIT 速度名不虚传 比一些其他商家要良心的多啊 _202609](https://www.nodeseek.com/post-950843-1)
- 任何一家的优化线路99.99%的人日常使用没有任何区别！
- 很正常吧，随便一台优化也能跑到1Gbps
- speedtest 跑本地测速没意义吧，只能证明洛杉矶本地互联带宽可以跑满2G

- 国际带宽又不值钱，说不定还是免费peering

- 关键还是看晚高峰吧 随便一家能不能和大妈比肩了
  - 晚高峰也是一样的啊，没见过谁家美西很惊艳，而且DMIT大陆方向单线程并不好。

- DMIT国内和国际互联确实很强，而且国际互联是我用下来最好的机器之一了，墨尔本到美西很多机器都不是最低延迟

- 看炒鸡吹的魔怔了吧 k系 瓦工系 xtom都随便跑这数据
美西而已 哪家都一样

- ## [感觉DMIT也没有那么神呀 _202609](https://www.nodeseek.com/post-948424-1)
  - 跟风买了一台。实际用下来，延迟和速度都没有我一直在用的日本软银线路好，最后还是退了。
- 这个主要是稳定，延迟肯定不如日本
- 看你买的什么了，如果是美西，那肯定是不如亚太的延迟的，不过重在一个稳定

- 你这定位都不一样，拿软银和美西优化来比较，软银白天能用，晚高峰就不行，DMIT美西优化就是抗晚高峰的情况的，白天+晚上高峰期 一样能用，全天平稳性强

- 这个主打的是晚高峰不丢包，你软银丢包丢飞起来了，软银就是普通线路。如果你对丢包不敏感，只对延迟和速度有需求，那么dmit就是垃圾。
- 但是晚高峰软银不好用啊，美西延迟再怎么样都要比亚太高，主要是稳定

- 我怀疑是你不会调优，没调优好之前是看不出来的

- 好歹对比个同位置的东西

- 本来就不行啊，总不可能我是 39.9 刀特价机所以线路差吧，电信宽带，DMIT pro wee。用起来和 vmiss tri 都没啥差异

- ## [【实测】DMIT LAX EB vs LAX PRO，天津联通晚高峰对比：EB 稳如老狗，PRO 晚高峰跨网回程被限到 90M _202609](https://www.nodeseek.com/post-950858-1)
  - 测试环境本地：天津联通家宽
  - 机器：DMIT LAX. EB、DMIT LAX. PRO（都是 EPYC Milan 1C2G、20G 盘，Debian）
  - 本地测试：ICMP ping 600 次（10 分钟）+ SSH 多连接吞吐（下载 8 条连接、上传 4 条连接）
  - 回程路由：
  - EB：CUG 10099 → 9929 → 天津 4837，全程联通
  - PRO：CN2 GIA → 上海 → 北京换到联通 4837 → 天津，中途换一次运营商
- 结论
  - 联通用户选 EB。三网回程基本是 9929 + CMIN2，晚高峰延迟、抖动、吞吐和中午一样。TcpQuality IPv4 回程 93 个测试点全部 0 丢包。
  - PRO 是电信向的线路。三网回程全走 CN2 GIA。服务器端单连接测速到北京联通有 573M，但我天津联通家宽晚高峰实测只有 90M，而且非常平，像是被限速了。推测是 CN2 回国后在北京换到联通那一段晚高峰限速。TcpQuality 里移动方向有少量丢包（河北 8%、山西 4%）。
  - 电信用户可以反过来看：EB 到上海电信单连接只有 136M、重传 0.92%，PRO 有 634M、重传 0%。
  - 两台 IP 都是原生、低风险，Netflix / Disney+ / TikTok / Prime Video / ChatGPT 全部原生解锁（美国）。
  - 亚洲方向中转（中午实测，0 丢包）：到台湾 HiNet 145ms、新加坡 171–175ms、香港 154–157ms、韩国 EB 159 / PRO 151ms、日本 EB 105 / PRO 151ms、日本 EB 105 / PRO 98ms。数据中心之间的线路很稳，但物理延迟摆在那里。
- 按照 DMIT 客服的回复，PRO 和 EB 的区别只在于中国方向，国际方向路由是一致的，而且联通和移动建议 EB 线路，电信建议 PRO 线路

- 可以试下v6。不过总的来说，联通移动还是建议用eb吧，且不说流量多了一倍，更主要是术业有专攻，能不跨网就别跨，否则大妈也不会搞两条产品线

- 感谢楼主这么详尽的实测！EB 全程 9929 不跨网确实稳，晚高峰还能跑满就很说明问题了。PRO 那个 90M 平顶确实像跨网段限速，我自己联通宽带也基本只选 EB 线路，同网互联省心不少。

- ## [dmit的INTRO很多人收，为什么lightlayer的圣何塞无人问津？ _202506](https://www.nodeseek.com/post-368226-1)
- lightlayer 邻居太逆天了 动不动送中送hk
  - 是这样，闪购新机，已送中（不是我干的）
- 有一堆11.9的邻居一起蹬，原价买肯定越想越亏

- 有点不公平了，电信要用DMIT的PRO做对比，都喜欢溢价收大妈是因为15天可以换IP，大妈对老用户好。

- ## [dmit.eb.intro 好在哪里 _202504](https://www.nodeseek.com/post-308855-1)
- 目前dmit价格最低的cmin2

- Intro 目前叠的buf如下：
业内第一线的服务，DMIT, 15天可换一次 IP
三网顶级线路体验
一年 29.9 刀
比起 eb.wee，只少了 500G 流量，但是硬件配置却是一样的，而这500G 一般人正常上网一个月也用不了 100G，妥妥的有余；主备兼顾；
官方支持的换油策略，完全不担心换手；
超量不停机；
再加一条，去程 9929 了，三网延迟稳定 130ms，美西极限延迟了。

- 主力机嘎嘎好使，我就是当工作环境主力用的，对电信来说，线路上应该没有比这个更好的美西线路了。

- ## [✨DMIT 一文（图）读懂大妈 所有机型（正价+特价），所有线路（Pro EB T1)，所有运营区域（洛杉矶 日本 中国香港），让大佬更容易做选择 |正文多分页（每日更新测评） _202604](https://www.nodeseek.com/post-694203-1)
- 读懂大妈 所有机型（正价+特价），所有线路（Pro EB T1)，所有运营区域（洛杉矶 日本 中国香港）
- 洛杉矶线路分为2个级别，3类产品：
2个级别分别是优化线路和非优化线路
3个产品分别是Premium（简称Pro），Eyeball（简称EB）和Tier 1（简称T1）

Pro系列是优化线路机器，双栈优化，IPv4-三网CN2GIA IPv6-三网9929/CMIN2
EB系列是优化线路机器，双栈优化，IPv4&IPv6-三网9929/CMIN2
T1系列是普通线路机器，双栈无优化，IPv4&IPv6-三网4837 163 CMI

- ## 📌 [DMIT(大妈) 全产品详细测评与产品介绍 _202512](https://www.nodeseek.com/post-552393-1)
- DMIT的产品名字标准构造是 LAX. AN5. Pro. TINY
  - 地点+硬件平台+线路+套餐 = 产品名字
  - 硬件平台(AN4/AS3/AN5等)一般可以不带，就直接用地点+线路+套餐指代产品
  - DMIT的线路就分为T1/EB/PRO三种，套餐可以分很多种，不同套餐对应不同的配置。
- PRO是电信联通移动三网CN2GIA，并且有IPV6优化，IPV6则是电信移动CMIN2，联通9929. 简单的说：电信用户无脑选。
  - 三网CN2GIA线路，电信用户毕业机器，相当优秀的线路，联通移动跨网可能会有限制，但实测下来区别并不大(EB系列移动联通延时会低点)，美西本身锁单线程200Mbps的，所以大部分机器速度都会稳定在150~180Mbps

- EB是电信联通9929，移动CMIN2路线，并且有IPV6优化，IPV6则是电信移动CMIN2，联通9929. 简单的说：就是联通移动最佳机器，无脑选即可。
  - 电信联通9929，移动CMIN2，相当于联通移动极致优化，电信普通优化，勉强能用(劝电信的老实买PRO系列)。国际互联和T1是一样的，非常优秀稳定，到常见机器的延时也很直。

- T1线路
  - 主打落地鸡，没有任何CN方向线路优化，但是国际互联相当不错，可以拉亚太其他落地，作为一个中转站或者直出也可以
  - 无优化线路，电信丢包绕路严重，移动联通部分地区快乐，整体还是不可直连的机器，不建议直连使用，推荐作为落地或者国际互联机器拉SG/TW/JP地区。

- US地区 DMIT的表现基本就是第一了，没有其他家机器能比了，三网都有对应的产品线，而且EB/PRO的线路附带IPV6优化，如果你是三网和电信用户就可以购买PRO系列，联通移动双线或者单线则直接购买EB。
  - PRO都对IPV6有优化，三网用户可以电信用IPV4(CN2GIA)，联通移动用IPV6(9929/CMIN2)，达到三网各自优化的效果
  - 联通移动单线用户无脑EB系列，性价比很高
  - T1三网无优化，推荐作为落地拉US家宽，本土互联非常稳定极致

- ## [DMIT 传家宝Pro. WEE对比EB. WEE _202603](https://www.nodeseek.com/post-659703-1)
- 电信之前差别不大 现在EB的9929线路晚高峰会抖动 体验比不上Pro了

- 我只能用亲身体验告诉你，移动用pro绝对不行，别看延迟和测速和EB相差无几，真用起来晚高峰体验很差
- Pro移动用得走v6 我看v6挺稳 因为移动v6走cmin2

- 你想试试pro怎么样你去买一个月付9.9的，然后退了不就行了，dmit退款政策不是很宽吗

- [DMIT 传家宝补货 快上！最低年付39刀起（附国内多节点ping检测图） _202512](https://www.nodeseek.com/post-553037-1)
- Pro系列为三网回程CN2 GIA线路，EB系列为电信/移动CMIN2，联通9929

- [好想收个DMIT的美西传家宝 _202609](https://www.nodeseek.com/post-943683-1)
- pro系列才能免费换ip，前提是被封了
- eb可以的，大妈的都行

- dmit换ip是所有产品都有，pro与eb只是优化方向有不同，配置都是一样的

- ## [请教 LAX. AS3. T1. WEE 和一些中转线路的知识 _202609](https://www.nodeseek.com/post-947315-1)
今天看到大妈放货的消息，想到一些问题，总结起来请教
1. LAX. AS3. PRO. TINY 直连优秀大家抢的这款居多
2. LAX. AS3. T1. WEE 这款也包含日本、新加坡两款因为直连差，所以更推荐用来落地、外贸、一些其他业务。

我的问题：
1. 那为什么要过「DMIT LAX. T1」，直接 「LAX. AS3. PRO. TINY 」连住宅IP不也是美国本土互联么？
2. 1的问题无论是否是必要的之后，那这里「LAX.AS3.PRO.TINY 」的部分是否可以用EVOXT的马来的VPS去替换（因为至少电信也是CTG GIA），或许比不了 LAX.AS3.PRO.TINY延迟低绕了弯路 ，但至少是可用的？
3. 衍生2的问题，要拉家宽至少中转是要对应自己的宽带网络有（CN2 GIA / 9929 / CMIN2 ）的，或者换个说法就是直连稳定无丢包？
4. 有条件 中转尽量家宽和中转同一个地区/国家？没条件的话要怎么判断是否拉得起来或者是适合的、稳定的、性价比高的？（因为我刷到说台北HiNet家宽对电信很难拉，本身台湾也没有直连好的VPS）

- 多了一层吧，T1是给你在海外用的，在国内用Pro接家宽就好

- 没必要中间加一个 T1。 T1 的用法应该是有沪日的朋友买来走日美 GSL，再去走家宽，而不是用美西优化。

- ## [DMIT VPS 求推荐 - LINUX DO _202609](https://linux.do/t/topic/2947399)
- 要么买 EB 要么买 Pro，T1 是不带任何优化的

- t1 无优化，线路就是普通线路，结合广播老巴西 ip 尚未完全拉到美国，没有购买价值
- 刚买完一个 t1 一个 pro 正在跑测试，t1 确实拉不要考虑了，pro 比我手里的 BWHdc9 结果稍微差一丢丢

- 传家宝都是活动年付机，等黑五圣诞看会不会放，正价机里电信买 pro，联通移动买 eb，t1 没有线路优化别图便宜买

- ## [请教dmit注册需要填真实的国内手机号吗 _202606](https://www.nodeseek.com/post-790132-1)
  - 以及地址填国内还是海外。dmit审核手机号和地址吗？
- 不需要，地址别填太假就行

# discuss-vendor-bwh/搬瓦工
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [为什么瓦工的溢价会普遍比dmit高呢 _202610](https://www.nodeseek.com/post-966444-1)
  - 只讨论特价年付机，biggerbox meagbox pro和 eb.wee pro.wee corna malibu等
  - 瓦工的原油基本都是1000以上，像mega基本都1800-2000了，但是malibu才1300，差距好大呀
- 瓦工放货比较少吧
- 瓦工不补货了，绝版当然贵
- 大妈去年年底补过一波了，所以便宜些

- 三网各自优化好呀，而且瓦工持有量应该比大妈少点

- 大妈要分流V6才是三网，比较麻烦

- 我当初本来是想买瓦工的，因为名气大，逛了坛子果断大妈，性价比太高了还不输瓦工，现在瓦工移动瘸腿了，正在庆幸还好当初是选的大妈，业务鸡，差一网都不行

- ## [为啥大家都盯着瓦工狂炒价格？ _202601](https://www.nodeseek.com/post-586645-1)
  - Megabox上天了，现在又开始炒荷兰， 大妈为啥没有这个待遇？
- 大妈补货啊， 不然也炒啊
- 如果再等几个月dmit不补货，一样炒的
- 大妈能把开机服务卖到崩溃，瓦工它行嘛，离开了它aff爹就活不下去的样子
- 因为MegaBox/BiggerBox 最后一次补货是在暑假，这就造成了稀缺性。
至于个人用户，DMIT黑五促销的时候，都买的差不多了，拿来这么多个人用户？

- 大妈相对不稀缺啊

- 无脑选大妈就好，在某些机房，大妈还是搬瓦工的上游，和搬瓦工的广播IP相比，我更喜欢大妈给的原生IP

- ## [大妈瓦工之下，谁是第三？ _202607](https://www.nodeseek.com/post-806449-1)
- 美西线路商家信誉来说大妈瓦工之下我认为是vmiss，没啥幺蛾子，好几年前的特价也一直保持着（好不好用另说）

- AWS/Azure/GCP

- lightlayer US SJC优化14.9刀或11.9刀

- vmiss 我去年买了 2 台 9929 的机器，到年初 IP 被封，花了 5 刀换 IP，然后又被封，我就没续费叻 ，结果现在想买也买不到了，神奇

- 能直接向三大运营商的海外公司签合同的大上游才能跟dmit／bwh做竞争吧

- ## [兄弟们坚持住听说在等2-3年硬件降价，需求减缓就能买到瓦工megabox 大妈malibu同款特价了 _202607](https://www.nodeseek.com/post-809114-1)
- 硬件压力会在28年初得到极大的缓解。
- 2-3年后内存降价 cpu/gpu/电源/光纤涨价 
- 好的，知道了，那溢价再涨一波，涨到溢价的部分足够三年的正价与特价的差额才行

- 又不是没有平替，vmiss啥的不也可以用，有业务需求的直接就正价，等特价的无非就是🪜，稳定性的话，大妈瓦工又不是不会被打，至于口子，正常200m都够用了，g口除了跑测速日常压根用不上。

- 升产能，需求不变。供需越来越近

- ## [抢不到瓦工和大妈，哪位大佬知道有平替这俩的 _202512](https://www.nodeseek.com/post-548605-1)
- lightlayer吧，反正别选netlab。

- vmiss，贵一些，好像有50-70%码子的传家宝

- 没有，建议白菜价租dmit lax echo（几乎半价）然后蹲

- 看你什么用，如果只是需要富强，搭车即可

- ## [大妈/瓦工热度那么高，市面上就真的没有他们的平替了吗？ _202606](https://www.nodeseek.com/post-794911-1)
- 真没 大商家 稳定 三网优化 口子大 流量大 超出限速 还能免费换IP 清退还有补偿的真不多了

- 没有这个价格和服务了，平替肯定多，但是价格或服务总得拉一个

- 要不是那些特价机，估计都没人看大妈跟瓦工

- 从来没有觉得这2家有啥好的。敏感时期IP整段Q，枪打出头鸟。

- ## [瓦工和大妈 谁是谁的平替呢 _202601](https://www.nodeseek.com/post-589466-1)
- 这俩都是富强的。大妈的u限制比瓦工少，瓦工的流量多。
单纯富强就瓦工，流量多就是性价比高。
想跑一点小东西就大妈，瓦工u限制的很厉害。有时候两个u比不上别人1个u

- 线路差不多
DMIT 免费换IP
DMIT 流量满了 不关机 满了还给几M 跑上网呢
DMIT AMD 配置
瓦工 个人 仅个人觉得 不值得

- ## [想当年minibox，邀请码都没人要。现在溢价这么高 _202605](https://www.nodeseek.com/post-719436-1)
- 当时claw把美西秒得渣都不剩，谁还去关注美西阿
- 现在没了？被打了？
  - 没有hk了，当时全部转移到jp或者新加坡了

- 其实我觉得即使是现在，一个月 200G 以内单向流量的情况下，阿里云hk 或 jp 抢占式开 cdt 照样吊打美西。（我这里瓦工 dc6 只能跑 400M 左右，但是阿里云 hk 或 jp 都能跑到 500M，延迟还比美西低那么多）

一个月就 5 块钱左右，2G 口 200G 单向流量。

唯一的缺点就是得折腾一下。

- 我觉得主要还是 ai 火起来之后美国家宽市场变大了，越来越多人需要美西线路中转，香港和日本中转美国家宽效果一般不是很好。

- ## [出一个瓦工 SPECIAL 10G KVM PROMO V5 - LOS ANGELES - CN2 GIA LIMITED EDITION - V2EX _202511](https://www.v2ex.com/t/1171583)
  - SPECIAL 10G KVM PROMO V5 - LOS ANGELES - CN2 GIA LIMITED EDITION
  - 年费$46.80
  - 限量版搬瓦工 CN2 GIA-E 方案，三网 CN2 GIA ，每个月 500G 流量，1Gbps 带宽。GIA-E 限量版可以选择包括 DC6 机房、DC9 机房、日本大阪、荷兰等机房。

- 这个被现在的 DC99 DC1 背刺的严重，应该没人要了。。。
- 这配置还能溢价出，除了 DC6 DC9 其他机房都不行，不如 box 系列
- 大小盒子便宜好多，不建议续费了

- 挺难出的，这一款。除了能换机房，其他没什么优势，主要是配置和流量比较低。
自打美西出了 box 系列，special 和 plan 就失去了过去的光环

- 现在瓦工不卖可以换机房的 vps 了

- ## [搬瓦工SPECIAL 10G KVM PROMO V5 帐单来了，准备弃了 _202409](https://www.nodeseek.com/post-159248-1)
  - 性能是真的烂，网络是真的稳。作为奠信用户，确实解决了我不少尴尬时刻（4837、9929、CMI2不行的时候，它从没有掉过链子）。

- 我的瓦工也准备扔了，太贵了，每年花几百就看油管完全没意义

- 瓦工这鸡存纯粹是智商税 这个钱都能买好几台配置比瓦工强好几倍的鸡了

- 现在不让迁移了，但是之前bug能够迁移，瓦工也没有清退

- ## [搬瓦工的特点及分析，附搬瓦工BOX系列套餐大全 _202509](https://www.nodeseek.com/post-447868-1)
  - 搬瓦工（BandwagonHost，简称 BWH、瓦工）是一家成立于加拿大的国外 VPS 服务商，官网（国内无法直接访问）为：https://bandwagonhost.com/
  - 镜像站（国内能访问）有：https://bwh81.net、https://bwh88.net、https://bwh89.net
- BOX系列
  - 线路均为回程，去程均为各自顶级优化，即电信CN2GIA、移动CMIN2、联通9929
  - 部分套餐，比如商务机房套餐，支持多机房切换，尤其是有 CN2 GIA、CMIN2、CN2 GT、香港/日本/美国洛杉矶等机房
  - 支持支付宝、PayPal 等常见支付方式。
- 缺点：
  - 1、搬瓦工的IP一旦被封后，需要花7刀更换
  - 2、搬瓦工原厂自带DNS，验证影响响应速度，比如谷歌，自带的DNS会增加四五十毫秒延迟
  - 搬瓦工的CPU性能限得比较死，对高负载的应用，不能得心应手
  - 部分机房硬件老化，虽然部分机房切换了AMD的新硬件，但部分机房，比如DC6依然使用的老E5

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
# discuss-lowendtak
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 
# discuss-nodeseek
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 💡 [来论坛1234天! 写点防骗指南!! _202610](https://www.nodeseek.com/post-963269-1)
- 鉴于最近骗子很多, 打算写点经验, 当然最稳的还是走中介, 但是有些小伙伴还是想省点钱。
- 在这里就涉及到怎么看交易对象, 这些纯粹是个人的看法和理解。我自己交易数据目前也有好几万了, 最大交易有几笔是3000-4000元的, 整体来说先货的在8-9成, 感谢信任我的朋友, 当然这么久从来没有骗过人也没有被骗过
- 防骗指南(综合因素不针对任何人):
  - 不要看到好价的东西觉得捡到便宜了直接甩钱到别人脸上, 觉得自己低级看到对方是3-5级的脑子热了就给钱了
  - 建议在注册时间在600天以下的交易对象都重点注意, 因为印象中在2年前还没有什么骗子, 基本上都是最近1年左右特别的多
  - 骗子套路最近又多起来了, 声称可以走中介, 但是最后因为各种理由忽悠你又不走中介了
  - 注册时间比较长, 但是主题, 回复内容很少很少的, 反之有些人可能拿注册时间很长的白号出售(然后近期大量用AI创建主题和回复制造假象, 然后回头就有人发帖说注册时间长, 主题回复也很多的也不靠谱了!)所以一定要注意主题和回复的内容是不是无意义的或者有多少交易内容的, 以及他是不是真的有交易, 这种对象都要特别特别注意除非他走中介
  - 交易的时候确定论坛ID和飞机对应上

- ## [nodeseek 有公开的 API 吗？ _202609](https://www.nodeseek.com/post-928160-1)
- 没有，自己解析 html

- ## [nodeseek 有没有 API 啊？ _202311](https://www.nodeseek.com/post-42734-1)
  - 我想每几分钟就爬出 cloudcone 鸡子的帖子，但是被 cloudflare 挡住了
  - 发现网站有RSS订阅，可以直接获取最新的帖子：
  - https://rss.nodeseek.com
  - https://www.nodeseek.com/rss.xml

- 有点难，我之前写脚本，自动爬Nodeseek每个帖子并且抽取详情，匹配关键字，也是被限流挡住了。
  - 等5s重试就行

- ## 🚀 [『重磅』NodeSeek社区的探针产品：NodeGet，公测！ _202605](https://www.nodeseek.com/post-709258-1)
  - 定位为下一代服务器监控管理工具，极致的自由度，限制你的玩法的只有想象力。
  - 完善的细粒度权限支持：以 Token 系统为基础，所有系统都强依赖本系统，实现完全自定义的权限支持
  - 极高的可拓展性：KV 系统实现任意数据存储，Js Worker 实现在原有架构基础上无限向上拓展功能。官方提供认证的 Js Worker 方便日常使用
  - 现代化的技术栈：使用 Rust 作为底层语言，配合 PostgreSQL / SQLite 储存数据。
  - 数据通信使用 WebSocket + JSON-RPC 主流方案，符合现代微服务架构
  - 完全前后端分离：彻底的前后端分离，所有操作都走 JSON-RPC API 接口。
  - Agent 原生多 Server 支持：不需要运行多个 Agent，只需要运行一个即可同时与无限多的 Server 通信，并且互不干扰
  - 与社区紧密相连：NodeGet 发根与 Nodeseek 社区，但从未强制与社区绑定起来。你可以自由地使用 NodeGet，并在社区中找到更多玩法
  - https://status.mock.moe
  - https://nodeget-statusshow-limited.pages.dev

- ## [【首发】机界，多平台关键词监控&提醒系统，支持LET、LES、NodeSeek、HostLoc _202302](https://www.nodeseek.com/post-1718-1)
  - 机界是一个综合订阅方案，通过抓取不同主机信息平台的新消息，推送到频道和群组。用户可以通过机器人设定监听的关键词，如果新消息的标题触发了关键词，会在群组中@监听的用户或者通过私人机器人通知用户。
  - 机器人用于添加、删除、查看监听的关键词，切换是否启用通知，以及邀请事宜。
  - 群组用于触发关键词后，@相应的用户，以及用户平时的讨论用
  - 频道用于展示所有的历史消息，也就是群组的纯净版
  - 🐛 似乎已关闭

- ## [发个吃屎的买鸡 _202609](https://www.nodeseek.com/post-929865-1)
  - 买cc的时候, 看见个帖子, 前两天cc的19.99那个, 我买了, 然后有评论说, 他那个也卖, 成想这个19.99的是一年这个价, 然后就按照坛友的价格给钱了.... 太忙了没看, 然后今天看了还剩两个月... 算了一下溢价快上天了.... 然后想着商量一下能不能我损失60, 然后机器还了... 没成.
  - 倒是没啥, 还是提醒大家多问问到期时间, 自己算算溢价吧. 这个屎我吃了就认了. 毕竟买定离手, 怪不得谁.
  - Chafferer 这个人不厚道 尽量别交易

- 4核2G60G 16刀一年 楼主的160 我这个就198吧。”这个鸡198被你买了？还剩2个月?
  - 嗯 吃了口屎 我tmd哪知道俩月
# discuss
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
