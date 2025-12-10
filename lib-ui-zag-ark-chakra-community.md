---
title: lib-ui-zag-ark-chakra-community
tags: [ark-ui, chakra-ui, community, ui, zagjs]
created: 2023-06-22T05:34:36.199Z
modified: 2023-06-22T05:34:53.757Z
---

# lib-ui-zag-ark-chakra-community

# guide

# discuss-ark
- ## 

- ## 

- ## If you're using shadcn/ui, swapping out Radix for Base UI or React Aria is a lot easier than you might think. _20251004
- https://x.com/colmtuite/status/1974194981461238254
- base-ui solved a perf problem I had with radix which re-rendered the whole app when a modal/popover was opened and moving to it was literally just telling codex to migrate the dialog and popover components to base-ui primitves. 

- probably the biggest “effort” would be refactoring all the asChild usages to render, especially in big codebases. but a codemod or just asking the ai to do it would be enough i guess

- ## ark looks like a nice radix-ui alternative tbf
- https://x.com/jjenzz/status/1996713641379274988
- its really awesome; being able to access internal state makes it easy to work with! they expose both the components AND the hooks + there's always a `<XXX.Context>` component with a render prop

- What’s about base ui ?
  - react only afaik
- yes except that it locks some components that you can easily find for shadcn/radix behind a paywall, and the ecosystem is around radix (maybe baseui in the future)
  - we do not lock any component behind a paywall. just added some complex compositions that you may find useful.
  - 确实很多付费组件 [Slider with Number Input | Ark UI](https://ark-ui.com/examples/slider-with-number-input)

- https://x.com/hugokorte_/status/1996594822677754175 _20251204
- Why use Base UI over Ark UI? It really confuses me people are creating framework specific headless solutions when there is Ark, a framework agnostic solution
  - The multi-framework approach sounds great, but who has ever managed to pull it off?
  - Ark UI React is downloaded x20 more times than the other frameworks
  - Ark UI React Checkbox is +1.8 kB gzipped compared to Base UI Checkbox. Is there a cost to do multi-framework?
# discuss
- ## 

- ## 

- ## 

- ## 

- ## The creators of @chakraui_ui are using @zag_js to create @ark_ui_20230330
- https://twitter.com/log1400/status/1641282604790947840
- Ark-ui handles the connection between framework primitives ( internal state, callback handlers etc ) with zagjs machines for you
