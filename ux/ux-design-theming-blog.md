---
title: ux-design-theming-blog
tags: [blog, design, theming]
created: 2020-12-29T18:00:51.271Z
modified: 2021-01-01T20:09:00.055Z
---

# ux-design-theming-blog

# theming with css vars

## [Theming With Variables: Globals and Locals_201803](https://css-tricks.com/theming-with-variables-globals-and-locals/)

- https://codepen.io/andresgalante/project/editor/DKPzvL

- Setting CSS variables to theme a design system can be tricky: 
  - if they are too scoped, the system will lose consistency. 
  - If they are too global, you lose granularity(细粒度).
- I’d like to try to boil design system variables down to two types: Global and Component variables. 
  - Global variables will give us consistency across components. 
  - Component variables will give us granularity and isolation. 
- I’ll be using CSS variables for this article but the concept applies to preprocessor variables as well.

- System-wide variables are general concepts defined to keep consistency across your components.
- we can define global `:root` vars and use them on the component

``` CSS
:root {
  --spacer-sm: .5rem;
  --spacer-md: 1rem;
  --spacer-lg: 2rem;
}

.btn {
  padding: var(--spacer-sm) var(--spacer-md);
}

.btn-rewrite {
  padding-left: 1rem;
  padding-right: 1rem;
}
```

- The main benefits of this approach(全局变量) are:
  - It achieves consistency since every component follows the same spacing.
  - It generates a single source of truth for spacers, and a single point for the author using our system to customize it.
  - It produces a common point of reference for designers and developers to work from. 
    - As long as the designers follow the same spacing restrictions, the translation to code is seamless.
- But it also presents a few problems:
  - The system loses modularity by generating a dependency tree.
    - Since components depend on global variables, they are no longer isolated.
  - It doesn’t allow authors to customize a single component without overwriting the CSS. 
    - For example, to change the padding of the alert without generating a system wide shift, they’d have to overwrite the alert component css 若要覆盖组件样式，需提供同名class来覆盖

- component variables are scoped to each module

``` CSS
.alert {
  --alert-color: #222;

  color: var(--alert-color);
  border-color: var(--alert-color);
}
```

- The main advantages are:
  - It creates a modular system with isolated components.
  - Authors get granular control over components without overwriting them. They’d just redefine the value of the variable.
- the problem
  - There is no way to keep consistency across components or to make a system wide change 

- ### The two-tier theming system
- The solution is a two-layer theming system where global variables always inform component variables
- **First tier: Global variables**(一般定义design tokens)
- The main reason to have global variables is to maintain consistency, and they adhere to these rules:
  - prefixed with the word `global` and follow the formula `--global--category--modifier--state--PropertyCamelCase`
  - They are concepts, never tied to an element or component
- **Second tier: Component variables**
- The second layer is scoped to theme-able component properties and follow these rules:
  - Assuming we are writing BEM, they follow this formula: `--block__element--modifier--state--PropertyCamelCase`
    - if you are not writing BEM class names the same principles apply, just replace the `block__element--modifier` with your `classname`
  - The value of component scoped variables is always defined by a global variable
  - A component variable always has a default value as a fallback in case the component doesn’t have the dependency on the global variables
- You’ll notice that we are defining locally-scoped variables with global variables.
  - This is key for the system to work since it allows authors to theme the system as a whole
  - On the other hand each component variable has a default value so a component can stand on its own, it doesn’t depend on anything and authors can use it in isolation.
- This setup allows for consistency across components, it generates a common language between designers and developers 
  - since we can set the same global variables in Sketch as bumpers for designers, and it gives granular control to authors.
- Why does this system work?
  - If we allow authors to easily theme the system without having to overwrite CSS, we’ll not only make their lives easier but also reduce the risk of breaking modules. 实现theming且不用覆盖类名
  - At the end of the day, a maintainable system is a good system.
  - The two-tier theming system generates modular and isolated components where authors have the possibility to customize them at a global and at a component level. 
- What values should became variables?
  - The more we allow authors in, the more vulnerable the system is to implementation issues.
  - To keep consistency, **set global variables for everything except layout values**; 
  - you wouldn’t want authors to break the layout.
  - And as a general rule, I’d recommend allowing access to components for everything you are willing to give support.
  - For the next version of PatternFly, we’ll allow customization for almost everything that’s not layout related: colors, spacer, typography treatment, shadows, etc.

