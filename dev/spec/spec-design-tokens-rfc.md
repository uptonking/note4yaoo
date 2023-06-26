---
title: spec-design-tokens-rfc
tags: [design-tokens, rfc, spec]
created: 2021-01-04T17:07:07.942Z
modified: 2021-01-04T17:07:34.171Z
---

# spec-design-tokens-rfc

# solutions

- design-tokens-catalog
  - style-dictionary强大之处在于可定制parser、transformer、formatter、actions

- ref
  - [Native modes and theming support](https://github.com/design-tokens/community-group/issues/210)
    - Currently(202303) the spec does not support theming

## w3c Design Tokens Format

- [Share your tools that support the DTCG format](https://github.com/design-tokens/community-group/issues/211)

- https://github.com/drwpow/cobalt-ui
  - https://cobalt-ui.pages.dev/
  - Cobalt turns your W3C design tokens into code
  - The general approach is similar to Style Dictionary or Universal Design Tokens to solve the problem of creating a single source of truth for design tokens that is platform-agnostic and easy to build tooling for.

- https://github.com/AnimaApp/design-token-validator
  - https://animaapp.github.io/design-token-validator-site/
  - check whether your design tokens adhere to this standard, and how you can improve your tokens to ensure that they do

### issues

- [Native modes and theming support](https://github.com/design-tokens/community-group/issues/210)
  - [Themes/Schemes vs. Design Tokens ](https://github.com/design-tokens/community-group/issues/187)
- [Remove REM/EM from specification?](https://github.com/design-tokens/community-group/issues/218)
- [$name property? human-readable](https://github.com/design-tokens/community-group/issues/112)
- [Standardizing the Handoff - Conceptual ](https://github.com/design-tokens/community-group/issues/220)
  - Token Naming Convention
  - Token Values
  - Token Structure
  - Token Modification Rules
  - Token Usage Guidelines

- [Conditional token values](https://github.com/design-tokens/community-group/issues/169)
  - This is fine and that is why $extension exists. It allows anyone to experiment.
- [Can alias tokens reference tokens in another file?](https://github.com/design-tokens/community-group/issues/166)
  - Specifying multiple files in a specific order for a CLI like your theoretical-token-tool example is OK. But might be more cumbersome in a GUI

- [Proposal for a Standardized Color Palette Specification](https://github.com/design-tokens/community-group/issues/186)
  - I'm sorry to say this is out of scope of this spec, and belongs in the realm of tooling.

### [Design Tokens Format Module](https://design-tokens.github.io/community-group/format/)

- A (Design) Token is an information associated with a name, at minimum a name/value pair.
- A token's type is a predefined categorization applied to the token's value.
- A group is a set of tokens belonging to a specific category.
- Composite (Design) Token
  - A design token whose value is made up of multiple, named child values
- When saving design token files on a local file system, it can be useful to have a distinct file extension 
  - .tokens, .tokens.json
- An object with a `$value` property is a token. 
  - Thus,  `$value` is a reserved word in our spec
  - Name and value are both required.
  - Token names are case-sensitive
- **All properties defined by this format** are prefixed with the dollar sign (`$`). 
  - This convention will also be used for any new properties introduced by future versions of this spec. 
  - Because of the decision to prefix group properties with a dollar sign ($), token properties will also use a dollar sign prefix. This provides a consistent syntax across the spec.
- **token and group names MUST NOT begin with the `$` character**.

- While `$value` is the only required property for a token, a number of additional properties MAY be added
- $description
- $type
  - Design tokens always have an unambiguous type, so that tools can reliably interpret their value.
  - If the $type property is not set on a token, then the token's type MUST be determined
  - if none of the parent groups have a $type property, the token's type cannot be determined and the token MUST be considered invalid.
  - Tools MUST NOT attempt to guess the type of a token by inspecting the contents of its value.
  - The $type property can be set on different levels: at the group level, at the token level
- $extensions property is an object where tools MAY add proprietary, user-, team- or vendor-specific data to a design token.
  - When doing so, each tool MUST use a vendor-specific key whose value MAY be any valid JSON data.
  - Tools that process design token files MUST preserve any extension data they do not themselves understand.
  - The extensions section is not limited to vendors. All token users can add additional data in this section for their own purposes.
- More token properties TBC

- A file MAY contain many tokens and they MAY be nested arbitrarily in groups
  - The names of the groups leading to a given token (including that token's name) are that token's path, which is a computed property. 
- Because groupings are arbitrary, tools MUST NOT use them to infer the type or purpose of design tokens.
  - Groups items (i.e. the tokens and/or nested groups) are unordered.
  - tools that parse or write design token files are not required to preserve the source order of items in a group.
- Group keys without a dollar sign ($) prefix denote: token name or nested group name
- Groups MAY include an optional $type property so a type property does not need to be manually added to every token
  - If a group has a $type property it acts as a default type for any tokens within the group, including ones in nested groups, that do not explicitly declare a type via their own $type property. 
- Token names are not guaranteed to be unique within the same file. The same name can be used in different groups.
  - translation tools MAY need to export design tokens in a uniquely identifiable way

- tokens can reference the value of another token
  - This spec considers the terms "alias" and "reference" to be synonyms and uses them interchangeably.
- For a design token to reference another, its value MUST be a string containing the period-separated (.) path to the token it's referencing enclosed in curly brackets.
- Tools SHOULD preserve references and therefore only resolve them whenever the actual value needs to be retrieved.
- Aliases MAY reference other aliases. In this case, tools MUST follow each reference until they find a token with an explicit value. Circular references are not allowed.
- 🚨 The format editors are currently researching JSON Pointer syntax to inform the exact syntax for aliases in tokens

- This spec defines a number of design-focused types and every design token MUST use one of these types.
- A token's type can be set directly by giving it a $type property specifying the chosen type. 
  - Alternatively, it can inherit a type from one of its parent groups, or be an alias of a token that has the desired type.
- If no explicit type has been set for a token, tools MUST consider the token invalid and not attempt to infer any other type from the value.
- If an explicit type is set, but the value does not match the expected syntax then that token is invalid and an appropriate error SHOULD be displayed to the user. 
- color
  - Represents a 24bit RGB or 24+8bit RGBA color in the sRGB color space. 
  - The value MUST be a string containing a hex triplet/quartet including the preceding `#` character. 
  - **To support other color spaces, such as HSL, translation tools SHOULD convert color tokens to the equivalent value** as needed.
- dimension
  - Represents an amount of distance in a single dimension in the UI, such as a position, width, height, radius, or thickness. 
  - The value must be a string containing a number (either integer or floating-point) followed by either a "px" or "rem" unit (future spec iterations may add support for additional units). 
  - This includes 0 which also MUST be followed by either a "px" or "rem" unit.
- fontFamily
  - Represents a font name or an array of font names (ordered from most to least preferred).
  - The value MUST either be a string value containing a single font name or an array of strings, each being a single font name.
- fontWeight
  - The value must either be a number value in the range [1, 1000] or one of the pre-defined string values defined in the table below.
- duration
  - Represents the length of time in milliseconds an animation or animation cycle takes to complete
  -  The value MUST be a string containing a number (either integer or floating-point) followed by an "ms" unit
- cubicBezier
  - Represents how the value of an animated property progresses towards completion over the duration of an animation, effectively creating visual effects such as acceleration, deceleration, and bounce. 
  - The value MUST be an array containing four numbers. T
- number
  - Numbers can be positive, negative and have fractions.
  - Example uses for number tokens are gradient stop positions or unitless line heights.
  - The value MUST be a JSON number value.
- Additional types
  - Types still to be documented here are likely to include:
  - Font style: might be an enum of allowed values like ("normal", "italic"...)
  - Percentage/ratio: e.g. for opacity values, relative dimensions, aspect ratios, etc. Not 100% sure about this since these are really "just" numbers. 
  - File: for assets - might just be a relative file path / URL (or should we let people also express the mime-type?)

- Composite types
  - The types defined in the previous chapters such as color and dimension all have singular values. 
  - However, there are other aspects of UI designs that are a combination of multiple values. 
  - For instance, a shadow style is a combination of a color, X & Y offsets, a blur radius and a spread radius.
  - Shadow styles are therefore combinations of values that follow a pre-defined structure.
  - Types like this are called composite types.
- a composite type has the following characteristics:
  - Its value is an object or array, potentially containing nested objects or arrays, 
  - Sub-values may be explicit values (e.g. "#ff0000") or references to other design tokens that have sub-value's type (e.g. "{some.other.token}").
- **there is nothing special about composite tokens**. 
  - They can have all the other additional properties like $description or $extensions. They can also be referenced by other design tokens.
- groups and composite tokens might look very similar. 
- However, they are intended to solve different problems and therefore have some important differences:
- Groups are for arbitrarily grouping tokens for the purposes of naming and/or organization.
  - tools MUST NOT try to infer any special meaning or typing of tokens based on a group they happen to be in.
- Composite tokens are individual design tokens whose values are made up of several sub-values.
  - **Their `type` must be one of the composite types defined in this specification.**
  - Therefore their names and types of their sub-values are pre-defined. 
  - Adding additional sub-values or setting values that don't have the correct type make the composite token invalid.
- strokeStyle
  - Represents the style applied to lines or borders. 
- border
  - The value MUST be an object with the following properties
  - Does it need more sub-values to account for features like outset, border images, multiple borders, etc.
- transition
  - Represents a animated transition between two states. 
- shadow
  - Represents a shadow style. 
- gradient
  - Represents a color gradient.
  - Does it need to also specify the type of gradient (.e.g linear, radial, conical, etc.)?
- typography
  - Represents a typographic style. 
  - Should the lineHeight sub-value use a number value, dimension or a new lineHeight type?

## Adobe DSP

- ref
  - https://github.com/AdobeXD/design-system-package-dsp
  - https://github.com/demianborba/spectrum-dsp

- DSP is a new open-format folder-structure created to help teams share design system information across tools.
- A Design System Package (DSP) is a folder containing subfolders with assets and JSON files that represent design system information:
- `dsp.json`
  - This is the entry point for the Design System Package (DSP). It includes package info, settings, and imports.
- `/assets`
  - contains all the static assets included in the DSP, such as SVG or PNG files.
- `/data`
  - contains all of the data that comprises the DSP format. 
  - The folder has no required files. 
  - File examples are components.json, docs.json, fonts.json and tokens.json.
- `/dist`
  - contains platform-specific code generated by a build system
  - vscode extension has Style Dictionary as its build system. 
  - Examples of folders created by a build system are /android, /css and /styledictionary. 
  - Dist also contains non-platform-specific code such as the Style Dictionary input files and folders (config and properties).
- `/ext`
  - hold files written by third party tools.
  - Its subfolders must follow the reverse domain name convention of "com_partner_name"
# DTCG(Design Tokens Community Group)
- Design tokens are indivisible pieces of a design system such as colors, spacing, typography scale.
- The DTCG’s goal is to provide standards upon which products and design tools can rely for sharing stylistic pieces of a design system at scale.

- https://github.com/design-tokens/community-group
  - https://twitter.com/DesignTokens
  - https://github.com/design-tokens/community-group/tree/example-token-files
    - 官网的例子基于theo实现
  - The DTCG was founded in June 2019. 
  - 松散的组织很难统一制定标准和推广标准，从19年到21年连个文档都没写出来
  - 更推荐参考大公司和知名项目的选择，如amazon的style-dictionary

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

```typescript
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

```JSON
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

```js
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
# [Universal Design Tokens (UDT) Specification](https://github.com/universal-design-tokens/udt/blob/master/packages/spec/docs/README.md)
- ref
  - https://udt.design/
  - 更新于201906

```JSON

{
  "$schema": "http://udt.design/schemas/dev/udt-schema.json",
  "tokens": [
    {
      "name": "Token A",
      "type": "color",
      "value": "@token-b"
    },
    {
      "name": "Token B",
      "id": "token-b",
      "type": "color",
      "value": "#123456"
    }
  ]
}
```

# Open UI
- open ui相对于dtcg的特点
  - 重点是通用ui组件的样式与交互规范，而dtcg重点是通用样式变量
  - 重点是帮助开发者和设计师互操作，而dtcg重点是各类设计工具的互操作

- The web deserves interoperability between component frameworks and design systems.
  - The UI community should standardize namings and structures for common components. 
  - We should also standardize a way of theming these components. 
  - We should set a path for existing solutions to converge and for browsers to natively provide these things in the future.

- ref
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

- [Component and token naming in Design Systems](https://medium.com/@NateBaldwin/component-and-token-naming-in-design-systems-366bad54843f)
- It’s perfectly fine for all of these unique class names to exist in a design system’s component ecosystem:
  - QuickActions, quickActions, quick-actions
  - “Wait, how do we know whether to use the QuickActions, quickActions, or the quick-actions?”
  - Nobody, ever
- What is problematic is when each library gives the same component a different name. 
    - For instance, if one team decided the Quick Actions component should be called Action Buttons.
- Another point to mention is that your component libraries are not necessarily going to be the very first to deliver a reusable set of components to your engineering team
  - In order to differentiate between components, a rationale solution is to prefix all component names, such as myDSButton.
- Summary
  - There’s no hard-and-fast rules or best practices for a single, system-wide naming convention or standard. 
  - What’s important is the various resources of your system are consistent in spirit
  - 没有统一标准，那就参考大公司或主流项目的规则

- [Design Tokens: How to use them effectively](https://uxdesign.cc/design-tokens-how-to-use-them-effectively-d495ff05cbbf)
- Types of Design Tokens
  - Global Token
  - Alias Token
  - Component-specific token
- We here pulled data from the Figma API. 
  - what we did was placed our base.json file created into our src.
  -  Styled Dictionary will help us to convert our token data which are base colors, typography, spaces, box shadow etc. in a single JSON file to design tokens.
- DT are the central source of truth for our tiny UI information to store
