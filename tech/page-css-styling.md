---
title: page-css-styling
tags: [blog, css, styling]
created: 2020-12-26T20:35:14.808Z
modified: 2021-01-19T10:58:58.943Z
---

# page-css-styling

# css-styling

## [Why We Don't Use a CSS Framework](https://www.infoq.com/news/2020/06/css-variables-design-systems/)

- Tolinski demonstrated how developers who do not need to support IE11 can leverage CSS variables to implement a custom design system with characteristically less overhead than a framework.
- The variable can be updated either via CSS or JavaScript. 
  - When such an update occurs, all dependent variables will be updated reactively. 
- CSS variables are scoped to the element(s) they are declared on and participate in the cascade.
- Tolinski reduced a design system to key components that make the design unique: color, type, spacing, characters, elevation, and elements (e.g. cards or accordions).
- Always use variables for any color, typography, spacing, 
  - and your entire site can be updated or configured in one fell swoop.
  - Don’t worry about creating unique components if they are all using custom properties.

## [Margin considered harmful](https://mxstbr.com/thoughts/margin/)

- Margin breaks component encapsulation with side effect. 
  - A well-built component should not affect anything outside itself.
- Margin makes reusability harder. 
  - Good components are usable in any context or layout.
- Margin conflicts with how designers think. 
  - Designers think about space in relation and context. 
  - They define how far a component should be from another component in a specific instance.
- By banning margin from all components you have to build more reusable and encapsulated components.
- Instead of margin I have started using spacer components, which move the responsibility of managing space to the parent-level.
  - Spacer components (such as Stack above) can restrict spacing values to steps on a scale. 
    - That way, all spacing automatically aligns to the grid.
  - Spacer components define how far a component should be from another component in a specific instance.
    - You have to define space in relation and context.

## [Margins and Composability in CSS](https://giuseppegurgone.com/margins-and-composability-in-css/)

- Composability is about making the pieces play nicely together.
- CSS Rules that affect composability compare to Lego studs: 
  - they let us assemble components in various combinations to satisfy specific user requirements.
- UI components are laid out and spaced in different ways to adapt to the context of the current view.
- In this game margins play a big role.
- Composability in CSS is ruled by margin among other things.
- Margins are often global and set to arbitrary standard values at the beginning of a project.
- There are some things to keep in mind when building UI components or a pattern library: 
  - Context and default margins
  - Margin direction

- When defining base styles or building a new component, it is hard to know in advance where UI components are going to be used.
- The effect of globals is unpredictable — this is a gotcha in JavaScript world, 
  - yet many CSS developers don’t want to accept the fact that this is true for styles too.
- UI components instead should be self-contained. 
- The **component root should be free of any rule that may affect composability**, specifically:
  - margins
  - layout rules like position (absolute/fixed), float, transform, etc
  - width
- We can then use higher-order components or utilities to fit the component into a specific context.

- The margin direction of child elements can also affect composability.
  - By choosing a single direction the effect of margins is more predictable and there are fewer side effects.
  - However child elements can still affect the surrounding components
- My suggestion is to always reset peripheral(次要的，辅助的；外围的，周围的) margins and to not set margins on the component root at all.

``` CSS
.list {
  margin: 0;
}

.list__item {
  margin-bottom: 2em;
}

.list__item:last-child {
  margin-bottom: 0;
}
```

- An improvement is to always use `margin-top` and `margin-left` and reset the `:first-child` instead.
- This is no different from resetting the `:last-child` except for the fact that the `:first-child` pseudo-class is supported by legacy browsers as well.
