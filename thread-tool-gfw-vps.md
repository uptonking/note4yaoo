---
title: thread-tool-gfw-vps
tags: [gfw, tool, vps]
created: 2023-03-18T17:51:46.658Z
modified: 2023-03-18T17:53:25.909Z
---

# thread-tool-gfw-vps

# discuss

- ## 

- ## 

- ## 

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