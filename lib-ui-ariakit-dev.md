---
title: lib-ui-ariakit-dev
tags: [ariakit, ui]
created: 2023-06-22T05:32:44.639Z
modified: 2023-06-22T05:32:58.602Z
---

# lib-ui-ariakit-dev

# guide

- features
  - low-level hooks/components
  - accessible-ui
  - 渲染灵活，支持自定义render和wrapElement

- pros
  - 支持多store
  - 支持batch-update

- cons
  - 组件比较少

- architecture
  - state: component-store
  - styling: unstyled
  - a11y: ariakit
  - motion

- patterns-common
  - collection
  - command-press-pointer
  - composite-arrow-keys
  - focus-tab
  - group-label + separator
  - portal

- tips
  - 从另一个角度看，对state/logic的复用，hooks本身就是一种实现方式，但hooks需放在组件内
  - 将state移出react的方案还可参考nanostores、redux
  - css样式可参考shadcn-ui、skeleton-ui、tailwind-ui、flowbite、daisyui组件
  - 实现agnostic的2种思路，一是类似ariakit只处理状态，二是类似tanstack将所有状态和事件移出去
    - ariakit的优点是对react更友好，core-store的核心状态~~不含外部event~~方便序列化
    - tanstack的优点是对多框架的支持更友好，事件也会作为props返回，默认非受控状态且支持部分受控状态
  - useSyncExternalStore对react友好，对其他框架不友好

- resources
  - [Ariakit | newsletter](https://newsletter.ariakit.org/)
# dev-to
- new-components
  - reakit: grid/input(已迁移少文档)
  - menu/select/combobox-autocomplete/radio/tabs
  - disclosure/dialog/popover
  - 👉🏻 card/list
  - form: switch/TextInput/search/slider
  - carousel/progress
  - sidebar
  - more: calendar, darg-layout, media
# dev

# codebase
- 每个组件大概分3部分
  - @ariakit/core中包含vanillajs实现的store
  - @ariakit/react-core中包含各组件的hooks和完全体组件，只依赖@floating-ui/dom
  - @ariakit/react只负责导出各种组件和types

- 代码量较少的组件
  - checkbox
  - disclosure

- react层的逻辑
  - 同步自定义store和reactState
  - 在react层通过useEvent准备事件监听器如onChange、处理animation
  - 组合a11y相关的mouse/keyboard事件
  - 根据props中的配置，给返回的props中加上a11y相关的attrs
  - 给组件props加上render和wrapElement
  - 组件api的设计更符合react

- useCheckboxStore
  - `store = useStore(() => Core.createCheckboxStore(props))`; 
    - 会在react组件内执行createStore，并通过useSyncExternalStore实现自定义useState方法
  - `return useCheckboxStoreProps(store, props)`; 
    - 注册listener，在core-store变化时更新props.value和setValue

- useCheckbox返回创建checkbox组件所有的props，
  - 但自身并未创建store，需要外部传入store
  - 自身只订阅了store的更新和rerender逻辑

- store和react组件的通信基于useSyncExternalStore

- state-read
  - `store.useState()` returns the entire state object and re-renders the component whenever the state changes.
    - 实现基于useSyncExternalStore
  - `store.getState()` won't trigger a re-render on the component.

- state-write
  - `store.setState()` can be used to mutate any state in the store. This method shouldn't be called during render

- createStore
  - 区分init/setup/setState的流程

- useStore 创建自定义store对象
  - Creates a React store from a core store object.
  - 在store变化时通过`useStoreState`触发rerender

- useStoreState
  - Subscribes to and returns a computed value of a store based on the selector function.
  - 基于useSyncExternalStore实现

- useStoreProps
  - Synchronizes the store with the props, including parent store props.
  - 注册listener，每次store变化时，调用props.setValue来更新业务层的状态值，一般还会触发业务层rerender

- 自定义store值的更新流程
  - 每次创建时(useCheckboxStore)会先创建自定义store对象，然后注册自定义store同步到业务层状态的方法setKey1，通过store.sync方法注册
  - 每次combobox.useState("open")会useSyncExternalStore，监听指定key的变化触发rerender，store.subscribe参数可空
  - 每次dialog.setState(v=>!v)时，实际触发 store.setState("value", value)更新值，会执行注册过的所有listeners方法包括setKey1

- store.setState
  - 逻辑很复杂，要点是支持多store、支持batch-update
# changelog
- 202304
  - [Component stores](https://newsletter.ariakit.org/p/component-stores)
# docs
- Ariakit exports a set of unstyled React components and hooks that you can use to build accessible web apps.
  - Ariakit provides unstyled components by default. 
  - Ariakit components accept all native props, including className, style, and ref.
- Ariakit renders elements with HTML attributes, such as role, that should not be used as CSS selectors as they're not part of the public API and may change in future minor and patch releases.
  - To safely use CSS selectors, utilize the `className` prop or provide your own `data-*` attributes to the component. 
- Some components, such as Popover, Menu, Hovercard, SelectPopover, ComboboxPopover, among others, expose CSS variables that you can use to customize their appearance.

- The `render` prop makes Ariakit components more versatile, allowing you to easily replace the default HTML element or enhance its features with custom components.
- When passing an HTML element to the render prop, all the HTML props returned by the original component will be passed to the rendered element. 
- With the render prop, you don't need to nest the children inside the rendered element. Instead, you can pass the children as usual to the original component to avoid extra nesting.

- the render prop can also receive a function that takes the original component's HTML props as a parameter and returns a React element. 
  - This provides you with greater control over the process of merging props
  - Another use case for the render function is to render elements between an internal wrapper and the rendered element. 
  - When a function is passed to the render prop, the HTML props will not be automatically merged into the returned React element. It's your responsibility to merge them within the function itself

- When using the render prop with a custom component, you must ensure the component is open for extension. 
  -  This means it should pass the incoming props, including event listeners and the forwarded ref prop, to the underlying element.
  -  Chain the event props with the internal event handlers, if any.

- Component stores allow you to read and write the state of Ariakit components
  - Then, you should pass the store to the wrapping components of that module
- Reading the state
  - combobox.useState(); 
  - combobox.useState("open"); 
  - store.useState((state) => state.activeId === id); 
  - combobox.getState(); 
- Writing the state
  - dialog.setState("open", true); 
  - dialog.setState("open", (open) => !open); 
  - dialog.setOpen((open) => !open); 

## Abstract components

- Collection
  - Track a collection of DOM elements in the exact order they're rendered in the DOM and watch the DOM for any change to their order.
- Command
  - Click with a mouse or keyboard to trigger an action
  - If you need a clickable element with a different semantic role (e.g., menuitem), and you're not using the specific Ariakit component (e.g., MenuItem), you can use Command.
- Composite
  - Provide a single tab stop on the page and navigate through the focusable descendants with arrow keys
- Separator
  - Distinguish sections of content or groups of Composite items. 
- Focusable
  - Click or press Tab to move focus to any React element using this abstract component that normalizes the focus behavior across browsers.
- Group
  - Group related elements in a generic container that may have a label. 
- Portal
  - Attach an element to a DOM node outside the parent component's hierarchy.
- Role
  - Provide the basic Ariakit features to any component.
- 
- 
- 
- 

# more
