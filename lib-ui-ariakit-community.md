---
title: lib-ui-ariakit-community
tags: [ariakit, community]
created: 2023-06-22T05:33:03.466Z
modified: 2023-06-22T05:33:12.658Z
---

# lib-ui-ariakit-community

# guide

# discuss-news
- ## 

- ## 

- ## ✨ New example: Select widget controlled by URL
- https://twitter.com/diegohaz/status/1755243647476342924
  - Next.js App Router with searchParams
  - Prefetching
  - Preview link on mobile

# discuss
- ## 

- ## 

- ## 

- ## New example: Combobox with tabs
- https://twitter.com/diegohaz/status/1738615278701892062
  - It combines Combobox and Tab components to create an accessible combobox widget, where options are organized into tabs.

- Very cool! How flexible it is to use a controlled content-editable element (a rich-text editor framework) instead of an input/textarea? Considering to integrate it in SlateJS.
  - It should be flexible enough, but it does require some effort from the developer. In the early days of Ariakit, I experimented with Lexical.js and made it work. The API has seen some improvements since then

- ## New example: Navigation Menubar
- https://twitter.com/diegohaz/status/1729471805637722297
  - [Navigation Menubar - Ariakit](https://ariakit.org/examples/menubar-navigation)
  - 演示提供了三角区域示例

- ## I'm thinking of writing a guide on Ariakit to clarify the code style choices made in the code examples showcased on the site.
- https://twitter.com/diegohaz/status/1685937027596926976
  1. Use interface instead of type.
  2. Declare named functions inside forwardRef.
  3. Import styles first.
  4. Import with the .jsx extension.

- Depending on what you want to enforce, I'd say to import the styles last (this allows to override styles imported by the other files more easily)

- ## I’ve been maintaining component libraries focused on accessibility for the past 6 years. While they help a lot, the amount of a11y that can be automated with a lib is 10% or less.
- https://twitter.com/diegohaz/status/1681697273342722049
  - Most a11y issues come from design, content, page structure, and relationships between multiple components.
  - A well-designed component library will increase awareness around a11y rather than make developers forget about it, because automatic accessibility isn’t really a thing.

- ## There's an @​ariakit/core library where most of the code will live._20230430
- https://twitter.com/diegohaz/status/1652542224679288832
  - Right now, it includes component stores, but it will have more component logic in the future.
  - Also, our integration tests are framework-agnostic already

- downshift was such an interesting project by @kentcdodds . 
  - It was my first encounter of a headless UI library that doesn't render HTML but just provide a bunch of props. 
  - I've been lately searching for UI libraries that has a foundation of such headless approach.
  - If the core library provides methods for actions and prop getters for potential elements, the next step would be to build actual components in any frontend framework.
  - Any UI library like that approach?
- @zag_js and/or ark-ui
- @tannerlinsley has a few! Virtualizers, tables, oh my!

- The dream is to get folks building such libraries with `Mitosis` which can be responsible for that adapter layer that changes for each web framework.
  - Interesting. In order for you to support all the frameworks, you've chosen to **write DSL and convert it to JSON**. Not what I had in mind, but it seems like a good idea.

- ember-headless-table is another headless ui library that doesn't render HTML on its own.
Instead, it provides the math, calculations, and props for managing common table features (because no one needs to be re-implementing those every time they switch companies)

- ## [ariakit RFC: Component stores_202209](https://github.com/ariakit/ariakit/issues/1875)

- https://codesandbox.io/s/ariakit-component-stores-forked-248do5
- The problems
- We can't reuse the state logic outside of React
- Host components render on every state update
- Methods as deps in useEffect, useCallback, etc.
- Component stores
- The store would be implemented with vanilla JS so we can reuse it in other frameworks. 
- The React hook would use the `useSyncExternalStore` hook internally, so we can keep it compatible with concurrent rendering.
- Accessing state inside event handlers without re-rendering
- Computed selectors can be easily achieved in userland

- [ariakit RFC: Support controlled state hooks](https://github.com/ariakit/ariakit/issues/487)
- another proposal will be fully possible in Reakit v3: a single parameter that can receive both uncontrolled and controlled state.
- `const state = useDialogState({ initialVisible: false })`; 
- `const state = useDialogState({ visible, setVisible })`; 

### [Framework-agnostic architecture for examples](https://github.com/ariakit/ariakit/issues/1854)

### [Offer Vue components / hooks](https://github.com/ariakit/ariakit/discussions/1723)

# discuss-reakit
- ## 

- ## 

- ## In @reakitjs' Menu/Submenu, there's some Math to calculate the pointer movement so it doesn't close the submenu while you're trying to move to it in a non-straight line._202007
- https://twitter.com/diegohaz/status/1283557473027346439
  - Solution consists in verifying if the cursor is moving in a virtual triangle area. This was one of the rare moments that I had to use Math from school in web dev. But school wasn't really helpful as I had to learn everything again to fix this.
  - https://github.com/ariakit/ariakit/blob/reakit/packages/reakit/src/Menu/__utils/useTransitToSubmenu.ts
  - 可参考 [useHover#safePolygon | Floating UI](https://floating-ui.com/docs/usehover#safepolygon)
  - [Better Context Menus With Safe Triangles — Smashing Magazine](https://www.smashingmagazine.com/2023/08/better-context-menus-safe-triangles/)

- ### Notion 优化了走直线选不中子级菜的问题，想起之前 @height_app 的一篇关于 context menus 细节的文章。
- https://twitter.com/leadream4/status/1629307997175549952
  - 一般的解决方案是加一个延迟，但是更好的方式是增加三角安全区域，亚马逊和苹果都是这样处理的。
  - [Breaking down Amazon's mega dropdown](https://bjk5.com/post/44698559168/breaking-down-amazons-mega-dropdown)
  - [A comprehensive guide to creating intuitive context menus - Height](https://height.app/blog/guide-to-build-context-menus)
  - [Invisible details - Building contextual menus - Linear Blog_202009](https://linear.app/blog/invisible-details).
  - `clip-path` is a cool css property that lets you define a region of the component that should be drawn to the screen. In this case we use a polygon to draw a triangle.
  - [MouseSafeArea.ts](https://gist.github.com/eldh/51e3825b7aa55694f2a5ffa5f7de8a6a)

- ### notion: Before, you had to be really precise with your cursor so menus wouldn’t disappear on you. Should feel much more polished now
- https://twitter.com/NotionHQ/status/1629175696177389569

- Can you open source your implementation?
  - looks like a delay when the menu loses focus, instead of closing immediately it waits for like 3 seconds

- I remember a talk from @peduarte for a similar functionality that they included in the dropdown for `@radix_ui` lib, curious about the implementation
  - [So You Think You Can Build A Dropdown? - Pedro Duarte - (Next.js Conf 2021) - YouTube](https://www.youtube.com/watch?v=pcMYcjtWwVI)

- ## A thread of threads about JavaScript, React, @reakitjs and front-end development in general_202008
- https://twitter.com/diegohaz/status/1291090534161887236
  - Why explicit hook-based APIs are better than implicit context-based APIs. And why they're not.
  - Menu/Submenu Math.
  - Composite widgets.
  - Avoiding unnecessary re-renders with React.memo and non-primitive props.
