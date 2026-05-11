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

- ## 

- ## [狐蒂云倒闭了，，，好牛批啊，连吃带拿 - LINUX DO _202605](https://linux.do/t/topic/2135602)
- 付费取数据也太不要脸了吧，吃相这么难看
- 无敌了，自己跑路，客户受到了损失还要付费才能取出原本自己的数据吗？

- 这一波跑路，其他厂家涨价太厉害了。简直牛逼啊

- 让我想起了前司的竞对公司的操作，也是业务到期了，然后甲方选了前司，竞对公司也是摆明了不打算干了，直接服务器拉闸了，用户数据直接锁死

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

- ## Vercel Labs 做了个端口转发工具，用稳定的命名 .localhost URL 替换 localhost:3000 这些端口号，让人类和 AI 代理都能轻松访问本地服务。
- https://x.com/geekbb/status/2023645651092075008
  - 以前开几个本地项目，端口记不住、端口冲突，现在代理自动分配随机端口，用命名URL替代数字端口。
  - 工作原理就是：跑一个本地代理在1355端口，所有 *.localhost:1355 都路由到它，然后它根据子域名转发到实际的应用端口。
- 你是否在找，nginx？

# more
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

- ## 

- ## 

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

- ## [有哪些性价比高的高配美国服务器 强调cpu和内存 线路似乎无所谓? - LINUX DO _202603](https://linux.do/t/topic/1792158)
  - 仔细计算 此帖应该终结了 我决定自己组建一台128gx86 或者直接mac, 这边问题是国内上行宽带升级一下 还有做好代理就好
- 
- 还有高配到底是啥高配，CPU单核强的，还是核数多的？还是内存大的，还是硬盘大的，还是带宽大流量足的，还是全都要？

- 直接干独服

- 我觉得最大预算会花在国内上行上

- 套cf只能不挑IP吧，带宽不够，访问速度一样上不来啊

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
# discuss-vpn-net/proxy
- ## 

- ## 

- ## 

- ## 

- ## 🧩 [[网络知识扫盲]网络结构与 VPN / 代理服务区别 - LINUX DO _202605](https://linux.do/t/topic/2152601)

> 文章的图片由AI生成，因为我的visio打不开了，PS、可画又太重，AI太好用了

> 站内最近来了好多新佬，于是根据自己所学和工作内容写一点扫盲贴 

### 碎碎念

很多初学者刚接触网络时，会把“联网”理解成：电脑连上 Wi-Fi（无线局域网），然后就能访问网站。这个理解不算错，但它只看到了最表层。真实的网络访问过程并不是电脑直接和网站服务器通信，而是经过了多个中间环节：终端设备、无线 AP 或交换机、路由器或网关、运营商网络，最后才到达互联网上的服务器

可以先把网络想象成一套“分层的交通系统”。你的电脑、手机、平板就是出发的人；家里的 Wi-Fi（无线局域网） 或交换机相当于小区道路；路由器相当于小区门口的岗亭和出口；运营商网络相当于城市主干道；互联网上的网站服务器则是你最终要到达的目的地。数据在网络里传输，也需要先判断“目的地在哪里”“从哪个出口走”“下一站交给谁”。这也是我们常说的“VPN”“代理”“翻墙”所要解决的核心问题甚至运行时的底层逻辑

一个最简单的家庭网络结构通常是这样的：

在这个结构中，手机和电脑并不是直接连接互联网，而是先连接到家里的路由器。路由器再通过光猫或运营商线路连接到互联网。很多家庭设备里，“光猫、路由器、交换机、无线 AP”的功能可能被集成在一个盒子里（智能家庭网关），所以普通用户会感觉“一个路由器就完成了所有事情”。但从网络原理上看，这些功能是可以拆开的

至于ISP、互联网之间的架构和互联关系，那复杂去了（
以中国骨干网演示，其包含：
包括中国科技网（CSTNET）、中国公用计算机互联网（CHINANET）、中国教育和科研计算机网（CERNET）、中国金桥信息网（CHINAGBN）

具体发展可以看维基百科： [中国互联网骨干网 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E4%B8%AD%E5%9B%BD%E4%BA%92%E8%81%94%E7%BD%91%E9%AA%A8%E5%B9%B2%E7%BD%91)

---

整个网络访问的底层逻辑就是：

 **找到目标地址，然后一跳一跳把数据送过去。** 