- discussion
  - We use exactly this pattern for our design system’s component library, but in CSS-in-JS (glamorous, in our case) rather than CSS/Sass/BEM. 
    - It’s worked well for us, and our consumers have appreciated the flexibility of customization.
  - I don’t agree that local theme variables must reference a global theme variable, though. 
    - While the exception, there are cases where a local variable can just be a direct value in our system, and I’d imagine that’s a shared need.
  - I love this concept of CSS variables and theming but is there any way to use this or something similar or will I have to have fallbacks for IE 11 thereby defeating the purpose.

## [Theming with CSS variables: Two layers theming_201904](https://dev.to/wendell_adriel/theming-with-css-variables-1o56)

- If in our project we group all variables in a single place (Global Variables), we create a single source of truth, but we lose the ability to modularize our theme 
  - and always when a dev needs to customize a component, he will need to overwrite the CSS rules.
- if we leave the variables scattered all around, we will create a modularized theme, but we lose the consistency between our components 
  - and if we need to make a general change, we will have a lot of work.
- To solve this issue we will think about our theme having two layers, we will have the Global Variables and the Modules Variables. 
  - That way we can get the best of the two worlds.

- ### [Two layers theming](https://codepen.io/WendellAdriel/pen/QPxRjN)
- Global variables are generic variables that will be used to keep the consistency between all our components
  - Some examples of global variables are font, default font-size and color palette. 
  - It's super simple to define global variables on CSS, we use the `:root` selector
  - It's not mandatory, but to make it simple to identify that a variable is global or not, I like to use the `global-` prefix
  - If we need to change any of these values in the middle of our project, we just need to change the variables declaration with the new values and it's done! 
    - That way we can create some sort of consistency in our product and also create a common reference point for devs and designers to work together in a quick and easy way.

- Modules Variables
  - Modules Variables are variables with a restricted scope where it's defined.
  - Every module variable MUST be defined using the value from a global variable 
  - and we also need to provide a fallback value for the case that the module will be used in an environment that doesn't provide global variables
  - It's not mandatory, but to make it simple to identify that a variable is a module variable, I like to use the `module-` prefix

``` CSS
:root {
  /* ... */
  --global-border-radius-sm: 3px;
  --global-text-color-light: #fff;
}

.btn {
  --btn-border-radius: var(--global-border-radius-sm);
  --btn-text-color: var(--global-text-color-light);
  border-radius: var(--btn-border-radius, 5px);
  color: var(--btn-text-color, #ddd);
}

.btn-primary {
  --btn-primary-bg: var(--global-color-primary);
  --btn-primary-border: var(--global-color-primary);
  background-color: var(--btn-primary-bg, #605770);
  border-color: var(--btn-primary-bg, #605770);
}

.btn-secondary {
  --btn-secondary-bg: var(--global-color-secondary);
  --btn-secondart-border: var(--global-color-secondary);
  background-color: var(--btn-secondary-bg, #7fc29b);
  border-color: var(--btn-secondary-bg, #7fc29b);
}
```

- The way that we built our theme, we make independent modules, 
  - because if they are being used on a context where we have the global variables, they will inherit the values from these variables, 
  - but if it doesn't find these variables, we also defined fallback values that will be used.
- It also made that changes can be really easy to be done

- ### [Working with multiple CSS themes](https://codesandbox.io/s/working-with-multiple-css-themes-03-forked-0wxui)
- In this article, we will put this into practice creating some simple themes and seeing how to change between them.
- `:root` selector can be used to store the global variables of our themes. 
- There are some ways of working with themes, but my favorite is to use the `data-` attributes on HTML. 
  - These `data-` attributes are a convention used to define custom attributes for tags and to identify which theme we're using we will create a data-theme attribute. 
  - All the elements with this attribute and their children will be modified. 
- Since our elements are already using the variables that we created, to create a new theme we just need to update the values of the ones that we need to modify, 
  - that way the values that we change will overwrite the others 
  - and the ones we don't change will be inherited from the `:root` element.
- Letting the user switch themes
  - let's remove the `data-theme="dark"` attribute from our `<html>` tag and create the element that will let the user switch themes when clicked.
  - let's add the needed action(event handler) to make that our theme will switch when the element is clicked
  - make theme update in a smoother way using css transition rule 
  - we can use the localStorage to store theme info

