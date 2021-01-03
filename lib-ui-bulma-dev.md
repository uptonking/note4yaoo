---
title: lib-ui-bulma-dev
tags: [bulma, lib, ui]
created: '2020-10-19T16:22:26.951Z'
modified: '2020-12-08T13:33:31.191Z'
---

# lib-ui-bulma-dev

# faq

## bulma vs bootstrap

- bulma pros
  - Modern features such ad flexbox, css vars, css grid
  - Simple grid system
    - a single .columns container to wrap as many .column items as you want.
  - Font Awesome 5 support
  - 100+ useful CSS helpers
  - No JavaScript

- bootstrap pros
  - jQuery plugins
  - big community
  - IE 11 compatibility
  - Additional elements
  - Accessibility with WCAG 2.0 guidelines

- ref
  - [Coming from Bootstrap](https://bulma.io/alternative-to-bootstrap/)
  - [Bulma vs Bootstrap - Developer Opinions](https://www.reddit.com/r/web_design/comments/9h8o3f/bulma_vs_bootstrap_developer_opinions/)

# guide

# [bulma overview](https://github.com/jgthms/bulma)

- [bulma docs](https://bulma.io/documentation/overview/start/)
- By default, columns are only activated from tablet onwards. 
  - This means columns are stacked on top of each other on mobile.
- Bulma is compatible with all icon font libraries: Font Awesome 5, Font Awesome 4, Material Design Icons, Open Iconic, Ionicons etc.

# components-catalog

- Elements(only require a single CSS class)
  - Block:a simple spacer tool.
  - Box
  - Button
  - Content: WYSIWYG generated content where only HTML tags are available
  - Delete cross
  - Icon
  - Image
  - Notification
  - Progress bars
  - Table
  - Tag
  - Title
- Components(multi-part components)
  - Breadcrumb
  - Navbar
  - Menu
  - Pagination
  - Dropdown
  - Card
  - Modal
  - Message
  - Panel
  - Tabs
- Layout
  - Container
  - Columns
  - Level: horizontal level which can contain almost any other element
  - Media Object
  - Hero
  - Section
  - Footer
  - Tiles: build 2-dimensional Metro-like, Pinterest-like grids

# theming 

- themes for bulma
  - https://jenil.github.io/bulmaswatch/

# book: Creating Interfaces with Bulma_Jeremy Thomas_2018

- bulma features
  - modern css framework with flexbox
  - 100% responsive, designed to be both mobile and desktop friendly
  - customizable with over 300 sass variables
  - css only, no js
