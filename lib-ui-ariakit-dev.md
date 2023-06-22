---
title: lib-ui-ariakit-dev
tags: [ariakit, ui]
created: 2023-06-22T05:32:44.639Z
modified: 2023-06-22T05:32:58.602Z
---

# lib-ui-ariakit-dev

# guide

- architecture
  - state: component-store
  - styling: unstyled
  - a11y: ariakit
  - motion

- resources
  - [Ariakit | newsletter](https://newsletter.ariakit.org/)
# dev

# codebase
- 每个组件大概分3部分
  - @ariakit/core中包含vanillajs实现的store
  - @ariakit/react-core中包含各组件的hooks和完全体组件，只依赖@floating-ui/dom
  - @ariakit/react只负责导出各种组件和types

- useCheckbox返回创建checkbox组件所有的props，
  - 但自身并未创建store，需要外部传入store
  - 自身只订阅了store的更新和rerender逻辑

- useCheckboxStore会在react组件内执行createStore，并通过useSyncExternalStore实现自定义useState方法
  - createStore，类似redux

- store和react组件的通信基于useSyncExternalStore

- createStore
  - 区分init/setup/setState的流程
# changelog
- 202304
  - [Component stores](https://newsletter.ariakit.org/p/component-stores)
# more
