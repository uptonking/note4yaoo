---
title: lib-saas-payloadcms-dev
tags: [lowcode, payloadcms]
created: 2023-02-05T18:39:26.796Z
modified: 2023-12-15T17:04:17.775Z
---

# lib-saas-payloadcms-dev

# guide

- pros
  - license: MIT, features-rich
  - code-first
  - field conditional logic
  - db support: MongoDB, Postgres, SQLite
  - 🛢️ 还支持使用已存在的db, 通过 beforeSchemaInit, 待验证
  - 添加表/数据模型无需重启服务
    - 内置数据库表名有统一前缀payload, 似乎有部分表名无前缀如imports/exports
  - Relationship Field: hasOne, hasMany
  - ⏳ versions: If you enable versions but keep draft mode disabled, Payload will simply create a new version of a document each time you update a document.
    - 👀 数据模型不是delta
  - draft
  - Live Preview: As you type, your changes take effect in real-time. No need to save a draft or publish your changes. 
    - 类似支持切换多设备尺寸的预览视图
    - 🐛 基于`window.postMessage`事件实现, 仅在同一浏览器自动更新, 其他浏览器不会更新
    - nextjs 设置 revalidate 时也会立即更新
  - Jobs Queue: Tasks, Workflows, Jobs, Queues
  - 🔌 Plugins
  - admin界面好用
  - Trash: soft delete

