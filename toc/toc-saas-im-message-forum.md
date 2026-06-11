---
title: toc-saas-im-message-forum
tags: [forum, im, repos, toc]
created: 2020-08-31T13:15:14.391Z
modified: 2021-05-14T15:04:15.333Z
---

# toc-saas-im-message-forum

# guide

- tips-chat sdk
  - usecase: 聊天消息、多人协作
  - 🧐💡 聊天社交应用通常具有巨大的先发优势，特别是数据格式和导入导出，主流参考zulip/mattermost
  - 主流im应用倾向于在chat流程中embed和操作其他平台的内容
  - 在chat-room内操作 doc/code
  - chat-sdk的设计考虑支持多种主流im应用

- tips-forum
  - forum的核心也是ugc内容，所以和blog功能相似度高
  - 💡 cms中的内容评论也可以作为forum
  - 商城app-store类产品的开发和imdb类似，偏向搜索

- 论坛选型参考
  - 尽量选择开源产品，方便自定义
  - 考虑导出数据的功能，可导出本论坛管理员和会员的交流帖子及评论
    - 开源论坛可直接copy数据库，不存在此问题
    - 付费产品如vanilla forum可导出mysql dump

- who is using #discourse
  - prosemirror
  - handsontable
  - yjs
  - tidb-tug
  - observablehq-notebook, tiddlywiki
  - openstreetmap

- forum-open
  - discourse
  - nodebb
  - spectrum
  - Mumble for voice and text, jitsi for video calls

