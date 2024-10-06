---
title: thread-tool-gfw-vps
tags: [gfw, tool, vps]
created: 2023-03-18T17:51:46.658Z
modified: 2023-03-18T17:53:25.909Z
---

# thread-tool-gfw-vps

# guide

# tools
- https://github.com/docmirror/dev-sidecar
  - 为开发者打辅助的边车工具
  - dns优选（解决***污染问题）
  - 请求拦截
  - github加速
  - Stack Overflow 加速
  - npm加速
  - 本应用启动会自动修改系统代理，所以会与其他代理软件有冲突，请务必不要一起使用。本应用主要目的在于直连访问github，如果你已经有飞机了，那建议还是不要用这个自行车（ds）了
# more-tools
- [pictriev, 人脸搜索引擎](http://www.pictriev.com/)
# discuss-stars
- ## 

- ## 

- ## [Clash 检测工具的原理 - V2EX](https://www.v2ex.com/t/1076961)
  - Clash / Clash Meta 核心设置了「Access-Control-Allow-Origin: *」，通配符允许了所有网站的脚本都能调用它。
  - 假设 9090 是您的 Clash API 端口（ Clash Verge 默认是 9097 ）。在 www.google.com 下按 F12 ，输入 await fetch("http://127.0.0.1:9090") 回车，你会发现请求成功了。
  - Clash 系列核心没有用户界面（ GUI ），但它可以在本地运行一个 HTTP 服务，方便各种 GUI 通过 HTTP 请求调用它的接口。Clash 系列核心必须开一个“后门”，也就是允许跨域资源访问，否则这些 GUI 将无法运作。
  - 不过，这个“后门”显然开得过大了。应该增加一个配置项，只允许特定网站，而不应使用 * 通配符。常见的端口有 9090 和 9097。如果不是，还可以遍历 1 - 65535 全部尝试一次。 
  - 成功利用可以获得对 Clash 核心的全部操控权限，包括获取服务器列表，修改代理规则等。
  - 只有 Access-Control-Allow-Origin 允许，才能进行跨域资源的访问，否则会出错。 实际上，出错不意味着没有请求发生。浏览器首先需要发送 HTTP OPTIONS 请求，才能知道 Access-Control-Allow-Origin 的情况。这个请求称为「 Preflight request 」。跨域检测通过之后，浏览器才会再去执行脚本指定的 HTTP 请求。 因此，即便浏览器报错拦截，实际上还是有请求发生了。这就是耗时检测的原理。
  - 在 Windows 平台，操作系统收到 TCP RST 报文后，并不会立即认为端口关闭，而会重试 2 秒后返回错误。因此对于耗时检测，耗时两秒左右的端口是关闭的，毫秒级别耗时的端口是打开的。 在 macOS 和 Linux 平台，情况则相反，端口关闭的耗时比端口打开的短。不过由于区分度太小，准确性较低。
- 其实还有一个保护叫做 PNA - Private Network Access ，防止处于相对更公共 ip 地址范围的网页访问更私有的网址，甚至连导航都不行
  - 只不过有一个小问题：它默认允许访问 127.0.0.1
- 其实给子域名绑一个 ip 指向 127.0.0.1 也不跨域。
- Clash For Windows 有一个随机混合端口功能，打开后应该能降低风险
- clash meta 本来就支持通过 external-ui 配置本地的 webui 资源，不知道为什么不默认禁止跨域
  - 不过我觉得加个密码就行了，端口响应 401 就认为是 clash 有点不靠谱
- 只有浏览器才有这么多安全限制，自己写代码访问 http 可以构造一切头部，就包括 webview ，可以轻松关掉跨域限制，你要什么 ua ，头部，我给你构造就是了
  - 而且不仅是网站在扫代理，各种游戏也会扫代理，以前就爆出腾讯的国外某款射击游戏会扫描全盘，看你有没有装什么远控或者代理投屏软件

- 看了下用 adblock 拦截 127.0.0.1:9090 就可以了
- uBlock Origin 的 Block Outsider Intrusion into LAN 规则也失效了，没拦下来

- 选择 1 ，用 FlClash 这类直接嵌入内核的软件，避免了外部通信，默认关闭外部面板访问。
  - 选择 2 ，用 sing-box 内核，1.10.0 版增加了 access_control_allow_origin

- mihomo 没有像 clash 一样 allow *，建议直接用 mihomo ，别用 clash 了
  - mihomo 是刚修好的，他们做了改进。 文中提到的 clash 系列就包括 mihomo ，也就是 meta 。 至于原版的 clash 核心，早删库了

- clash verge 设置 api key 可以解决

- ## 💡 [在线检测您是否在使用 Clash](https://x.com/geekbb/status/1840655693398855930)
  - https://mikewang000000.github.io/ClashScan/
- 看代码就是直接 fetch 遍历, 扫描localhost的所有端口来访问clash api
  - 本地打开端口扫描？Chrome 能让你随便访问本地端口？

    - Clash 同源策略是 *，所以能请求成功

  - 浏览器对跨站访问 localhost 的控制也只是 CORS 吗？没有额外策略？

    - 据我所知没有的, 还有个 PNA 策略

- 其实这种思路挺有意思的，而且不只能应用到Clash上。假设某个监听本地端口的应用程序没有正确的配置CORS，使用这种方式远程攻击方可以用客户自己的浏览器来跳过客户的防火墙，最终操作这个应用程序去进行某些操作/变更。
- 确实是 chrome only，Safari 无效。
- 并不对 扫不出来软路由
- 我之前可以扫出来，把ublock的规则拉满就不行

- ## 🆚️ Forward Proxy vs Reverse Proxy
- https://twitter.com/sahnlam/status/1744600844195205473
- A forward proxy (or just proxy) is a server that sits between user devices and the internet. A forward proxy is commonly used for:
  - Protecting client privacy and anonymity
  - Avoiding browsing restrictions
  - Blocking access to certain content
- A reverse proxy is a server that accepts requests from clients, forwards them to backend web servers, and returns the responses to the clients. The clients interact with the reverse proxy as if it was the origin server. Reverse proxies are good for:
  - Protecting backend servers from direct exposure to clients
  - Load balancing requests across multiple backend servers
  - Caching static content closer to clients for faster delivery
  - Terminating SSL connections and offloading encryption/decryption tasks from the backend servers
- The key difference is that a forward proxy acts on behalf of clients, while a reverse proxy acts on behalf of servers. 
  - Forward proxies handle outbound requests to external servers, while reverse proxies handle inbound requests coming from clients.

# discuss
- ## 

- ## 

- ## 一款能将临时 IP 变成固定 IP 的代理池中间件：ProxyCat。
- https://x.com/GoJun315/status/1842511148077420982
  - 支持多协议、动态获取、自动验证，配合高并发异步处理，轻松应对各种网络环境和高流量需求。
  - 同时可部署于云端或本地，适用于需要频繁更换IP的网络操作，如网络安全测试。

- ## 上次为了备案买的阿里云主机，一直闲置着不知道来干嘛，
- https://x.com/tualatrix/status/1805087644579401738
  - 不如建个服务用来测试海外网站的访问速度
- 装了个服务器端的VSCode环境
- 站长之家 里面有各种小工具，我之前测国内bing的可用性

- ## 看到一个 repo，搜集了各种内网穿透软件的列表
- https://twitter.com/vikingmute/status/1756495063474188788
  - 没想到这种类型的软件也这么卷啊，相同类型的软件还能创造这么多，两屏幕都拉不到底，足可以看到程序员对这种软件的喜爱
  - 对于大部分人来说，使用 Cloudflare Tunnel 是很好的选项（我自己一直用的它），买个域名就可以完美实现各种功能，除了在国内速度有点慢。
  - 或者使用Tailscale，用起来很简单，App 交互做的很棒，我也简单使用过，喜欢。
  - 当然如果你要自部署，作者推荐 FRP
- 目前没有一个能跟CF比的。CF直接内置了SSL证书自动续签。

- ## 为什么没有Proxifier的开源替代品？
- https://twitter.com/mnixry/status/1737033830953795624
- 这玩意全套可以商用的源码售价目前在15000左右
- 最烦proxy，直接路由分流不好么？
  - 有的情况下需要按进程分流
- 网关按ip分流，结合域名分流。最简单.proxy十分头大
- 不好做，没怎么见过开源社区研究 LSP/WFP，开源社区好像都在折腾 tuntap

- ## 各家网站对 IP 的封禁策略都不一样，大陆用户真的很头疼。
- https://twitter.com/LaiskyCai/status/1723152619739476078
  - 有的网站必须挂 warp 才行，比如 openai、strip 等。
  - 有的网站禁用了 warp，比如 vultr。
  - 有的网站对 warp 非常不友好，比如 google。
  - 所以出口 ip 不但不要是跨境 ip，具体怎么出也得看情况切换。

- ## 大家检测某网站在国内的连通性都使用什么工具呀？用站长之家这个不知道准不准。（感觉网站上广告太多了
- https://twitter.com/EryouHao/status/1644164933855363072
- [阿里云 网络拨测工具](https://boce.aliyun.com/detect/http)
- 以前 https://17ce.com 最好用，现在改用 https://itdog.cn 了

- ## 如果你有自己的 VPS，想获得长期稳定的科学上网服务，可以这样做（用了多年）：
- https://twitter.com/Barret_China/status/1637136780574203906
  1. 在任意云服务商购买域名，例如阿里云，低价域名一年只需花费 9 块钱
  2. 在阿里云上将域名的 NS 修改成 Cloudflare 的 NS，这样就可以在 Cloudflare 配置 DNS 了，也可以直接在 Cloudflare 购买域名，贵一点且要美刀
  3. 配置 DNS，将域名指向自己的服务器 IP，同时开启 Cloudflare DNS 的代理能力，相当于让请求打到 Cloudflare，然后再转发到自己的服务器
  4. 如果想保险一点，可以将代理协议修改成 socks5 或者 wss，基于 TCP 的流量，识别和拦截成本会高一点，这么处理后流量混淆的必要性也不大了
  - 开启了代理之后，Cloudflare 会隐藏后端服务器，暴露的是它自己的 IP。Cloudflare 维护了一个 IP 池，一旦某些 IP 被屏蔽，它会自动识别并修改域名对应的 A 记录，以确保服务的稳定性。
  - 证书也可以用 Cloudflare 生成的，十分方便。
- 其实如果自己有 VPS，最稳定使用的方法还是买一个不走公网的专线机场，然后用代理链来使用自己的节点。既避免了倍防火墙和谐或者公网传输不畅的问题，还能确保地址的稳定性。只需要使用离自己的服务器最近的机场节点做代理链就行了。当然，成本不低，但非常稳定。尤其针对那些对 IP 风控敏感的服务。
- 延迟无法忍受