- cons
  - 对 db rename/schema-change 不友好, 社区建议手动migrate 
  - 对协作的支持不友好, 目前采用的是锁方案 [feat: adds the ability to lock documents while they are being edited _202409](https://github.com/payloadcms/payload/pull/7970)
  - 提供形式和使用方式是code, 易用性不高
  - VC-backed, v2功能更丰富但引入大量依赖如drizzle/nextjs
    - 已被figma收购
  - ~~mongodb only~~ , support mysql/pg now

- features
  - code-first
  - preview button in admin ui: view only

- roadmap
  - multi tenancy 多租户
  - 快速复制一张表结构，然后导入数据

- [Payload is acquired by Figma _202506](https://www.figma.com/blog/payload-joins-figma/)
  - [Payload is joining Figma ](https://payloadcms.com/posts/blog/payload-is-joining-figma)
  - [Payload is joining Figma! · payloadcms/payload · Discussion _202506](https://github.com/payloadcms/payload/discussions/12843)
# dev
- [How To Build A Multi-Tenant App With Payload](https://payloadcms.com/blog/how-to-build-a-multi-tenant-app-with-payload)
# changelog

## v4.0.0_2026

### [Payload 4.0: Admin UI Redesign, TanStack, MCP, and More _202606](https://payloadcms.com/posts/blog/payload-40-admin-ui-redesign-tanstack-mcp-and-more)

> a redesigned admin UI, first-class hierarchies, better digital asset management, improved MCP support, Payload skills, and early TanStack support.

- One of the biggest pieces of Payload 4.0 is a full redesign of the admin panel.
  - The goal is not to change how Payload works. The goal is to make the experience cleaner, more consistent, easier to extend, and better aligned with the quality bar people expect from modern tools.
  - removing Sass, improving Tailwind compatibility

- TanStack support is coming
  - Payload 3.0 brought Payload and Next.js together, but the long-term plan was never to support only Next.js.
  - For 4.0, we’re building a framework adapter pattern that separates Payload’s framework-specific pieces from the core. That includes admin rendering, React Server Components, loaders, and API mounting.

- Payload has had the nested docs plugin for a long time, but the use case has grown beyond page trees and nested URLs.
  - In 4.0, we’re bringing hierarchies into Payload core
  - That means folders, tags, taxonomies, nested content structures, and tree-based organization can all be built on the same underlying primitive. This will eventually replace the nested docs plugin and unlock better UI patterns for navigating and organizing content.

- Better digital asset management
  - Many teams already use Payload to manage large libraries of images, PDFs, videos, and other files. 
  - A lot of this is still being shaped

- Payload skills and better agent workflows
- MCP should work out of the box

## [v3.0.0_202411](https://payloadcms.com/posts/blog/payload-30-the-first-cms-that-installs-directly-into-any-nextjs-app)

> Payload 3.0: The first CMS that installs directly into any Next.js app

- Payload is the only Next.js CMS—in a way that no other CMS can come close to. It installs directly into your app folder without any third-party SaaS services—no free trials, no free tier, no subscriptions. 
- we are now Next.js native. Payload now installs fully in any Next.js app, including both the admin panel and full backend—right in your app folder.
- Another major update is that we’ve marked PostgreSQL and Lexical as stable. We’re also shipping SQLite and Vercel PostgreSQL database adapters, thanks to Drizzle, using the same code across all three adapters.

- Server components and server functions
  - you can use the local API in server components and server functions to query and mutate your data in Payload. This goes straight to the database without needing a third-party API.
  - This is the fastest way to manage data in a Next.js app, and Payload is the only CMS that supports this capability.

- Enhanced portability across front-end frameworks
  - use it seamlessly with Astro, SvelteKit, Remix, or any Node environment.

- Lexical is now stable, with new features to enhance the editor experience. Payload now supports inline and block-level components within Lexical. 
- `join` field allows for more complex database architectures. 
- Another new addition is the Select and Populate APIs. These features help you optimize queries by selectively loading only the fields you need. You can reduce the JSON output significantly, tailoring your queries to retrieve only the essential data. 
- a fully functional jobs queue, a common feature in frameworks like Laravel and Rails. With this, you can defer tasks separately from the main API, run them on a schedule, or set up workflows with multiple tasks that run in a specific order.
- Live Preview, introduced in 2.0, is now stable, with added support for server components. Previously, Live Preview required client-side rendering, but now you can use server components across your entire front end.

- Removed GraphQL overhead: GraphQL will now only start if you’re using it, which reduces Payload’s initialization time.

## v2.0.0_202310

- [Announcing Payload 2.0: Postgres, Live Preview, Lexical RTE, and More](https://payloadcms.com/blog/payload-2-0)
- Payload is half CMS, half app framework and we are doing things differently than all the other cms
- With Payload, you actually have full control over your backend and you don't have to just "surrender to SaaS". 
- You bring your own database, and when you have the ability to customize the backend, magical things can happen. Your CMS starts to feel more like an app framework akin to Laravel
- Underpinning(支持; 巩固, 构成…的基础) almost everything we've done in 2.0 is a new "adapter pattern" that we've built into the fabric of Payload core.
- We've built this adapter pattern into three places:
  - All database interactions
  - The bundler that's used to compile the admin panel for production
  - The rich text editor used within the admin panel
- Postgres Support
  - we've replicated everything that MongoDB can do—but in Postgres which is now available in Payload 2.0 as beta.
  - Everything is done in the exact way that you'd expect coming from a relational DB world. Arrays automatically create new tables (not JSON columns), and you can still do relationships within arrays. Blocks can be nested and relate to other blocks. Relationships feature ordering out-of-the-box.
- Drizzle ORM
  - Here are a few reasons we chose Drizzle to power our Postgres adapter: 
  - It's got extremely minimal overhead.
  - It's got first-class TypeScript support, which is obviously important to Payload.
  - It's fast.
  - You can make a single query to the DB and auto-join all the tables you need. Huge.
  - You can define schemas dynamically, which means we don't have to maintain a separate ORM-specific schema file and can continue to leverage the Payload config as the schema source-of-truth.
  - And now that we have the hard parts done, we can easily add support for MySQL and SQLite in the near future. DynamoDB, too, when Drizzle supports it.
- Honestly I still think that MongoDB is the best choice for most Payload projects, because there is less technical complexity involved and fewer tables (collections) to deal with.
  - But if your project calls for a schema that is well-known, flat, and might benefit from the constraints of  the relational world, then by all means, go for Postgres. 
  - The only thing that we do not officially support in Postgres yet is the **Point field** but other than that, everything we have in MongoDB can be accomplished within Postgres. Even querying on JSON / Rich Text fields.
- Another feature we've added is full database transaction support. 
  - Transactions in databases are great if you need to perform lots of updates in one fell swoop, but have the entire thing fail if one of the operations fails.
  - Payload now uses it seamlessly under the hood.
- Vite Support
  - we looked at rspack which claims to be a drop-in Webpack replacement built on Rust, but we ran into a few discrepancies(差异；不符；不一致) with how rspack handles things vs. Webpack. So we paused work there. Maybe we will pick it back up at some point, but that point is not today.
  - I'm personally excited for Turbopack but right now it only works in NextJS.
- Live Preview
  - Now you can easily add live preview to any collection or global so your editors can preview what they're doing directly inside Payload.
  - They built a beautiful live preview plugin and were able to accomplish all of this strictly by extending Payload through a plugin, and we were able to pull their work directly into Payload core. Open source at its finest.
- Completely new rich text editor
  - Our rich text editor has been built on Slate since we launched, and while Slate is great, it can be difficult to build custom elements for. 
  - we hired Alessio from our community and he's taken his Lexical editor up a notch.
  - Thanks to our new rich text editor adapter pattern, you can still use Slate, but we're going to focus new efforts on the Lexical editor.
- Monorepo
  - In order to keep up with the new adapter patterns I've discussed above, and not end up with one fafillion separate repos, we've moved Payload over to PNPM and it's now a monorepo.
  - It's also helped us ensure test coverage with things like database adapters. Our entire integration test suite runs on MongoDB and on Postgres. 
- Performance boosts
  - we've completely refactored how the draft querying works and it's now lightning fast no matter how many docs you have.
- What's next?
  - Improve the way we "split" server-side code and admin code from the Payload config. 
  - Add multiplayer editing.
  - Add true visual editing directly from the frontend of your website.
  - Add AI writing assistants.
# more
- [Chore/nextjs preview example_202301](https://github.com/payloadcms/payload/pull/1950)
