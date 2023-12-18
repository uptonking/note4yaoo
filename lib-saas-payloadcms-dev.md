---
title: lib-saas-payloadcms-dev
tags: [lowcode, payloadcms]
created: 2023-02-05T18:39:26.796Z
modified: 2023-12-15T17:04:17.775Z
---

# lib-saas-payloadcms-dev

# guide

- pros
  - code-first
  - field conditional logic

- cons
  - ~~mongodb only~~, support mysql/pg now
  - VC-backed

- features
  - code-first

- roadmap
  - multi tenancy 多租户
  - 快速复制一张表结构，然后导入数据
# dev
- [How To Build A Multi-Tenant App With Payload](https://payloadcms.com/blog/how-to-build-a-multi-tenant-app-with-payload)
# changelog

## v2.0_202310

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
