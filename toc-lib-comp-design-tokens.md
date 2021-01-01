---
title: toc-lib-comp-design-tokens
tags: [design-system, design-tokens]
created: '2020-10-23T03:56:35.731Z'
modified: '2020-11-13T07:30:23.361Z'
---

# toc-lib-comp-design-tokens

## design-tokens-popular

- https://github.com/Shopify/polaris-tokens
  - /150Star/MIT/202012/theo
  - https://polaris-tokens.herokuapp.com/
  - Design tokens for Polaris, Shopify’s design system
- https://github.com/salesforce-ux/design-system/tree/master/design-tokens
  - https://www.lightningdesignsystem.com/design-tokens/
  - Using the Lightning Design System markup and CSS framework results in UIs that reflect the Salesforce Lightning look and feel.
- https://github.com/opentable/design-tokens
  - https://opentable.github.io/design-tokens/
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
  - https://rei.github.io/rei-cedar-docs/tokens/all-tokens/
  - Tokens for cedar design system
  - We follow the basic structure of style-dictionary with the exception being that our tokens don't follow the implicit `category-type-item` structure 
    - and we abstract that into a separate `category` key
- https://github.com/sproutsocial/seeds-packets
  - https://seeds.sproutsocial.com/resources/tokens/
  - the design tokens that power Sprout Social's design system
- https://github.com/thumbtack/thumbprint-tokens
  - https://thumbprint.design/tokens/scss/
  - Thumbprint Tokens are published as JavaScript, SCSS, Swift, and Kotlin.

## design-tokens-examples

- https://github.com/kaelig/google-spreadsheets-theo-demo
  - Design tokens, managed via Google Spreadsheets, generated using Theo
  - todo 使用腾讯文档管理design tokens
- https://github.com/dbanksdesign/style-dictionary-google-sheets
  - This example is based on the google-spreadsheet-theo example
  - You write your design tokens in a Google spreadsheet and then this will take that it and put it into Style Dictionary 

 

- https://github.com/component-driven/react-design-tokens
  - React components to document design tokens in a styleguide

