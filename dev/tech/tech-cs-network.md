---
title: tech-cs-network
tags: [cs, network]
created: 2020-07-12T13:29:12.095Z
modified: 2020-10-22T14:01:30.508Z
---

# tech-cs-network

# summary

- topics
# [计算机网络与docker网络](https://github.com/zhangguanzhang/simple-container-network-book/blob/master/eBook/directory.md)
- OSI 网络模型是国际标准化组织提出的一个网络互联抽象概念模型，并不实际存在，是为了在一个宏观而非细节的角度上，让人理解网络是如何运作的。
- TCP/IP 五层或者四层模型是对于开发人员来讲的一个学习分层模型，每层的封装增加的信息为以下：
  - 应用层     │ 应用数据
  - 传输层     │ TCP/UDP头部(其中有源目端口号) + 上一层的内容
  - 网络层     │ IP头部（其中有源和目的IP地址） + 上一层内容            
  - 数据链路层  │ 以太网帧头（其中有源目MAC地址）+ 上一层内容 + 尾部的帧校验
  - 物理层     │ 把上一层内容按照每个比特位转换电信号或光信号

- 网络层发现 223.5.5.5 不在自己同一个二层内网，需要发往网关，会先发一次 arp 请求获取网关的 MAC
  - 然后封装 数据链路层 里的目标 MAC 地址为网关地址

- 很多时候作为一个开发你可能都无法 ssh 登录该机器（或者说其实也不用登录机器），最简单就是二分排查，也就是网络层到底可达没（不关注上层的端口 TCP/UDP 传输层），
  - 我们可以利用网络层的 ICMP 协议。也就是 ping 该机器的 IP，Linux 防火墙一般都会放行 ICMP 协议的（以及 Linux 内核参数默认是允许回复 icmp 请求的），所以可以先 ping 下，通了和不通都能说明接下来的排查方向
# more
