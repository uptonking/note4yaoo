---
title: lib-collab-crdt-community-pm-showcase
tags: [community, crdt, showcase]
created: 2023-11-01T03:15:08.731Z
modified: 2024-08-11T07:21:11.986Z
---

# lib-collab-crdt-community-pm-showcase

# guide

# discuss
- ## 

- ## Architectures for Central Server Collaboration
- https://news.ycombinator.com/item?id=40579892
- 
- 
- 
- 

- ## 📓 My presentation about "Collaborative editing in Jupyter" at PyData Paris has been accepted _202406
- https://x.com/davidbrochart/status/1796838314386866396
  - I'll talk about the latest developments and how CRDTs are making their way and redefining the architecture of Jupyter(Lab): chat system, server-side execution...

- I'm not sure how collaboration plays with JupyterHub, since you get a dedicated Jupyter Server/Lab instance for each user. I don't know if there is a way to share a server between multiple users with JupyterHub?
- Interested to know how collaborative editing in jupyter can play a roller in a jupyter hub
  - If it's not possible now, I think we should find a way to fund the dev work to bring this to jupyterhub. It feels like a no brainer since the hub is the most common multi-user technology in the jupyter ecosystem. Would have a huge impact
- RTC on JupyterHub is documented here 
  - [Real-time collaboration without impersonation — JupyterHub documentation](https://jupyterhub.readthedocs.io/en/stable/tutorial/collaboration-users.html)

- https://x.com/davidbrochart/status/1796138236516991392
  - CRDTs are making their way into JupyterLab, with a new collaborative input widget
  - This allows multiple users to type into the input box, and to recover the widget after closing/reopening the window, preventing the notebook from deadlocking.

- ## A long-standing issue in Jupyter is about to get fixed: getting back a notebook state when reconnecting.
- https://twitter.com/davidbrochart/status/1722564382813516093
  - It will be available in jpterm and jupyverse first, then in JupyterLab.
  - This demo shows that outputs are restored but it will also work with widgets. It's all powered by CRDT.
- I think jpterm will be the playground for most innovations in the Jupyter ecosystem, before they land in JupyterLab. The reason is the same as the one behind Textual: it's easier to use than web technology.

- ## 🌰 分享我设计的基于CRDT的软件架构 hamsterbase
- https://twitter.com/hamsterbase/status/1590005075581497344
  1. 以 CRDT 文件作为 single source of truth, 保证向前向后兼容。
  2. 以 sqlite 数据库作为缓存。 sqlite 的数据库格式可以按照需求任意设计，可以随意修改。
  3. 不同客户端直接通过点对点同步 CRDT 文件，支持完全离线可用，同步无冲突。
- 数据库的crdt同步怎么设计的
  - 一个网页对应一个 CRDT 的文件（类似于 JSON）
  - 每次同步的时候，获取对方的文件列表、本地的文件列表
  - 对列表进行 DIFF, 发送本地多的，拉取本地少的。

- 你可以在本地跑 hamsterbase 试试看。 文件结构都在本地的
  - 可以把文件的版本号放在前面，这样可以在不读取完整文件的情况下获取当前的所有 CRDT 文件。

- 可以把 CRDT 同步抽象出来，同步服务不需要关心 CRDT 的格式
  - 这个是我从零设计的。 CRDTSyncDir 可以用 webdav , fs , oss , http 实现。 
  - 每次同步就是拿本地 fs 实现的 dir 和 http 实现的 remote dir 同步。

```typescript

interface CRDTSyncDir{
  listAllFiles();
  fileStat(id,version)
  listVersions(id)
  getVersion(id)
  read(id,version,filter)
  write(id,content)
}

```
