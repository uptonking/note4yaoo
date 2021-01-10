---
title: web-css-variables
tags: [css, css-vars, style]
created: '2020-11-01T06:32:11.038Z'
modified: '2021-01-01T20:18:11.427Z'
---

# web-css-variables

# guide

- faq-not-yet
  - inline样式的css vars的性能

- css vars优点
  - 浏览器直接支持
  - 实现简单theme切换非常方便，不用下载额外css文件，相关计算交给浏览器

- css vars缺点
  - css变量值必须是any valid CSS value
  - css内置的计算函数不够丰富

- css vars的值也采用css属性值的层叠规则
  - 据此可基于css变量实现theme
    - 要考虑代码清晰、明确
    - 要考虑包含css变量的读写操作多不多，性能影响

- tips
  - 若var()函数的fallback值包含大量计算，会导致性能问题
  - css-variables除了存储样式常用变量，还可以用来存储状态变量，通过`style={{ '--box-size': size }}`的形式传入，用来实现动态样式很方便

``` JS
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

# theming-examples

- Themes becomes easier with css custom properties (css variables). 
- The basic idea is that you have your variables, and on theme change you change the color of the variables.
  - On root level set your variables for your default theme.
  - Have a class with the describing the theme, in my example it is .dark-theme
  - Set a class on the body when dark-theme is active with js, or postback depending on your backend and wanted approach. 
  - the approach on saving the theme all depends on what kind of site you have SPA, Wordpress, . NET ect. 
    - I seen mentions about saving it in the database and user, that kinda don't hold up if you don't have user signing. 
    - One approach is to save it in the browsers local storage and read it when you load the page.

``` CSS
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

``` JS
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

``` html
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

``` CSS
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

``` JS
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

``` CSS
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

# ref

- [Theming with CSS Custom Properties](https://ramenhog.com/blog/2017/06/07/theming-with-css-custom-properties)
  - https://codepen.io/uptonking/pen/yLavavm
  - Please feel free to play around with the Slack demo codepen
  - 本示例通过js直接修改css变量的值
  - `element.style.setProperty(`--${this.id}`, this.value);`更新css变量
  - store the new theme string in LocalStorage with a specific keyname
    - whenever the app loads, we get that theme from LocalStorage
- [How To Create a Dark-Mode Theme Using CSS Variables](https://www.digitalocean.com/community/tutorials/css-theming-custom-properties)
  - 本示例通过在最外层元素添加带css变量主题值的类名覆盖原值
