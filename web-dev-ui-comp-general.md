---
title: web-dev-ui-comp-general
tags: [components, ui]
created: '2021-03-16T15:12:30.702Z'
modified: '2021-03-16T15:12:58.491Z'
---

# web-dev-ui-comp-general

# 

# button

## faq

### `<a>`作为button使用时，无法使用<kbd>Tab</kbd>键获得焦点

- `<a role="button">anchor</a>` 无href属性就无法tab键focus
- `<a>anchor</a>` 无href属性就无法tab键focus
- `<a href="#">anchor</a>` 可focus，但会跳转到顶部
- `<a tabindex="0">anchor</a>` 可focus，不跳转
