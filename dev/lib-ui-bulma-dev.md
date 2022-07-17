---
title: lib-ui-bulma-dev
tags: [bulma, lib, ui]
created: 2020-10-19T16:22:26.951Z
modified: 2020-12-08T13:33:31.191Z
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

# theming 

- themes for bulma
  - https://jenil.github.io/bulmaswatch/

- [Support for css variables_202007](https://github.com/jgthms/bulma/issues/3028)
  - I have a few branches working on it. I only need to find the best way to implement it.
  - https://github.com/jgthms/bulma/tree/css-variables-with-fallback

``` CSS
/* theming by add a data-theme="dark" to the <body> element */
:root,
[data-theme="default"] {
  --color-primary: black;
  --color-bg: white;
}

[data-theme="dark"] {
  --color-primary: white;
  --color-bg: black;
}

body {
  background-color: var(--color-bg);
  color: var(--color-contrast-high);
}
```

- [Optional CSS Variables and multi-theme ability_202006](https://github.com/jgthms/bulma/pull/2981)
  - https://github.com/Tofandel/bulma
  - This PR does this successfully with a lot of ingeniousity by maximizing backward compatibility, 
    - the framework can be compiled exactly like before with no css variables, 
    - it can be compiled with all the css variables for outside theming 
    - or it can be compiled with a set of themes for bundled theming
  - The only tradeoff of this solution is that because of the wrapping of each variable, the git diff is large
  - and will require future PR to follow the new syntax (though it's not a hard syntax, just slightly repetitive)
  - I do like the idea of having a separate themable css file 
    - but I think most of the JS functions could have been done in Sass/Ruby.
    - Also there’s duplication in the css vars
      - we could use hsl values instead of having a literal value as well. 
      - Because then we’d only need to change a color in a single location.
    - I also think the final output is missing the point of having the css vars, as the initial variable names are completely gone.
  - I like the idea of having a separate themable Bulma CSS file. 
    - I’m not super keen of introducing a JS build process but it seems like the only solution for a few of the problems.
    - The major issue I see right now is how most of the initial and derived variables become deprecated, even for non-themable setups
    - I also think it’s not necessary to transform all Bulma variables into CSS variables. For theming purposes and dark mode support, colors would largely suffice.

- https://github.com/wtho/bulma-css-vars
  - Bulma CSS Vars extends Bulma to use CSS variables, 
  - that can be set to arbitrary values at runtime on the website and installs fallbacks for browsers without CSS variables capabilities.

# issues

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

# book: Creating Interfaces with Bulma_Jeremy Thomas_2018

- bulma features
  - modern css framework with flexbox
  - 100% responsive, designed to be both mobile and desktop friendly
  - customizable with over 300 sass variables
  - css only, no js
