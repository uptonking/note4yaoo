---
title: note-ux-design-system
tags: [design, ux]
created: '2020-10-03T15:32:13.983Z'
modified: '2020-10-03T15:33:01.333Z'
---

# note-ux-design-system

## design-system-overview

- A design system is a collection of documentation on principles and best practices, that helps guide a team to build digital products.

- design system properties
  - Source code: Publically viewable source code
  - Components: Contains coded patterns and examples.
  - Designers Kit: Includes a Sketch/Photoshop/Figma etc. file for designers.
  - Voice & Tone: Provides guidance on how language should be used.
  - company
  - description
  - preview-image
  - docs-site-url
  - js-framework: react, vue, angular, web-comp
  - typescript
  - css-in-js
  - design-tokens
  - animation
  - design-principles
  - storybook
  - status: deprecated, active, inactive
  - other props
    - bundler
    - guidelines
    - color-palette
    - color-naming
    - contrast-analysis
    - typography
    - icons
    - grid/space
    - data-viz
    - accessibility
    - distribution

## design system tutorials

- https://www.learnstorybook.com/design-systems-for-developers/
  - how to transform component libraries into design systems
- https://www.uxpin.com/create-design-system-guide/create-ui-inventory-for-design-system
- [10 Best Design Systems and How to Learn (and Steal) From Them](https://designerup.co/blog/10-best-design-systems-and-how-to-learn-and-steal-from-them/)
  01. Google Material Design System
  02. Apple Human Interface Guidelines
  03. Microsoft Fluent Design System
  04. Atlassian Design System
  05. Uber Design System
  06. Shopify Design System
  07. IBM Carbon Design System
  08. Mailchimp Design System
  09. Salesforce Lightning Design System
  10. Helpscout Design System
- [creating themeable design systems_2018_Brad Frost](https://bradfrost.com/blog/post/creating-themeable-design-systems/)
  - TL; DR: Design systems + CSS Zen Garden = Awesome.
  - Each component in a design system contains its own structure, style, and behavior.
  - In my own design system work, I’ve found there’s often a finite number of ways to structure a component (with HTML) and make it interactive (with JavaScript), but the styling possibilities are seemingly endless.
  - we can create systems that allow for a lot of aesthetic flexibility while still retaining a shared underlying structural foundation.
  - So how do we actually go about creating design systems that can serve wildly different brands, audiences, and contexts?
  - From Salesforce’s Lightning Design System, which popularized the term “design tokens” in design systems
  - Design tokens move variables to a higher level, making it easier to manage brand attributes without diving deep into a codebase
  - First tier variables define the brand’s core attributes, serving as the raw materials for the UI’s visual design
  - The second tier takes the first-tier variables and starts applying them to high-level applications within the UI.
  - The third tier is component-specific variables, which are found in each component’s partial. 
  - We can now map the high-level application variables to specific components.
  - Atomic design is a methodology for creating thoughtful UI design systems: all of the vastness and complexity of our UI universe can be broken down into a finite set of atomic elements. 
  - Components are included inside of more complex components, which are in turn included inside even more complex components. 
  - This Russian-nesting-dolls approach to UI design systems helps teams thoughtfully create the whole experience and the parts of the whole at the same time.
  - Using the variable system described above, we can define the button atom‘s visual styles for 5 unique brands.
  - A molecule is a component made up of a handful of atoms. A card molecule is a common component that can house all sorts of different content.
  - An organism is a complex component that’s made up of atoms, molecules, or other organisms.
- [Atomic Design: Blowing Up What You Thought You Knew About Web Design](https://www.elegantthemes.com/blog/design/atomic-design)
  - interfaces are made up of components that can be categorized into building blocks
  - Atoms, Molecules, Organisms, Templates, Pages
