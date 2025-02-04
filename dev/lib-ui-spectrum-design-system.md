---
title: lib-ui-spectrum-design-system
tags: [adobe-spectrum, design-system, design-tokens, ui]
created: 2021-04-12T16:52:40.979Z
modified: 2021-04-12T18:07:11.417Z
---

# lib-ui-spectrum-design-system

# [Principles](https://spectrum.adobe.com/page/principles/)

- Our principles in action
  - For all platforms
    - both desktop and mobile
  - For everyone
    - from color and type to interaction and language 
  - Evolving and transparent
    - a list of open issues, and a design checklist
  - Built by a community

# [design-tokens](https://spectrum.adobe.com/page/design-tokens/)

- Design tokens are all the values needed to construct and maintain a design system — spacing, color, typography, object styles, animation, etc. — represented as data.

- Design token types
- Global tokens are the primitive values in our design language, represented by context-agnostic names. 
  - Our color palette, animation, typography, and dimension values are all recorded as global tokens. 
  - These can be directly used, and are inherited by all other token types.
- Alias tokens relate to a specific context or abstraction. 
  - Aliases help communicate the intended purpose of a token, and are effective when a value with a single intent will appear in multiple places.
- Component-specific tokens are an exhaustive representation of every value associated with a component. 
  - They often inherit from alias tokens, but are named in a way that allows engineering teams to be as specific as possible in applying tokens in component development.
- Usage guidelines
  - Use global tokens sparingly
  - Use aliases wherever they can apply
  - Use component-specific tokens for their respective component
