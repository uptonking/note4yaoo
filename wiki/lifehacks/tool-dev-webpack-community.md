---
title: tool-dev-webpack-community
tags: [community, rspack, toolchain, webpack]
created: 2023-12-25T19:29:33.445Z
modified: 2023-12-25T19:29:47.236Z
---

# tool-dev-webpack-community

# guide

# discuss-stars
- ## 

- ## [What is the difference between `main` and `module` vs `exports` in package.json? - Stack Overflow](https://stackoverflow.com/questions/68572936/what-is-the-difference-between-main-and-module-vs-exports-in-package-json)
- "exports" field superseded the "module" field. 
  - "module" itself has never been an official standard but it became so widespread that at some point it was a de facto standard.
  - Note that the "module" field is still being used by TypeScript if tsconfig's moduleResolution is set to node
- The "main" field is supported in all versions of Node.js, but its capabilities are limited: it only defines the main entry point of the package.
- The "exports" provides a modern alternative to "main" allowing multiple entry points to be defined, conditional entry resolution support between environments, and preventing any other entry points besides those defined in "exports"

# discuss-rspack-not-yet
- ## 

- ## 

- ## 
# discuss-rspack
- ## 

- ## 

- ## 

- ## [rspack 4.0 版本新模块解析 styled-components 报错](https://github.com/web-infra-dev/rspack/issues/4770)
- Module resolution has to go from `"module": "./dist/styled-components.esm.js"` , then to `browser's "./dist/styled-components.esm.js": "./dist/styled-components.browser.esm.js"` part in order for things to get resolved correctly.
  - oxc_resolver is currently not doing the second part
  - I'll try and patch it tomorrow. ✅

- ## [NormalModuleReplacementPlugin is not a constructor_202306](https://github.com/web-infra-dev/rspack/issues/3522)
  - [fix(rspack): add fileReplacements support_merged✅_202308](https://github.com/nrwl/nx-labs/pull/231)

# discuss
- ## 

- ## 

- ## Do you know webpack can't guarantee the order of CSS chunks? 
- https://twitter.com/rspack_dev/status/1722493364774568218
  - Therefore, it's unwise to rely on the order of CSS chunks if your CSS depends on cross-module orders. 

- ## You either die a startup, or scale enough to return to webpack.
- https://twitter.com/ScriptedAlchemy/status/1729761667204915238
- What are some features only possible in webpack?
  - In webpack and rspack, it’s language agnostic. It compiles to any target. Its optimization phase produce’s smaller artifacts than others, except for closure compiler. Chunk and bundle split is most accurate and adaptable. You have a runtime to manage module loading, and allow you to orchestrate and interact with it. Hmr works consistently. It can cache builds. You can build things like build doctor

- ## Surprisingly it is the persistent cache, fast prebundle of esbuild and the lazy compilation brought by esm that make Vite perform quickly, while the bundleless brought by esm actually slows down Vite. 
- https://twitter.com/hardfist_1/status/1729677009989587120
  - lazy compilation, persistent cache and fast bundle are the key, not bundleless.

- ## Do you know webpack supports skipping the parsing of large files through the use of the `module.noParse` option?
- https://twitter.com/rspack_dev/status/1719707638496125128

- ## There has been a recent trend where people see one incident of a slow Vite app and start dismissing the whole bundle-less dev setup as "bad".
- https://twitter.com/youyuxi/status/1730537401217610234
- Bundle-less is slower on each reload even with all the caching in the world.
- I think it’s fair to say that the bundle-less approach is fast for smaller apps but slows down the more modules you add, and you have to pay this cost on every page load rather than only once up front. Bundlers have gotten a ton faster in the last few years, so I think people are just wondering whether it’s still the right trade-off.

- ## 💡 That's actually the reason why @rspack_dev and Turbopack both give up Native ESM(bundleless), _20231128
- https://twitter.com/rspack_dev/status/1729435649177235539
  - It's not only bad for production scenarios but also bad for development scenarios.
- [Bundling vs Native ESM - Why Turbopack? – Turbopack](https://turbo.build/pack/docs/why-turbopack#bundling-vs-native-esm)
  - Frameworks like Vite use a technique where they don’t bundle application source code in development mode. Instead, they rely on the browser’s native ES Modules system. This approach results in incredibly responsive updates since they only have to transform a single file.
  - We experimented with this approach, but ran into scaling issues with large applications made up of many modules. 
  - A flood of cascading network requests in the browser lead to a relatively slow startup time. 
  - For the browser, it’s faster if it can receive the code it needs in as few network requests as possible - even on a local server.
  - That’s why we decided that, like webpack, we wanted Turbopack to bundle the code in the development server.

- I really really wanted bundleless to work. Such an attractively simple solution! We built @nextjs Live in part to test out this hypothesis. Everything was “browser native”, from ESM to the the runtime (WinterCG). Then we tested it with Vercel’s homepage. 30s+ load times.
  - We even tried to “bundle the bundleless” as a tarball and do the unpacking in the browser to eliminate waterfalls. Still slow because it has to pack all the files. If we instead discover dependencies and pack them only… we’re back to bundling

- https://twitter.com/devongovett/status/1730229238513520933
  - Glad Parcel stayed on the bundling train this whole time. Seems like the lessons we learned 10 years ago with require.js are finally being re-learned.
  - Another problem with native ESM is that it doesn’t tree-shake, so if you import a single thing from a module with a lot of exports (eg large component library), you could be downloading hundreds or thousands of unnecessary files. Recently made a tiny Vite test app which took 12 seconds to load in development due to that.
