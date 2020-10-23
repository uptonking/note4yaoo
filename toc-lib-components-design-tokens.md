---
title: toc-lib-components-design-tokens
tags: [design-tokens]
created: '2020-10-23T03:56:35.731Z'
modified: '2020-10-23T03:57:36.637Z'
---

# toc-lib-components-design-tokens

## guide

- design-tokens-awesome-catalog
  - 主流token工具及标准参考
    - system-ui-theme-specification
    - salesforce-theo-spec
    - style-dictionary-properties
    - airbnb-lona-spec
    - universal-design-tokens-schemas
  - https://github.com/sturobson/Awesome-Design-Tokens
    - A list of repos that contain a companies' Design Tokens

- https://github.com/design-tokens/community-group
  - The DTCG was founded in June 2019. 
  - Design tokens are indivisible pieces of a design system such as colors, spacing, typography scale.
  - The DTCG’s goal is to provide standards upon which products and design tools can rely for sharing stylistic pieces of a design system at scale.
  - [[RFC] Format specification](https://github.com/design-tokens/community-group/issues/1)
  - [[RFC] Theming](https://github.com/design-tokens/community-group/issues/2)

- https://github.com/system-ui/theme-specification
  - The theme object is intended to be a general purpose format for storing design system style values, scales, and/or design tokens.

- design-tokens-spec
  - https://github.com/airbnb/Lona/blob/master/docs/file-formats/README.md
  - https://github.com/airbnb/Lona/blob/master/docs/file-formats/component.md

## design-tokens-examples

- https://github.com/Shopify/polaris-tokens
  - Design tokens for Polaris, Shopify’s design system
- https://github.com/salesforce-ux/design-system/tree/master/design-tokens
  - Using the Lightning Design System markup and CSS framework results in UIs that reflect the Salesforce Lightning look and feel.
- https://github.com/opentable/design-tokens
  - A place where OpenTable engineers and designers openly work together
  - store shared design attributes such as colors, fonts, widths, animations, etc.
- https://github.com/kiwicom/orbit-design-tokens
  - We use design tokens instead of static values like HEX codes for color or sizing units.
- https://github.com/mineral-ui/mineral-ui/tree/master/packages/mineral-ui-tokens
  - This package uses Theo to generate output in a variety of formats.
- https://github.com/FirefoxUX/design-tokens
  - A design token is an abstraction of a visual property such as color, font, width, animation, etc. 
  - These raw values are language application agnostic and once transformed and formatted can be used on any platform.
- https://github.com/infor-design/design-system/tree/master/design-tokens
  - Design tokens are metadata about a visual design system.
- https://github.com/envato/foundation-design-system-tokens
  - Design Tokens for the Foundation Design System
- https://github.com/Skyscanner/backpack/tree/master/packages/bpk-tokens
  - Design tokens for colours, spacing, font, etc.
- https://github.com/buildit/gravity-particles
  - The "single source of truth" for design tokens and assets used throughout Buildit's Gravity design system
- https://github.com/rei/rei-cedar-tokens
  - Tokens for cedar design system

## design-tokens-tools

- https://github.com/amzn/style-dictionary
  - /1.3kStar/Apache2/202010
  - use design tokens to define styles once and use those styles on any platform or language. 
  - A style dictionary is a collection of style properties, key/value pairs that describe stylistic attributes like colors, sizes
  - A style dictionary defines these style properties in JSON files, and can also include static assets like images and fonts.
- https://github.com/salesforce-ux/theo
  - /1.5kStar/BSD/201810
  - Theo can consume the centralized Design Tokens and output files for each platform.
  - A Design Token file is written in either JSON (JSON5 supported) or YAML and should conform to the spec
- https://github.com/airbnb/Lona
  - /7.3kStar/MIT/202010
  - A design system is defined in JSON as a collection of:
    - Components (can be nested)
    - Colors, Text Styles, Gradients, and Shadows
    - Data Types
- https://github.com/yarastqt/themekit
  - /20Star/MPL2/202009
  - This system is based on style-dictionary API and redefinition levels
  - allows you to collect tokens for a specific platform such as desktop or touch, by default tokens included only from common platform.
- https://github.com/diez/diez
  - /829Star/AGPLv3/202008
  - Write & maintain styles in one place, then compile & consume them everywhere
  - Diez supports any UI component library or codebase written in Swift, Objective-C, Kotlin, Java, TypeScript, JavaScript/JSON, CSS, or SCSS.
  - Diez's toolkit comes in four parts:
    - Compiler — converts (transpiles) TypeScript tokens into native packages for iOS, Android, and Web.
    - Framework — a library of common design token patterns
    - Extractors — automate the retrieval of design tokens from Figma, Sketch, Adobe XD, and InVision DSM
    - Documentation Generator — build customizable static HTML docs from any Diez project, complete with markdown-rendered code comments. 
- https://github.com/ui-js/chromatic
  - A tool to help manage design systems by generating platform-specific files from a source file describing design tokens.
  - From a single token file, generate platform specific artifacts: 
    - for the web (Sass, CSS)
    - for iOS (JSON, plist)
    - for Android (XML)
- https://github.com/universal-design-tokens/udt
  - an open-standard file format for expressing design token data.