``` CSS
/* default theme */
:root {
  --global-bg-color: #fff;
  --global-font-family: Verdana, sans-serif;
  --global-text-color: #222;
  --global-link-color: blue;
  --global-link-hover: lightblue;
}

/* dark theme */
html[data-theme='dark'] {
  --global-bg-color: #444;
  --global-text-color: #ddd;
  --global-link-color: yellow;
  --global-link-hover: lightyellow;
}
```

``` JS
document
  .getElementById("theme-toggle")
  .addEventListener("click", toggleTheme);

function toggleTheme() {
  const htmlTag = document.getElementsByTagName("html")[0]
  if (htmlTag.hasAttribute("data-theme")) {
    htmlTag.removeAttribute("data-theme")
    return
  }

  htmlTag.setAttribute("data-theme", "dark")
}
```

- we can also apply themes to specific zones in our app. 
  - let's apply that to some elements

## [Global and Component Style Settings with CSS Variables_202006](https://www.sarasoueidan.com/blog/style-settings-with-css-variables/)

- Firstly, I create a `_settings.scss` stylesheet. 
  - This stylesheet contains the global settings for the project. 
  - These settings are usually derived from the design style guide provided by the design team I’d be working with.
  - Just like the style guide contains settings for visual styles like colors, box shadow styles, font styles, type scales, etc., the `_settings` stylesheet contains variables that serve as the code equivalent of those settings, 
    - and that are used across the CSS to maintain visual consistency across the project.

- I organize my patterns so that each pattern lives in its own directory, containing the component’s HTML template, CSS, and vanilla JavaScript files, along with any additional Fractal(tool, like storybook)-specific assets (such as config files).
- My goal from creating this library is to create a tool that allows me to prototype faster, and that’s flexible and efficient enough to use across different projects. 
  - And since patterns are usually styled differently across my projects, I wanted a way to simplify the process of customizing or “configuring” them for each project. Enter CSS Variables.
- For each pattern, I’ve found myself modifying the same properties whenever I needed to use it — like the font, colors (text, background, border), box shadow, spacing, etc. 
  - So I figured it would be useful and time-saving if I created variables for those properties, define those variables in the ‘root’ of the component, and ‘pass in’ the values for these variables when I use the pattern as I need. 
  - This way I can customize or theme the component by changing the property values in one rule set, instead of having to jump between multiple ones to do so.
  - For each property, I set a default or empty value and change that value when I use the component in a new project as I need.
  - The rest of the rule sets for the select component contain fixed rules or styles that most likely won’t change across projects

## [ionic Dark Mode CodePen](https://ionicframework.com/docs/theming/dark-mode)

- 基于css vars实现theming的示例
  - https://codepen.io/uptonking/pen/YzGewVQ

``` JS
// ====== 根据media query自动切换theme ======
// Use matchMedia to check the user preference
const prefersDark = window.matchMedia('(prefers-color-scheme: dark)');

toggleDarkTheme(prefersDark.matches);

// Listen for changes to the prefers-color-scheme media query
prefersDark.addListener((mediaQuery) => toggleDarkTheme(mediaQuery.matches));

// Add or remove the "dark" class based on if the media query matches
function toggleDarkTheme(shouldAdd) {
  document.body.classList.toggle('dark', shouldAdd);
}

// ====== 手动切换theme ======
// Query for the toggle that is used to change between themes
const toggle = document.querySelector('#themeToggle');

// Listen for the toggle check/uncheck to toggle the dark class on the <body>
toggle.addEventListener('ionChange', (ev) => {
  document.body.classList.toggle('dark', ev.detail.checked);
});

const prefersDark = window.matchMedia('(prefers-color-scheme: dark)');

// Listen for changes to the prefers-color-scheme media query
prefersDark.addListener((e) => checkToggle(e.matches));

// Called when the app loads
function loadApp() {
  checkToggle(prefersDark.matches);
}

// Called by the media query to check/uncheck the toggle
function checkToggle(shouldCheck) {
  toggle.checked = shouldCheck;
}
```

# more-theming

## [Theming React Components with CSS Variables_202004](https://blog.bitsrc.io/theming-react-components-with-css-variables-ee52d1bb3d90)

- ### Methodology #1: Scope Custom CSS Props
- Definitions:
  - Theme: A CSS class with a set of custom CSS properties. 
    - The class serves as a way to scope sets of custom CSS properties. 
    - Sets of CSS custom properties are named the same across themes.
- Workflow:
  - All themeable CSS properties, for all components, will be defined as custom CSS properties (as opposed to constant values).
  - The `App` component will be the only component that has a theme className (e.g. `.dark-theme` ).
  - Changing themes will be done by replacing the `className` of the `App` component. All descendants of the `App` component will receive new custom CSS properties by inheritance.

