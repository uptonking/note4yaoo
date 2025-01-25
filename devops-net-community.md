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

# discuss-tunnel/gateway
- ## 

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
# discuss
- ## 

- ## 

- ## 发现一个Tailscale服务端的开源替代品，Headscale，可以用它自建Tailscale服务，客户端还是Tailscale，但是可以完全掌控在自己手里，不限制用户数和设备数
- https://x.com/ShouChen_/status/1868228852449005735