这里面最关键的几个角色分别是：

 **终端设备** ，也就是你的电脑、手机、平板。它们是发起访问的一方

 **Wi-Fi / 交换机** ，负责把你的设备接入局域网。无线设备通过 Wi-Fi 接入，有线设备通过网线接入

 **路由器 / 网关** ，负责判断数据要不要出门。如果访问的是家里同网段的设备（局域网），比如访问 NAS、打印机、旁路由，那可能还在局域网里转；如果访问的是 L 站、百度、Steam、ChatGPT 这类互联网服务，那就要交给网关往外发

 **运营商网络** ，也就是电信、联通、移动这些 ISP 提供的网络。家里的路由器再往外走，通常就进入运营商网络了

 **互联网服务器** ，也就是你最终访问的网站、游戏服务器、接口服务等

这里有个很重要的点： **电脑并不知道整个互联网怎么走，它只需要知道“下一跳交给谁”。** 
对于普通家庭网络来说，这个“下一跳”通常就是默认网关，也就是家里的路由器。比如你的电脑 IP 是：

```
192.168.31.58
```

而路由器地址是：

```
192.168.31.1
```

那么电脑访问外网时，大概率就是把数据先交给 `192.168.31.1` ，后面的事情交给路由器处理。

在真正访问网站之前，还有一个很重要的小步骤： **DNS 解析** 。

因为人方便记的是域名，比如 `google.com` 、 `bilibili.com` ，但网络设备真正通信时用的是 IP 地址。所以浏览器访问网站前，会先问 DNS 服务器：

```
google.com 对应的 IP 是多少？
```

DNS 服务器返回一个 IP 地址后，电脑才会拿着这个 IP 去查路由表，判断目标是不是本地网段、要不要交给默认网关、下一跳该往哪里走。也就是说，DNS 解决的是“目标地址是谁”的问题，路由和网关解决的是“数据怎么过去”的问题

简单理解就是：

```
DNS：把域名翻译成 IP路由：决定去这个 IP 怎么走网关：负责把数据转发到下一跳
```

所以 DNS 很重要，但它只参与“找地址”这一步，并不等于真正帮你建立了一条到目标网站的通路

这时候就能顺便理解一下早期很多“冲浪姿势”的区别了。最初级的做法，可能只是不用运营商默认下发的 DNS，改成其他 DNS。这个动作本质上只是改变了“域名找谁解析”，比如你访问 `google.com` ，先要问 DNS：这个域名对应哪个 IP？如果原来的 DNS 解析不正常，换 DNS 可能会让你拿到一个看起来更正常的结果（有将DNS解析到中间代理服务器以达成本地不使用代理软件也能访问google的效果，前提是 本机-DNS代理服务器-解析后IP 这条路径没断）。但注意，DNS 只负责把域名翻译成 IP，它不负责帮你把数据送到目标服务器。所以如果后面的路由、连接、策略本身已经不通，那单纯换 DNS 就没用了

再往上一级，就是大家早些年常说的“蓝灯 VPN”这类工具。普通用户会把它统称为 VPN，但从原理上看，它更像是在本机和远端服务器之间建立了一条“中间通道”：你的浏览器请求不再直接走“电脑 → 路由器 → 运营商 → 目标网站”这条原始路径，而是先交给这个客户端，再由它转发到远端节点，最后再去访问目标网站。也就是说，它解决的不只是“域名解析”的问题，而是进一步改变了流量实际经过哪里

所以从低级到高级可以这么理解：

```txt
改 DNS：
只改变“域名问谁解析”

代理：
改变“某些应用请求交给谁转发”

VPN / 隧道：
改变“系统或部分流量从哪条路径出去”
```

这也是为什么有时候换 DNS 有用，有时候又完全没用；为什么有些工具只影响浏览器，有些工具却能影响整个系统。它们本质上动的不是同一个层面：有的动 DNS，有的动应用流量，有的动路由和隧道。理解了这个分层，后面再看 VPN、代理、透明代理、旁路由，就不会觉得它们都是一团胡辣汤了（胡辣汤真好喝吧）

---

说到这里，就可以正式区分一下 **代理**和**VPN** 了。

很多人平时会把这类工具都叫成“VPN”，比如蓝灯 VPN、机场 VPN、科学上网 VPN。但从技术上看，它们未必都是真正意义上的 VPN。有些是代理，有些是隧道，有些是代理客户端加规则分流，有些才是比较标准的 VPN

