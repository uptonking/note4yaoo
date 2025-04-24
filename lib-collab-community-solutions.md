---
title: lib-collab-community-solutions
tags: [collaboration, community, solutions]
created: 2024-01-28T09:04:55.644Z
modified: 2024-01-28T09:05:12.586Z
---

# lib-collab-community-solutions

# guide
- 协同的使用场景非常广泛
  - 包括多人操作
  - 包括在线面试的画板
# discuss-stars
- ## 

- ## 

- ## As modern web apps become more realtime and collaborative (Figma, Canva, Notion, Linear, etc.), systems and frameworks are being actively developed to support this need. 
- https://twitter.com/joygao/status/1784012670263550129
- On a high level, I find them bucketing into one of these approaches:
- 1) Via a modern database with built-in subscription features. 
  - Examples: - @supabase - @rethinkdb - @convex_dev - @fauna - @skiplabs 's SKDB (and of course our good ol' @Firebase )
- 2) Via a sync engine that hooks into existing database and subscribe for changes. 
  - Examples: - @figma 's Multiplayer - @linear 's sync engine - @asana 's Luna Framework - @prisma Pulse
  - sorry, r/Multiplayer/LiveGraph. Our multiplayer is more like a standalone sync engine, so perhaps it's worth separating this into 2a) and 2b).
- 3) Via a local-first storage, with option to sync to a managed or self-hosted database (or even client-side peer-to-peer sync, shoutout to Ditto). 
  - Examples: - @ditto - @ElectricSQL - @liveblocks - @replicache
- There's no clear answer in terms of approaches and is case-by-case depending on your need for offline functionalities, permissions, scalability, and team expertise.
- In general, as we are pushing more complexity to the edge/client (need for responsiveness, offline, scale, data ownership and security), I think 3) is currently the most actively developed space, and likely will continue to gain popularity over time.

# discuss-partykit
- ## 

- ## 

- ## PartyKit is just great for building super fast applications *even if you're not doing multiplayer*. _202401
- https://twitter.com/tomus_sherman/status/1742538924587634881
- How about we make the realtime part more pervasive? Change the industry instead of changing the messaging Even the most basic CRUD app could have improved UX with realtime, hard to implement right now even with something like PartyKit though
  - The framework needs to provide absurdly easy-to-use and reason about primitives. Makes me think of Meteor, which did this very thing with minimongo and op-log tailing.

# discuss-vnc/novnc
- ## 

- ## 

- ## [用浏览器远程控制 PC 电脑桌面：noVNC - 知乎 _202405](https://zhuanlan.zhihu.com/p/700346357)
- 最近想要在微软 XBOX 游戏机远程访问电脑桌面，发现可以用 noVNC 这款软件来实现浏览器远程访问桌面。
  - 只要在 PC 电脑安装上 noVNC 服务，XBOX 通过 Edge 浏览器就可以远程访问了。

- 安装 UltraVNC 软件（开源免费桌面远程工具）
  - 还支持设置分辨率、画质

- 通过 noVNC 实现的远程桌面访问方式，不受平台设备限制，只要有浏览器就能远程访问，另外因为是在局域网访问的，所以基本没啥延迟，如果需要外网访问自行研究内网穿透。

- ## 推荐一个可自托管的虚拟浏览器，可以直接部署到一个VPS上，然后就可以实现团队间共享一个持久化Session的浏览器。
- https://x.com/Stephen4171127/status/1883559372204491156
- 试过了，卡顿很厉害。还不如vpn加windows虚拟机
- 这种用类似于novnc实现的浏览器项目都不是很好用，带宽和延迟一旦不够就会让整个界面都很卡，甚至是完全不可用的地步
- aws的remote desktop考虑一下？

# discuss-rdp
- ## 

- ## 

- ## 🆚 [What's the difference between RDP vs VNC? - Super User](https://superuser.com/questions/32495/whats-the-difference-between-rdp-vs-vnc)
- RDP is semantic. The RDP is aware of controls, fonts, and other similar graphical primitives. 
  - This means that when rendering a screen across a network, this information is used to compress the data stream significantly. For instance, if you know that this region of the screen if occupied by a button, with the color grey, then you don't need to send an image of the button across the network, but merely information such as location of this button, size and color.

- VNC is "dumb" in this respect, and largely functions by sending the actual images across the network.

- RDP is tightly coupled to the Windows platform whereas VNC is available for most platforms. 
  - RDP is also seen as far more performant than VNC, due to the semantic advantage.

- RDP stands for Remote Desktop Protocol. 
  - It is a proprietary protocol built by Microsoft to let users to graphically control remote computer.
  - RDP logs in a remote user to the server computer by effectively creating a real desktop session on the server computer including a user profile.
  - RDP works in the same way as if the user had logged in to the physical server directly.
  - ✨ RDP can support multiple remote users logged in to the same server that completely unaware of each other.
  - RDP supports multiple monitors, if the client has them

