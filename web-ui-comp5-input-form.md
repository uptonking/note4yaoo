---
title: web-ui-comp5-input-form
tags: [components, form, ui, web]
created: 2021-04-23T15:20:03.201Z
modified: 2021-07-28T20:11:24.350Z
---

# web-ui-comp5-input-form

> 数据输入类组件，表单组件

# guide
- form设计
  - form提交后，若请求处理失败，应该保持旧的输入记录方便用户直接修改，而不是展示空白form让用户重新输入
# switch

## [Switch Pattern | APG | WAI | W3C](https://www.w3.org/WAI/ARIA/apg/patterns/switch/)

- switches can only be used for binary input while checkboxes and toggle buttons allow implementations the option of supporting a third middle state. 

- it is critical the label on a switch does not change when its state changes.

- If the switch element is an HTML `input[type="checkbox"]`, it uses the HTML `checked` attribute instead of the `aria-checked` property.

- ## [Building a switch component](https://web.dev/building-a-switch-component/)
- This demo uses `<input type="checkbox" role="switch">` for the majority of its functionality, which has the advantage of not needing CSS or JavaScript to be fully functional and accessible.

- https://github.com/argyleink/gui-challenges/blob/main/switch/style.css

- ## [Build an accessible Switch Component with React and Typescript.](https://levelup.gitconnected.com/build-an-accessible-switch-component-with-react-and-typescript-d455a405aaa)
- HTML unfortunately does not support native switch elements. 
  - We can opt for a simple `<input type="checkbox" role="switch" />`, remove all default browser styles using the CSS declaration `appearance: none;` and apply our own custom styles

- ## [The good, the bad and the toggle.](https://uxdesign.cc/the-good-the-bad-and-the-toggle-2abc0fbbd099)
- Do not use toggles in forms. Use checkboxes or radio buttons instead.
- Do not use toggles in filters or multiple selections of elements.
- Use toggles for settings and changes that have an immediate effect on the UI (same applies for the segmented control).
- Avoid mixing toggle button groups and segmented controls.
- Avoid using switches with multiple options.

- ### [Checkbox or switch?](https://bootcamp.uxdesign.cc/checkbox-or-switch-97dd932b01c0)
- If the actions rely on each other, for instance, choosing one will choose the others as well, then use checkbox
- Switch takes more space, and this big space provides more design possibilities.
- There are gaps between guidelines and actual practices

- ### [checkboxes - Checkbox vs toggle](https://ux.stackexchange.com/questions/63884/checkbox-vs-toggle)
# discuss
- ## 

- ## 

- ## 

- ## Using the JavaScript `FormData` Web API, you can progressively enhance a simple, accessible form, into a more dynamic form, without the downsides of heavy JS frameworks that do the same thing.
- https://twitter.com/SaraSoueidan/status/1521469586691997696
  - [Progressive Enhancement and HTML Forms: use FormData](https://www.bram.us/2022/04/22/progressive-enhancement-and-html-forms-use-formdata/)