---

### 网络代理

先说代理。

代理的核心逻辑很简单： **你不直接访问目标网站，而是把请求先交给一个中间服务器，让它帮你访问** 

比如原本访问路径是：

```
电脑 → 路由器 → 运营商 → 目标网站
```

使用代理之后，路径可能变成：

```
电脑 → 本地代理客户端 → 远端代理节点 → 目标网站
```

这时候，目标网站看到的访问来源通常就不是你本机所在的出口，而是代理节点的出口。对用户来说，感觉像是“换了一个出口上网”；对网络来说，本质是请求被转发了一次

常见的 HTTP 代理、SOCKS5 代理、Shadowsocks、V2Ray、Trojan、Hysteria、TUIC 这类东西，虽然实现方式不同，但从大方向上看，都可以理解为： **让某些流量先交给代理节点，再由代理节点访问目标服务** 

所以现在很多代理客户端里面会有“规则模式”“全局模式”“直连模式”这些选项，并且流量出口的IP质量（落地IP）很大程度上（99%都不为过）决定了你访问目标服务器时的“网络质量”，这也是为什么那么多佬买代理服务时写着“解锁流媒体、chatgpt”等标注，并且各个节点、平台的价格区分也很明显，如果落地IP被标记为风险IP，通过这个IP地址访问的请求会被目标服务器拦截

简单理解：

```
规则模式：该走代理的走代理，不该走代理的直连
全局模式：大部分流量都交给代理
直连模式：不走代理，按原始网络路径访问
```

---

### VPN技术

然后再说 VPN。

VPN 的全称是 Virtual Private Network，中文一般叫“虚拟专用网络”或者“虚拟私有网络”。它原本更多是企业场景里的东西，比如员工在家办公，需要访问公司内网的 OA、文件服务器、堡垒机、数据库、代码仓库，就可以通过 VPN 接入公司网络

它的感觉更像是：

```
我虽然人在外面，但通过一条虚拟隧道，临时接入了公司内网。
```

传统 VPN 更关注的是“接入一个远端网络”，而不是单纯帮你访问某个网站

比如公司内网是：

```
10.10.0.0/16
```

你在家里连上公司 VPN 后，电脑可能会多出一块虚拟网卡，然后获得一个公司分配的虚拟地址。之后访问公司内网资源时，系统会把这些流量送进 VPN 隧道

所以 VPN 更像：

```
给电脑多接了一根虚拟网线
```

而代理更像：

```
找了一个中间人帮你转发请求
```

二者都可能改变流量路径，但改变的方式不一样

可以粗暴总结成：

```
代理：重点是“请求由谁代发”
VPN：重点是“设备接入哪个网络”
代理更偏应用层：浏览器、软件、域名、规则
VPN 更偏网络层：虚拟网卡、路由表、隧道、地址池
```

当然，现实中这两个概念经常混在一起。很多所谓“一键 VPN”工具，底层未必是传统企业 VPN，而可能是代理、隧道、虚拟网卡、规则分流混合在一起。用户不关心它背后到底是 SOCKS、TUN、HTTP、WireGuard 还是其他协议，只要能让目标服务访问成功，就会统一叫它“VPN”，我甚至见到过X音、X站上，拿着截图说国家不是禁止VPN吗为什么手机系统设置里有VPN设置，XX品牌是不是有异心（

这就像很多人把所有联网设备都叫“路由器”，但实际里面可能同时包含了光猫、NAT、DHCP、无线 AP、交换机、防火墙等功能，甚至将IPS、防火墙、负载均衡等网络设备统称为“电脑”的行为（毕竟框式、盒式设备，你就说外层那个能不能被叫“机箱”吧）

从工程角度看，最好还是拆开理解：

```
DNS：解决域名到 IP 的问题
代理：解决某些请求交给谁转发的问题
VPN / 隧道：解决流量从哪条虚拟路径出去的问题
规则分流：解决哪些流量直连，哪些流量走代理的问题
旁路由 / 透明代理：解决不在每台设备上单独配置客户端，也能接管流量的问题
```

写到这里，就能解释现在常见的“机场”了

所谓“机场”，一般不是单独指某一种协议，而更像是一种服务形态。它通常包含：

