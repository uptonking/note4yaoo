---
title: lib-office-fumadocs-docs
tags: [docs, fumadocs]
created: 2026-07-13T21:24:02.888Z
modified: 2026-07-13T21:24:31.775Z
---

# lib-office-fumadocs-docs

# guide

# overview
- The Fumadocs framework refers to a combination of UI + Core + Content Source, Fumadocs is more of a mental framework and each layer can be a library on its own.
- While most frameworks are configured with a configuration file, they usually lack flexibility when you hope to tune its details. You can’t control how they render the page nor the internal logic.
  - Fumadocs expects you to write code and cooperate with the rest of your software, it shows you how the app works and fully customisable, instead of a configuration file.

- You'll have to configure i18n routing on your React framework and Fumadocs.
  - Fumadocs is not a full-powered i18n library, it's up to you 

- Fumadocs UI maintains support for both Base UI and Radix UI, while it uses Base UI by default.
  - Fumadocs UI adds its own colors, animations, and utilities with Tailwind CSS preset.
  - 支持 accordion, file-tree, image, tabs
  - Layouts: docs, notebook, flux, home, Page

- 
- 
- 
- 
- 

# docs

- 
- 
- 
- 
- 

## [MDX](https://www.fumadocs.dev/docs/mdx)

- Fumadocs MDX is a tool to transform content into type-safe data, similar to Content Collections.
  - Fumadocs MDX is a bundler plugin, 支持 nextjs, vite, runtime-loader
- It is not a full CMS but rather a content processing layer for React frameworks, you can use it to handle blog posts and other contents.
- Collection refers to a collection containing a certain type of files. You can define collections in the config file (source.config.ts).
  - Fumadocs MDX transforms collections into type-safe data, accessible in your app. 

- Although Fumadocs MDX can handle nearly 500+ files, it could be slow and inefficient. A huge amount of MDX files can cause extremely high memory usage during build and development mode.
- The main solution is to make the compilation on-demand, such that content is only loaded when it's being requested.
  - Create your custom content source with remoting content loading.

- By default, all Markdown and MDX files need to be pre-compiled first. The same constraint also applies to the development server.
  - You can enable Async or Dynamic mode on doc collections to improve this.
- Async mode will generate collection outputs using async imports.
- Dynamic mode works by performing on-demand compilation, then execute the output on runtime.
  - Dynamic mode comes with some limitations on MDX features.
  - No import/export allowed in MDX files. For MDX components, pass them from the components prop instead.
  - Images must be referenced with URL (e.g. /images/test.png). Don't use file paths like ./image.png. You should locate your images in the public folder and reference them with URLs.

- @fumadocs/local-md is a content source for local Markdown/MDX files, it is bundleless (works fully at runtime) by design.
  - local-md works at runtime, but during development you can connect to its dev server for file watching.
  - When compiling Markdown files (*.md), @fumadocs/local-md uses a virtual JavaScript engine to avoid eval() at runtime.

- MDX Remote can compile MDX content to JSX nodes. Since it doesn't use a bundler, there's some limitations: Images have to be optimized at runtime. No imports and exports in MDX files.
  - Without Server Components, you can enable skipRender and pass the compiled code to client instead

## [ssg](https://www.fumadocs.dev/docs/deploying/static)

- By default, Fumadocs use a server-first approach which always requires a running server to serve.
- You can output a static build by configuring your React framework.

- 
- 
- 
- 
- 
- 

# more
