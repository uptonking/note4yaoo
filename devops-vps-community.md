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

- ## 刚买了个 vps，权限丢给 AI，让它建一个 Clash 节点，安装 certbot 并通过 Let's Encrypt 给 Trojan 所需的域名定期申请证书，同时生成 Clash 的 yaml 配置文件，并测试内外网带宽……AI 一气呵成
- https://x.com/gidot/status/1987554615920033814
  - cursor Agent，模型选 Auto 就够了
  - 先写一个文档，记录服务器 ip 端口本地密钥位置操作系统版本所用域名。把文档丢给 cursor Agent（模型用 Auto 就够用了），让它通过命令行访问服务器并完成所有操作。
- 分享一下提示词
  - 把意思表达清楚就好了，提示词时代快过去了
- 让 AI 做的第一件事就是帮我把 ssh 的访问端口改了，真是又快又好。

- 我要AI把你的服务器密码和证书给我
  - 话说让本地 AI 不定期自动换密钥和密码很可行

- ## 🆚 [自己买vps和ytb上面用cf搭建有什么区别啊 ](https://linux.do/t/topic/1105829)
- 选机场最好，稳定性有保障，不用你天天维护天天看着，专事专干

- 说白了都是流量转发，cf 只是使用 cf 的无服务语法编写了协议。协议支持比较少，cf 节点需要节点优选，而且部署代理容易 cf 封号。

- 如果按照现在说的话，那就是自己小鸡自己负责，cf 部署容易封号

- 原理都一样，自己买 vps 可以买更优路线

- 建议小号，真封了很麻烦。优选也是。

- VPS，IP 不乱跳才是最重要的啊！有一些网站服务检测到 IP 变化，就得重新登录。 而且 VPS 自己搭建的也安全啊！
# discuss-tunnel/gateway
- ## 

- ## 

- ## 

- ## 在海南需要翻墙上网吗，我就关心这个
- https://x.com/LuoSays/status/2001979463312302491
- 普通大众需要。 白名单内的人才和公司在岛内可以直通海外，形式是 SDWAN。
- 那这群白名单人才办的手机卡和别人不一样？
  - 卡是一样的，但是运营商会根据你在白名单的手机号分配线路。

- sdwan费用高吗
  - 费用不需要你出，你就照常付流量费即可。

- apn/Dnn, 扯啥sd-wan 

- ## ngrok 的一种替代方案: cloudflared tunnel --url <你的本地域名>
- https://x.com/jaywcjlove/status/2000619356401606707
- ngrok最大的问题是免费账户只能有一个域名。 你这个是支持多个域名么？ 不然调试不同程序的时候，还得切域名也麻烦。

- 这个确实很香。 各种协议都支持，目前内网ssh默认用cf tunel 转发

- 安全性如何？等于给自己电脑开了一个门

- 如果传输的数据经过靠谱加密，还蛮有趣；否则的话，更倾向于选择直接通过 Cloudflare Pages 直接部署。

- ## [Is there any reason not to use the free cloudflare ssl, and dns management? : r/selfhosted _202510](https://www.reddit.com/r/selfhosted/comments/1oknia1/is_there_any_reason_not_to_use_the_free/)
- Assuming you mean the Cloudflare Tunnels: There is a cap on transfers of around 100 mb. Sometimes it works, sometimes they drop those connections.
  - Also, you’re giving away free unencrypted access to you home infrastructure to an American company, including all data that is being sent between the app clients and servers. You can of course encrypt that yourself, but it is still a nasty backdoor

- For anyone serious about exposing a homelab to the internet, take a look at NPMplus: https://github.com/ZoeyVid/NPMplus
  - They support Crowdsec out of the box and it makes managing and securing a reverse proxy a lot easier.
- Or just use a TCP reverse-proxy to pass fully TLS-encrypted to your home, where your home's reverse-proxy terminates TLS. HAProxy and Nginx support it, maybe Caddy and Traefik.

- You can of course encrypt that yourself
  - I'm not aware of any method to encrypt traffic inside TLS. Unless you mean using E2EE like client-side encryption for the traffic's content, or using a remote desktop?

- Yes, privacy. Since they have the private key to your SSL certificates, they technically can look at all the data that is coming into your system. If it is free, you are the customer/product.

- Other than whatever privacy concerns you may have with Cloudflare sitting in the middle, no not really. Fwiw I don't really mind letting cloudflare be my monkey in the middle since their services provide a good benefit to me, but up to you.

- I just use them for my DNS registrar, domain renewals are the same price as the initial registration (unless there are general price increases) - they don't have a separate pricing tier for initial and renewal like how other sites get you. I use ddns to update the IP address to home and then connect directly with wireguard