- VNC stands for Virtual Network Computing. 
  - It is an open platform independent graphical desktop sharing system designed to remotely control another computer.
  - VNC follows the older model of simply showing whatever is on the screen with no forced logins required.
  - VNC connects a remote user to the computer itself by sharing its screen, keyboard and mouse.
  - when several users (including the one operating the real physical monitor and keyboard) connect to the same server they see the same thing and they type on the same keyboard.
  - 🔒 VNC has security implications; if you remote into a machine that an Administrator is logged into, you'll effectively be an Administrator. And if you're both trying to use the computer at the same time, it's even more fun!

- ## [如何评价微软的远程桌面？ - 知乎](https://www.zhihu.com/question/26816582)
- 远程桌面的隐藏配置都明文保存在 RDP 文件里。

- VNC这些是帧传输协议，类比一下就是看直播。
  - RDP协议支持指令传输协议，使得一些窗体渲染可以发生在客户端上，这使得传输协议天然可以做到很小，同等网络条件下，带宽消耗更小，性能更高。当然也支持了直播的方式做兜底。

- ## 🚀 Cloudflare now provides clientless, browser-based support for the Remote Desktop Protocol (RDP) _202503
- https://x.com/Cloudflare/status/1903076650952335699

- [RDP without the risk: Cloudflare's browser-based solution for secure third-party access _202503](https://blog.cloudflare.com/browser-based-rdp/)
  - Short-lived SSH access made its debut on Cloudflare’s SASE platform in October 2024.
  - Cloudflare has architectured a high-performance RDP proxy that leverages the modern security controls already part of our Zero Trust Network Access (ZTNA) service.
  - Cloudflare's browser-based RDP solution is the newest addition to Cloudflare Access alongside existing clientless SSH and VNC offerings, enabling secure, remote Windows server access without VPNs or RDP clients.
  - Users only need a web browser — no native RDP client is necessary! RDP servers are accessed through our app connector, Cloudflare Tunnel, using a common deployment model of existing Access customers. There is no need to provision user devices to access particular RDP servers, making for minimal setup to adopt this new functionality.
  - 💡 How it works
  - Cloudflare’s implementation leverages IronRDP, a high-performance RDP client that runs in the browser.
  - Unlike Java-based Apache Guacamole, another popular RDP client implementation, IronRDP is built with Rust and integrates very well with Cloudflare’s development ecosystem.
# discuss
- ## 

- ## 

- ## [A simple way to build collaborative web apps | Hacker News _202108](https://news.ycombinator.com/item?id=28209736)
- I've worked in the space for a while (Fluid Framework) and there's a growing number of libraries addressing realtime collab. 
  - One of the key things that many folks miss is that building a collaborative app with real time coauthoring is tricky. Setting up a websocket and hoping for the best won't work. 
  - The libraries are also not functionally equivalent. Some use OT, some use CRDTs, some persist state, some are basically websocket wrappers, fairly different perf guarantees in both memory & latency etc. The very different capabilities make it complicated to evaluate all the tools at once.
- PouchDB+CouchDB work well out of the box with minimal fuss for open pieces you can just plug into this role. PouchDB handles the client's state persist and replication on the client, couchdb is the reliable cloud service you can replicate to. 
  - Meteor, at least their pre-apollo stack had realtime collab type features with their mini-mongo client and oplog tailing.
- You could build this with couchdb multi master regional servers and pouchdb on the client and have full consistency with the replication both to clients and servers as well as conflict resolution (in case of collision) done for you.

- We implemented all that manually, more or less in swift (and sqlite), then react+redux, and on the back end - postgres and python+flask. Works flawlessly so far. We do have the same setup more or less, with listeners triggering UI updates and push messages signalling the clients to fetch data from the server. Then, on the server, we have two dbs -> one where we store each update or create message, in a postgres-based queue, and another one, in a normalised format which we use for login (it's way faster than replaying all messages from the queue). 
  - We gave up on the websocket part and implemented basic polling, because they were not supported by App Engine at the time (things might have moved on since then, which is a couple of years ago). Yet, for a note/todo/habit tracking app, it simply doesn't need to be real-time from our experience

- Thanks for mentioning Meteor, which also impressed me a lot when it first came out. I think it didn't take off because it tries to do too much (frontend + backend + db). And one smart move by Replicache is that it tries to integrate nicely with the rest of your stack.

- Replicache's creator Aaron has a pretty good Twitter thread explaining the difference among Replicache, WebSocket and (classic) CRDTs. I will summarize briefly here:
  - WebSocket (and Phoenix Channel) is just a communication method. To maintain consistency and resolve conflict, you need something like Replicache.
  - CRDTs are more suitable for p2p scenario while Replicache works better for client-server apps.
  - Phoenix's Presence is built with CRDT but it's just a single feature, not a general CRDT toolkit.

- At FastComments we store every change as an event, which can either be pushed or polled. Clients subscribe, and poll on reconnect.
  - The integrations work kind of like DB slave replication. They do an initial sync and then maintain state via the event stream.
