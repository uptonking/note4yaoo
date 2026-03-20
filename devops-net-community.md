---
title: devops-net-community
tags: [community, devops, network]
created: 2024-11-16T10:58:13.978Z
modified: 2024-11-16T16:58:32.628Z
---

# devops-net-community

# guide

- ip
  - [Trusted IP Data Provider, from IPv6 to IPv4 - IPinfo.io](https://ipinfo.io/)
  - [IP Address Lookup - Check Location of Your Public IP](https://iplocation.io/ip/103.72.147.240)
# discuss-stars
- ## 

- ## 🆚 [tx/rx which direction : r/networking](https://www.reddit.com/r/networking/comments/6muphz/txrx_which_direction/)
- Rx is "receive", i.e. stuff coming in and waiting in queue to be processed.
  - Tx is "transmit", i.e. stuff waiting in queue to go out.

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

# discuss-ssh
- ## 

- ## 

- ## 服务器 ssh 被扫了 16w 次，就离谱。
- https://x.com/hubingkang/status/1900362862767595638
  - `sudo lastb | wc -l` 

- 紧查了查，我的几台国外服务器，20多万次。国内的反而少一点，不到两万次。但是我内网穿透的家里主机，竟然也有将近2万次，家里的电脑密码很简单，也不知被攻破了没
  - 家里内网得注意，一被破解了不是盗取资料就是要勒索了。

- 慌什么，用密钥登录他又无法攻破
  - 有些用密钥，有些用的密码

- 用fail2ban拦截
  - 还可以自动报 http://blocklist.de，顺便做个 crontab 每天拉那个网站的 ip 黑名单
# discuss-dns
- ## 

- ## 

- ## YaDNSb - 一个 DNS 服务器性能基准测试工具！支持 IPv4、IPv6、DoH、DoT 和 DoQ - 基本上所有的 DNS 协议
- https://x.com/geekbb/status/1928287578983186678
- 更适合中国宝宝体质的 DNS 测速工具：https://github.com/xxnuo/dns-benchmark/tree/master

# discuss-wireshark
- ## 

- ## 

- ## 

- ## 

- ## [Wireshark-MCP：为 LLM 提供原生的pcap包分析能力  - LINUX DO _202603](https://linux.do/t/topic/1784146)
  - 主要解决 AI 辅助网络排障和安全分析时，缺乏底层数据包操作能力的痛点。底层基于真实的 tshark / Wireshark 套件，你可以直接把 .pcap 文件丢给 CodeX 或 Claude，
  - 它会自动提取数据帧，基本覆盖 Tshak 全部功能，已经精简过Tool Calling 的上下文，可用于应急响应分析已经 CTF 竞赛

# discuss
- ## 

- ## 

- ## 

- ## 发现一个Tailscale服务端的开源替代品，Headscale，可以用它自建Tailscale服务，客户端还是Tailscale，但是可以完全掌控在自己手里，不限制用户数和设备数
- https://x.com/ShouChen_/status/1868228852449005735
