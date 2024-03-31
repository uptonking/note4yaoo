---
title: toc-saas-im-message-forum
tags: [forum, im, repos, toc]
created: 2020-08-31T13:15:14.391Z
modified: 2021-05-14T15:04:15.333Z
---

# toc-saas-im-message-forum

# guide

- tips
  - forum的核心也是ugc内容，所以和blog功能相似度高
  - 商城app-store类产品的开发和imdb类似，偏向搜索
  - 💡 cms中的内容评论也可以作为forum

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
  - observablehq-notebook
  - tiddlywiki
  - openstreetmap

- forum-open
  - discourse
  - nodebb
  - spectrum
  - Mumble for voice and text, jitsi for video calls

- chat-open
  - mattermost
  - Zulip
  - gitter
  - telegram的client都是开源的, webK/webA
  - [5 open source alternatives to Slack for team chat | Opensource.com](https://opensource.com/alternatives/slack)
# forum-popular
- https://github.com/discourse/discourse /GPLv2/202401/ruby/js
  - 依赖emberjs、postgresql、redis
  - discussion platform built for the next decade of the Internet.
- https://github.com/forem/forem /AGPLv3/202402/ruby/js
  - https://forem.com/
  - the platform that powers dev.to
  - We run on a Rails backend, and we are currently transitioning to a Preact-first frontend.
- https://github.com/withspectrum/spectrum /js/archived
  - 依赖express、graphql、apollo、draft-js、redux、rethinkdb
  - Spectrum aims to be the best platform to build any kind of community online by combining the best of forums and real-time chat apps.
  - RethinkDB: Data storage

- https://github.com/apache/incubator-answer /apache2/202401/go/ts
  - https://answer.apache.org/
  - https://meta.answer.dev/
  - A Q&A platform software for teams at any scales. 
  - Plugins: redis/es/algolia
- https://github.com/casbin/casnode /apache2/202312/go
  - Open-Source Forum and Social Platform, Alternative to StackOverflow & Flarum
  - Go (Beego) + MySQL

- https://github.com/NodeBB/NodeBB /GPLv3/202401/js
  - https://nodebb.org/
  - Node.js based forum software built for the modern web
  - powered by Node.js and supports either Redis, MongoDB, or a PostgreSQL database
  - It utilizes web sockets for instant interactions and real-time notifications
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

- ddd-forum /1.8kStar/ISC/202306/ts
  - https://github.com/stemmlerjs/ddd-forum
  - https://dddforum.com/
  - Hacker news-inspired forum app built with TypeScript using DDD practices from solidbook.io.
  - 后端依赖 express、sequelize、redis
  - 前端依赖 react、redux、react-quill
  - https://github.com/dyarleniber/typescript-ddd-forum

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

- https://github.com/freedit-org/freedit /MIT/202402/rust
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

- https://github.com/carbon-bond/carbonbond
  - 一個次世代的論壇。它在文章之間的交互作用
  - 前端：使用 typescript + React
  - 后端：使用 Rust

- https://github.com/proshoumma/ReForum /201809/js/archived
  - A minimal forum board application. 只是仪表板
  - Built on top of React-Redux frontend, ExpressJS-NodeJS backend (with PassportJS for OAuth) and MongoDB databse.

- https://gitlab.com/tildes/tildes /AGPLv3/202306/python/jinja
  - https://tildes.net/
  - a non-profit community site
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

- https://github.com/chatwoot/chatwoot /202402/ruby/js/vue
  - https://www.chatwoot.com/help-center
  - Customer engagement suite, an open-source alternative to Intercom, Zendesk, Salesforce Service Cloud etc.
# im-instant-messaging-chat
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
  - https://github.com/spacebarchat/client /AGPLv3/202312/ts
    - https://app.spacebar.chat/
    - Open source, themeable and extendable discord-compatible native Spacebar client
    - 依赖mobx-react-lite、react-markdown、react-virtualized
  - https://github.com/spacebarchat/fosscord-web-client /archived
  - https://github.com/SpacingBat3/WebCord /MIT/202402/ts
    - A Discord and SpaceBar-based client implemented without Discord API.
    - A major rewrite of the client is being worked on
  - https://github.com/morroid/Morroid /MIT/202306/ts/archived
    - A reverse-engineered discord server written in typescript
  - https://github.com/spacebarchat/spacebarchat /仅文档

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

- https://github.com/xiweicheng/tms /MIT/202309/js/vue2/java/inactive
  - TMS是基于频道模式的团队沟通协作+轻量级任务看板，支持mardown、富文本、在线表格和思维导图的团队博文wiki，i18n国际化翻译管理的响应式web开源团队协作系统。

- Linen /1.2kStar/AGPLv3/202311/ts/discord-like
  - https://github.com/Linen-dev/linen.dev
  - https://www.linen.dev/
  - Linen is a Google-searchable community chat tool. 
  - Linen was built as an alternative to closed tools like Slack and Discord.
  - 依赖headlessui、tanstack-query、nextjs、swr、prisma、express、zod

- https://github.com/Privoce/vocechat-web /GPLv3/202403/ts
  - Private Hosted IM and Social Channels, Easy Integration to Your Site or App
  - VoceChat is a superlight Rust powered chat App, API and SDK that prioritizes private hosting
  - 依赖react、redux-toolkit、plate、tui-editor、localforage
  - https://github.com/Privoce/vocechat-server-rust /202303/rust/inactive
    - superlight rust written social server.

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

- https://github.com/mattermost/mattermost /AGPLv3/202402/go/ts
  - https://mattermost.com/
  - open source platform for secure collaboration across the entire software development lifecycle.
  - written in Go and React and runs as a single Linux binary with MySQL or PostgreSQL.
  - A new compiled version is released under an MIT license every month on the 16th.
  - You are licensed to use compiled versions of the Mattermost platform produced by Mattermost, Inc. under an MIT LICENSE

- https://github.com/sdelements/lets-chat /MIT/201708/js/inactive
  - https://sdelements.github.io/lets-chat/
  - Self-hosted chat app for small teams
  - 依赖express.oi、mongoose、nunjucks、passport

- https://github.com/RocketChat/Rocket.Chat /MIT+EE/ts/meteor
  - https://rocket.chat/
  - fully customizable communications platform developed in JavaScript for organizations with high standards of data protection.
  - We are a MERN based application enabling real-time conversations

- https://github.com/juravlevdima/PERN-chat
  - Chat made with PERN Stack & Socket. IO
  - React | React Router | Redux Toolkit
  - Real-time chat using web-sockets

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
  - https://github.com/RahulM4/letschat-vercel-api /202311/js
  - https://github.com/RahulM4/LetsChat /202310/js/fe+be

- https://github.com/revoltchat/backend /AGPLv3/202402/rust
  - https://revolt.chat/
  - https://developers.revolt.chat/api/
  - Monorepo for Revolt backend services
  - https://github.com/revoltchat/revite
    - Revolt client built with Preact

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

## chatbot

- https://github.com/baptisteArno/typebot.io
  - https://typebot.io/
  - Typebot is an open-source alternative to Landbot. 
  - a conversational form builder that you can self-host.
  - builder依赖slate-react、tanstack-table
  - It allows you to create conversational apps/forms (Lead qualification, Product launch, User onboarding, Customer support), embed them anywhere on your web/mobile apps, and collect results in real-time.

- koishi /2kStar/MIT/202303/ts
  - https://github.com/koishijs/koishi
  - https://koishi.chat/
  - Koishi 是一个跨平台、可扩展、高性能的跨平台聊天机器人框架。
  - Koishi 提供了高度便利的控制台，让你无需基础让你在几分钟之内搭建自己的聊天机器人。
  - 支持 QQ，Telegram，Discord，飞书等主流聊天平台，支持多账户和跨平台数据互通
  - 提供在线插件市场，即使没有任何编程基础，也能轻松在控制台中下载安装插件
  - 依赖satorijs、minato(db-driver)、cordis(aop)

- https://github.com/mckaywrigley/chatbot-ui
  - https://www.chatbotui.com/
  - Chatbot UI is an advanced chatbot kit for OpenAI's chat models built on top of Chatbot UI Lite using Next.js, TypeScript, and Tailwind CSS.
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
# notification
- https://github.com/novuhq/novu /MIT/202402/ts
  - The open-source notification infrastructure for products. 
  - Novu provides a unified API that makes it simple to send notifications through multiple channels, including In-App, Push, Email, SMS, and Chat. 
  - With Novu, you can create custom workflows and define conditions for each channel, ensuring that your notifications are delivered in the most effective way possible.
  - Single API for all messaging providers (In-App, Email, SMS, Push, Chat)
  - Equipped with a CMS for advanced layouts and design management
  - https://github.com/novuhq/blog/tree/main/forum-system-with-react-novu-node
    - [Building a forum with React, NodeJS - DEV Community](https://dev.to/novu/building-a-forum-with-react-nodejs-6pe)
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
# more
