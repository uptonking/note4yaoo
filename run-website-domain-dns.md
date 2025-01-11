---
title: run-website-domain-dns
tags: [dns, domain, website]
created: 2023-02-07T10:48:06.931Z
modified: 2023-02-07T10:48:41.342Z
---

# run-website-domain-dns

# guide

# discuss
- ## 

- ## 

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
