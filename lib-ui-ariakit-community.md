---
title: lib-ui-ariakit-community
tags: [ariakit, community]
created: 2023-06-22T05:33:03.466Z
modified: 2023-06-22T05:33:12.658Z
---

# lib-ui-ariakit-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 🌰 Here's a demo that combines Tag with Combobox:
- https://twitter.com/diegohaz/status/1768330706281754720
- dialog is anchored relative to the tag. Vs anchoring off of the input and matching it's width (and thus also not moving around as tags are added).
  - I tested both cases, and the UX seemed improved when suggestions were displayed closer to the editing point. But, of course, it's entirely configurable.

- It's something I want to add to our component and was wondering what's an elegant API for it.
  - I haven't considered a specific API for that. There's a lower-level TagAdd component that can be rendered as a combobox item

- ## 🌰 New example: Select widget controlled by URL
- https://twitter.com/diegohaz/status/1755243647476342924
  - Next.js App Router with searchParams
  - Prefetching
  - Preview link on mobile

# discuss-ui-a11y
- ## 

- ## 

- ## 
# discuss-baseui
- ## 

- ## 

- ## 

- ## 

- ## v1.0.0-rc.0 _20251204
- https://x.com/colmtuite/status/1996767313199083665
- Looks nice but what’s the difference with shadcn?
  - Base UI is not comparable to shadcn/ui, which is a set of styled comps with a high-level API surface, and a styling engine + theme.
  - Base UI is comparable to Radix Primitives, which is an unstyled lib.
  - You can use Base UI together with shadcn/ui.

- Shadcn is built on top of Radix UI. Radix Ui provides a set of accessible ui primitives that are unstyled. Base UI does the same. So base Ui is comparable to Radix UI. Potentially, shadcn can use base ui. If I'm not mistaken the guys who made base ui made radix ui.
  - Correct. You can use shadcn/ui with Base UI. It's especially easy with AI. You can ask an llm to install a shadcn/ui component but use Base UI, and it usually works pretty well.
  - Base UI has more components, more features, better a11y, better edge-case handling, better perf, and is actively maintained by a full-time team.

- ## [[discussion] Create codemod to ease Radix Primitives migration? _202510](https://github.com/mui/base-ui/issues/2970)

- ## [[discussion] Base UI Integration with SolidJS · Issue · mui/base-ui _202507](https://github.com/mui/base-ui/issues/2200)
- 👷: We're focusing solely on React now, as it's the most popular library by far. We want to do it right, and we don't have the capacity to work on multiple implementations.
  - We may consider other integrations in the future, but I believe it won't be a matter of writing an adapter layer but building the library from scratch to achieve the best performance 

- Our general stance (written in 2025) around non-React framework support is:
  - React is already a LOT to focus on. It's much better to be world-class at 1 thing, than OK-ish at 3.

- ## What exactly keeps you from using Radix in production? _202506
- https://x.com/colmtuite/status/1935629877069172861
- 👷: i mean there is nobody at the wheel. would you continue using react if the whole team left, fb stopped investing in it, issues/prs went ignored for ages, and 3 years passed without any significant improvements? it's just not an option for any serious company.
  - there has been practically nobody working on it (besides one part-time maintainer). many issues have been ignored and/or closed, prs are being ignored. the whole radix team left years ago. the company who own the project told me they want to kill it.
- Accessibility issues that have been unresolved for years too

- So is base ui the drop in replacement for radix then?
  - "drop-in replacement" is subjective. we designed base ui for an easy migration path from radix.

- Is there something like @shadcn built on @base_ui ?
- https://github.com/borabaloglu/9ui /MIT/202511/ts
  - A collection of components that you can copy and paste into your project. Built with Base UI and Tailwind CSS.

- Is Base UI funded?
  - yes. the whole base ui team (currently 5 people) is employed full-time by MUI. MUI is doing many millions in ARR, has been profitable for years, and the whole business model is based on ui dev.
  - this was the primary reason i chose the join mui + work on base ui here.