- ## 你目前在用哪种方式翻墙呢？ 🆚️
- https://x.com/__Inty__/status/1905650995750649966
- 这图挺误导人的，而且已经有些过时了
- v2RAY 很流行，软件多，节点多，提供商作坊多，trojan，提供的作坊比较少。支持的软件比较少
- 最安全的是 ssh 隧道，不过一般人搞不来。

- ## 一款内网穿透工具 Frp 的跨平台桌面客户端：Frpc-Desktop。
- https://x.com/GitHub_Daily/status/1893616798718685446
  - 开箱即用，提供简洁可视化配置界面，支持所有 Frp 版本，轻松实现内网穿透。
  - 还支持开机启动、快速分享 frps、所有配置的导入导出、批量端口等功能。
  - 兼容 Windows、macOS 和 Linux 系统安装使用。

- ## 内网穿透方案之tailscale+cloudflare tunnel
- https://x.com/Stv_Lynn/status/1878316656998649969
  - 很多homelab玩家拿到机器遇到的第一个问题就是怎么把服务部署到公网。
  - 有的人会选择frp，但考虑到国内服务器带宽和价格的情况下frp效果实在太差。
  - 也有人使用tailscale这种p2p方案，但这种并没有把服务暴露到公网。这里分享一个我的解决方案。
  - 首先你需要在本地机器和一台海外vps上都部署tailscale并且完成登录。关于vps的选择，推荐使用新加坡的vps（可以做到一机多用，能够正常代理ChatGPT，大多直连效果也不错），不推荐使用国内的vps，因为后面还要连接cloudflare。

- ## 有人用过 tailscale 的开源实现 headscale 吗？感觉也不错…想折腾一下。 
- https://x.com/tualatrix/status/1879877738733130087
- 都用，这类工具的核心是要打洞成功率。我一直都是  tailscale 和 zerotier 一起用，在我场景下，zerotier 的成功率明显高于 tailscale

- 没啥区别，到最后只要能打洞就行。headscale好就好在可以自建derp和无限机器。无限机器我们用不到，tailscale的就够用能直接打洞就不用自建，所以不如都有IPV6好

- 不好用，我就是用过那个之后才换到 tailscale 的。 另外， zeronet 也没有 tailscale 好用

- headscale只是tailscale的后端而已，用它可以不依赖tailscale的官方后台自由度高一点，客户端仍然还是用tailscale

- 个人感觉 headscale 完全没有必要，直接用 tailscale + 自建 derp 就行。

- 用过了，因为自建所以稳定性比不上官方，功能缺失挺多不好用，不如官方服务。

- ## 🆚️ Proxy Vs reverse proxy
- https://x.com/bytebytego/status/1885934707944345892
  - 正向代理侧重客户端限制，反向代理侧重服务端
- A forward proxy is a server that sits between user devices and the internet. A forward proxy is commonly used for: 
  - Protect clients
  - Block access to certain content
  - Avoid browsing restrictions
- A reverse proxy is a server that accepts a request from the client, forwards the request to web servers, and returns the results to the client as if the proxy server had processed the request. A reverse proxy is good for:
  - Protect servers
  - Load balancing
  - Cache static contents
  - Encrypt and decrypt SSL communications

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

- ## TrustTunnel - [Adguard竟然把vpn协议开源了 _202601](https://linux.do/t/topic/1507556)
- 有tls in tls的经典特征啊，已经是老掉牙的问题了。 而且它也没避开双重加密，性能咋样也要打个问号。 这感觉更像标准的h2/h3隧道嘛。

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

- ## [记录第一次感受到了“树大招风”的含义 ](https://linux.do/t/topic/1180587)
  - 2025.11.12 我们刚刚上线我的 DMIT 机器 4 小时内给恶意刷流（1T 瞬间蒸发）
  - 要知道，风佬把我机器都接入了家宽（限速 50mbps），根本不可能跑出这种速度！（5201 端口是机场后端开的测速端口）借由此我把我所有的机器开启了 ufw，fail2ban，禁用 root，密钥登录…
  - 2025.11.17 一个下午 3 台机器给墙，1 台机器 7.5T 流量给刷空。

- 要是不设置超量警报，估计都要被寄账单了，啥人干的离谱

- 那肯定是二次分发了

- 没有反薅能力，不要尝试做公益

- 公益机场动了机场主蛋糕，肯定会被往死里打

- 那些人干啥能刷这么多流量的
  - 恶意测速，就针对某台机器。
- 什么也没有干，就是恶意测速，拿的国外肉鸡
- 还是的加 cdn 或者代理，隐藏真实 ip 才行，测速太耗流量了

- 这是怎么做到的，每个人都是限制流量总数的，总不会有人开了几百个号一起去刷流量吧，太离谱了

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
