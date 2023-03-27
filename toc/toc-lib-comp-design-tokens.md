---
title: toc-lib-comp-design-tokens
tags: [design-system, design-tokens, toc]
created: 2020-10-23T03:56:35.731Z
modified: 2021-01-01T22:09:59.545Z
---

# toc-lib-comp-design-tokens
- 设计样式时theming可参考
  - material, bootstrap, flat/metro, neumorphism, monochrome

## w3c-design-token

- https://github.com/drwpow/cobalt-ui
  - https://cobalt-ui.pages.dev/
  - Cobalt turns your W3C design tokens into code
  - The general approach is similar to Style Dictionary or Universal Design Tokens to solve the problem of creating a single source of truth for design tokens that is platform-agnostic and easy to build tooling for.
  - https://github.com/LiamMartens/w3c-design-tokens-lib

- https://github.com/lukasoppermann/style-dictionary-utils
  - a collection of parsers, filters, transformers and formats for Style Dictionary that make working with w3c design tokens a lot easier.
# style-dictionary-examples
- https://github.com/infor-design/design-system
  - https://design.infor.com/code/ids-enterprise/latest
  - including design tokens, which are design metadata, and basic tools like Sketch files and icons.
  - 实现了theming，每个主题最后输出成1个大css文件，全是css变量，全局变量有前缀，组件级变量无前缀
- [Fluid Design System Design Tokens Intro](https://www.engie.design/fluid-design-system/design-tokens/)
  - We introduce Design Tokens thanks to style-dictionary.
  - Variable naming convention follows CTI (Category/Type/Item) structure.
  - CSS4 variable tokens, 
  - JSON tokens, CSS4 variable SASS support, FIGMA tokens
- https://github.com/AlaskaAirlines/AuroDesignTokens
  - https://auro.alaskaair.com/getting-started/developers/design-tokens
  - Abstract UI atomic values to support the Auro Design System.
  - 未实现theming，全是css变量，生成的变量有前缀
- https://github.com/rei/rei-cedar-tokens
  - https://rei.github.io/rei-cedar-tokens/
  - https://rei.github.io/rei-cedar-docs/tokens/all-tokens/
  - Tokens for cedar design system. 
  - 未实现theming，全是scss变量，生成的变量有前缀
  - We follow the basic structure of style-dictionary with the exception being that our tokens don't follow the implicit `category-type-item` structure
    - and we abstract that into a separate `category` key
- https://github.com/lyne-design-system/lyne-design-tokens
  - Design Tokens for Lyne Design System
  - token只有10个左右很少，样式输出根据模版web-scss.template, commonjs.template
  - https://github.com/lyne-design-system/lyne-components
    - based on standard compliant Web Components compiled by StencilJS
- https://github.com/didoo/style-dictionary-demo
  - demonstration of a (possible) setup of Style Dictionary for the generation of design tokens. 
  - It's been created as a companion to a Medium article that I have written to share my experience in setting up Style Dictionary for our Cosmos Design System in Badoo.
- https://github.com/ivandata/another-way-to-create-themes
  - 例子基于vue，但样式部分很清晰，s-d生成的全是sass变量
  - Code example for [Another way to create themes](https://imalov.dev/articles/another-way-to-create-themes/) article.

 

- https://github.com/growingio/gio-design-tokens
  - https://gio-design-tokens.vercel.app/
  - GrowingIO Design Tokens， 文档基于storybook

- more-tokens-repos
  - https://github.com/natura-cosmeticos/natds-commons/tree/master/packages/natds-themes

- more-tokens-npm
  - https://www.npmjs.com/package/@mozaic-ds/tokens
  - https://www.npmjs.com/package/@inmotionnow/momentum-tokens
  - https://www.npmjs.com/package/@tiendanube/design-tokens-nimbus

## style-dictionary-tools

- https://github.com/amzn/style-dictionary
  - /1.3kStar/Apache2/202010
  - 支持编译输出ios的.h文件、android的.xml文件、web的.scss文件
  - 优点在于属性值能够方便地以cascade层次覆盖
  - use design tokens to define styles once and use those styles on any platform or language. 

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
  - https://github.com/lukasoppermann/design-token-transformer
# theo-examples
- theo tokens文档展示的模版
  - 最新文档：polaris、schedio
  - 旧版文档：localiza、orbit、pagnet、siku、sparkpost-matchbox

- https://github.com/spartanbio/schedio-tokens
  - https://spartanbio.github.io/schedio-tokens/
  - https://polaris-tokens.herokuapp.com/
- https://github.com/SparkPost/design-tokens
  - https://sparkpost.github.io/design-tokens/
  - https://design.sparkpost.com/design/tokens/
  - https://github.com/SparkPost/matchbox/tree/main/packages/design-tokens
  - SparkPost's design system tokens
  - 新版和旧版实现，都使用了theo
- https://github.com/Pagnet/design-tokens
  - https://pagnet.github.io/design-tokens/
  - Design tokens for the Blu design system

 

- https://github.com/kiwicom/orbit-design-tokens
  - https://github.com/kiwicom/orbit/tree/master/packages/orbit-design-tokens
  - https://orbit.kiwi/design-tokens/
  - Design tokens store visual design attributes.
  - 属性名使用的是camelCase
- https://github.com/sikucss/siku
  - Siku’s CSS

- more-theo
  - https://github.com/guigonzalez/designtokens
  - https://github.com/voorhoede/deltares-design-tokens
  - https://github.com/inspark/inspark-design-system-web
  - https://github.com/ubergrape/grape-ds
  - https://github.com/wuerthcs/aurora-design-token
  - https://github.com/alanfernandesti/localiza-designtokens
# design-tokens-tools
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

- https://github.com/amzn/sketch-constructor
  - Read/write/manipulate Sketch files in Node without Sketch plugins!
  - 提供了示例 you can generate a Sketch file from a Style Dictionary. 
# ref
- Has anyone catalogued popular theme token systems where I can read about them? They are so similar AND unique.
- https://twitter.com/dbanksDesign/status/1341449787468439553
  - One has tokens like color & space; another has colors & spacing; another has colors & space.
  - I don’t imagine they can merge either, as that might be a breaking change.
  - Adobe probably has one of the most (if not the most) well-thought out and complex token structures in the game
  - For Style Dictionary, we created a built-in naming/structure we called a CTI structure (category, type, item). 
    - This is not an enforced structure in any way, but just a default we came up with
