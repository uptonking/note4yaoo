---
title: thread-coding-toys
tags: [coding, thread, toys]
created: 2023-03-24T04:43:32.474Z
modified: 2023-03-24T04:44:07.520Z
---

# thread-coding-toys

# guide

# discuss
- ## 

- ## 

- ## 

- ## 我把Edge浏览器的Bing侧边栏搬到了Chrome里了！
- https://twitter.com/wong2_x/status/1673170198902472705
  - 功能和在Edge里一样，除了基础的聊天外，还可以基于当前浏览的网页/PDF进行对话。
  - 实现原理：Edge里的Bing侧边栏实际上是用iframe嵌入了一个网页，这个网页和浏览器之间进行通信，获得当前正在浏览的网页等信息。这个插件做的就是在Chrome里模拟这个过程。比较麻烦的是逆向网页和浏览器的通信以便让读取网页能够工作
  - https://github.com/wong2/bing-chat-sidebar-for-chrome

- ## 看到有同学在重复造 tgbot 的轮子，想了一下把我的机器人开源了。仓库拖下来就能跑，配置写在代码里头自己改
- https://twitter.com/Lakr233/status/1638774978316480513
  - 支持私聊群聊回复连续对话，每一个对话一个单独的历史记录。最大支持 16384 token 的上下文（只要你显卡撑得住）。默认邀请制激活，记得设置管理员的聊天 id。

- at least 8G of GPU memory 我不配
