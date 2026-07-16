---
title: lib-office-fumadocs-dev
tags: [documentation, fumadocs]
created: 2026-07-13T21:23:19.390Z
modified: 2026-07-13T21:23:42.886Z
---

# lib-office-fumadocs-dev

# guide

- pros
  - composable framework: Separated as Content → Core → UI
    - portable to any React.js framework: Next.js, Tanstack Start, React Router, Waku 
  - headless mode to plug your own UI with Fumadocs CLI
  - flexible content source: local md, MDX Remote, build your own with Loader API
  - Story: a simple, docs-focused alternative of Storybook
  - 提供了 fumadocs-preview cli 工具， 支持快速查看markdown文件夹
    - Fumapress 和 preview 采用了类似的思路，但需要 npm i/run
  - Integrate with Orama Search and Algolia Search easily
  - Access Control: allows only MDX files with frontmatter permission: public to be shown
  - [Partial Versioning](https://www.fumadocs.dev/docs/navigation): separate versions by folders as Layout Dropdown, or a Git branch for a version of docs
  - MDX runtime支持 nextjs, vite, runtime-loader

- cons
  - 强调直接用code，而不是配置文件, 虽然功能强，但可复用性低
  - 对于外部md和图片资源，需要copy到当前目录，因为web server在当前目录启动

- 对obsidian的支持
  - 需要手动将ob的 .md 转换为 符合fuma格式 .mdx， 然后再对.mdx生成页面
  - 对图片的支持不好 Error: [Remark Image] Failed obtain image size 
  - 不支持bases
  - 对包含emoji的文件名支持不好

- features
  - 👀 Server-first Approach: fetch data from server to display content, or integrate with CMS receiving realtime updates. 
  - MDX: a superset of Markdown with JSX syntax
  - Fumapress is a React.js framework for Fumadocs, every feature needs only a plugin – embracing simplicity fully for those who just want a working docs.

- who is using #fumadocs
  - shadcn/ui, hero-ui
  - better-auth
  - zod, prisma
  - blocknote-docs
  - extend-ui

- tips
  - ?
# draft
- rewrite fumadocs-preview with tanstack-start
  - 尝试将平台配置放在类似.obsidian的 .dreamansion 文件夹, 最好能使用指定配置文件方便快速测试

- fumadocs-payload-template 提供了使用fumadocs作为cms前端的方案
  - 项目是一个nextjs全栈webapp, 准确点来说是个payloadcms全栈项目
  - 访问/docs相关url时， nextjs server page相关的逻辑会根据url通过 fumadocs Loader API 获取文件内容， 然后去 payload 数据库里面读取内容
  - 页面渲染的内容是 Serialize Payload's Lexical editor content to HTML， 而不是fumadocs转换而来的html
  - fumadocs主要使用的是 fumadocs-ui/layouts, fumadocs-core/search, 而fumadocs-mdx似乎未使用
  - 编辑页面内容使用的是payload admin管理界面提供的lexical编辑器
  - 🐛 似乎会将所有文件内容拉回本地， search使用了 createSearchAPI 根据所有内容创建索引

- 
- 
- 
- 
- 
- 
- 

# maybe
- 偏静态文档站的使用方式/启动方式大多是cli或者直接npm run 
  - docusaurus: npx create-docusaurus@latest my-website classic
    - md内容目录在 my-website/docs
    - 需要执行 npm i 
  - fumadocs/nextra: 需要执行 npm i , 以代码运行
    - 提供了 fumadocs-preview cli 工具， 支持快速查看markdown文件夹
  - quartz: 需要执行 npm i , 以代码运行
  - docsify: 提供了cli来执行
    - docsify init ./docs: 自动创建文件 index.html, README.md 
    - docsify serve docs: 启动一个本地服务器，可以方便地实时预览效果
# pm-docs
- 文件数据的标识
  - db可用id，文件可用路径
  - 若直接复制/移动文件夹，那用软件打开同一目录的效果如何变化
    - 可参考简单文件操作的效果

- 文档系统一般设置3级权限
  - admin/superuser/owner: 所有页面的crud， 管理人员
    - org: 所有页面的crud， 不管理人员
  - editor: 仅edit自己
  - viewer: 仅read
# dev-xp
- 默认支持 .mdx/.md 文件

- .mdx文件的第一行不能是空行，否则第二行的frontmatter也无法解析
  - 浏览器console异常为 Error: [MDX] invalid frontmatter， - title: Invalid input: expected string, received undefined

- DocsPage 自定义页面的结构
  - DocsTitle
  - DocsDescription
  - DocsBody
    - html content
# more

# examples

- https://github.com/fuma-nama/fuma-editor
  - 半成品

- https://github.com/bapspatil/fumadocs-payload-template /202603/ts
  - This example demonstrates how to integrate Payload CMS with Fumadocs for content management. 
  - It showcases a complete documentation site powered by Payload CMS with a custom fumadocs source adapter.
  - Payload CMS Integration: Full headless CMS backend for documentation
  - Custom Source Adapter: Transform Payload data into fumadocs format
  - Built-in search via fumadocs
  - 使用mongodb
  - 使用文档详细
  - 在admin管理界面创建doc点击publish后， 主页默认就会看到doc， 点击文档的 Edit Page 按钮就会跳转到admin管理界面进行编辑
  - Lexical Editor: Rich text editing with HTML serialization
  - sync Source Access: due to React's cache() requiring async initialization.
  - https://github.com/MFarabi619/fumadocs-payloadcms /202603/ts
    - deploy-ready example for using Fumadocs with Payload CMS combined into a single Next.js app.
    - 使用sqlite
  - https://github.com/lefolalan/fumadocs-payload-mvp /202605/ts
    - Payload CMS + Fumadocs MVP (demo docs)
  - https://github.com/mrpitch/payloadcms-fumadocs /202509/ts
    - documentation platform that combines PayloadCMS for content management with Fumadocs for documentation rendering. Built with Next.js and PostgreSQL.
    - Server-side rendering and static generation (Next.js)
    - Database-backed content storage (PostgreSQL)
    - [Fumadocs Integration](https://github.com/mrpitch/payloadcms-fumadocs/blob/main/docs/fumadocs-integration.md)
      - Server-side rendering
      - Table of contents generation
      - Full-text search

## starter/boilerplate

- https://github.com/techwithanirudh/fumadocs-starter /MIT/202604/ts
  - https://fumadocsstarter.vercel.app/
  - A fully-fledged Fumadocs starter template with built-in plugins, AI features, and everything you need to build your next docs site.
  - ships with an AI assistant that runs on your content. It streams answers from OpenAI's gpt-5-mini model through AI SDK.
  - official OpenAPI integration 
- https://github.com/fuma-nama/nextjs-fumadocs /202512/ts
  - https://nextjs-fumadocs.vercel.app/
  - View the Next.js docs with Fumadocs. 
- https://github.com/Deveripon/fuma-docs-starter /202512/ts
  - Premium Docs Starter Kit A professional, high-performance documentation starter kit built with Next.js 15, Fumadocs, and Tailwind CSS 4

- https://github.com/gfazioli/next-app-fumadocs-template
  - Next.js App Router + Mantine + Fumadocs (headless) template — 100% Mantine UI, no Tailwind

- https://github.com/typst-gost/typst-fumadocs /MIT/202512/mdx
  - https://typst-gost.github.io/typst-fumadocs/docs
  - Interactive Typst documentation powered by Fumadocs with live code editing and real-time rendering.

- https://github.com/devfolioco/guide-fumadocs /202606/ts
  - https://guide.devfolio.co/
  - a modern documentation site built with Fumadocs and Next.js, featuring analytics, user feedback, and more.
