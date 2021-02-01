---
title: spec-design-tokens-rfc
tags: [design-tokens, rfc, spec]
created: '2021-01-04T17:07:07.942Z'
modified: '2021-01-04T17:07:34.171Z'
---

# spec-design-tokens-rfc

# DTCG(Design Tokens Community Group)

- Design tokens are indivisible pieces of a design system such as colors, spacing, typography scale.
- The DTCG’s goal is to provide standards upon which products and design tools can rely for sharing stylistic pieces of a design system at scale.

- https://github.com/design-tokens/community-group
  - https://twitter.com/DesignTokens
  - The DTCG was founded in June 2019. 
  - 官网的例子基于theo实现

- 主流tokens工具及标准参考
  - system-ui-theme-specification
  - salesforce-theo-spec
  - style-dictionary-properties
  - airbnb-lona-spec
  - universal-design-tokens-schemas

## [[RFC] Format specification](https://github.com/design-tokens/community-group/issues/1)

- Principles
  - For core properties (name, value, description…), a design token file must be both human-editable and human-readable
  - The format is simple, extensible, and as unopinionated as possible
  - Vendors (design system tools, design tools…) can store information for their own usage, both globally and for each token
  - The format translates well to existing design tools, in order to facilitate adoption

``` typescript
interface TokenList {
  // Where tokens are stored (in an array)
  tokens: Token[];
  // is this useful? should it be optional or not?
  version?: string;

  // Optional metadata
  data?: Data;

  // What other global properties are needed? (type, category, group…)
}

interface Token {
  name: string;
  value: any;
  description?: string;
  data?: Data;
  // What other properties are needed? (type, category, group…)
}

interface Data {
  // Vendor-prefixed data
  // for example: `data: { vendor: { "@sketch": {} } }`
  vendor?: object;

  // Any number of additional properties can live here,
  // for example, for storing additional information related to the token
}

```

``` JSON
{
  tokens: [
    {
      name: 'Foo',
      value: 'Bar'
    },
    {
      name: 'I am a token',
      value: 'This is a value',
      description: 'A nice description.',
      data: {
        myOwnFlag: true,
        oneMoreThing: 'yay'
        vendor: {
          '@sketch': {
          },
          '@figma': {
          }
        }
      }
    }
  ],
  data: {
    vendor: {
      '@sketch': {
      },
      '@figma': {
      }
    }
  }
}

```

## [[RFC] Theming](https://github.com/design-tokens/community-group/issues/2)

- Here's a rough draft that essentially mimics how the CSS cascade works

``` js
// Defaults
[
  { name: 'tokenA', value: 'foo' },
  { name: 'tokenB', value: 'bar' },
]

// Overrides for dark mode, loaded subsequently
[
  { name: 'tokenA', value: 'baz' },
]

// Should resolve to:
[
  { name: 'tokenA', value: 'baz' },
  { name: 'tokenB', value: 'bar' },
]
```

## [Design Tokens Community Group Charter](https://github.com/design-tokens/community-group/blob/master/CHARTER.md)

- Scope of Work
  - Enabling sharing color palettes or themes between multiple design tools
  - Allowing design system tooling to share a common language with other parts of the design process
  - Lowering the bar for design and development teams to deploy design tokens in their workflows

- Out of Scope
  - TBD: Identify topics known in advance to be out of scope

- Specifications
  - format, grammar, syntax
  - color
  - spacing
  - durations
  - typography
  - any other design token-related specifications

# Open UI

- open ui相对于dtcg的特点
  - 重点是通用ui组件的样式与交互规范，而dtcg重点是通用样式变量
  - 重点是帮助开发者和设计师互操作，而dtcg重点是各类设计工具的互操作

- The web deserves interoperability between component frameworks and design systems.
  - The UI community should standardize namings and structures for common components. 
  - We should also standardize a way of theming these components. 
  - We should set a path for existing solutions to converge and for browsers to natively provide these things in the future.

- https://github.com/WICG/open-ui
  - https://open-ui.org/components/button
- https://wicg.io/
  - to define the next generation of web technologies.

## [Web Incubator Community Group Charter](https://wicg.github.io/admin/charter.html)

- These are the goals Open UI believes will realize the above vision.
  - Document component names as they exist today
  - A common language for describing UIs and design systems
  - Browser standards for web app components

- Scope of work
  - Utilize descriptivism of common patterns to identify and standardize on:
    - Component names and parts
    - States
    - Behaviors
    - How behaviors transition state (eg: keyboard or pointer interaction)
  - The necessary accessibility requirements (this is not in place of WAI-ARIA or WCAG but linking where appropriate to alleviate implementor pain)
  - Upon discovery of gaps in the web platform, denote those and raise relevant issues to standards bodies
  - Design system terminology

- Out of scope
  - Standardization of appearance of the component

# ref

- https://github.com/malerba118/react-handoff
  - https://codesandbox.io/s/async-night-7kyrq?file=/src/App.tsx
  - 依赖chakra-ui, emotion
  - aimed to turn any react app into a visual editor where you can visually tweak and persist props from the browser.
  - enables designers and developers to work in parallel
  - 修改后组件的配置可以导出为json，而组件的默认值从json初始化
