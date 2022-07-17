---
title: lib-fwk-nextjs-dev
tags: [framework, lib, nextjs]
created: 2020-12-12T19:19:27.854Z
modified: 2020-12-12T19:22:00.735Z
---

# lib-fwk-nextjs-dev

- The React Framework with all the features you need for production

# guide

- features
  - opinionated react framework with features for production out of the box
  - ssr support
    - seo搜索引擎优化、加快首屏显示
    - hybrid static & server rendering
    - Pre-render pages at build time (SSG) or request time (SSR) in a single project
  - Zero config with flexible customization
  - file-system based routing
    - route pre-fetching
  - Incremental Static Regeneration
    - Add and update statically pre-rendered pages incrementally after build time.

- usecase
  - 针对重消费者业务的seo
  - 落地页(Landing page)
  - 博客页面(Blog posts)
  - 帮助文档(help and documentation)
  - 营销页面、产品介绍页面(Marketing pages)

- who is using
  - vercel/nextjs
  - more
    - [Companies/Sites using Next.js](https://github.com/vercel/next.js/discussions/10640)

- examples
  - libs

- tips
  - 考虑引入nextjs的收益是否够高，适合开发应用而不适合库

# pieces
- ## [Gatsby vs Nextjs vs Storybook](https://component-controls.com/blogs/gatsby-vs-nextjs-vs-storybook)
- gatsby is the original static site generator for react and continues to be a leader in this space.
- nextjs was known for SSR, however recent builds allow creating highly optimized static sites.
- while storybook is not a general-purpose SSG, it comes with its own SSG engine under the hood.

# ref