```
节点订阅、链接代理、协议、流量倍率、分流规则、客户端配置
```

用户买到的不是一个“VPN 软件”，而是一组可以导入客户端的代理节点。然后再用 Clash、sing-box、v2rayN、Shadowrocket、Stash 这类客户端进行管理

所以现代机场更像：

```
机场服务商提供节点、客户端负责连接节点、规则决定哪些流量走节点、远端节点负责访问目标网站
```

这和蓝灯的区别在于，蓝灯更像一个封装好的工具，用户只管打开；机场更像一套“节点订阅 + 客户端 + 分流规则”的组合，可玩性更高，但理解成本也更高

最后还要提一句安全和隐私问题

只要你使用代理、VPN、机场、蓝灯这类中间转发工具，本质上都是把一部分流量交给了中间节点。即使 HTTPS 可以保护网页内容不被随便看见，中间节点通常仍然可能知道你连接了哪些目标 IP、哪些域名、连接时间、流量大小等信息

所以这类工具不是“绝对安全”，更不是“完全匿名”。它只是改变了流量路径

通俗点说：

```
不用代理：你信任本地网络、运营商、目标网站
用代理 / VPN：你额外信任了代理节点或 VPN 服务商
```

所以选择这类服务时，风险不只在技术协议，也在服务商本身。来路不明的客户端、奇怪的订阅链接、免费节点、盗版安装包，都可能比协议本身更危险

----

### 代理协议

传统代理协议和现代代理协议

说到代理协议，就很容易出现一个误区：很多人会把“代理软件”“代理协议”“代理节点”“订阅链接”“客户端内核”全部混在一起叫

比如有人会说：

```txt
我用的是 Clash 协议
我买了一个 V2Ray
我这个 VPN 是 SOCKS5 的
我导入了一个机场协议
```

严格来说，这些说法都不太准确，交流、排障时容易造成误导

更准确的拆法应该是：

Clash / sing-box / v2rayN / Shadowrocket：
客户端、前端、内核或规则管理工具

HTTP / SOCKS5 / Shadowsocks / VMess / VLESS / Trojan / Hysteria / TUIC：
代理协议或代理协议族

TCP / UDP / TLS / QUIC / WebSocket / gRPC：
承载代理流量的传输方式或封装方式

订阅链接：
把一堆节点信息打包给客户端读取的配置入口

机场：
提供节点、订阅、流量计费、线路维护的一种服务形态

所以不要看到一个软件名字，就以为它本身就是协议。软件是软件，协议是协议，节点是节点，规则是规则

简单类比一下：

```txt
协议：
规定双方怎么说话

客户端：
负责帮你把话说出去

节点：
负责远端帮你转发

订阅：
负责把一堆节点信息发给客户端

规则：
负责决定哪些流量走哪个节点
```

---

### 传统代理协议

比较典型的传统代理协议有：

```
HTTP Proxy
HTTPS Proxy / HTTP CONNECT
SOCKS4
SOCKS5
```

这些协议出现得比较早，设计目标也比较直接： **让应用程序把请求交给代理服务器，由代理服务器帮忙访问目标** 

比如 HTTP 代理，主要服务对象就是浏览器、爬虫、下载器这类使用 HTTP 协议的应用。客户端不是直接访问目标网站，而是把 HTTP 请求发给代理服务器，代理服务器再去访问目标站点

访问路径大概是：

```
浏览器 → HTTP 代理服务器 → 目标网站
```

如果访问的是 HTTPS 网站，就会用到 HTTP CONNECT。它的逻辑可以简单理解为：浏览器先对代理服务器说：

```
我要连接 example.com:443，你帮我打通一条 TCP 通道
```

代理服务器同意之后，浏览器再通过这条通道和目标网站进行 TLS 握手。这个时候代理服务器更像是在中间帮你“打洞”和“转发字节流”，而不是直接理解里面的 HTTPS 内容

所以 HTTP CONNECT 大概是：

```
浏览器 → 代理服务器：CONNECT example.com:443
代理服务器 → 目标网站：建立 TCP 连接
浏览器 ↔ 目标网站：在这条连接里进行 TLS 加密通信
```

这就是为什么 HTTPS 网站的内容一般不会被普通 HTTP 代理直接看到，但代理服务器仍然可能知道你连了哪个目标地址、什么时候连、流量有多大

