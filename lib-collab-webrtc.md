---
title: lib-collab-webrtc
tags: [collaboration, webrtc]
created: 2022-10-11T08:55:01.873Z
modified: 2022-10-11T08:55:15.326Z
---

# lib-collab-webrtc

# guide

# [给好奇者的 WebRTC](https://webrtcforthecurious.com/zh/)
- https://github.com/webrtc-for-the-curious/webrtc-for-the-curious

- 目前，大多数部署的应用程序都通过客户端 / 服务器方式进行连接。
  - 客户端 / 服务器方式连接要求服务器具有稳定且公开可用的传输地址。客户端与服务器联系，然后服务器做出响应。
- WebRTC 不使用客户端 / 服务器模型，它建立点对点（P2P）连接。 
  - 在 P2P 连接中，创建连接的任务被平均分配给两个对等方。
  - 👉🏻 这是因为无法猜测 WebRTC 中的传输地址（IP 和端口），而且，在会话过程中，传输地址甚至可能会变更。
  - WebRTC 将收集所有可能收集的信息，并将尽力实现两个 WebRTC Agent 之间的双向通信。
- 建立点对点连接实际上可能会非常困难。
  - 这些 Agent 可能位于没有直接连接的不同网络中。
  - 即使在两个 Agent 可以直接连接的情况下，你可能还会遇到其他问题。比如在某些情况下，两个客户端使用不同的网络协议（UDP <-> TCP）或使用不同的 IP 版本（IPv4 <-> IPv6）。
- 上面描述的连接过程是通过 Interactive Connectivity Establishment（交互式连接建立 /ICE） 实现的。这是另一个在 WebRTC 之前就已经出现的协议。
  - ICE 是一种用来寻找两个 ICE Agent 之间通信的最佳方式的协议。
  - 每个 ICE Agent 都会发布如何访问自己的方式，这些路径被称为候选地址（candidates）。
  - 候选地址本质上是一个传输地址，ICE Agent 认为这个传输地址可能可以被对端访问到。
  - 接下来 ICE 将确定候选地址的最佳搭配。
- 对于同一网络中的主机来说，互相连接非常容易。
  - 例如在 192.168.0.1 -> 192.168.0.2 之间通讯就很容易！这两个主机无需任何外部帮助即可相互连接。
- 但是，使用 Router B 的主机无法直接访问 Router A 背后的任何主机。你如何区分 Router A 后面的 192.168.0.1 主机和 Router B 后面相同 IP 的主机之间的区别呢？它们都使用内网 IP！
- 有些网络不允许 UDP 通信，或者也有可能不允许 TCP。有些网络的 MTU（Maximum Transmission Unit/ 最大传输单元）可能非常低。网络管理员可以更改许多变量，这些修改可能会使通信变得困难。
- 防火墙 /IDS 规则
  - 另一个问题是深度数据包检查和其他智能过滤方式。某些网络管理员将运行一些软件，这些软件会试图处理每个数据包。
  - 很多时候，这些软件无法识别 WebRTC 的数据包，由于它们不知道如何处理，它们可能会阻拦这些数据包，例如，它们可能将 WebRTC 数据包视为不在端口白名单上的可疑 UDP 数据包。
- NAT（网络地址转换）映射是使得 WebRTC 连接成为可能的魔法。WebRTC 就是使用 NAT 让处于完全不同的子网中的两个 peer 进行通信，从而解决了上述 " 不在同一网络中 " 的问题。
  - NAT 映射不使用中继，代理或服务器。
  - 想要这样通信的话，你需要创建一个 NAT 映射。
  - 在这个例子中，创建一个 NAT 映射，就像是在路由器中做了一次自动化的端口转发。
- NAT 映射的缺点是：映射的形式不止一种（例如静态端口转发），并且映射的实现方式在不同的网络中也是不一样的。ISP 和硬件制造商可能会以不同的方式来实现 NAT 映射。在某些情况下，网络管理员甚至可能禁用它。
- 好消息是，NAT 映射的所有行为都是可以理解和观察到的，因此 ICE Agent 能够确认其创建了 NAT 映射，并确认该映射的属性。