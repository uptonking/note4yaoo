---
title: lib-collab-community-websocket-webrtc
tags: [collaboration, community, webrtc, websocket]
created: 2022-10-11T08:56:11.457Z
modified: 2022-10-11T09:03:07.297Z
---

# lib-collab-community-websocket-webrtc

# guide

# discuss

## [WebRTC和WebSocket有什么关系和区别？](https://www.zhihu.com/question/424264607)

- 这两种技术本质上半毛钱关系都没有，除了它们都可以在web中用之外。
  - socket 和 rtc 有多大区别，这两种技术就有多大区别。
- websocket就是借助于http建立一个tcp的连接，然后在这个tcp连接中传输websocket这种特定协议对应格式的二进制分帧数据。
  - 简单点说，websocket 就是封装了 tcp 来给 web 的 JavaScript 用。
- webrtc则主要是给rtc封装了个web端的js接口。
  - 底层webrtc的库需要完成全部 rtc 相关的逻辑，包括 p2p连接，音视频的，采集，处理，编码，解码，传输，拥塞控制等等等一大堆东西。
  - 另外，传输层协议，webrtc主要在用udp，而不是websocket的 tcp。
- 但说它们一点关系也没有，其实也不一定。
  - 有些 webrtc 的部署方案中，会把 websocket 用作信令协议的传输通道。

### [WebRTC(Web Real-Time Communication)实时通信技术介绍](https://www.zhihu.com/question/424264607/answer/2394172608)

- https://github.com/caiya/webrtc-p2p
  - 在两个浏览器中进行实时视频通话
- https://github.com/caiya/webrtc-p2p-datachannel
  - p2p视频聊天，加入datachannel进行简单的消息发送

- https://github.com/hughfenghen/rtc-live-show
  - 基于WEB RTC + rrweb实现的页面“直播”demo

- WebRTC目的是无插件实现web端的实时通信的能力。
- WebRTC提供了视频会议的核心技术，包括音视频的采集、编解码、网络传输、展示等功能，并且还支持跨平台，包括linux、windows、mac、android等。

- 👉🏻 建立WebRTC连接需要如下几个步骤：
- 获取本地媒体（getUserMedia()，MediaStream API）
- 在浏览器和对等端（其它浏览器或终端）之间建立对等连接（RTCPeerConnection API）
- 将媒体和数据通道关联至该连接
- 交换会话描述（RTCSessionDescription）

- 在WebRTC中，信令起着举足轻重的作用。但实现没有标准化，比如http、websocket、xmpp等。
- 信令就是协调通讯的过程，一旦信令服务建立好了，两个客户端之间建立了连接，理论上它们就可以进行点对点通讯了。
  - 协商媒体功能和设置
  - 标识和验证会话参与者的身份（交换SDP对象中的信息：媒体类型、编解码器、带宽等元数据）
  - 控制媒体会话、指示进度、更改会话、终止会话
  - 双占用分解
- WebRTC要求在两个对等端建立双向的信令通道，通常有三种方式来传输WebRTC信令：http、websocket、数据通道

- WebRTC提供了浏览器端的P2P通信，但并不意味着WebRTC不需要服务器。
- 撇开应用服务器不说，至少以下两种服务器是必须的：
  - 浏览器之间建立通信前交换各种元数据（信令）的服务器（信令服务）
  - 穿越NAT和防火墙的服务器（stun、turn、rsip等）

- 元数据是通过信令服务器中转发给另一个客户端，但是对于流媒体数据，一旦会话建立，首先尝试使用点对点连接。
  - 简单一点说就是：每个客户端都有一个唯一的地址，他能用来和其他客户端进行通讯和数据交换。
- WebRTC使用RTCPeerConnection建立连接传送流数据，在建立RTCPeerConnection实例之后，想要建立点对点的信道，需要做两件事：
  - 确定本机上的媒体流的特性，比如分辨率、编解码能力啥的（SDP描述符）
  - 连接两端的主机的网络地址（ICE Candidate）
- WebRTC定义了两组主要的功能，分别是：媒体捕获（getUserMedia()）、媒体传输。
  - 对等连接和提议/应答协商的概念是媒体传输的核心。
- RTCPeerConnection接口是WebRTC的主要API，用来在P2P端建立媒体连接及数据连接路径。
- RTCDataChannel，数据通道是浏览器之间建立的非媒体的交互连接。
  - 即不传递媒体消息，绕过服务器直接传递数据。
  - 相比WebSocket、http消息，数据通道支持流量大、延迟低。
- 单个对等连接中的多个数据通道底层共享一个流，所以只需一次offer、answer即可建立首个数据通道。之后再建立数据通道无需再次进行offer、answer交换。

## [到底什么是WebRTC服务器，以及它是如何联接通话的](https://webrtc.org.cn/webrtc-server/)

- WebRTC并不是真正意味着你不需要服务器来协商和联接通话。它只意味着，在多数情况中，你可以直接地在浏览器之间进行通信。
- 要想让任何WebRTC服务正常的工作，你需要如下2个后端服务器
- 信令服务器
  - 对于浏览器的对话来说，最重要的就是某种中介器—一个了解通话双方端点的服务器。
  - 这就是信令服务器，负责协商会话，而且可能是最接近WebRTC服务器的东西了。
  - 通常，这个服务器也会穿过会话发送相关数据。
  - 信令服务器可以实施像SIP或XMPP的标准化协议，或者私有协议。
  - 有时，信令内容也会作为Web服务器的一部分来操作网页。其他情况中，信令服务器就专门用来处理信令了。
- TURN和STUN服务器
  - 当通话两端端点都检测到了对方的时候，他们会尝试着在其之间建立直接联接—有时候会有用，但也有不起作用的时候。
  - 当没有用的时候，是因为在通信通道上的网络地址转换或者防火墙机制，要么掩盖了浏览器的地址，将其从私人IP地址转换到公共地址，要么它们认为这个会话是不安全的，以至于它们会阻拦流入的数据流并且不允许通话的进行
  - 为了克服这些问题，WebRTC使用了STUN和TURN，它们是要求服务器构件来协助协商媒体传输的协议，而且有时将所有的媒体都中继给TURN服务器。
- 媒体服务器
  - 甚至在协商信令以及联通媒体之后，我们可能还想要在服务端处理媒体。
  - 这种功能是需要有的，因为这样用户就可以实施一个有着大量参与者的会话，并且记录存档会话或会话到其他类型的网络协议的网关。
  - 在这些情况中，我们就会用到后端的媒体服务器。