SOCKS 代理比 HTTP 代理更“通用”一点

HTTP 代理主要面向 HTTP/HTTPS 流量，而 SOCKS5 不太关心上层到底是什么应用协议。你可以把它理解成一种更底层一点的“通用转发协议”

它不管你后面跑的是：

```
HTTP、HTTPS、SSH、游戏流量、IM通信、其他TCP应用
```

只要应用支持 SOCKS5，或者客户端能把流量转给 SOCKS5，它就可以帮忙转发

所以 SOCKS5 的感觉更像：

```
应用程序：我要连接 1.2.3.4:443
SOCKS5 代理：彳亍，我帮你连
```

它比 HTTP 代理更通用，但它本身并不等于“安全”。很多传统 HTTP 代理、SOCKS5 代理在协议层面并不自带强加密。也就是说：

```
SOCKS5 是代理协议不是加密协议
```

如果你裸连一个不可信 SOCKS5 代理，它能转发你的流量，但不代表这条“你到代理服务器之间的链路”天然就是安全的

---

传统代理协议的特点可以总结成这样：

```
HTTP 代理：更偏 Web 场景，主要处理 HTTP / HTTPS 请求
SOCKS5：更通用，可以转发更多类型的 TCP 流量，也可以支持 UDP 相关能力
优点：简单、成熟、兼容性好、很多软件原生支持
缺点：本身通常不强调加密和复杂网络环境适应能力很多时候需要应用主动支持代理
如果 DNS 处理不当，可能出现 DNS 泄露如果代理链路裸奔
安全性依赖外层加密
```

这里的 DNS 泄露也很好理解

比如浏览器使用了 SOCKS5 代理，但 DNS 解析还是本机自己向本地 DNS 服务器查询，那么就可能出现这种情况：

```
网页请求走了代理
DNS 查询没走代理
```

这样一来，虽然真正访问网站的数据流被转发了，但“你查询过什么域名”这件事，仍然可能暴露在本地网络或运营商侧（ **现在来看，如何解决DNS泄露，也是防拉闸的必要学习内容** ）

所以代理不是只看“能不能连上”，还要看：

```
应用流量走没走代理
DNS查询走没走代理
UDS流量走没走代理
IPv6流量走没走代理
规则有没有匹配错
```

这也是为什么很多人会遇到这种情况：

```
浏览器正常、命令行不正常（chatgpt能打开，但是codex、claude cli、反重力没法用）
网页正常、游戏不正常（同样是chatgpt、google能打开，但是一些国际服游戏没法正常登录）
IPv4正常、IPv6泄露访问网站正常，但是DNS检测不正常
```

因为它们走的不是同一层逻辑。

---

### 现代代理协议

现代代理协议之所以出现，是因为传统代理协议在现实网络环境里逐渐不够用了

传统 HTTP / SOCKS5 的目标很单纯：转发请求

但后来大家需要解决的问题变多了：

```textile
代理链路要不要加密？
移动网络丢包高怎么办？
UDP 应用怎么处理？
多个连接能不能复用？
规则分流怎么做？
DNS 怎么接管？
不同网络环境下怎么保持稳定？
客户端如何统一管理多种协议？
```

于是就出现了很多现代代理协议或协议族，比如：

```
Shadowsocks
VMess
VLESS
Trojan
Hysteria
TUIC
NaiveProxy
```

还有一些经常和它们一起出现的传输或封装方式：

```
TLS
WebSocket
gRPC
HTTP/2
QUIC
Reality
uTLS
```

有的协议不仅用于代理，你也可以在easytier这类软件上看到

这里要注意，后面这些不一定都是“代理协议本体”，很多是传输层、加密层、伪装层或握手特征相关的方案。现实里它们经常组合在一起，所以普通用户会感觉名词特别多

比如一个节点可能看起来是：

```
VLESS + TCP + TLS
VLESS + Reality
Trojan + TLS
Shadowsocks + plugin
Hysteria2 + QUIC
TUIC + QUIC
```

这就像你寄快递：

```
代理协议：包裹里面的内容怎么组织
传输协议：用货车、飞机、轮船还是高铁送
加密层：包裹要不要上锁
规则分流：哪些包裹走哪条线路
客户端：快递驿站和调度系统
```

所以现代代理不是单一技术，而是很多层东西叠在一起，是一种多种技术不断迭代互相承载使用的结果

