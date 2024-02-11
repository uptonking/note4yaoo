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
# discuss-stars
- ## 

- ## 

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

# more-tools
- [pictriev, 人脸搜索引擎](http://www.pictriev.com/)
