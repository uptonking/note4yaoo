---
title: toc-saas-im-message-forum
tags: [forum, im, repos, toc]
created: 2020-08-31T13:15:14.391Z
modified: 2021-05-14T15:04:15.333Z
---

# toc-saas-im-message-forum

# guide
- forum的核心也是ugc内容，所以和blog功能相似度高
- 商城app-store类产品的开发和imdb类似，偏向搜索

- 论坛选型参考
  - 尽量选择开源产品，方便自定义
  - 考虑导出数据的功能，可导出本论坛管理员和会员的交流帖子及评论
    - 开源论坛可直接copy数据库，不存在此问题
    - 付费产品如vanilla forum可导出mysql dump

- [Telegram导出](https://twitter.com/Benbinbin_fun/status/1572137020004401153)
  - Telegram 很多方面都比微信优胜，单是支持导出数据（包括 chat 和自己创建的 channel）这一点就有足够的优势了
  - 而且导出的格式可以选择 HTML 或 JSON，HTML 格式方便普通用户直接用浏览器打开查看，而支持导出为 JSON 格式，则考虑到二次开发的便利性，足够良心
  - 但是之前的无故封号事件还是太伤害我对电报的信任了
# forum-for-dev
- slack
- gitter
- spectrum
- discord
- discourse
  - http://www.discourse.org/

- https://github.com/42wim/matterbridge /202212/go
  - bridge between mattermost, IRC, gitter, xmpp, slack, discord, telegram, rocketchat, twitch, ssh-chat, zulip, whatsapp, keybase, matrix, microsoft teams, nextcloud, mumble, vk and more with REST API
  - Mattermost isn't required to run matterbridge

- https://github.com/withspectrum/spectrum /archived
  - 依赖express、graphql、apollo、draft-js、redux、rethinkdb
  - Spectrum aims to be the best platform to build any kind of community online by combining the best of forums and real-time chat apps.
- https://github.com/discourse/discourse
  - 依赖ruby、emberjs、postgresql、redis
  - discussion platform built for the next decade of the Internet.

- https://github.com/NodeBB/NodeBB /js
  - Node.js based forum software built for the modern web

- ddd-forum /1.5kStar/ISC/202204/ts/hacker-news
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
  - forks
    - https://github.com/BrunoAmerio/orca

- MBBS /52Star/MIT/202207/ts/功能全
  - https://github.com/linfaxin/MBBS
  - http://mbbs.cc/
  - 轻量级全功能论坛、移动/PC双端适配、无依赖一键启动、技术栈 express + sqlite + react
  - 后端依赖express、sequelize、sqlite3、svg-captcha
  - 前端依赖mui、ahooks、umi3
  - 全功能论坛：板块/楼中楼/角色权限/审核/富文本编辑/个性化配置/邮件通知 等
  - 自带授权登录：免开发支持 QQ/微信/支付宝 授权登录

- cnode
  - https://github.com/cnodejs/nodeclub
    - Nodeclub 是使用 Node.js 和 MongoDB 开发的社区系统
    - 依赖mongodb4、redis4
  - https://github.com/cnodejs/egg-cnode
    - CNode 社区 Egg 版本; /201810
- https://github.com/ChenJiaH/react-cnode
  - 基于react&react-router-dom，利用CNode API重写CNode社区。
  - 依赖只有react-router.v5, react, axios

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

- https://github.com/amirfakhrullah/bloqdown
  - Simple Markdown Forum/Blog site using Next.js, NextAuth, TypeScript, tRPC, Prisma and PlanetScale
  - 风格类似github
  - Creating fully typesafe APIs using tRPC
  - Auth using NextAuth (Github Provider)
  - Display repository data using GitHub API
  - https://github.com/planetscale/nextjs-planetscale-starter
    - A Next.js starter app with NextAuth.js (Auth), Prisma (ORM), and PlanetScale (database), ready to be deployed on Netlify

- https://github.com/proshoumma/ReForum
  - A minimal forum board application. 只是仪表板
  - Built on top of React-Redux frontend, ExpressJS-NodeJS backend (with PassportJS for OAuth) and MongoDB databse.

- https://github.com/heybereket/oasis /202107/inactive
  - The chat and forums platform for communities
  - 后端依赖 express、typeorm、passport
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

- https://github.com/EricBollar/Fullstack-Forum
  - fullstack forum built using industry-standard tools such as Next.js and PostgresQL.

- https://github.com/halchester/csqa /inactive/unfinished
  - https://csqa.vercel.app/
  - CSQA is a Progressive Web App aimed for those who wanna ask silly questions but afraid to get downvoted on stackoverflow

- https://github.com/seawind8888/Nobibi /202011/ts/inactive
  - Nobibi 是一款轻量级开源社区，包含前后台
  - 前台考虑 SEO 使用 next.js + antd 服务端渲结构
  - 后台系统基于Ant Design Pro(react + dvajs + umijs)搭建开发
  - 后端接口为 koa+moogoose

- https://github.com/romerorocha/reddit-clone-api
  - Forum API Server
  - 依赖express，不依赖orm  

- https://github.com/dafengzhen/youdeyiwu-frontend
  - 依赖typescript + react + next、axios、react-query、bootstrap
  - https://github.com/dafengzhen/youdeyiwu-backend
    - 依赖java 17 + spring-boot + jpa、mariadb 10.6、redis、rabbitmq、minio
  - https://github.com/dafengzhen/youdeyiwu-editor
    - 以 ckeditor5 classic editor 为基础自定义构建，集成了自定义和常用插件

- https://github.com/gudfhr95/stelllar
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
# forum-non-nodejs
- https://github.com/dakshit050/AskAnything
  - a social discussion platform Developed for college/school students to solve their doubts online

- https://github.com/debiki/talkyard
  - A structured discussions platform — brings together the main features from StackOverflow, Slack, Discourse, Reddit/HackerNews, and Disqus blog comments.
  - Client: React.js, TypeScript, Webdriver.io.
  - Server: Scala and Play Framework. OpenResty, some Lua. React.js in Java's Nashorn Javascript engine.
  - Databases: PostgreSQL, Redis, ElasticSearch.

- https://github.com/carbon-bond/carbonbond
  - 前端：使用 typescript + React
  - 后端：使用 Rust
# im-instant-messaging-chat
- https://github.com/mastodon/mastodon
  - Your self-hosted, globally interconnected microblogging community
  - 依赖ruby

- tailchat /401Star/apache2/202302/ts
  - https://github.com/msgbyte/tailchat
  - Alternative application of discord and slack. 
  - 后端依赖@socket.io/admin-ui、ejs、mongoose、moleculer-minio、redlock(redis)、moleculer微服务
  - 前端依赖zustand、antd、ahooks、use-gesture、immer、react-dnd、react-virtuoso
  - 前端微内核架构+后端微服务架构，Tailchat 已经为集群化部署做好了准备。
  - 主要功能模块
    - 用户管理
    - 聊天系统
    - 插件系统
    - 开放平台

- Linen /1.2kStar/AGPLv3/202302/ts/discord-like
  - https://github.com/Linen-dev/linen.dev
  - https://www.linen.dev/
  - Linen is a Google-searchable community chat tool. 
  - 依赖headlessui、tanstack-query、nextjs、swr、prisma、express、zod
  - Linen was built as an alternative to closed tools like Slack and Discord.

- https://github.com/laudspeaker/laudspeaker
  - Open Source Cross Channel Customer Messaging Platform that you can self host. 
  - alternative to Braze / Iterable / One Signal / Customer Io

- koishi /2kStar/MIT/202303/ts
  - https://github.com/koishijs/koishi
  - https://koishi.chat/
  - Koishi 是一个跨平台、可扩展、高性能的跨平台聊天机器人框架。
  - Koishi 提供了高度便利的控制台，让你无需基础让你在几分钟之内搭建自己的聊天机器人。
  - 支持 QQ，Telegram，Discord，飞书等主流聊天平台，支持多账户和跨平台数据互通
  - 提供在线插件市场，即使没有任何编程基础，也能轻松在控制台中下载安装插件
  - 依赖satorijs、minato(db-driver)、cordis(aop)

- https://github.com/satorijs/satori
  - The Universal Messenger Protocol
  - QQ Guild、Feishu、telegram、discord

- https://github.com/baptisteArno/typebot.io
  - https://typebot.io/
  - Typebot is an open-source alternative to Landbot. 
  - a conversational form builder that you can self-host.
  - builder依赖slate-react、tanstack-table
  - It allows you to create conversational apps/forms (Lead qualification, Product launch, User onboarding, Customer support), embed them anywhere on your web/mobile apps, and collect results in real-time.

- https://github.com/juravlevdima/PERN-chat
  - Chat made with PERN Stack & Socket. IO
  - React | React Router | Redux Toolkit
  - Real-time chat using web-sockets

- https://github.com/Privoce/vocechat-web
  - Private Hosted IM and Social Channels, Easy Integration to Your Site or App
  - VoceChat is a superlight Rust powered chat App, API and SDK that prioritizes private hosting
  - 依赖react、redux-toolkit、plate、tui-editor、localforage
  - [Will the server be open source?](https://github.com/Privoce/vocechat-web/issues/19)
    - rust写的 会开源 但是还没准备好

- https://github.com/fonoster/fonoster
  - open-source alternative to Twilio

- https://github.com/penghuwan/online-chat-app
  - 一个在线聊天室，实现了登陆注册功能和聊天功能，
  - 实时通信部分基于Socket.io实现，后端采用Koa框架组织业务逻辑，前端采用React编写，同时用Webpack作为打包工具

## chatbot

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
# notification
- https://github.com/novuhq/novu
  - The open-source notification infrastructure for products. 
  - Add a notification center for your React, Vue and Angular apps rocket

- https://github.com/novuhq/novu
  - Novu provides a unified API that makes it simple to send notifications through multiple channels, including In-App, Push, Email, SMS, and Chat. 
  - With Novu, you can create custom workflows and define conditions for each channel, ensuring that your notifications are delivered in the most effective way possible.
  - Single API for all messaging providers (In-App, Email, SMS, Push, Chat)
  - Equipped with a CMS for advanced layouts and design management
# meetings
- https://github.com/lukevella/rallly /ts
  - https://rallly.co/
  - an open-source scheduling and collaboration tool designed to make organizing events and meetings easier
  - Built with Next.js, Prisma, tRPC & TailwindCSS
# more-forum
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