以已经被揭解剖的 Shadowsocks 为例，它可以粗略理解成一种“加密的代理转发协议”

传统 SOCKS5 更像是：

```
应用 → SOCKS5 代理 → 目标服务器
```

而 Shadowsocks 更像是：

```
应用 → 本地 SOCKS/HTTP 入站 → 本地 Shadowsocks 客户端 → 加密连接 → 远端 Shadowsocks 服务端 → 目标服务器
```

应用本身可能只知道自己在连本地的 SOCKS5 端口，比如：

```
127.0.0.1:7890
```

但后面的加密、远端连接、节点出口，都是代理客户端和远端服务端在处理

所以用户看到的是“我设置了一个本地代理端口”，但实际背后可能是：

```
本地应用流量→ 本地代理端口→ 代理客户端加密封装→ 远端节点解密转发→ 目标网站
```

这也是现代代理客户端常见的工作方式： **在本机开一个本地代理入口，然后把不同应用的流量接进来，再按规则转发到不同节点** 

---

VMess、VLESS、Trojan 这类协议则更多出现在 V2Ray / Xray 生态中

可以非常粗暴地理解：

```
VMess：早期 V2Ray 生态中常见的代理协议，有自己的认证和传输设计
VLESS：更轻量的协议设计，本身不负责加密，通常依赖 TLS、Reality 等外层安全机制
Trojan：设计思路上更接近“跑在 TLS 里的代理协议”，经常和 HTTPS/TLS 场景一起出现
```

所以它们看起来更复杂，但也更适合现在这种复杂网络环境

---

Hysteria 和 TUIC 这类协议，经常会和 QUIC、UDP 联系在一起

传统代理很多是基于 TCP 的，而 TCP 在高延迟、丢包、跨境链路、移动网络切换等场景下，体验可能会比较差。QUIC 基于 UDP，在连接迁移、拥塞控制、弱网恢复等方面有自己的优势

所以 Hysteria / TUIC 这类协议的目标，往往不是单纯“能不能代理”，而是更关注：

```
高延迟环境下的体验丢包环境下的速度
UDP应用支持移动网络切换连接恢复能力
```

这也是为什么有些人会觉得：

```
同一个节点，某些协议看网页差不多
但看视频、打游戏、跑大文件、移动网络下体验差很多
```

因为协议本身、传输方式、拥塞控制、服务端线路、落地 IP、运营商路由，都会影响最终体验

不要把所有问题都归结为“节点好不好”，也不要归类于某机场好不好，补药迷信单一节点口牙！

实际影响因素很多：

```
本地网络质量
本地运营商
中转线路
远端入口
落地出口
目标网站
代理协议
传输层协议
客户端实现
规则匹配
DNS
策略
```

其中任何一层拉胯，最后表现出来都可能是笼统的：

```
慢卡打不开能打开但加载不全网页可以，APP不行
白天可以，晚上不行
手机可以，电脑不行
```

网络排障永远是分层看，不要一上来就玄学

