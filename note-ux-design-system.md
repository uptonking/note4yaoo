---
title: note-ux-design-system
tags: [design, design-system, ux]
created: '2020-10-03T15:32:13.983Z'
modified: '2020-12-29T16:19:03.703Z'
---

# note-ux-design-system

- A design system is a collection of documentation on principles and best practices, that helps guide a team to build digital products.

## guide

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

## pieces

## discuss

- ### In our design system, we have 2 different space scales:
  - https://twitter.com/markdalgleish/status/1280029511807983617
    - Between UI elements (e.g. within a `<Stack>`)
    - Between wrapping lines of text (implicit in the relationship between font size and line height)
    - Change one, you have to manually adjust the other.
  - We shouldn’t use `line-height` at all, 
    - we should have line spacing (the distance between to `x-height` lines and block spacing (the distance between two sibling block elements), 
    - with block spacing derived from the larger line spacing of the two blocks (but still overwritable)
    - That’s not ideal from a typography perspective, but neither is what we have now 
    - and at least this way it would always be clear where spacing is coming from and how to adjust it to an exact value without having to do math
    - `x-height` is not used in all writing systems, so this is a tricky one. All solutions might need to be locale aware
  - I've found the best way to handle it is to set both based on the same baseline value. So like, 4dp or 8dp.
    - The scales can have different values, but it works if they're all based off the same baseline value.
    - Or polyfill line-height-step (and send me the link if you do!)
    - When you say "change one", what would you be changing? You mean changing the actual space scale?
      - Yeah, but more likely is that you're changing your typography.
    - The only solution I've seen for type setting issues is line-height-step
  - Can you hoist them into custom properties and calcs? 
    - my hunch(直觉，预感) is that you should have a single space scale that's derived from your typographical scale. 
    - The space between lines and the space between UI elements both come from a single design decision.
    - Building systems for system's sake, huh?
      - In my experience, only one out of ten designers are actually designing UI all based on typographic baselines, 
      - and eventually they move on from their print layout practises and accept that it's impossible to enforce baselines on the web.
    - What I'm aiming for is a component system that follows the baseline grid for you automatically, and we're having a lot of success with it.
  - Material UI uses a `gutterBottom` prop to add same space below an typography element element.  
    - Don't know if that would be better than adding Stack between multiple texts

## ref

- https://www.learnstorybook.com/design-systems-for-developers/
  - how to transform component libraries into design systems
- https://www.uxpin.com/create-design-system-guide/create-ui-inventory-for-design-system
- [Pattern Lab](https://patternlab.io/) /inactive
  - Pattern Lab is a frontend workshop environment that helps you build, view, test, and showcase your design system's UI components.
  - https://github.com/pattern-lab/patternlab-node
    - The Node version of Pattern Lab
