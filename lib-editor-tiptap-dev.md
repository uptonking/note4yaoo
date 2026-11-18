---
title: lib-editor-tiptap-dev
tags: [lib, prosemirror, text-editor, tiptap-editor]
created: 2021-05-06T09:45:58.536Z
modified: 2023-02-05T19:03:27.730Z
---

# lib-editor-tiptap-dev

# guide

- features
  - headless without any css
  - framework-agnostic
  - realtime collaboration with yjs
  - customizable with a ton of extensions
  - typescript
  - 协同后端实现hocuspocus
  - 支持多层嵌套拖拽
  - 示例丰富(drawing), RAG生成示例
    - 编辑器内嵌入iframe

- who is using #tiptap
  - gitlab
  - mantine-ui-editor
  - gamma-ppt
  - Flowbite
  - hashnode
    - https://twitter.com/sandro_vol/status/1676869292724305920

- resources
  - [General block dragging feature](https://github.com/ueberdosis/tiptap/issues/323)
  - https://tiptap.dev/guide/node-views/examples#drag-handles
# faq-not-yet

# more

# changelog
- resources
  - [Tiptap | Release Notes & Updates ](https://webflow.tiptap-lab.com/blog/release-notes)
  - [Tiptap is now a YC-backed company. - Tiptap Insights _202307](https://tiptap.dev/blog/insights/tiptap-ycombinator)

## v3.0.0

- [Launch YC: Tiptap 3.0 Beta: The Next-Gen Open Source Editor _202505](https://www.ycombinator.com/launches/NR5-tiptap-3-0-beta-the-next-gen-open-source-editor)
- [Tiptap 3.0 is stable – Tiptap Release Notes _202507](https://tiptap.dev/blog/release-notes/tiptap-3-0-is-stable)

- Meta‑packages
  - We bundled common extensions into @tiptap/extensions, @tiptap/extension‑list, @tiptap/extension‑table, and @tiptap/extension‑text‑style. Less boilerplate, better tree-shaking.
  - All floating menus now use Floating UI. Smaller bundle, better positioning, same API
  - Pro → OSS: Features like Drag-handle, Emoji, Math, File Handling, and more are now open-source.
  - Server‑friendly: You can now create editors without DOM elements. Great for SSR frameworks like Next.js and Nuxt.
  - Static Renderer: Convert Tiptap content to HTML, Markdown, React components, or your own format with @tiptap/static-renderer.

- 
- 
- 
- 
- 
- 

## v2.0.0

- [It’s public! The Tiptap v2.0 beta _202104](https://tiptap.dev/blog/release-notes/tiptap-public-beta)

- we have built this three years ago, without knowing what we are going to run into. 
- for v2, It’s (finally) framework-agnostic, written in TypeScript, comes with a handful of new and amazing extensions, has hundreds of tests, 150 pages of documentation, first class collaborative editing support, integrations for Vue 2, Vue 3, and React, guides for Svelte, Alpine, Nuxt.js, a modern CDN build, SSR utilities, more than 80 interactive examples 

- 
