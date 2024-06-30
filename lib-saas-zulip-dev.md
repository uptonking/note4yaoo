---
title: lib-saas-zulip-dev
tags: [im-chat, zulip]
created: 2024-06-23T02:06:55.899Z
modified: 2024-06-23T02:09:33.877Z
---

# lib-saas-zulip-dev

# guide
- pros
  - 100% open-source, not open-core
  - export支持html
    - import支持mattermost/RocketChat
  - guest mode with login
  - unlimited message history search
  - unlimited file sharing and storage
  - Voice and video calls (1on1/group): Choose a call provider (Zoom, Jitsi, etc.)
  - client-apps: mobile, pc, terminal

- cons
  - widget服务端相关功能未提供plugin api，需要fork代码手动修改
  - ui seems outdated

- features
  - designed around conversations that are labeled with topics, to make communication organized and efficient

- who is using #zulip
  - ?

- tips-im-chat
  - usecase: 聊天消息、多人协作
  - 🧐💡 聊天社交应用通常具有巨大的先发优势，特别是数据格式和导入导出，主流参考zulip/mattermost
  - 主流im应用倾向于在chat流程中embed和操作其他平台的内容
  - 在chat-room内操作 doc/code

- chat-sdk的设计考虑支持多种主流im应用
  - 与ai或bot的对话可参考类似产品的设计和api，如chatgpt、copilot
  - 以stream形式返回响应
# draft

# dev-xp

# changelog

# more
