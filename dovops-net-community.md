---
title: dovops-net-community
tags: [community, devops, network]
created: 2024-11-16T10:58:13.978Z
modified: 2024-11-16T10:58:31.291Z
---

# dovops-net-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-nignx
- ## 

- ## 

- ## 之前在服务器上用 docker 跑服务，需要折腾一下 Nginx 转发到 80 端口再套 Cloudflare 的解析。
- https://x.com/Stv_Lynn/status/1856325914076033419
  - 现在发现根本用不着这么烦，直接用 Cloudflare Tunnel 把端口转发出来就行了，甚至还能保护源站不被 censys 扫到。
  - 延迟会有一点差异。免费，能接受

- 在本机调试也是这样用，非常方便。

- 再来个tailscale，可以一个端口都不开

- 自用服务用tunnel 不错，但是没日志输出，跟nginx不一样

- 多一层还是有好处的，一个宽字符*dns记录多个子域名转到nginx上然自动proxy到多个容器上，如果tunnel负载加上nginx负载

- 然而用这个还是需要有域名，若是要用国内的云服务商，通过域名访问就要ICP备案
# discuss
- ## 

- ## 

- ## 