``` CSS
.light-theme {
  --primary-color: #007bff;
  --disabled-color: #6c757d;
}

.dark-theme {
  --primary-color: #000000;
  --disabled-color: #4a4a4b;
}
```

- ### Methodology #2: Set CSS Custom Props
- Definitions:
  - Selected properties: CSS variables that are used directly as CSS properties to all themeable UI components. 当前值
  - Stored properties: CSS variables that are not used directly to style components but are used to store sets of values. 备用值
  - Theme: A set of stored properties, representing a particular styling.
- Workflow:
  - We set the ‘selected properties’ to a theme (a set of ‘stored properties’). This will serve as our default theme.
  - All themeable CSS properties, for all components, will be defined as selected properties (as opposed to constant values or sets of CSS variables, representing a specific and constant theme).
  - We use JS to replace all variables that serve as values for our ‘selected properties’ with another set of variables from the ‘stored properties’.

``` CSS
/* 这里可以抽出同名变量，然后写成3个class */
:root {
  /* Set the deafult values */
  --selected-primary-color: var(--light-primary-color);
  --selected-disabled-color: var(--light-disabled-color);

  /* Set the 'light' theme */
  --light-primary-color: #007bff;
  --light-disabled-color: #6c757d;

  /* Set the 'dark' theme */
  --dark-primary-color: #000000;
  --dark-disabled-color: #4a4a4b;
}
```

``` JS
const setTheme = (themeName) => {

  // Get all 'selected' custom CSS properties from the ':root'.
  // These are the variables that are actually used (as oppose to vars to store the alternatives from different themes)
  const selectedCssProps = Array.from(document.styleSheets)
    .reduce(
      (acc, sheet) =>
      (acc = [
        ...acc,
        ...Array.from(sheet.cssRules).reduce(
          (def, rule) =>
          (def =
            rule.selectorText === ":root" ? [
              ...def,
              ...Array.from(rule.style).filter(name =>
                name.startsWith("--selected")
              )
            ] :
            def),
          []
        )
      ]),
      []
    );

  // Set the selected values to values of a different theme
  selectedCssProps.forEach(prop => {
    // set each selected variable with its analogous variable from the new theme
    document.documentElement.style.setProperty(prop, `var(--${themeName}${prop.substring(10)})`);
  });

}
```

# ref

- [Theming with CSS Custom Properties_201706](https://ramenhog.com/blog/2017/06/07/theming-with-css-custom-properties)
  - https://codepen.io/uptonking/pen/yLavavm
  - Please feel free to play around with the Slack demo codepen
  - 本示例通过js直接修改css变量的值
  - `element.style.setProperty(`--${this.id}`, this.value);`更新css变量
  - store the new theme string in LocalStorage with a specific keyname
    - whenever the app loads, we get that theme from LocalStorage
- [Flash of Unstyled Dark Theme](https://webcloud.se/blog/2020-04-06-flash-of-unstyled-dark-theme/)
  - Naive Implementation
    - Statically generated sites are "pre-rendered" HTML files usually served from CDN
    - As part of pre-rendering CSS is also applied, usually with some CSS-in-JS framework involved. 
      - On first paint, the user will see a pre-rendered page. 
      - Once client-side JS runs and detects the users preferred theme, the page will re-render.
      - If the users preferred theme is different from the default theme, the page re-render will be perceived as a "flash" between the two.
      - On a slow connection it can be very distracting and confusing as it takes a longer time for client-side JavaScript to execute.
      - On a slow connection it can be very distracting and confusing as it takes a longer time for client-side JavaScript to execute.
  - Improved implementation
    - avoidable with usage of CSS media queries and global CSS custom properties (commonly referred to as CSS variables)
    - If you're just rendering the page based on user OS theme preference, this problem can and should be solved in CSS, not in JavaScript. 
      - Use the `prefers-color-scheme` media query in the `<head>` section of your HTML.
  - Allow users to switch themes
  - Persist user theme preference
  - Listen to thematic changes in user OS
- [Theming With CSS Variables](https://dev.to/idoshamun/theming-with-css-variables-322f)
  - https://codepen.io/idoshamun/pen/moKZBN
  - 非常简单的示例，不依赖js文件，使用css vars切换主题
  - `onclick="document.documentElement.classList.toggle('theme-1')">`