题外话：如果佬想测以本地网络出发，看代理质量的方式，可以看我这个帖子： [[开源][图一乐] 代理拔线？以本地网络环境给代理订阅做个体检 - LINUX DO](https://linux.do/t/topic/2046076)

---

不过也不要把“现代协议”神化。

不是说协议越新就一定越快，也不是名字越花就一定越稳。

很多时候，真正决定体验的不是协议名字，而是后面的线路质量和落地质量。

比如：

```
一个普通协议 + 优质线路 + 干净落地IP
可能体验很好
一个很新的协议 + 烂线路 + 风险落地IP
照样打不开、很慢、被风控
```

这也是为什么很多机场会强调：

```textile
入口线路
中转线路
IEPL / IPLC
BGP
CN2
CMI
落地地区
原生 IP
流媒体解锁
ChatGPT 解锁
倍率
```

---

还有一个常见误区： **代理协议不等于匿名协议** 

很多人会觉得用了代理之后，自己就“隐身”了，甚至跑去X和reddit键政，更有甚者在国内实名制平台挂个代理就开始大扯特扯，这是我不理解的

代理最多改变的是访问路径和出口地址：

```textile
目标网站看到的是代理节点IP
不一定直接看到你的家庭宽带IP
```

但这不代表你完全匿名

因为中间仍然有很多角色可能掌握不同信息：

```textile
本地网络：
可能知道你连接了某个代理节点

运营商\云服务商：
可以对流量进行长期监测、解包解封装、监控流量去向

代理服务商：
可能知道你的账号、连接时间、流量大小、目标连接信息

目标网站：
知道代理出口 IP、浏览器指纹、登录账号、行为特征

客户端软件：
如果来路不明，本身也可能成为风险点
现在很多机场趁机推私有协议闭源客户端
不排除打算跑路前收集一波用户信息卖了的可能
```

- ## [国外30T数据传输到国内，有什么好的办法？ - LINUX DO _202605](https://linux.do/t/topic/2131246)
  - 国外买的业务数据，需要传输到国内本地，30T左右的数据，实际情况是直连下载只有几K的速度，用VPN会快但这个流量费肯定很夸张，是否有免费或低成本的解决方案呢？

- 物理传输啊，直接使用最本质的传输方式，发个国际快递
- 最快的就是物理硬盘， 走DHL很快的
- 30T除了物理传输我想不到任何其他快速传输的方式，建议买机械硬盘，然后飞机飞过去然后再飞回来
- 联系对方硬盘打包数据，然后联系物流给运过来吧，让物流顺便解决海关问题。只靠网络传输不止流量，高带宽专线也够贵的，况且30T得传到什么时候去了
- 当地买硬盘，快递寄回来，然后再卖掉，说不定还能挣一笔 
  - 关税警告
- 买个30T以上的磁带， 然后存在磁带里面打包寄回来。
- 可以直接硬盤郵寄，或者上大內存vps做中轉分批 transfer

- 买个阿里云国际的服务器，高带宽，通过服务器中转回国内。也可以通过谷歌网盘啥的，或者看看国内大厂提供的国际网盘服务。

- 👀 网盘长时间大流量也容易被运营商ban
  - 最合适的只有买四张16T的hc550，二手价格大概1-2k
  - 数据存两份，分两个快递发回来。
  - 回国以后再把四张hc550折一点价出掉，这个型号nas佬很乐意收

- 不着急的话可以用OneDrive分批次传输呀
- 买个onedrive？ 搭配世纪互联？ 他们应该有内网 我记得内网传输很快
  - 就算是会员，他家一个账号，流量也限制200g还是500g来着，超过一定流量之后，速度就限制死了，还有可能直接封号

- 之前通过aws 进行数据传输3t差不多花了1天

- 30T的vpn也没多少钱吧, 机场或者10刀左右好像也有无限流量的机子甚至cloudflare搭建一个还能免费.200兆的话10来天就行吧, 快一点500兆的话甚至几天就行

- 有个方法 开google的那个30t，然后webdav绑定到koofr，下载速度不算太慢，可以不用梯直接下载。
- 上传谷歌盘, 买个会员2T, 分卷压缩, 1G一个包, 弄程序自动上传下载

- 两边安装tailscale/zerotier 等局域网组网工具，然后传输试试，运气好能直连的的话速度会快很多，不能直连走中继的话也可以试试搞个云服务器做中继，然后限速跑(防止超过服务器月流量限制)

- 30T其实不多啊，刷PT的谁不是几百T起步，30T可能半个月就能拉回来了

- 节点的话其实用DO也不是很贵，找个10水滴的号直接就能跑60T了

- 我记得曾经有天才上传到 npm 服务器上
- npm不好搞了，我之前传了几十t全给我删了

- 30TB真不算多，大概不到100Mbps全速跑一个月的数据量。找一个活多个速度还可以的服务器做中转，完全可以的。

- 
- 
- 
- 

- ## [自己搞定了动态家宽，只有垃圾VPS成本，想赚钱却没这个胆 - LINUX DO _202605](https://linux.do/t/topic/2126280)
  - 最近这段时间一直在研究家宽，现在弄好了，成本只有垃圾vps的成本（有一定内存要求），支持多个国家节点，我看家宽都卖的挺贵的，想用来做副业赚点，但看了一下有法律风险，奈何胆子太小，不敢弄了，还是自用算了
- ping0 不准的，也就给小白看看，可以用 ipinfo 看看，出口是不是被标记成 VPN 了
  - https://ipinfo.io/47.149.27.10

# discuss-cloud-infra
- ## 

- ## 

- ## 

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
# discuss
- ## 

- ## 

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
