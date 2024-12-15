---
title: devops-net-community
tags: [community, devops, network]
created: 2024-11-16T10:58:13.978Z
modified: 2024-11-16T16:58:32.628Z
---

# devops-net-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-nginx
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
# discuss-net-protocols
- ## 

- ## 

- ## 最近几天折腾各种隧道：二层隧道（vxlan，pptp，l2tp，ikev2），三层隧道（openvpn，wireguard），四层隧道（redsocks，tproxy），七层隧道（shadowsocks，trojan），还漏了啥么
- https://x.com/skywind3000/status/1864123514728665559
- 理论上越底层效率越高?
  - 主要是内核支不支持

- pptp ，l2tp 至少是我十年前的玩法了，基本上部署出来直接秒封，流量特征太明显，换 IP 也没用。后面 shadowsockets 也不太行，真正抗的时间久的还是 trojan。
- 经验来看，这些大部分都很容易被封，特别是古老的pptp、l2tp这类。ikev2、vpn这些一旦频率过高也会封。

- l2tp/ipsec 数据层就是走的 gre 封装
# discuss-tcp
- ## 

- ## 

- ## 这个网站很有意思，致力于简化TCP分析，让TCP分析变得跟看聊天记录一样简单。
- https://x.com/austinit/status/1863763735602725345
  - [ChatTCP：上传PCAP文件在线进行TCP分析](https://online.chattcp.com/zh)

# discuss
- ## 

- ## 

- ## 发现一个Tailscale服务端的开源替代品，Headscale，可以用它自建Tailscale服务，客户端还是Tailscale，但是可以完全掌控在自己手里，不限制用户数和设备数
- https://x.com/ShouChen_/status/1868228852449005735
