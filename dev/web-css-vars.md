---
title: web-css-vars
tags: [css, css-vars, style]
created: 2020-11-01T06:32:11.038Z
modified: 2021-01-29T18:55:16.043Z
---

# web-css-vars

# faq

## css vars的范围问题

- tips
  - 当前范围中使用的css变量的值，由父级中同名变量的值决定；
  - 当前范围中声明的css变量的值，只是声明一个同名变量，具体计算发生在当前元素的子元素之中
  - 书写css变量值时，尽量不要存在循环引用，否则某个样式值表现为浏览器默认色或颜色值默认值，难以分析原因，如halfmoon的border hover色

- resources
  - [Use CSS Variables instead of React Context](https://epicreact.dev/css-variables/)

- ### [CSS Variables not global?](https://stackoverflow.com/questions/61553471/css-variables-not-global)

- why does the div not appear when the button is hovered over?

```HTML
<button>Hover</button>
<div></div>
```

```CSS
:root {
  --op: hidden;
}

button:hover {
  background-color: yellow;
  --op: visible;
}

div {
  visibility: var(--op);
  width: 100px;
  height: 100px;
  background-color: red;
}
```

- That's not working because you are setting the variable only for the button, so you are not overriding the global variable.

- 测试
  - chrome浏览器中，button默认的bg-color是rgb(239, 239, 239)
  - 若强行设置background-color: var(--my-bg); 且--my-bg未定义，则bg-color时rgb(0, 0, 0, 0)
  - 未定义的color类css变量默认是时透明色
  - 注意可能会使用button自身的默认色

- ### [Overriding :root CSS variables from inner scopes](https://stackoverflow.com/questions/58206867)
# guide
- faq-not-yet
  - 使用css vars和普通css书写class的性能对比
  - 更新样式时，可通过切换包含css vars新值的class类名，可通过js修改css vars的值，性能对比
    - 甚至还可以直接设置style属性的值来更新css vars的值

- css-vars pros
  - 浏览器直接支持，浏览器内置，符合标准
  - 实现简单theme切换非常方便，不用下载额外css文件，相关计算交给浏览器

- css-vars cons
  - 依赖浏览器，直接使用css variables的组件很难跨平台
  - 修改任何值时都会执行层叠覆盖，类似react context影响所有后代
    - 所以不适合用来实现通用的状态管理
  - css变量值必须是any valid CSS value
    - css的值的数据类型太单一，js的值可以函数、Map等，js更灵活
  - css内置的计算函数不够丰富，如比不过polish

- css vars的值也采用css属性值的层叠规则
  - 据此可基于css变量实现theme
    - 要考虑代码清晰、明确
    - 要考虑包含css变量的读写操作多不多，性能影响

- css-vars-basics
  - css变量名区分大小写
  - css变量名中可包含dash和underscore，，注意sass变量的下划线和横杠不区分
  - css变量值遵循css样式值的层叠规则
  - css变量值的赋值可以使用另一个css变量
  - css变量值会提升，所以可先使用再声明
  - 使用css变量值时，不能用加号构建字符串，可用`width: calc(var(--offset) * 1px);`
    - 不能用`font-size: var(--scale) + 'px';`
  - css变量值不能用在普通样式属性名，不能用在media query名称中

- tips
  - 若`var()`中的fallback值包含大量计算，会导致性能问题
  - css-variables除了存储样式常用变量，还可以用来存储状态变量，通过`style={{ '--box-size': size }}`的形式传入，用来实现动态样式很方便

```JS
// To use the values of custom properties in JavaScript, it is just like standard properties.

// get variable from inline style
element.style.getPropertyValue("--my-var");

// get variable from wherever
getComputedStyle(element).getPropertyValue("--my-var");

// set variable on inline style
element.style.setProperty("--my-var", jsVar + 4);
```

- css-vars-tools
  - [CSS variables (Custom Properties) polyfill for IE11](https://github.com/nuxodin/ie11CustomProperties)
  - https://github.com/notoriousb1t/awesome-css-variables
# css-vars-examples
- css vars的值，可以先使用，再声明定义，即存在类似js变量的变量提升

```HTML
<div>
  <h1 class="theme-red-text">hello</h1>
</div>
```

```CSS
.theme-red-text {
  --pf-global--Color--100: var(--pf-global--Color--dark-100);

  color: var(--pf-global--Color--100);
}

div {
  --pf-global--Color--dark-100: coral;
}
```

# theming-examples
- Themes becomes easier with css custom properties (css variables). 
- The basic idea is that you have your variables, and on theme change you change the color of the variables.
  - On root level set your variables for your default theme.
  - Have a class with the describing the theme, in my example it is .dark-theme
  - Set a class on the body when dark-theme is active with js, or postback depending on your backend and wanted approach. 
  - the approach on saving the theme all depends on what kind of site you have SPA, Wordpress, . NET ect. 
    - I seen mentions about saving it in the database and user, that kinda don't hold up if you don't have user signing. 
    - One approach is to save it in the browsers local storage and read it when you load the page.

```CSS
:root {
  --primary-color: deepskyblue;
}

body.dark-theme {
  --primary-color: deeppink;
}

.block {
  margin-bottom: 3rem;
  padding: 2rem;
  background-color: var(--primary-color);
}
```

```JS
const themeSwitcherButton = document.querySelector('.js-theme-switcher')

themeSwitcherButton.addEventListener('click', function() {
  const body = document.querySelector('body')

  if (body.classList.contains('dark-theme')) {
    body.classList.remove('dark-theme')
  } else {
    body.classList.add('dark-theme')
  }
})
```

```html
<body>
  <p class="block">
    my background color is picked from the theme
  </p>

  <button class="js-theme-switcher">Theme switcher</button>
</body>
```

- 简短示例
  - If the `body` element has the `theme-dark` class, it will use the variables defined for that class. 
  - Otherwise, it will use the default `:root` variables.

```CSS
:root {
  --background-color: white;
  --text-color: black;
}

.theme-dark {
  --background-color: black;
  --text-color: white;
}

body {
  background-color: var(--background-color);
  color: var(--text-color);
}
```

- [CodePen demo(这个示例样式过多)](https://codepen.io/BarthyB/pen/EBzxje)
- I define the color variables depending on the app container's class (.light or .dark). 
- Simply toggling those classes will then change the site's theme.

```JS
document.addEventListener("DOMContentLoaded", function() {
  const app = document.querySelector(".app");
  const themeName = document.querySelector(".theme-name");
  const button = document.querySelector(".btn-switch");
  let currentTheme = app.classList.contains("light") ? "light" : "dark";

  button.addEventListener("click", function() {
    app.classList.remove(currentTheme);
    currentTheme = currentTheme === "light" ? "dark" : "light";
    app.classList.add(currentTheme);

    themeName.innerText = currentTheme;
  });
});
```

# css-variables-blog
- ## [Pragmatic, Practical, and Progressive Theming with Custom Properties](https://csswizardry.com/2016/10/pragmatic-practical-progressive-theming-with-custom-properties/)
- My usual advice to companies and clients who want to implement theming in their UIs is simply don’t.
- There are very few specific cases where theming will provide business value, but for the most part, it is a lot more hassle(困难，麻烦；争论，分歧) than it’s worth. Theming
  - increases the complexity of your code; 
  - reduces clarity when debugging; 
  - brings higher maintenance overhead; 
  - and increases testing time.
- Exceptions are usually white-label solutions in which a customer purchases a license for your software, and then wish to run it as though it was their own platform. 
  - Most other cases are not business critical, so do yourself—and your team—a favour and avoid it if at all possible.
- However, with that said, by using some newer CSS features we can provide certain styles of theming with greatly reduced overhead. 
- Theming—certainly for the purposes of this article—refers to the act of laying a veneer over the top of an already styled website: an optional extra which alters or customises the UI. 
- A slightly more specific subset of theming is user customisation. 
- The primary use case for being able to redefine css custom property values in the browser is to help us with Twitter-style user customisation: that is to say, allowing users to choose their own colour values through some kind of UI.
- What we have now is:
  - Our own CSS which defines global variables for theming values.
  - Those same variables are implemented with fallbacks in case they weren’t defined properly, or become invalid.
  - This is only executed if we know our browser supports custom properties.
  - If our browser doesn’t support custom properties, we fall back to our default theme.
  - Users can pass their own values into our static stylesheet by redefining their own custom properties via a GUI.
  - We drop those newly defined custom properties into the HTML so that they can be picked up at runtime and thus reskin the UI.
- If you wish to implement something like this, please feel free to introduce the preprocessor layer yourself
- Theming, the vast majority of the time, is a complete nice-to-have. 
  - It is not business critical or usually even important. 
  - If you are asked to provide such theming, do not do so at the expense of performance or code quality.

- ## [Using CSS custom properties (variables)](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- Declaring a custom property is done using a custom property name that begins with a double hyphen (`--`), and a property value that can be any valid CSS value.
  - Custom property names are case sensitive
- Note that the selector given to the ruleset defines the scope that the custom property can be used in. 
  - A common best practice is to define custom properties on the `:root` pseudo-class, so that it can be applied globally across your HTML document
  - you maybe have a good reason for limiting the scope of your custom properties.
- Custom properties do inherit. 
  - This means that if no value is set for a custom property on a given element, the value of its parent is used. 
  - Custom properties are scoped to the element(s) they are declared on, and participate in the cascade: 
    - the value of such a custom property is that from the declaration decided by the cascading algorithm.
- Keep in mind that these are custom properties, not actual variables like you might find in other programming languages. 
  - The value is computed where it is needed, not stored for use in other rules. 
  - For instance, you cannot set a property for an element and expect to retrieve it in a sibling's descendant's rule. 
  - **The property is only set for the matching selector and its descendants**, like any normal CSS.
- Using the `var()` function, you can define multiple fallback values when the given variable is not yet defined; 
  - this can be useful when working with Custom Elements and Shadow DOM.
  - The function only accepts two parameters, assigning everything following the first comma as the second parameter. 
  - If that second parameter is invalid, such as if a comma-separated list is provided, the fallback will fail.
  - The technique has been seen to cause performance issues as it takes more time to parse through the variables.
  - The syntax of the fallback, like that of custom properties, allows commas. 

```CSS
.two {
  /* Red if --my-var is not defined */
  color: var(--my-var, red);
}

.three {
  /* pink if --my-var and --my-background are not defined */
  color: var(--my-var, var(--my-background, pink));
}

.three {
  /* Invalid: "--my-background, pink" */
  color: var(--my-var, --my-background, pink);
}

.four {
  /* defines a fallback of red, blue */
  color: var(--foo, red, blue);
}
```

- The classical CSS concept of validity, tied to each property, is not very useful in regard to custom properties. 
  - When the values of the custom properties are parsed, the browser doesn't know where they will be used, 
  - so must, therefore, consider nearly all values as valid.

- When the browser encounters an invalid `var()` substitution, the initial or inherited value of the property is used.
  - Check if the property color is inheritable.
- While a syntax error in a CSS property/value pair will lead to the line being ignored, using a cascaded value, invalid substitution -- using a custom property value that is invalid -- is not ignored, leading to the value to be inherited.
  - 无效的css变量值，也会被继承，参与层叠规则

- ## [CSS Variables: Why Should You Care?](https://developers.google.com/web/updates/2016/02/css-variables-why-should-you-care)
- CSS variables, more accurately known as CSS custom properties, are landing in Chrome 49.
  - Currently Chrome 49, Firefox 42, Safari 9.1, and iOS Safari 9.3 support custom properties.
- They can be useful for reducing repetition in CSS, and also for powerful runtime effects like theme switching and potentially extending/polyfilling future CSS features.
- While tools like SASS or LESS have boosted developer productivity immensely, the preprocessor variables that they use suffer from a major drawback, 
  - which is that they’re static and can’t be changed at runtime. 
  - Adding the ability to change variables at runtime not only opens the door to things like dynamic application theming, 
  - but also has major ramifications for responsive design and the potential to polyfill future CSS features.
- `var(<custom-property-name> [, <declaration-value> ]? )`
  - Fallback values can be a comma separated list, which will be combined into a single value. 
  - For example `var(--font-stack, "Roboto", "Helvetica");` defines a fallback of `"Roboto", "Helvetica"`. 
  - Keep in mind that shorthand values, like those used for margin and padding, are not comma separated
- This technique is especially useful for theming Web Components that use Shadow DOM, as custom properties can traverse shadow boundaries. 
  - A Web Component author can create an initial design using fallback values, and expose theming “hooks” in the form of custom properties.
- Working with custom properties in JavaScript

```

/* CSS */
:root {
  --primary-color: red;
}

p {
  color: var(--primary-color);
}

<!-- HTML -->
<p>I’m a red paragraph!</p>

/* JS */
var styles = getComputedStyle(document.documentElement);
var value = String(styles.getPropertyValue('--primary-color')).trim();
// value = 'red'
document.documentElement.style.setProperty('--primary-color', 'green');

```

- ## [Theming With CSS Variables_hot and cold vars_201910](https://blog.prototypr.io/css-variables-90cc4cdf41e9)

- ref
  - [demo: button comp before theming](https://codesandbox.io/s/silly-silence-efgfw)
  - [demo: themed button](https://codesandbox.io/s/dracula-bh1d6)
  - [demo: dark themed button](https://codesandbox.io/s/neon-mtj7)
  - 所有示例都没有提供来回切换theme的功能，只提供了实现theme的方法
    - 通过`className="dracula-theme_btn"`传入新类名，此法不推荐

- There was a use case — to build a scalable design system with an easy customize method for the Whitelabel option when a client wants to have their own colors and typography, styles.
  - The easiest way is to use CSS variables — manage hundreds of places where you implemented different styles much better with a small list of variables.
  - And much more comfortable is just add one new CSS file instead of menage variables with preprocessors or JS. Also, because initial design-tokens in our project always should be the same and updated with our latest default styles. I consider a new CSS file with new variables that will override current variables like a web-manifest file.
  - Also, we have deeply nested components, one library import another and another import a new one. It means that we can’t override SASS variables or properties that are stored in the imported libraries, where we can override only styles.
- Therefore, the best solution here will be to have union variables which we can override no matter if they nested it another library or no.
- You can’t use CSS variables in media-queries, but there is a solution (in the future)— CSS Environment Variables. 
  - It has not so wide coverage like CSS variables, but it’s a matter of time.

- Our first artboard in the project — Design Tokens— the foundation.
- I suggest you separate design tokens into 2 pieces — native and preprocessor's variables or hot and cold variables.
- we can’t use CSS variables for media-queries, so, we will make variables for `Grid`s as cold (SASS) variables.
- Also, we will make `Spacer`s as cold variables as well, because there is no case when you will change them globally, 
  - like to change spacer M with8px value to16px, it will break all our designs.
- Making a component with isolated variables
  - We already used Sass and CSS variables in the Layout component, but here is a different case where we will use “nested variables” 
  - it means that we will add CSS variables inside components classes, not in the `:root` because we want to isolate and protect the component’s variables.
- Add variable `--btn-text-clr`. 
  - This variable will cover not only the text color but, also, the icon fill as well because the icon and the text always will have the same color. 
  - And this is the big advantage of CSS variables that we can actually override several properties only by one variable.
- Theming
  - We need to create a new stylesheet and override inside the root all variables that we want to change and import this file in the index.js
  - but there is a problem — we also need to change the text and the icon color to more contrast — from black to white.
  - To do so, we need to create a new modifiers group consists of classes that we will add to elements with privite variables.
  - then add this class .dracula-theme_btn to the element, you want to change.
  - So, by one shot we changed two properties color and fill. Using this approach we can change any privite variable.
  - There is another way
    - you can store privite variables for certain components in the root it depends. 
    - But here I prefer to add an additional class to change.

- In this article, I tried to show how we can theme a website with CSS variables without JS, combine CSS and SASS variables, override several CSS props only by one variable.
- Like I mentioned before we have nested libraries and components that we can’t change, so we can’t add hooks in certain components, only change their CSS. 
  - But still if you are doing everything from the scratch there are good articles about CSS variables + JS
# discuss
- ## 

- ## 

- ## 

- ## [What are the advantages and disadvantages of CSS variables? - Stack Overflow](https://stackoverflow.com/questions/3130741/what-are-the-advantages-and-disadvantages-of-css-variables)
- The only disadvantage that I can think of is the added complexity of having to use or write a pre-processor, and appropriately manage the caching of the output in order not to have each request pass through the pre-processor.
- A concrete problem I could foresee is that developers might have editors/IDE's that knows how to deal with CSS, but don't know how to deal with your dialect of CSS. That could restrict said developers quite a bit.

# ref
- [Theming with CSS Custom Properties](https://ramenhog.com/blog/2017/06/07/theming-with-css-custom-properties)
  - https://codepen.io/uptonking/pen/yLavavm
  - Please feel free to play around with the Slack demo codepen
  - 本示例通过js直接修改css变量的值
  - `element.style.setProperty(`--${this.id}`, this.value);`更新css变量
  - store the new theme string in LocalStorage with a specific keyname
  - whenever the app loads, we get that theme from LocalStorage
- [Theming With Variables: Globals and Locals_201803](https://css-tricks.com/theming-with-variables-globals-and-locals/)
- [Theming with CSS variables: Two layers theming_201904](https://dev.to/wendell_adriel/theming-with-css-variables-1o56)
- [How To Create a Dark-Mode Theme Using CSS Variables](https://www.digitalocean.com/community/tutorials/css-theming-custom-properties)
  - 本示例通过在最外层元素添加带css变量主题值的类名覆盖原值

- [CSS variables: Scoping](https://blog.logrocket.com/css-variables-scoping/)
  - The place in the CSS hierarchy where you declare a CSS variable will determine its level of visibility throughout the lower levels of the hierarchy.
  - CSS variables are hoisted and they are moved on the top of the CSSOM before rendering the styles of respective HTML elements in the browser.
  - Just like in JavaScript, CSS variables can be hoisted. 
    - This means that CSS variables can be used before they are declared.
