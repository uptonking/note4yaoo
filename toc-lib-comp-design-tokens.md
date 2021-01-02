---
title: toc-lib-comp-design-tokens
tags: [design-system, design-tokens, toc]
created: '2020-10-23T03:56:35.731Z'
modified: '2021-01-01T22:09:59.545Z'
---

# toc-lib-comp-design-tokens

## style-dictionary

- https://github.com/amzn/style-dictionary
  - /1.3kStar/Apache2/202010
  - 支持编译输出ios的.h文件、android的.xml文件、.scss文件
  - 优点在于属性值能够方便地以cascade层次覆盖
  - use design tokens to define styles once and use those styles on any platform or language. 
  - A style dictionary is a collection of style properties, key/value pairs that describe stylistic attributes like colors, sizes
  - A style dictionary defines these style properties in JSON files, and can also include static assets like images and fonts.
  - https://amzn.github.io/style-dictionary/#/architecture
  - [can't generate css variables to a specific class_202007](https://github.com/amzn/style-dictionary/issues/448)
    - You could write a custom format that does this too if you can't wait for that change to be made into the core library
  - [Discussion: outputting files 1:1](https://github.com/amzn/style-dictionary/issues/251)
    - Because of the way Style Dictionary works, by merging all source token files together first, there is no easy way to have a 1-to-1 mapping of source token file to build artifact. 
    - [feat(examples): add matching build files example](https://github.com/amzn/style-dictionary/pull/481)
      - example of automatically generating 1:1 token files based on a custom filter.
  - [Get ready for v3](https://amzn.github.io/style-dictionary/#/version_3)
    - Transitive transforms is the big one that required a big re-architecture of how the Style Dictionary build process works.
      - The new build process is similar, except that it recursively transforms and resolves aliases, only deferring a transform to the next cycle if the token has an unresolved alias. 
      - **Use cases this change opens up**:
      - Having variable references in outputs
      - Combining values like using HSL for colors
      - Modifying aliases like making a color lighter or darker
    - Custom parser support
      - The addition of custom parser support allows you to define your tokens in any language you like
    - Adding filePath and isSource entries on tokens (help with debugging.)
    - Typescript typings
    - Formats
      - Adding javascript/module-flat format that's just like the json/flat format, but exported as a cjs module
    - todo
      - Use ES6 where possible, Better log levels

 

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