- ## [[RFC] Base UI customization API change · mui/base-ui _202402](https://github.com/mui/base-ui/discussions/157)
- I would promote the usage of the Radix Slot Component (literally or trying to follow @nihgwu nihgwu/create-slots or please take ownership of creating a RFC) and hopefully align the Mui, Radix, Headless, and React Aria ecosystem to optimize such components and patterns to a point where the React team would take ownership of providing a built-in capability to have Slots
  - The browser itself already has this developer.mozilla.org/en-US/docs/Web/HTML/Element/slot, and many other ecosystems (like Vue) are given to have the Slot pattern.

- Interesting, so you eventually chose the same approach AriaKit ariakit.org/guide/composition, and I like it
  - The most ergonomic approach is RAC's style, I had the same idea about 3 years ago, but given the context of RSC, all those context base solution don't seem so plausible, and I'm leaning to render style more, as it just requires React basics to implement it while the other solutions are full of hidden black magics

- ## [Need Help: MUI for Our Design System? : r/reactjs _202407](https://www.reddit.com/r/reactjs/comments/1drxu78/need_help_mui_for_our_design_system/)
- So the big plan is to invest into headless with Base UI, and to make both MUI Material and MUI Joy themes, so the logic & features of all components are shared, and then styling/customization is independent and easily swappable.
  - The driver for all that is that we're aware that Material Design is losing popularity because people aren't blind and google is not very good at design. But we can't just switch to a more modern look because, well, it's not MUI Material if it's not Material Design. So we want to make theming much more convenient so we're not tied to MD.
  - But that means MUI Joy is a bit slowed down at the moment until we figure out all the pieces of the big plan.

- ## 🚀 Introducing @base_ui _20241218
- https://x.com/colmtuite/status/1869053012712550819
  - ✔️ 25 accessible UI components
  - ✔️ Unstyled. Compatible with any styling engine.
  - ✔️ Fully composable with an open API
  - First awesome feature is nested dialogs
- Potentially a controversial one, but after literally a a year of research and debate, we settled on the `render` prop for component replacement and composition.
- Curious whether there is a public record of why it was chosen over `asChild` ? Would be interested to read why `render` was chosen instead
  - We actually researched about 7 or 8 different APIs. Long story short: `asChild` can be a footgun, `render` is more obvious what's going on in the code, and it's more inline with React's vibes.

- 🆚 what's the the distinction/direction of these compared to what's going on with radix ui?
  - There's not much going on with radix rn. Almost 2 years since the last new radix component, just 1 part-time maintainer. All original devs left a long time ago.
  - So rather than a new direction, the idea is to provide a familiar alternative.
  - It's not built on Radix
  - Radix has not been actively maintained for a long time. None of the original team have been working on it for 1–2 years. Issues often take a long time to be resolved. It's been 4 years since launch, and still no Combobox, Carousel, DatePicker etc. The project is effectively dead

- 🆚 When comparison with React Aria?
  - Spoiler alert: it will be prioritised like: 1. stability 2. radix parity (Toast, Menubar, NavigationMenu etc.), then Combobox and other comps
- Looks like a strong competition to React Aria from Adobe, I guess. What’s the main difference of Base UI?
  - RA is streets ahead in terms of number of components, especially the complex components. It's also more stable and mature. I'd say the main difference would be DX + API design. Lots and lots of small differences across the board.

- How is it related to MUI base UI? Has it been split out? Confused because some of the authors are MUI (former?) employees
  - It is funded by the same company, just a different brand. All current MUI employees, not former.

- I can see lots of familiarities coming from @ark_ui_

- https://x.com/colmtuite/status/1869424949758439919
  - When a small startup creates OSS as a side project, there is always the risk that it will go away at some point. 
  - The main reason I chose MUI is so that the project won't be a side hustle. Components are the business model here, and the company has been profitable for years.
# discuss
- ## 

- ## 

- ## 🌰 It doesn't take much to turn your @ariakitjs Disclosures into an Accordion. I've abstracted this away into a hook so you don't have to.
- https://twitter.com/hnkhandev/status/1765661923801231769
  - https://gist.github.com/hnkhandev/a78bbce431e73ea25e78671ae5420958

- ## 🌰 New example: Combobox with tabs
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