- chat-open
  - mattermost
  - zulip
  - gitter
  - telegram的client都是开源的, webK/webA
  - rocketChat(meteor)
  - Spacebar(discord-like)
  - [5 open source alternatives to Slack for team chat | Opensource.com](https://opensource.com/alternatives/slack)
# forum-popular
- https://github.com/discourse/discourse /GPLv2/202401/ruby/js
  - 依赖emberjs、postgresql、redis、Sidekiq(job-processing by Redis) 
  - discussion platform built for the next decade of the Internet.
- https://github.com/forem/forem /AGPLv3/202402/ruby/js
  - https://forem.com/
  - the platform that powers dev.to
  - We run on a Rails backend, and we are currently transitioning to a Preact-first frontend.
- https://github.com/withspectrum/spectrum /js/archived
  - 依赖express、graphql、apollo、draft-js、redux、rethinkdb
  - Spectrum aims to be the best platform to build any kind of community online by combining the best of forums and real-time chat apps.
  - RethinkDB: Data storage

- https://github.com/apache/answer /15kStar/apache2/202509/go/ts
  - https://answer.apache.org/
  - https://meta.answer.dev/
  - A Q&A platform software for teams at any scales. 
  - Plugins: redis/es/algolia
  - 依赖注入使用wire
  - 依赖gin、xorm
  - [Elasticsearch is a good candidate for the underlying database? _202210](https://github.com/apache/answer/issues/29)
    - In Answer project, we use XORM to be the abstraction layer of database, so all data operations are designed for relational database. 
    - If you want to use ElasticSearch, you need to write your own data access layer. 
- https://github.com/casbin/casnode /apache2/202312/go
  - Open-Source Forum and Social Platform, Alternative to StackOverflow & Flarum
  - Go (Beego) + MySQL

- https://github.com/NodeBB/NodeBB /GPLv3/202401/js
  - https://nodebb.org/
  - https://community.nodebb.org/
  - Node.js based forum software built for the modern web
  - powered by Node.js and supports either Redis, MongoDB, or a PostgreSQL database
  - 〰️ It utilizes web sockets for instant interactions and real-time notifications
  - Hosting NodeBB for a few years with custom sso plugin. NodeBb is awesome but the plug-in ecosystem is hell, as most plugins don't get regular updates and break on new versions (break like you can no longer activate them because semver rules mismatch)
  - [Local development should use non-daemonised DB](https://github.com/NodeBB/NodeBB/issues/1094)
    - We're definitely fans of re-use, and we do use existing modules, though in certain cases (DBAL and template engine), we roll our own for performance and workflow purposes.

- MBBS /52Star/MIT/202312/ts/功能全
  - https://github.com/linfaxin/MBBS
  - http://mbbs.cc/
  - http://bbs.mbbs.cc/
  - 轻量级全功能论坛、移动/PC双端适配、无依赖一键启动、技术栈 express + sqlite + react
  - 后端依赖express、sequelize、sqlite3、svg-captcha
  - 前端依赖mui、ahooks、umi3
  - 全功能论坛：板块/楼中楼/角色权限/审核/富文本编辑/个性化配置/邮件通知 等
  - 自带授权登录：免开发支持 QQ/微信/支付宝 授权登录

- ddd-forum /1.8kStar/ISC/202306/ts/inactive
  - https://github.com/stemmlerjs/ddd-forum
  - https://dddforum.com/
  - Hacker news-inspired forum app built with TypeScript using DDD practices from solidbook.io.
  - 后端依赖 express、sequelize、redis
  - 前端依赖 react、redux、react-quill
  - https://github.com/dyarleniber/typescript-ddd-forum

- https://github.com/replyke/monorepo /apache2/202509/ts
  - https://replyke.com/
  - [I built Replyke: an open-source social infrastructure layer (comments, feeds, notifications, profiles) for your apps : r/reactjs](https://www.reddit.com/r/reactjs/comments/1nv6zaa/i_built_replyke_an_opensource_social/)
    - It’s a non-intrusive data layer that integrates with your existing systems
    - No changes to your data or auth
    - Full-featured comment sections with @mentions/Threaded-replies/Likes
  - https://github.com/replyke/express
    - Open-Source Framework for Social Features. 
    - Build social apps faster with powerful API and SDKs for JavaScript, React, and React Native
  - https://github.com/replyke/reel-snap
    - a modern boilerplate for building social networks inspired by TikTok and Instagram Reels. 
    - It comes with fully functional authentication, dynamic feeds, profiles, and a suite of social features. 
    - ReelSnap is powered by Replyke
    - Thanks to Replyke, ReelSnap comes with a robust, plug-and-play backend. This project functions perfectly well without a server, making it easy to get started.
  - https://github.com/replyke/social-network-tutorial
    - This project demonstrates how to create a fully functional social network using Replyke 
    - [How to Build a Social Network in 1 Day: Part 1 - Introduction - DEV Community](https://dev.to/tsabary/how-to-build-a-social-network-in-1-day-part-1-introduction-1a3d)

- orca /1.1kStar/MIT/202203/ts/inactive/功能全
  - https://github.com/DimiMikadze/orca
  - https://dimimikadze.github.io/orca-docs/
  - Build modern community apps with React and Node.
  - 后端依赖express、mongoose、passport、nodemailer
  - 前端依赖redux、styled-components、react-query
  - 实现了私信messenger、通知notification、newsfeed，即im+博客文章
  - 🍴 forks
  - https://github.com/BrunoAmerio/orca

- cnode
  - https://github.com/cnodejs/nodeclub
    - Nodeclub 是使用 Node.js 和 MongoDB 开发的社区系统
    - 依赖mongodb4、redis4
  - https://github.com/cnodejs/egg-cnode
    - CNode 社区 Egg 版本; /201810
- https://github.com/ChenJiaH/react-cnode
  - 基于react&react-router-dom，利用CNode API重写CNode社区。
  - 依赖只有react-router.v5, react, axios

- https://github.com/heybereket/oasis /202107/inactive
  - The chat and forums platform for communities
  - 后端依赖 express、typeorm、passport
  - Backend and GraphQL API
  - React GraphQL Hooks

- https://github.com/matevsh/web-forum /ts/代码少
  - SPA full-stack app mainly focused on forum functionality
  - 后端依赖express、prisma
  - 前端依赖react

- https://github.com/mightofcode/v3ex-react
  - https://v3ex.mocyx.com/
  - 技术栈： Koa、React、Nextjs、Mongodb、mongoose

- - https://github.com/youknowznm/rhaego /202204/js
  - 基于 react + koa, 开箱即用的 Material Design 风格博客系统
  - 基于嵌入式数据库 NeDB, 即插即用
  - 未使用任何组件库 / 样式库 / 动画库

- https://github.com/amirfakhrullah/bloqdown /BSD/202304/ts
  - Simple Markdown Forum/Blog site using Next.js, NextAuth, TypeScript, tRPC, Prisma and PlanetScale
  - 风格类似github
  - Creating fully typesafe APIs using tRPC
  - Auth using NextAuth (Github Provider)
  - Display repository data using GitHub API
  - https://github.com/planetscale/nextjs-planetscale-starter
    - A Next.js starter app with NextAuth.js (Auth), Prisma (ORM), and PlanetScale (database), ready to be deployed on Netlify
# forum-non-nodejs
- https://github.com/LemmyNet/lemmy /AGPLv3/202402/rust
  - https://join-lemmy.org/
  - Lemmy is similar to sites like Reddit, Lobste.rs, or Hacker News
  - 依赖Actix、Diesel、Inferno
  - anyone can easily run a server, and all these servers are federated (think email), and connected to the same universe, called the Fediverse.
  - A forum software that supports ActivityPub federation. 
  - The web framework used is Actix, the frontend is in JavaScript
  - https://github.com/LemmyNet/lemmyBB
    - A Lemmy frontend based on phpBB 3.3.

- https://github.com/freedit-org/freedit /MIT/202406/rust
  - https://freedit.eu/
  - The safest and lightest forum, powered by rust
  - 依赖axum、cached、captcha、jieba-rs、tower
  - Easy to deploy: one binary to run, using embedded database sled
  - No javascript at all, for safety maximization
  - Markdown support
  - inn: Subgroup like Subreddits
  - solo: Personal space like Twitter

- https://github.com/kenyipp/discuz /MIT/202302/rust/inactive
  - This rust-based forum server, named Discuz, is a sample project showcasing the use of Actix-web for CRUD operations, authentication, routing, pagination and more.
  - not thoroughly tested

- https://github.com/corepaper/morum /AGPLv3/202306/rust
  - A forum software that leverages the Matrix Protocol

- https://github.com/libreddit/libreddit /AGPLv3/202311/rust
  - An alternative private front-end to Reddit

- https://github.com/joschan21/breadit /202307/ts/inactive
  - Modern Fullstack Reddit Clone in Next.js 13 & TypeScript
  - https://github.com/shadeemerhi/reddit-clone-yt /202301/ts
- https://github.com/puzzlerush/reddit-clone /202108/js
  - Full stack reddit clone built with React, Redux, Node.js, Express, and PostgreSQL.
- https://github.com/romerorocha/reddit-clone-api
  - Forum API Server
  - 依赖express，不依赖orm
- https://github.com/codelucas/flask_reddit /201802/python
  - Reddit clone in flask + python + nginx + https

- https://github.com/mybb/mybb /LGPLv3/202312/php
  - https://mybb.com/
  - a free and open source forum software
- https://github.com/flaskbb/flaskbb /BSD/202303/python/inactive
  - https://flaskbb.org/
  - A classic Forum Software in Python using Flask

- https://github.com/divanov11/Mumble /apache2/202108/js
  - https://www.mumble.dev/
  - open source social media platform and public forum for questions and discussions, built for developers.
  - https://github.com/divanov11/mumbleapi /202107/python
    - Backend/API for the Mumble.dev, an open source social media application.
  - https://github.com/divanov11/mumble2 /202205/js
    - https://www.mumble2.dev/
    - A real time messaging & video calling.
    - Create an account on agora.io and create an app to generate an APP ID

- https://github.com/dakshit050/AskAnything
  - a social discussion platform Developed for college/school students to solve their doubts online

- https://github.com/debiki/talkyard /AGPLv3/202310/scala
  - A structured discussions platform — brings together the main features from StackOverflow, Slack, Discourse, Reddit/HackerNews, and Disqus blog comments.
  - Client: React.js, TypeScript, Webdriver.io.
  - Server: Scala and Play Framework. OpenResty, some Lua. React.js in Java's Nashorn Javascript engine.
  - Databases: PostgreSQL, Redis, ElasticSearch.

- https://github.com/carbon-bond/carbonbond /202304/rust/ts/inactive
  - 一個次世代的論壇。它在文章之間的交互作用
  - 前端：使用 typescript + React
  - 后端：使用 Rust

- https://github.com/proshoumma/ReForum /201809/js/archived
  - A minimal forum board application. 只是仪表板
  - Built on top of React-Redux frontend, ExpressJS-NodeJS backend (with PassportJS for OAuth) and MongoDB databse.

- https://gitlab.com/tildes/tildes /AGPLv3/202306/python/jinja
  - https://tildes.net/
  - a non-profit community site

- https://github.com/rocboss/paopao-ce /4.4kStar/MIT/202508/go
  - An artistic "twitter like" community built on gin+zinc+vue+ts 清新文艺微社区
  - 配置文件中的 Features 小节是声明paopao-ce运行时开启哪些功能项
  - 依赖gin、gorm、resty、lumberjack、jwt
# forum-nodejs
- jixialunbi /12Star/GPLv3/202211/ts
  - https://github.com/bs32g1038/jixialunbi
  - http://www.jixialunbi.com/
  - 微社区系统
  - 前端依赖ant-design，nextjs
  - 后端依赖nestjs、mysql、prisma、meilisearch、skia-canvas、canvaskit-wasm、passport
- node-blog /111Star/MIT/202207/ts
  - https://github.com/bs32g1038/node-blog
  - https://www.lizc.net/
  - react blog project base on nestjs, mongoose, typescript, react, ant-design, nextjs

- https://github.com/ValeriaSWE/Valeria-Forum
  - Valera Roleplay Forum - Gymnasiearbete
  - 后端依赖 express、mongoose、multer

- https://github.com/seawind8888/Nobibi /202011/ts/inactive
  - Nobibi 是一款轻量级开源社区，包含前后台
  - 前台考虑 SEO 使用 next.js + antd 服务端渲结构
  - 后台系统基于Ant Design Pro(react + dvajs + umijs)搭建开发
  - 后端接口为 koa+moogoose

- https://github.com/EricBollar/Fullstack-Forum
  - fullstack forum built using industry-standard tools such as Next.js and PostgresQL.

- https://github.com/halchester/csqa /inactive/unfinished
  - https://csqa.vercel.app/
  - a Progressive Web App aimed for those who wanna ask silly questions but afraid to get downvoted on stackoverflow

- https://github.com/liyupi/code-nav /MIT/202111/js/ts/java
  - https://www.code-nav.cn/
  - 以 “帮助大家发现优质编程资源，提升学习效率” 为目标
  - server使用spring

- https://github.com/dafengzhen/youdeyiwu-frontend
  - 依赖typescript + react + next、axios、react-query、bootstrap
  - https://github.com/dafengzhen/youdeyiwu-backend
    - 依赖java 17 + spring-boot + jpa、mariadb 10.6、redis、rabbitmq、minio
  - https://github.com/dafengzhen/youdeyiwu-editor
    - 以 ckeditor5 classic editor 为基础自定义构建，集成了自定义和常用插件

- https://github.com/joincomet/comet /202107/ts
  - All-in-one chat and forums for communities
  - 依赖express、apollo-server-express、graphql、metascraper
  - switch from ws to SSE
- https://github.com/gudfhr95/stelllar /202212/ts/archived
  - Forum & Chat for Communities
  - 依赖nestjs、graphql、mikro-orm、next13

- https://github.com/SABERGLOW/Mimir
  - A forum-based knowledge hub using Next.js & Tailwind CSS
  - 依赖graphql

- https://github.com/plebbit/plebbit-js
  - plebbit-js is an NPM module to wrap around the IPFS APIs used by plebbit. It is used in all clients: CLI, Electron (desktop GUI) and web.

- https://github.com/reiwa/swimmy
  - online forum for Japanese built with mui and Blitz.js
# forum-ui
- https://github.com/cwellsx/view
  - https://cwellsx.github.io/view/
  - Forum software written using ReactJS and TypeScript.
  - 无后端实现，但定义了后端数据类型，mockFetch
  - 论坛风格类似stackoverflow

- https://github.com/seudosan/forumu
  - React library for manage forms 

- https://github.com/AliFarajzade/foruma
  - NextJs, TypeScript Forum Website Designed with ChakraUI.
- https://github.com/ruheni/discussions
  - https://discussions.fly.dev/
  - WIP(barely alpha): Community discussions web app
  - Database ORM with Prisma
  - Styling with Chakra UI

- https://github.com/Qiming-Liu/ThinkMoreForum-Frontend
  - ThinkMore Forum frontend build with Next.js, Typescript, MUI.
  - As a discussion platform, it is multifunctional, interactive, and mobile-ready. 
  - Administrators can easily set the look and topic of the forum, manage user permissions, and customize the site footer.
  - https://github.com/Qiming-Liu/ThinkMoreForum-Backen d /java
    - Forum backend build with Spring Boot, JWT, Prometheus.
# customer-support
- https://github.com/laudspeaker/laudspeaker /AGPLv3/202401/ts
  - https://laudspeaker.com/
  - Open Source Cross Channel Customer Messaging Platform that you can self host. 
  - alternative to Braze / Iterable / One Signal / Customer Io

- https://github.com/fonoster/fonoster /MIT/202312/ts
  - https://fonoster.com/
  - open-source alternative to Twilio
  - Engage with your customers with voice or messaging with a single, easy-to-use platform.
  - Multitenancy

- https://github.com/chatwoot/chatwoot /MIT/202402/ruby/js/vue
  - https://www.chatwoot.com/help-center
  - Customer engagement suite, an open-source alternative to Intercom, Zendesk, Salesforce Service Cloud etc.
# chat-im-instant-messaging-chat
- https://github.com/42wim/matterbridge /202212/go
  - bridge between mattermost, IRC, gitter, xmpp, slack, discord, telegram, rocketchat, twitch, ssh-chat, zulip, whatsapp, keybase, matrix, microsoft teams, nextcloud, mumble, vk and more with REST API
  - Mattermost isn't required to run matterbridge

- https://github.com/satorijs/satori /MIT/202402/ts
  - The Universal Messenger Protocol
  - QQ Guild、Feishu、telegram、discord

- https://github.com/spacebarchat/server /AGPLv3/202402/ts
  - https://spacebar.chat/
  - https://docs.spacebar.chat/
  - Spacebar server - A reimplementation of the Discord.com backend, built with typescript
  - Spacebar is a free and open source, full stack reverse engineering and reimplementation of Discord.
  - 依赖typeorm、lambert-server、amqplib、i18next、multer、ws
  - We aim to reverse engineer and add additional features to the Discord backend, while remaining completely backwards compatible with existing bots, applications, and clients.
  - You should be able to use any client designed for Discord.com to connect to a Spacebar instance. However, some incompatibilities still exist between Spacebar and Discord. 
  - 🐛 Currently there is no voice or video support in any Spacebar instance. This is a very difficult feature to get working, especially given that we must implement it the exact same way as Discord.com for client compatibility
  - [Plugin system _202208](https://github.com/spacebarchat/server/issues/840)
    - A server plugin may be used to control controlled accounts and bots. This would also be useful to subject them to policies as if they were users.
  - [Embeds - Spacebar Documentation](https://docs.spacebar.chat/setup/server/configuration/embeds/)
    - Embeds in Spacebar are external content that is displayed within your messages when linked to. 
  - https://github.com/spacebarchat/client /AGPLv3/202312/ts
    - https://app.spacebar.chat/
    - Open source, themeable and extendable discord-compatible native Spacebar client
    - 依赖mobx-react-lite、react-markdown、react-virtualized
    - [Roadmap · spacebarchat/client _202209](https://github.com/spacebarchat/client/issues/94)
  - https://github.com/spacebarchat/fosscord-web-client /archived
  - https://github.com/SpacingBat3/WebCord /MIT/202402/ts
    - A Discord and SpaceBar-based client implemented without Discord API.
    - A major rewrite of the client is being worked on
  - https://github.com/morroid/Morroid /MIT/202306/ts/archived
    - A reverse-engineered discord server written in typescript
  - https://github.com/spacebarchat/spacebarchat /仅文档

- Linen /1.2kStar/AGPLv3/202404/ts/discord-like
  - https://github.com/Linen-dev/linen.dev
  - https://www.linen.dev/
  - https://slack-chats.kotlinlang.org/
  - Linen is a Google-searchable community chat tool. 
  - Linen was built as an alternative to closed tools like Slack and Discord.
  - 依赖headlessui、tanstack-query、nextjs、swr、prisma、express、zod

- tailchat /2.4kStar/apache2/202403/ts
  - https://github.com/msgbyte/tailchat
  - https://tailchat.msgbyte.com/
  - Not only another Slack, Discord, Rocket. Chat....
  - Next generation noIM application in your own workspace
  - 目前现有的 IM 应用都仅仅把目光局限在聊天本身，而 IM 天然作为一个多人协作方式，在我看来应当能够承担更多的职责，将外部的应用以 IM 为转发方式形成自己独特的工作流。
  - 设计了以 IM 为中心，第三方应用为增强功能，中间以插件系统作为胶水连接层的个人 / 团队高度自定义的应用平台。
  - Tailchat 这样的一个从底层设计之初就为了拓展而存在的即时通讯应用。
  - 通过 Tailchat 的插件系统，开发者可以很轻松的将喜欢的应用以一种非常自然的方式作为 Tailchat 的一部分
  - 后端依赖@socket.io/admin-ui、ejs、typegoose、mongoose、moleculer微服务、moleculer-minio、redlock(redis)
  - 前端依赖zustand、antd、ahooks、use-gesture、immer、react-dnd、react-virtuoso
  - 前端微内核架构+后端微服务架构，Tailchat 已经为集群化部署做好了准备。
  - 二维的群组空间，通过频道来分割不同的话题
  - 主要功能模块
    - 用户管理
    - 聊天系统
    - 插件系统
    - 开放平台
  - [feat: add AI Assistant plugin for Tailchat _202305](https://github.com/msgbyte/tailchat/commit/060d07ae8ee36dcf088ad253a18e6cabcd80f4d7)
  - [期望可以支持和机器人进行私信聊天 (已支持) _202402](https://github.com/msgbyte/tailchat/issues/212)
  - [可以像ChatGPT一样消息可以流式加载吗 _202311](https://github.com/msgbyte/tailchat/issues/185)
    - 可以有替代方案实现。默认没有
  - [希望添加后台权限组功能和内置新的语音插件 _202307](https://github.com/msgbyte/tailchat/issues/117)
    - 没有计划去做更加细分的权限控制。欢迎pr
    - websocket 开放平台sdk正在开发中

- https://github.com/xiweicheng/tms /MIT/202309/js/vue2/java/inactive
  - TMS是基于频道模式的团队沟通协作+轻量级任务看板，支持mardown、富文本、在线表格和思维导图的团队博文wiki，i18n国际化翻译管理的响应式web开源团队协作系统。

- https://github.com/Privoce/vocechat-web /GPLv3/202403/ts
  - Private Hosted IM and Social Channels, Easy Integration to Your Site or App
  - VoceChat is a superlight Rust powered chat App, API and SDK that prioritizes private hosting
  - 依赖react、redux-toolkit、plate、tui-editor、localforage
  - https://github.com/Privoce/vocechat-server-rust /202303/rust/inactive
    - superlight rust written social server.

- https://github.com/revoltchat/backend /1.1kStar/AGPLv3/202406/rust
  - https://revolt.chat/
  - https://developers.revolt.chat/api/
  - Monorepo for Revolt backend services
  - https://github.com/revoltchat/revite
    - Revolt client built with Preact

- https://github.com/yinxin630/fiora /MIT/202207/ts/inactive
  - https://yinxin630.github.io/fiora/
  - An interesting open source chat application. 
  - Developed with node.js, mongoDB, socket.io and react
  - backend, frontend, Android and iOS apps

- https://github.com/zulip/zulip /apache2/202401/python/django
  - https://zulip.com/
  - open-source team collaboration tool with unique topic-based threading that combines the best of email and chat to make remote work productive and delightful.
  - Zulip is the only modern team chat app that is designed for both live and asynchronous conversations.
  - The Zulip Botserver is a Python (Flask) server that implements Zulip's outgoing webhooks API
  - https://github.com/zulip/docker-zulip
    - This image is not designed to make it easy to run multiple copies of the zulip application server container (and you need to know a lot about Zulip to do this sort of thing successfully). 
    - If you're interested in running a high-availability Zulip installation, your best bet is to get in touch with the Zulip support team at support@zulip.com.

- https://github.com/mattermost/mattermost /AGPLv3/202402/go/ts
  - https://mattermost.com/
  - open source platform for secure collaboration across the entire software development lifecycle.
  - written in Go and React and runs as a single Linux binary with MySQL or PostgreSQL.
  - A new compiled version is released under an MIT license every month on the 16th.
  - You are licensed to use compiled versions of the Mattermost platform produced by Mattermost, Inc. under an MIT LICENSE

- https://github.com/openimsdk/open-im-server /15.3kStar/AGPL > apache2/202510/go
  - https://openim.io/
  - Unlike standalone chat applications such as Telegram, Signal, and Rocket. Chat, OpenIM offers an open-source instant messaging solution designed specifically for developers rather than as a directly installable standalone chat app
  - Comprising OpenIM SDK and OpenIM Server, it provides developers with a complete set of tools and services to integrate instant messaging functions into their applications
  - 依赖gin、gorm、rockscache、jwt、websocket、grpc、gokit、cobra
  - 202311改为使用mongodb，未使用gorm，[Feat/mongo pr](https://github.com/openimsdk/open-im-server/pull/1447)
  - 🏠 Microservices Architecture: Supports cluster mode, including a gateway and multiple rpc services.
  - Diverse Deployment Options: Supports source code, Kubernetes, or Docker deployment.
  - Supports large-scale groups with hundreds of thousands, millions of users, and billions of messages.
  - OpenIM aims to provide developers with the necessary tools and framework to implement efficient instant messaging solutions in their applications.
  - OpenIMSDK, designed for OpenIMServer, is an IM SDK created specifically for integration into client applications.
  - [[FEATURE REQUEST] Proposal for Integration of FerretDB as an Alternative Database Backend for OpenIM _202404](https://github.com/openimsdk/open-im-server/issues/2250)
    - OpenIM currently relies on MongoDB for data storage. This proposal aims to integrate FerretDB, a MongoDB-compatible open-source database that avoids licensing constraints and offers more backend storage options, enhancing OpenIM's adaptability and performance.
  - [[Deployment] Could im change mongdb to another database？ _202505](https://github.com/openimsdk/open-im-server/issues/2868)
    - we don’t have that plan at the moment.
    - This is typically not a small task; you’ll need to implement all of the database interfaces under `Open-IM-Server\pkg\common\storage\database`.
    - [How to modify the code to use PostgreSQL instead of MySQL _202309](https://github.com/openimsdk/open-im-server/issues/1138)
    - We plan to replace MySQL with MongoDB
  - [[FEATURE REQUEST] Can Openim use PGMQ as the message queue processor to minimize middleware? _202412](https://github.com/openimsdk/open-im-server/issues/2921)
    - pgmq can be used as a replacement for Kafka, abandoning heavy components such as Kafka. Kafka is too resource-intensive.
    - If the community plans to implement all of this in the future, I will reopen it
  - [Multi-tenant _202505](https://github.com/openimsdk/open-im-server/issues/3373)
    - The multi-tenant feature obviously has many benefits. Unfortunately, we don't plan to develop this in the open-source version.
  - https://github.com/openimsdk/openim-sdk-core /447Star/AGPL/202509/go
    - the core SDK of OpenIM, serving as the cross-platform foundation for all open-source OpenIM SDKs (excluding mini web).
    - All open-source OpenIM SDKs (except mini web) are built upon this core layer, ensuring consistency, stability, and seamless cross-platform integration.
  - https://github.com/openimsdk/openim-electron-demo /AGPL
    - Instant Messaging web desktop Windows/Mac/Linux

- https://github.com/juravlevdima/PERN-chat /ISC/202212/ts/inactive
  - Chat made with PERN Stack & Socket. IO
  - PostgreSQL | Sequelize
  - React | React Router | Redux Toolkit

- https://github.com/sdelements/lets-chat /MIT/201708/js/inactive
  - https://sdelements.github.io/lets-chat/
  - Self-hosted chat app for small teams
  - 依赖express.oi、mongoose、nunjucks、passport
  - https://github.com/RahulM4/LetsChat /202310/js/fe+be
    - https://github.com/RahulM4/letschat-vercel-api /202311/js

- https://github.com/RocketChat/Rocket.Chat /MIT+EE/ts/meteor
  - https://rockhttps://github.com/RocketChat/Rocket.Chatet.chat/
  - fully customizable communications platform developed in JavaScript for organizations with high standards of data protection.
  - We are a MERN based application enabling real-time conversations
  - 依赖meteor、mongodb
  - Rocket. Chat uses the Meteor open-source framework, and the data is typically stored in MongoDB

- https://gitlab.com/gitterHQ/webapp /MIT/202302/js/archived/gitlab
  - https://gitter.im/
  - a community for software developers. 
  - This codebase even covers a lot of the mobile and desktop applications which embed a web frame.
  - Mongodb (persistent storage)
  - Elasticsearch (search)
  - Redis (caching and some persistent storage)
  - Neo4j (suggestions)
  - [Feature parity of Matrix-based Gitter regarding GitHub/GitLab integration _202301](https://gitlab.com/gitterHQ/webapp/-/issues/2861)
    - Following the recent announcement that Gitter is on the verge of migrating to be fully backed by Matrix, I am curious about what is the plan for features that are not (yet?) available on the Matrix side of things. Specifically, GitHub/GitLab-related features, like synced room management permissions with GitHub organization membership, issue
  - [Gitter is open source | Hacker News_201707](https://news.ycombinator.com/item?id=14694283)
  - https://gitlab.com/gitterHQ/realtime-client
    - Gitter uses Faye for it's realtime communications. 
    - It uses Faye as a fairly low-level messaging interface, and it can be quite difficult to implement an application correctly on top of it, especially when dealing idiosyncrasies(气质，习性) in the protocol
    - It uses Backbone Collections to represent Gitter data. The client will populate the collection and maintain the state of the collection to match the server-side representation of the state.
  - https://github.com/gitterHQ/gitter /201707

- https://github.com/TryQuiet/quiet /GPLv3/clang/cpp/ts
  - https://www.tryquiet.org/
  - A private, p2p alternative to Slack and Discord built on Tor & IPFS

- https://github.com/meetfranz/franz /4.4kStar/apache2/202308/js
  - https://meetfranz.com/
  - free messaging app for services like WhatsApp, Slack, Messenger and many more

- https://github.com/penghuwan/online-chat-app /201908/js
  - 一个在线聊天室，实现了登陆注册功能和聊天功能，
  - 实时通信部分基于Socket.io实现，后端采用Koa框架组织业务逻辑，前端采用React编写，同时用Webpack作为打包工具

- https://github.com/adrianhajdin/project_chat_application /202009/js
  - In this tutorial we are going to build and deploy a real time chat application. 
  - Covered topics: React.js, Node.js, Express.js, and Socket.io.
  - https://github.com/adrianhajdin/chat_application

- https://github.com/brave-chat/brave-chat /MIT/202309/js
  - The ultimate slack alternative built with React, MUI, Redux, and friends.

- https://github.com/jungleworks/fugu-server /apache2/202108/js
  - https://github.com/jungleworks/fugu-frontend /ts
  - open source, private cloud, Slack-alternative

- https://github.com/MehraDevesh2022/chat-mind /202308/js
  - a full stack chat application that allows users to communicate with each other in real-time. 
  - built with the MERN stack and Socket. IO
  - 依赖express-fileupload、mongoose、socket.io、bcryptjs、react-scrollable-feed、mui.v4
  - It supports features like user authentication, one-on-one chat, group chat, user profile management, and more.

- https://github.com/teamgram/teamgram-server /apache2/202402/go
  - https://teamgram.net/
  - Unofficial open source mtproto server written in golang with compatible telegram client.
  - [Durov's reasoning on not open sourcing the server code : r/Telegram](https://www.reddit.com/r/Telegram/comments/ktthig/durovs_reasoning_on_not_open_sourcing_the_server/)
    - Publishing the server code doesn’t improve security, because - unlike with the client-side code - there’s no way to verify that the same code is run on the servers.
  - https://github.com/DrKLO/Telegram /GPLv2/202402/java/cpp
    - Telegram for Android source
    - [Pavel Durov on Twitter: The source code of Telegram for iOS and Android is open and free. Enjoy! : r/Android _201703](https://www.reddit.com/r/Android/comments/62lg6j/pavel_durov_on_twitter_the_source_code_of/)
    - but this doesn't change the fact their server is proprietary and crypto is questionable. 
    - [Why Telegram code is so ugly? : r/androiddev _201907](https://www.reddit.com/r/androiddev/comments/cazz4h/why_telegram_code_is_so_ugly/)
  - https://github.com/Telegram-FOSS-Team/Telegram-FOSS /GPLv2/202401/java/cpp
    - Unofficial, FOSS-friendly fork of the original Telegram client for Android
  - https://github.com/TGX-Android/Telegram-X /GPLv3/202402/java
    - alternative Telegram client for Android

- https://github.com/balzack/databag /761Star/apache2/202406/go/js
  - A federated messenger for self-hosting
  - Decentralized (direct communication between app and server node)
  - Federated (accounts on different nodes can communicate)
  - Public-Private key based identity (not bound to any blockchain or hosting domain)
  - End-to-End encryption (the hosting admin cannot view topics if sealed)
  - Audio and Video Calls (nat traversal requires separate relay server)
  - Topic based threads (messages organized by topic not contacts)
  - Lightweight (server can run on a raspberry pi zero v1.3)

## chatbot

- https://github.com/baptisteArno/typebot.io
  - https://typebot.io/
  - Typebot is an open-source alternative to Landbot. 
  - a conversational form builder that you can self-host.
  - builder依赖slate-react、tanstack-table
  - It allows you to create conversational apps/forms (Lead qualification, Product launch, User onboarding, Customer support), embed them anywhere on your web/mobile apps, and collect results in real-time.

- koishi /5.2kStar/MIT/202507/ts
  - https://github.com/koishijs/koishi
  - https://koishi.chat/
  - Koishi 是一个跨平台、可扩展、高性能的跨平台聊天机器人框架。
  - 支持 QQ，Telegram，Discord，飞书等主流聊天平台，支持多账户和跨平台数据互通
  - 提供在线插件市场，即使没有任何编程基础，也能轻松在控制台中下载安装插件
  - 随时随地通过控制面板监控运行状态，控制机器人的行为，甚至上号聊天
  - 依赖satorijs、minato(db-driver)、cordis(aop)
  - 经过了长达四年的迭代，Koishi 已经发展出了丰富的插件生态和与之匹配的健壮系统。超过 1000 个官方和社区插件覆盖了机器人开发的方方面面，从平台支持、数据库、资源存储、网页控制台、状态管理到具体的业务功能一应俱全
  - https://github.com/koishijs/novelai-bot /2.5kStar/MIT/202503/ts
    - 基于 NovelAI 的画图机器人
    - [feat: add support for ComfyUI _202406](https://github.com/koishijs/novelai-bot/pull/254)
      - 只支持了基本的text2image和image2image功能

- https://github.com/mckaywrigley/chatbot-ui
  - https://www.chatbotui.com/
  - Chatbot UI is an advanced chatbot kit for OpenAI's chat models built on top of Chatbot UI Lite using Next.js, TypeScript, and Tailwind CSS.

## chat-solutions

- https://github.com/Libera-Chat/sable /AGPLv3/202405/rust
  - https://libera.chat/
  - Sable is an experimental chat server designed to address many of the fundamental limitations of legacy IRC server software. 
  - Server nodes communicate using a Gossip-like protocol, removing the need for a spanning-tree routing and making netsplits
  - Events are propagated between servers via a gossip protocol.

- https://github.com/agnaistic/agnai /AGPLv3/202406/ts
  - https://agnai.chat/
  - AI Agnostic (Multi-user and Multi-bot) Chat with Fictional Characters. 
  - Designed with scale in mind.
  - AI Roleplay Chat with Personalised Characters with your favorite AI services.
  - Based upon the early work of https://github.com/PygmalionAI/galatea-ui /AGPLv3/202302/ts/inactive
  - MongoDB and Redis are optional! Agnaistic will run in "Guest Only" mode if MongoDB is not available.
  - Group Conversations: Multiple users with multiple bots
  - Multiple AI services: Support for Kobold, Novel, AI Horde, Goose, OpenAI, Claude, Replicate, OpenRouter, Mancer
  - Memory/Lore books
  - Optional: Wikipedia Article and PDF embedding
  - MongoDB for persistence
  - Redis for distributed messaging for websockets.
  - SolidJS for interactivity
  - redux

- https://github.com/justadudewhohacks/websocket-chat /201802/js
  - Websocket based group chat app built with socket.io and react.

- https://github.com/featherscloud/chat /MIT/202406/ts
  - https://featherscloud.github.io/chat
  - A local-first chat application with user login
  - A local-first chat application built with different frameworks.
  - Works offline
  - Does not need a server, Can be deployed like any static website
  - 依赖 @featherscloud/auth、@automerge/automerge-repo

## chat-sdk

- https://github.com/lobehub/lobe-chat /32.8kStar/MIT/202406/ts/国内团队
  - https://chat-preview.lobehub.com/
  - https://lobehub.com/docs/usage/start
  - An open-source, modern-design ChatGPT/LLMs UI/Framework.
  - Supports speech-synthesis, multi-modal, and extensible (function call) plugin system.
  - https://github.com/lobehub/chat-plugin-sdk
    - https://chat-plugin-sdk.lobehub.com/
    - SDK for LobeChat function calling plugins
  - https://github.com/lobehub/lobe-chat-plugins
    - https://chat-plugins.lobehub.com/
    - This is the plugin index for LobeChat. It accesses `index.json` from this repository to display a list of available plugins for LobeChat to the user.
  - https://x.com/arvin17x/status/1803761433714507850
    - 目前 #LobeChat 1.0 的技术栈：
    - 应用框架：React 18 + NextJS 14 App Router
    - UI： Ant Design V5 和 Lobe UI
    - 样式库：和 antd 搭配的 CSSinJS 方案 antd-style
    - 前端状态管理： zustand
    - 前端请求库： swr
    - 前端数据库： IndexedDB 与 dexie.js（ORM）
    - 服务端用户鉴权： Clerk 为主，也支持 NextAuth
    - 服务端数据库： Postgres （Serverless 和 普通都支持）
    - ORM: Drizzle ORM
    - 服务端请求框架： tRPC
    - 感觉上面这一套，还能优化就是 Dexie.js 了，希望今年底之前能迁移到 pglite + electric-sql 的新方案，实现真正的 Local First 完全体
    - 现阶段用 pg 就是有一个全套的 auth + 服务端数据库，数据按用户维度保存。不用 pg 走前端db，消息按浏览器维度保存 (换个浏览器数据就没了) 未来个人知识库(文件上传)的功能只会做在 pg 版本上。因为社区不存在纯前端的生产级的 RAG 解决方案。

- https://github.com/vercel/ai-chatbot /apache2/202503/ts
  - https://chat.vercel.ai/
  - A full-featured, hackable Next.js AI chatbot built by Vercel
- https://github.com/vercel/ai /apache2/202406/ts
  - https://sdk.vercel.ai/docs
  - Build AI-powered applications with React, Svelte, Vue, and Solid
  - Vercel AI SDK abstracts away the differences between model providers, eliminates boilerplate code for building chatbots
  - [Allow custom MCP transport _202503](https://github.com/vercel/ai/issues/5179)
    - The new MCP API is great but it's harded-coded with 2 default transport at the moment. Instead, it should accept custom transport.
    - To use AI SDK in non-standard JS environment like Electron / Tauri, browser code that has access to equivalent Node.js APIs for IO but not the same.
  - https://x.com/nicoalbanese10/status/1806680358093541401
    - this is all you need to use chrome's built in ai model with the vercel ai sdk
    - no api keys, no configuration, running locally in the browser
- https://github.com/steven-tey/chathn
  - Chat with Hacker News using natural language. Built with OpenAI Functions and Vercel AI SDK.
- https://github.com/rajeshdavidbabu/pdf-chat-ai-sdk /MIT/202403/ts
  - AI powered Next.js app to chat with your PDF files and get a streamed response using Vercel's AI SDK, Langchain and PineconeDB
- https://github.com/FradSer/next-ai-starter /MIT/202501/ts
  - This Next.js project, built with create-next-app, integrates the Vercel AI SDK for AI capabilities and shadcn/ui for a customizable interface
  - App Router实现了基本的页面跳转逻辑

- https://github.com/slackapi/node-slack-sdk /MIT/202406/ts
  - https://slack.dev/node-slack-sdk
  - Slack Developer Kit for Node.js
  - This SDK is a collection of single-purpose packages. The packages are aimed at making building Slack apps easy, performant, secure, and scalable.
  - 

- https://github.com/lucgagan/completions /MIT/202310/ts
  - https://ray.run/
  - Node.js SDK for interacting with OpenAI Chat Completions API.
  - This SDK makes it simple to: Implement chat in Node.js and browser

- https://github.com/howdyai/botkit /MIT/202204/ts/inactive
  - Botkit is an open source developer tool for building chat bots, apps and custom integrations for major messaging platforms
  - Botkit is part of the Microsoft Bot Framework 

- https://github.com/microsoft/botframework-sdk
  - https://github.com/Microsoft/botbuilder-js /MIT/202406/ts
  - Bot Framework provides the most comprehensive experience for building conversation applications.
  - With the Bot Framework SDK, developers can build bots that converse free-form or with guided interactions including using simple text or rich cards that contain text, images, and action buttons.
  - https://github.com/LuciaHarcekova/ChatGPTMSBotFrameworkWithOpenAI /202304/c#/inactive

- https://github.com/glowing-bear/glowing-bear /GPLv3/202404/js
  - https://www.glowing-bear.org/
  - A web client for WeeChat
  - a web frontend for the WeeChat IRC client and strives to be a modern interface. 
  - https://github.com/weechat/weercd /python
    - WeeChat IRC testing server.

## im/mq-sdk

- https://github.com/emqx/MQTTX /apache2/202503/ts/vue
  - https://mqttx.app/
  - All-in-One MQTT 5.0 client toolbox for Desktop, CLI and WebSocket.
  - 依赖electron、vue-element、typeorm、sqlite、mqttjs
  - MQTTX is a cross-platform MQTT 5.0 client tool open sourced by EMQ, which can run on macOS, Linux and Windows, and supports formatting MQTT payload.
  - MQTTX simplifies test operation with the help of a familiar, chat-like interface
  - MQTTX is designed to connect to test MQTT Brokers such as EMQX, The one-click connection and simple graphical interface make it easy to connect to EMQX or EMQX Cloud to debug and explore functional features.
  - `MQTT` stands for MQ Telemetry Transport. It is a publish/subscribe, extremely simple and lightweight messaging protocol, designed for constrained devices and low-bandwidth, high-latency or unreliable networks.
# mastodon
- resources
  - https://joinmastodon.org/apps
  - [Statuzer: Multi-accounts, multi-columns Mastodon client](https://statuzer.com/)
  - [Elk](https://elk.zone/m.webtoo.ls/public/local)
  - [Phanpy](https://phanpy.social/)

- mastodon /34.8kStar/AGPLv3/202211/js/ruby
  - https://github.com/mastodon/mastodon
  - https://joinmastodon.org/
  - Your self-hosted, globally interconnected microblogging community
  - https://github.com/mastodon/mastodon-android

- https://github.com/tleb/awesome-mastodon
  - Curated list of awesome Mastodon-related stuff
  - https://github.com/nathanlesage/academics-on-mastodon
    - lists consisting of academics on Mastodon

- https://github.com/rustodon/rustodon /AGPLv3/201908/rust
  - A Mastodon-compatible, ActivityPub-speaking server in Rust
  - it's synchronous server ( old Rocket, Old diesel ). 
  - I didn't realize older versions of rocket.rs weren't async.

- https://github.com/neet/masto.js /ts
  - Mastodon API client for JavaScript, TypeScript, Node.js, browsers

- https://github.com/cheeaun/phanpy /js
  - https://phanpy.social/
  - opinionated Mastodon web client
  - Multiple accounts
  - Single or multi-column
  - 还列出了很多平替 Alternative web clients
  - Preact - UI library
  - Valtio - State management
  - React Router - Routing
  - masto.js - Mastodon API client

- https://github.com/soapbox-pub/soapbox /ts/类似twitter
  - https://gitlab.com/soapbox-pub/soapbox
  - https://soapbox.pub/
  - A social media frontend with a focus on custom branding and ease of use
  - You can run Mastodon+Soapbox, Rebased+Soapbox, and more.
  - Soapbox is the frontend (what users see) while Mastodon is the backend (data, APIs). You can mix-and-match in the Fediverse ecosystem.
  - Soapbox was born out of the need to build independent platforms with a unique identity and brand.

- https://github.com/elk-zone/elk /ts/vue
  - https://elk.zone/
  - A nimble Mastodon web client
  - https://github.com/Distal-Labs/elk
    - A friendly fork of Elk

- https://github.com/NicolasConstant/sengi /AGPLv3/ts/angular
  - https://nicolasconstant.github.io/sengi/
  - Mastodon & Pleroma Multi-account Desktop Client
  - It takes inspiration from the old Tweetdeck client, the new Tweetdeck webapp and Mastodon UI.
  - [Color themes](https://github.com/NicolasConstant/sengi/issues/396)
    - 只有darkMode，没有lightMode
  - It is strongly focused on multi-accounts usage and One column at a time display
  - It is released as a browser webapp and also packaged as an cross-platform desktop application (Mac, Windows, and Linux).
  - https://github.com/NicolasConstant/sengi-electron /AGPLv3/js
    - build the Electron Wrapper available for the webapp Sengi.

- pinafore /808Star/AGPLv3/202211/js/svelte2/deprecated
  - https://github.com/nolanlawson/pinafore
  - https://pinafore.social/
  - Alternative web client for Mastodon
  - Offline support in read-only mode
  - Progressive Web App features
  - Multi-instance support
  - Support non-Mastodon instances (e.g. Pleroma) as well as possible
  - [Retiring Pinafore_202301](https://nolanlawson.com/2023/01/09/retiring-pinafore/)
    - I don’t have the energy to do this anymore. 
    - I suspect one of the reasons for this is that Pinafore is written in Svelte v2 and Sapper – both of which are deprecated in favor of Svelte v3 and SvelteKit
  - Non-goals
    - React Native / NativeScript / hybrid-native version
    - Android/iOS apps (using Cordova or similar)
    - Multi-column support
  - https://github.com/NickColley/semaphore
    - Semaphore continues the Pinafore project

- whalebird-desktop /672Star/MIT/202211/ts+vue
  - https://github.com/h3poteto/whalebird-desktop
  - An Electron based Mastodon, Pleroma and Misskey client for Windows, Mac and Linux

- https://github.com/tuskyapp/Tusky
  - An Android client for the microblogging server Mastodon
  - Completely open-source - no non-free dependencies like Google services

- https://github.com/cloudflare/wildebeest /ts
  - Wildebeest is an ActivityPub and Mastodon-compatible server whose goal is to allow anyone to operate their Fediverse server and identity on their domain without needing to keep infrastructure, with minimal setup and maintenance, and running in minutes.
  - Wildebeest runs on top Cloudflare's Supercloud, uses Workers, Pages, Durable Objects, Queues, the D1 database to store metadata and configurations, Zero Trust Access to handle auth
# activitypub
- https://github.com/evanp/onepage.pub /apache2/202401/js
  - robust ActivityPub server in one page
  - it's a demonstration of how to build an ActivityPub server, with most of the important parts implemented
  - it's also a platform for testing and experimentation with new client apps and new server features.

- https://github.com/superseriousbusiness/gotosocial /AGPLv3/202401/go
  - https://docs.gotosocial.org/
  - Fast, fun, small ActivityPub server
  - an ActivityPub social network server, written in Golang.
  - you can keep in touch with your friends, post, read, and share images and articles.
# helpdesk/feedback/ticket
- [Canny: Customer Feedback Management Software and Tools](https://canny.io/)
  - [Chakra UI Feedback](https://chakra-ui.canny.io/)
  - [Graze for Mastodon Feedback](https://graze.canny.io/)

- https://github.com/Peppermint-Lab/peppermint /AGPLv3/202403/ts
  - https://peppermint.sh/
  - open source ticket management & help desk solution. 
  - A freshdesk alternative
  - Markdown based Notebook with todo lists
  - A log of client history

- https://github.com/django-helpdesk/django-helpdesk /1.6kStar/BSD/202510/python
  - A Django application to manage tickets for an internal helpdesk. Formerly known as Jutda Helpdesk.
  - django-helpdesk includes a basic demo Django project so that you may easily get started with testing or developing django-helpdesk. 

- https://github.com/polonel/trudesk /apache2/202311/js/inactive
  - http://trudesk.io/
  - an open-source help desk/ticketing solution
  - built with nodejs and mongodb; Elasticsearch 8 is optional 

- https://github.com/astuto/astuto /AGPLv3/202403/ruby/ts
  - https://feedback.astuto.io/
  - A free, open source, self-hosted customer feedback tool

- https://github.com/getfider/fider /AGPLv3/202307/go/ts/inactive
  - https://fider.io/
  - Open platform to collect and prioritize feedback

- https://github.com/letsrevel/revel-backend /MIT/202511/python
  - Revel is an event management and ticketing platform designed with community at its heart
  - Django REST API, business logic, database models
  - https://github.com/letsrevel/revel-frontend /MIT/svelte
# notification
- https://github.com/novuhq/novu /38kStar/MIT+EE/202510/ts
  - The open-source notification infrastructure for products. 
  - Novu provides a unified API that makes it simple to send notifications through multiple channels, including In-App, Push, Email, SMS, and Chat. 
  - With Novu, you can create custom workflows and define conditions for each channel, ensuring that your notifications are delivered in the most effective way possible.
  - Single API for all messaging providers (In-App, Email, SMS, Push, Chat)
  - Equipped with a CMS for advanced layouts and design management
  - "Open Core", where the core technology is fully open source, licensed under MIT license, and the enterprise code is covered under a commercial license
  - [Clarity/notes regarding the project license _202411](https://github.com/novuhq/novu/issues/6820)
  - https://github.com/novuhq/blog/tree/main/forum-system-with-react-novu-node
    - [Building a forum with React, NodeJS - DEV Community](https://dev.to/novu/building-a-forum-with-react-nodejs-6pe)

- https://github.com/caronc/apprise /15.6kStar/BSD/202601/python
  - Push Notifications that work with just about every platform
  - Apprise allows you to send a notification to almost all of the most popular notification services available to us today such as: Telegram, Discord, Slack, Amazon SNS, Gotify, et
  - Supports the handling of images and attachments (to the notification services that will accept them).
  - all messages sent asynchronously.
# meetings
- https://github.com/lukevella/rallly /ts
  - https://rallly.co/
  - an open-source scheduling and collaboration tool designed to make organizing events and meetings easier
  - Built with Next.js, Prisma, tRPC & TailwindCSS

- https://github.com/geekeren/GuangGuForum
  - 过早客论坛微信小程序
  - 技术设计初衷：尽量在无任何后端代理完成所有功能，降低后期维护复杂度和运营成本，直接在小程序端拉取并解析网站的HTML，转成json数据，渲染小程序界面
  - 本项目基于 Taro 框架开发，技术上支持 Android/IOS 多端，但考虑到过早客是一个相对轻量级的网站，小程序已经足够满足需求而且用户无需安装应用。

- https://github.com/neodb-social/neodb
  - Boofilsic/NeoDB is an open source project and free service to help users manage, share and discover collections, reviews and ratings for culture products (e.g. books, movies, music, podcasts, games and performances) in Fediverse.
  - NeoDB.social and NiceDB are free services hosted by volunteers.

- https://github.com/m1guelpf/refract
  - https://refract.withlens.app/newest
  - A Hacker News style forum, built on the Lens Protocol.
  - composed of Next.js and Tailwind CSS, with RainbowKit, ethers, & wagmi for all your web3 needs
  - 依赖ethers、graphql、next12

- https://github.com/weissthorn/weiss
  - Modern, Minimalistic Discussion Software
  - 依赖rethinkdb
# blogs
- https://github.com/thematters/matters-web /apache2/202402/ts
  - https://matters.town/
  - Website of Matters. Town, built with Next.js
  - IPFS-based decentralized social media
  - 依赖apollo-client、tiptap、d3-selection、d3-shape、firebase、next-with-apollo、react-markdown、wagmi
  - https://github.com/thematters/matters-server /apache2/202402/ts
    - Server code
    - 依赖@apollo/server、graphql、knex
# sms
- https://github.com/happyfox-dot/Msg2Computer /NC/202606/kotlin/js
  - 一个跨设备验证码与消息同步工具。它由 Android 手机端和 Windows 桌面端组成，用于把手机收到的验证码短信、普通短信、App 通知，以及本机保存的 TOTP 动态验证码，同步到你授权的设备节点。
  - [[开源分享] 验证码流转工具，将消息推送给多个电脑/手机，避免每次打开手机看验证码 - LINUX DO _202606](https://linux.do/t/topic/2376521/6)
# more
