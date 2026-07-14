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
  - headless mode to plug your own UI with Fumadocs CLI
  - portable to any React.js framework: Next.js, Tanstack Start, React Router, Waku 
  - flexible content source: local md, MDX Remote, build your own with Loader API
  - Story: a simple, docs-focused alternative of Storybook
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

# dev-xp

- 默认支持 .mdx/.md 文件

- .mdx文件的第一行不能是空行，否则第二行的frontmatter也无法解析
  - 浏览器console异常为 Error: [MDX] invalid frontmatter， - title: Invalid input: expected string, received undefined
# more

# examples

- https://github.com/fuma-nama/fuma-editor
  - 半成品

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
