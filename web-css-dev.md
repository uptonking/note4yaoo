---
title: web-css-dev
tags: [css, web]
created: '2020-07-18T06:10:49.149Z'
modified: '2021-02-07T18:27:52.684Z'
---

# web-css-dev

# naming

## css-vars-naming

- ### [adobe spectrum css Class Naming Conventions](https://github.com/adobe/spectrum-css/wiki/Class-Naming-Conventions)
- Our naming convention is based on SUIT CSS
- In Spectrum, we have two sizing notions:
  - Scale
    - This is the overall size of all components on the page, 
    - it's either medium for desktop, or large for touch.
  - T-shirt size
    - This is the size of a specific component, basically a variant/modifier that resizes one instance of a component only. 
    - A component whose size is set with t-shirt sizing is still affected by scale.
- t-shirt size
  - 效果是用[postcss-remapvars](https://www.npmjs.com/package/postcss-remapvars)自动生成各组件各套size对应的css vars变量名
    - 会自动生成各主题类名下该组件级变量的新值，新值由全局级变量设置
    - 只有size主题通过此法实现，各颜色的主题直接通过设置变量新值实现
  - Traditionally, in CSS, we define modifier classes that change various properties of a given component.
  - this would mean that we would have 5 separate modifier classes (XS, S, M, L, XL) that each re-define the same set of properties.

``` CSS
.spectrum-Button {
  /* ... */
}

.spectrum-Button--sizeM {
  height: var(--spectrum-button-primary-m-height);
  border-radius: var(--spectrum-button-primary-m-border-radius);
}

.spectrum-Button--sizeL {
  height: var(--spectrum-button-primary-l-height);
  border-radius: var(--spectrum-button-primary-l-border-radius);
}
```

  - Using the magic of CSS custom properties and a few PostCSS plugins, we can ensure that ALL possible modified tokens for t-shirt sizing are automatically reflected in the CSS, with no manual effort outside of defining the modifier classes one time.
  - Spectrum Tokens provides all tokens for all t-shirt sizes of a given component, whether or not they change between sizes. 
  - Every variable is consistently named in this form:

``` CSS
/* --spectrum-COMPONENT-SIZE-VARIANT-PROPERTY-STATE */
--spectrum-button-m-primary-height: var(--spectrum-alias-item-height-m);
--spectrum-button-l-primary-height: var(--spectrum-alias-item-height-l);
```

  - Now, instead of directly referencing `--spectrum-button-m-primary-height` in the code, we'll actually drop the size and simply reference `--spectrum-button-primary-height`
  - We actually define that variable on the modifier class for the t-shirt size
  - As you can see, when you apply a t-shirt size class, the only thing that changes is the variables that drive the original class' properties. 
    - Instead of re-defining properties, we're re-defining variables! 
    - This means there's a single definition of the CSS height property for .spectrum-Button, not 5 (one for each t-shirt size).

``` CSS
.spectrum-Button {
  height: var(--spectrum-button-primary-height);
}

.spectrum-Button--sizeM {
  --spectrum-button-primary-height: var(--spectrum-button-primary-m-height);
}

.spectrum-Button--sizeL {
  --spectrum-button-primary-height: var(--spectrum-button-primary-l-height);
}
```

- That's nice, but how do we do this at scale?
  - That's where `@remapvars`(postcss-remapvars) comes in. 
  - Instead of manually writing out those `.spectrum-Button--size*` modifier classes, we generate them
- But there are like a thousand variables in there!
  - Right. Spectrum Tokens re-defines all possible variables, even color (which doesn't change between t-shirt sizes)! 
  - We really don't use all of those variables in our implementation, so we can start by filtering out color

- ### patternfly css
- [Patternfly 4 Guidelines](https://pf4.patternfly.org/guidelines/)
- PatternFly follows [Harry Robert's CSS Guidelines](https://cssguidelin.es/) with some exceptions, deviations and additions.
- PatternFly follows a two-layer theming system where global variables always inform component variables. 
- Global variables
  - The main reason to have global variables is to maintain consistency. 
  - `--pf-global--concept--PropertyCamelCase--modifier--state`.
    - a `concept` is something like a `spacer` or `main-title`.
    - a `PropertyCamelCase` is something like `BackgroundColor` or `FontSize`.
    - a `modifier` is something like `sm`, or `lg`.
    - a `state` is something like `hover`, or `expanded`.
  - They are concepts, never tied to an element or component. 
    - This is incorrect: `--pf-global--h1--FontSize`, 
    - this is correct: `--pf-global--FontSize--3xl`.
- Component variables
  - component custom properties allow for consistency across components, generates a common language between designers and developers, and gives granular control to authors.
  - `--pf-c-block[__element][--modifier][--state][--breakpoint][--pseudo-element]--PropertyCamelCase`
    - `--pf-c-block` refers to the block, usually the component or layout name (i.e., `--pf-c-alert`).
    - `__element` refers to the element inside of the block (i.e., `__title`).
    - `--modifier` refers to a modifier class such as .`pf-m-danger`, and is prefixed with `m-` in the component variable (i.e., `--m-danger`).
    - `--state` is something like `hover` or `active`.
    - `--breakpoint` is a media query breakpoint such as `sm` for `$pf-global--breakpoint--xs`.
    - `--pseudo-element` is one of either `before` or `after`.
  - The value of a component variable is always defined by a global variable.
  - It's possible to include multiple elements, modifiers, states, and breakpoints in a single component variable.
  - The order of elements, modifiers, states, and breakpoints in the variable name should match the selector order.

- Comment all magic values
  - If a situation arises where a value needs entering into the style sheets that isn't already defined in the global variables this should serve as a red flag to you.
  - In the case where a 'magic' value needs entering, ensure a comment is added on the line above to explain its relevance.

- PatternFly uses Sass to preprocess CSS.
  - As a general rule avoid Sass nesting to increase specificity. 
  - Try not to nest more than three layers deep.
  - Limit nesting to the following use cases:
    - Modifiers
    - Media queries
    - States, pseudo-classes, and pseudo-elements
    - Combinators
  - We create global Sass variables to keep a Bootstrap theme in sync. These values also inform our component level variables.
  - Since our components are isolated and modular, try to avoid @mixin and @extend because they generate a dependency.

- While the default styles applied to an element might not provide a visual indication of target area, the styles that display on hover should. 
  - To ensure that these styles accurately convey the target area of an element where the user can click, :hover styles should be applied to the clickable element of a component, and not to a larger wrapping element.

- 对于dark主题的button，因为按本项目的约定，组件级变量名会是唯一的，
  - 所以实现暗主题其实不需要`.pf-t-dark .pf-c-button{--pf-c-button--m-primary--Color: var(--pf-global--primary-color--dark-100);}`，
  - 直接将组件级变量的新值写在`.pf-t-dark{--pf-c-button--m-primary--Color:var(--pf-global--primary-color--dark-100);}`也是可以的

## [BEM](https://en.bem.info/methodology/quick-start//)

- ### Block
  - A functionally independent page component that can be reused. 
  - In HTML, blocks are represented by the class attribute.
- The block name describes its purpose ("What is it?" — menu or button), not its state ("What does it look like?" — red or big).
- The block shouldn't influence its environment, meaning you shouldn't set the external geometry (margin) or positioning for the block.
- You also shouldn't use CSS tag or ID selectors when using BEM.
- Blocks can be nested in each other.
- You can have any number of nesting levels.

- ### Element
  - A composite part of a block that can't be used separately from it.
- The element name describes its purpose ("What is this?" — item, text, etc.), not its state ("What type, or what does it look like?" — red, big, etc.).
- The structure of an element's full name is `block-name__element-name`. 
  - The element name is separated from the block name with a double underscore
- Elements can be nested inside each other.
- You can have any number of nesting levels.
- An element is always part of a block, not another element. 
  - This means that element names can't define a hierarchy such as `block__elem1__elem2`.
  - The block name defines the namespace, which guarantees that the elements are dependent on the block (block__elem).
- An element is an optional block component. Not all blocks have elements.
- Should I create a block or an element?
  - Create a block If a section of code might be reused and it doesn't depend on other page components being implemented.
  - Create an element If a section of code can't be used separately without the parent entity (the block).
  - The exception is elements that must be divided into smaller parts – subelements – in order to simplify development. 
    - In the BEM methodology, you can't create elements of elements. 
    - In a case like this, instead of creating an element, you need to create a service block.

- ### Modifier
  - An entity that defines the appearance, state, or behavior of a block or element.
  - The modifier name describes its appearance, its state and its behavior
  - The modifier name is separated from the block or element name by a single underscore
- Types of modifiers
  - Boolean
    - Used when only the presence or absence of the modifier is important, and its value is irrelevant. For example, disabled. If a Boolean modifier is present, its value is assumed to be true.
    - The structure of the modifier's full name follows the pattern:
    - `block-name_modifier-name`
    - `block-name__element-name_modifier-name`
  - Key-value
    - Used when the modifier value is important. For example, menu_theme_islands
    - The structure of the modifier's full name follows the pattern:
    - `block-name_modifier-name_modifier-value`
    - `block-name__element-name_modifier-name_modifier-value`
- A modifier can't be used alone

- ### File structure
  - A single block corresponds to a single directory.
  - The block and the directory have the same name. 
  - Names of element directories begin with a double underscore
  - Names of modifier directories begin with a single underscore
  - Implementations of elements and modifiers are divided into separate technology files.
    - For example, header__input.js and header_theme_islands.css.
  - You aren't required to follow the recommended file structure
  - You can use any alternative project structure that follows the BEM principles for organizing the file structure, such as Flat, Flex

## [SUIT CSS naming conventions](https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md)

- Utilities can be applied directly to any element within a component.
  - `u-[sm-|md-|lg-]<utilityName>`

- Variables
  - Variables used in components should have a flat structure after their namespace.
  - `--ComponentName[-element/descendant|--modifier][-onState]-(cssProperty|variableName)`

``` CSS
:root {
  --ComponentName-backgroundColor --ComponentName-descendant-backgroundColor --ComponentName--modifier-backgroundColor --ComponentName-onHover-backgroundColor --ComponentName-descendant-onHover-backgroundColor
}
```

- Non-component variables must be written in camel case.
  - For shared use, they should be authored in a `theme.css` file

``` CSS
:root {
  --fontSize: 16px;
  --fontFamily: sans-serif;
  --lineHeight: 1.4;

  --spaceSmall: 10px;
  --spaceMedium: 15px;
  --spaceLarge: 20px;
}
```
