---
title: note-ux-design-theming-blog
tags: [blog, design, theming]
created: '2020-12-29T18:00:51.271Z'
modified: '2020-12-29T18:01:11.468Z'
---

# note-ux-design-theming-blog

## theming with css vars

### [Theming With Variables: Globals and Locals_201803](https://css-tricks.com/theming-with-variables-globals-and-locals/)

- https://codepen.io/andresgalante/project/editor/DKPzvL

- Setting CSS variables to theme a design system can be tricky: 
  - if they are too scoped, the system will lose consistency. 
  - If they are too global, you lose granularity(细粒度).
- I’d like to try to boil design system variables down to two types: Global and Component variables. 
  - Global variables will give us consistency across components. 
  - Component variables will give us granularity and isolation. 
- I’ll be using CSS variables for this article but the concept applies to preprocessor variables as well.
- System-wide variables are general concepts defined to keep consistency across your components.
  - used to to keep consistency
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
    - For example, to change the padding of the alert without generating a system wide shift, they’d have to overwrite the alert component css
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
- **The two-tier theming system**
- The solution is a two-layer theming system where global variables always inform component variables
- First tier: Global variables(一般定义design tokens)
- The main reason to have global variables is to maintain consistency, and they adhere to these rules:
  - prefixed with the word `global` and follow the formula `--global--category--modifier--state--PropertyCamelCase`
  - They are concepts, never tied to an element or component
- Second tier: Component variables()
- The second layer is scoped to theme-able component properties and follow these rules:
  - Assuming we are writing BEM, they follow this formula: `--block__element--modifier--state--PropertyCamelCase`
  - The value of component scoped variables is always defined by a global variable
  - A component variable always has a default value as a fallback in case the component doesn’t have the dependency on the global variables
- You’ll notice that we are defining locally-scoped variables with global variables.
  - This is key for the system to work since it allows authors to theme the system as a whole
- On the other hand each component variable has a default value so a component can stand on its own, it doesn’t depend on anything and authors can use it in isolation.
- This setup allows for consistency across components, it generates a common language between designers and developers 
  - since we can set the same global variables in Sketch as bumpers for designers, and it gives granular control to authors.
- Why does this system work?
  - If we allow authors to easily theme the system without having to overwrite CSS, we’ll not only make their lives easier but also reduce the risk of breaking modules. 
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

### [Theming with CSS variables_201904](https://dev.to/wendell_adriel/theming-with-css-variables-1o56)

- **Two layers theming**
  - https://codepen.io/WendellAdriel/pen/QPxRjN
- Global variables are generic variables that will be used to keep the consistency between all our components
  - Some examples of global variables are font, default font-size and color palette. 
  - It's super simple to define global variables on CSS, we use the `:root` selector 
- Modules Variables
  - Every module variable MUST be defined using the value from a global variable 
  - and we also need to provide a fallback value for the case that the module will be used in an environment that doesn't provide global variables

- **Working with multiple CSS themes**
  - https://codesandbox.io/s/working-with-multiple-css-themes-03-forked-0wxui
- the `:root` selector can be used to store the global variables of our themes. 
- To create a default theme for our app, we will define some variables in this selector that will be used by our elements
- Now that we already have our default theme, we can work in a new theme for our app. 
  - There are some ways of working with themes, but my favorite is to use the `data-` attributes on `<HTML>` element. 
  - These `data-` attributes are a convention used to define custom attributes for tags and to identify which theme we're using we will create a `data-theme` attribute. 
  - All the elements with this attribute and their children will be modified. 
- Letting the user switch themes
  - First, let's remove the `data-theme="dark"` attribute from our `<html>` tag and create the element that will let the user switch themes when clicked.

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

### [ionic Dark Mode CodePen](https://ionicframework.com/docs/theming/dark-mode)

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

## more-theming

## ref

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