- more
  - [Figmagic — Design System template 4.0](https://www.figma.com/community/file/821094451476848226)

## style-dictionary

- https://github.com/amzn/style-dictionary
  - /1.3kStar/Apache2/202010
  - 支持编译输出ios的.h文件、android的.xml文件、.scss文件
  - 优点在于属性值能够方便地以cascade层次覆盖
  - use design tokens to define styles once and use those styles on any platform or language. 
  - A style dictionary is a collection of style properties, key/value pairs that describe stylistic attributes like colors, sizes
  - A style dictionary defines these style properties in JSON files, and can also include static assets like images and fonts.
  - https://amzn.github.io/style-dictionary/#/architecture
  - [feat: add support for !default in SCSS variables format](https://github.com/amzn/style-dictionary/pull/359)
  - [can't generate css variables to a specific class_202007](https://github.com/amzn/style-dictionary/issues/448)
    - You could write a custom format that does this too if you can't wait for that change to be made into the core library

 

- https://github.com/bem/themekit
  - /42Star/MPL2/202011
  - Themkit is a build system for design-tokens for any platform. 
  - This system is based on style-dictionary API and redefinition levels, which allows you to describe platform-specific values. 
  - Clear format (json or yaml) for developers and designers.
  - Define tokens once and get result for any format, for example js, css or json.
  - Every part of the theme or some of the tokens is extendable and overridable.
- https://github.com/jakobw/style-dictionary-format-json-schema
  - Generating a JSON schema describing the structure of your Style Dictionary files and including all style property names makes it possible for text editors to provide you with autocompletion. 
- https://github.com/demianborba/spectrum-dsp
  - Adobe Spectrum Design System Package (DSP) beta, including design tokens, typography collections of tokens and components with Spectrum React code snippets.
  - Please use the Adobe XD extension for VS Code to open this and other DSP
- https://github.com/lukasoppermann/design-tokens
  - Figma plugin to export design tokens to json in an amazon style dictionary compatible format.

 

- https://github.com/AlaskaAirlines/AuroDesignTokens
  - Abstract UI atomic values to support the Auro Design System.
  - 未实现theming
- [Fluid Design System Design Tokens](https://www.engie.design/fluid-design-system/design-tokens/)
  - We introduce Design Tokens thanks to style-dictionary.
  - Variable naming convention follows CTI (Category / Type / Item) structure.
  - CSS4 variable tokens, 
  - JSON tokens, CSS4 variable SASS support, FIGMA tokens
- https://github.com/didoo/style-dictionary-demo
  - demonstration of a (possible) setup of Style Dictionary for the generation of design tokens. 
  - It's been created as a companion to a Medium article that I have written to share my experience in setting up Style Dictionary for our Cosmos Design System in Badoo.
  - https://github.com/exanic/cosmos-style-dictionary
    - This example code is bare-bones to show you what this framework can do. 
- https://github.com/karlyanelson/style-dictionary-demo
  - This example code is bare-bones to show you what this framework can do.
- https://github.com/ivandata/another-way-to-create-themes
  - Code example for [Another way to create themes](https://imalov.dev/articles/another-way-to-create-themes/) article.

- more-tokens-repos
  - https://github.com/natura-cosmeticos/natds-commons/tree/master/packages/natds-themes

- more-tokens-npm
  - https://www.npmjs.com/package/@mozaic-ds/tokens
  - https://www.npmjs.com/package/@inmotionnow/momentum-tokens
  - https://www.npmjs.com/package/@tiendanube/design-tokens-nimbus

## design-tokens-tools

- https://github.com/salesforce-ux/theo
  - /1.5kStar/BSD/201810
  - 支持编译输出scss, less, styl, js, html, json, xml, Custom Format (function)
  - Theo can consume the centralized Design Tokens and output files for each platform.
  - A Design Token file is written in either JSON (JSON5 supported) or YAML and should conform to the spec
- https://github.com/diez/diez
  - /829Star/AGPLv3/202008
  - Write & maintain styles in one place, then compile & consume them everywhere
  - Diez supports any UI component library or codebase written in Swift, Objective-C, Kotlin, Java, TypeScript, JavaScript/JSON, CSS, or SCSS.
  - Diez's toolkit comes in four parts:
    - Compiler — converts (transpiles) TypeScript tokens into native packages for iOS, Android, and Web.
    - Framework — a library of common design token patterns
    - Extractors — automate the retrieval of design tokens from Figma, Sketch, Adobe XD, and InVision DSM
    - Documentation Generator — build customizable static HTML docs from any Diez project, complete with markdown-rendered code comments. 
- https://github.com/airbnb/Lona
  - /7.3kStar/MIT/202010
  - Lona is a collection of tools for building design systems and using them to generate cross-platform UI code, Sketch files, and other artifacts.
  - Lona consists primarily of 3 parts:
    - Lona Components - A data format, .component, for cross-platform components
    - Lona Studio - A GUI tool for designing .component files
    - Lona Compiler - A CLI tool & API for generating UI code from .component files
  - The Lona Compiler converts .component files to UI code for various targets.
    - iOS / macOS (Swift); 
    - React DOM / React Native / React Sketchapp (JavaScript)
    - Android (Kotlin)
  - A design system is defined in JSON as a collection of:
    - Components (can be nested)
    - Colors, Text Styles, Gradients, and Shadows
    - Data Types
  - https://github.com/airbnb/Lona/blob/master/docs/file-formats
- https://github.com/universal-design-tokens/udt
  - /80Star/ISC/202005
  - open-standard file format for expressing design token data.
- https://github.com/ui-js/chromatic
  - A tool to help manage design systems by generating platform-specific files from a source file describing design tokens.
  - From a single token file, generate platform specific artifacts: 
    - for the web (Sass, CSS)
    - for iOS (JSON, plist)
    - for Android (XML)
- https://github.com/mrmartineau/design-system-utils
  - /444Star/MIT/201911
  - a micro framework that standardises your design-system tokens & provides helpful utility functions to access the information. 
  - It can be used with styled-components, emotion, glamorous or any other CSS-in-JS framework.

- https://github.com/mikaelvesavuori/figmagic
  - Generate design tokens, export graphics, and extract design token-driven React components from your Figma documents. 
  - Originally inspired by Salesforce Theo.
  - Figmagic requires that your document structure is identical to what I show in the template
  - [Figmagic — Design System template 4.0](https://www.figma.com/community/file/821094451476848226)
  - https://github.com/B3nnyL/figgo
    - A cli tool makes your Figma and local design token stay in sync
  - https://github.com/mikaelvesavuori/figmagic-example
    - Using Figmagic with Webpack 4, React 16, Styled Components.
