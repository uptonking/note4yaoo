---
title: run-website-domain-dns
tags: [dns, domain, website]
created: 2023-02-07T10:48:06.931Z
modified: 2023-02-07T10:48:41.342Z
---

# run-website-domain-dns

# guide

- [快速查看您的连接位址在cloudflare的印象 - 教程 - IDC Flare](https://idcflare.com/t/topic/39100)
  - [Test Page · Cloudflare Tools](https://cloudflare.manfredi.io/test/)
# discuss-stars
- ## 

- ## 

- ## 买域名第一看不是看稳定吗？怎么看价格了？淘宝余毒太深啊
- https://x.com/mutigsak/status/1882416622234931271

# discuss
- ## 

- ## 

- ## 

- ## 准备申请公网 IP，直接在中国电信官方 App 找人工客服就可以了，很方便。
- https://x.com/tualatrix/status/1880138030587212052
  - 有了公网 IP 后，最终我给我的 Mac mini 选择的内网穿透方案是：Surge Ponte，开箱即用，真的非常方便。
  - 中国电信还有提速包，最近降价了，花9元就可以把上行带宽提升到 100M（默认 30M）。等有需要也可以使用，虽然只是临时手段
- 不行啊
  - 说明新宽带不行了，我是很早入网的。

- 联通改桥接模式后，拨号时+adsl1 ，直接就是公网 IP。远程访问家里的 Mac mini  ，你是主要把它做 NAS 来用了吧。
  - 我改了桥接之后直接正常拨号就是公网
- 你这个是某一个地区的联通，每一个地方都不一样

- 我们这里399套餐起步才能使用公网

- ## 如果你要购买域名，并想比较首年价格、续费和隐私服务，最佳选择是：tld-list .com
- https://x.com/hellokaton/status/1877639948079182029
  1. 价格透明：实时对比70多家注册商报价
  2. 无隐藏费用：显示续费价格，不会被“首年优惠”套路
  3. 一站式搜索：900多个顶级域名任你选择

- ## 国内可备案的域名后缀比以前增加了很多，但是好像毫无规律可言。
- https://x.com/TooooooBug/status/1875539868463591879
  - 比如.pw域名是帕劳的国家域名，可以备案，但是.app这种通用顶级域名却不能备案
- 要域名注册局在中国开分公司，然后去工信部申请。 也就是可以让工信部一键 server hold , .app 属于谷歌注册局，当然不会去申请了 目前 Godaddy、Identity Digital 还算积极，申请的挺多

- 腾讯云好还是阿里云好？ 单纯只是买域名备案，不用服务器
  - 这俩在域名和解析这方面都差不多。不过阿里收购了万网， 腾讯收购了 dnspod 。至于备案啥的，也基本差不多（实际上最后就是比较下当时的价格和优惠以及一些额外的优惠。 哪家便宜选哪家

- 可备案的后缀前提是对应的后缀在国内有注册公司申请，并且能一键 Client Hold。像 me run 等我记得都是同一家公司申请的。app dev 这种谷歌自有的域名后缀，只能是有生之年了

- .pw 是 Radix Registry 在运营，然后在中国申请了备案许可。
  - .ai 与 Identity Digital 合作了，应该很快也可以在国内备案了

- ## Would you prefer a subdomain or sub-folder for your customer pages?
- https://twitter.com/LuoBaishun/status/1622731914531463170
  - I chose to go with subdomain (http://example.earlybird.im) instead of subfolder (http://earlybird.im/example), but I noticed that some of my competitors are using subfolders. Am I doing it wrong?
- Cost related can you fund a wildcard SSL cert for the sub domains, or automate letsencrypt? Sub folder would be cheaper to secure and no need to catch all on the DNS.
- For SEO purposes. subfolder works better.
- The subdomain is fine, sub-folder should all be SEO-related contents.
