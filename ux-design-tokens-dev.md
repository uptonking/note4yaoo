---
title: ux-design-tokens-dev
tags: [design-system, design-tokens, ux]
created: '2020-12-31T20:07:19.497Z'
modified: '2021-01-01T20:09:10.218Z'
---

# ux-design-tokens-dev

## guide

- https://github.com/design-tokens/community-group
  - https://twitter.com/DesignTokens
  - The DTCG was founded in June 2019. 
  - The DTCG’s goal is to provide standards upon which products and design tools can rely for sharing stylistic pieces of a design system at scale.
  - [[RFC] Format specification](https://github.com/design-tokens/community-group/issues/1)
  - [[RFC] Theming](https://github.com/design-tokens/community-group/issues/2)

- design-tokens-awesome-catalog
  - 主流token工具及标准参考
    - system-ui-theme-specification
    - salesforce-theo-spec
    - style-dictionary-properties
    - airbnb-lona-spec
    - universal-design-tokens-schemas
  - https://github.com/sturobson/Awesome-Design-Tokens
    - A list of repos that contain a companies' Design Tokens

- design-tools
  - Figma
  - AdobeXD
  - Canva
  - 稿定设计

- https://github.com/system-ui/theme-specification
  - The theme object is intended to be a general purpose format for storing design system style values, scales, and/or design tokens.

- design-tokens-spec
  - [Airbnb Lona Component Definition](https://github.com/airbnb/Lona/blob/master/docs/file-formats/component.md)
    - Currently component data is encoded in JSON.
    - JSON is problematic because it's not easily mergeable or human-editable. 

## pieces

- Should I use theo or style dictionary?
  - 结论是，推荐使用json格式来描述design tokens
  - Both are good! Both have very active communities on the design systems slack. 
  - You can also create a custom one (Adobe did this). 
  - Theo uses `yaml` or `json` and takes a file-in file-out strategy. 
  - Style Dictionary uses `json` or `js` modules and merges all token files into 1 big object.

- Salesforce’s Design Tokens. Amazon’s Style Dictionary. Airbnb’s Style Expressions. Naming is hard.

- I figure a way to implement design tokens on @framer X using style-dictionary.
  - The output is a collection of CSS Variables and I was able to use them on CSS objects, with Styled components, and with Emotion.

## discuss

 

- ### Why is a design system conflated by so many with code components, where it can be actually expressed as lower level tokens?
- https://twitter.com/oleg008/status/1095652075705434112
  - Why would you want to make the source of truth so much more complex than identifiers of a color or a behavior?
  - Is it basically bc naming things is hard?
- TLDR from responses I see 2 valid points:
  1. Tokens are instructions, someone has yet to build a component properly.
  2. Tokens need to contain very detailed information about each component's property, which is hard because there are a lot of them
- This is going to become a lot more common. We're seeing advanced tools specifically for designing color.
  - we will have tools for shadow, spacing, type scale etc.
  - Export JSON and the engineers take it from here.

- ### You are a web developer. You get handed a design for a Website
- https://twitter.com/elibelly/status/1214591804034764801
  - For simplicity's sake, let's say it's a one-pager with all the trimmings (nav, footer, menu, content, a form, etc)
  - What are the first three things you do?
- eg
  1. Print it and identify the different "components of the page" by drawing around them on paper
  2. Check if there's any further design considerations to be had (responsiveness, error states...)
  3. Identify design tokens (colors, fonts...)
- eg
  4. Write all the semantic, accessible HTML as if CSS and JavaScript don't exist
  5. Parse the design for component patterns, common spacing values, colors, typography, states, alt text, accessible naming, etc.
  6. Begin styling and adding functionality with a design system mindset
- eg
  4. Take the time to look at the design and really comprehend it without doing anything else
  5. Make a judgment whether anything about this is going to require anything more than plain html/css/js 
  6. Make a time/effort estimate 

## ref

- [Documenting Design Tokens](https://dbanks.design/blog/documenting-design-tokens/)
