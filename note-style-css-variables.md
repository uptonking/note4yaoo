---
title: note-style-css-variables
tags: [css, css-variables, style]
created: '2020-11-01T06:32:11.038Z'
modified: '2020-11-01T06:32:38.093Z'
---

# note-style-css-variables

## guide

- 使用css variables
  - css-variables除了存储样式常用变量，还可以用来存储状态变量，通过`style={{ '--box-size': size }}`的形式传入，用来实现动态样式很方便
  - To use the values of custom properties in JavaScript, it is just like standard properties.
    - `element.style.getPropertyValue("--my-var");`
    - `element.style.setProperty("--my-var", jsVar + 4);`

- css vars的值也才用css样式值的层叠规则
  - 据此可基于css变量实现theme

## theming-examples

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

## css-variables-blog

- ### [Pragmatic, Practical, and Progressive Theming with Custom Properties](https://csswizardry.com/2016/10/pragmatic-practical-progressive-theming-with-custom-properties/)
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

## ref

- [Theming with CSS Custom Properties](https://ramenhog.com/blog/2017/06/07/theming-with-css-custom-properties)
  - Please feel free to play around with the Slack demo codepen
  - 本示例通过js直接修改css变量的值
  - 使用`element.style.setProperty(`--${this.id}`, this.value);`更新css变量
  - store the new theme string in LocalStorage with a specific keyname
    - whenever the app loads, we get that theme from LocalStorage
- [How To Create a Dark-Mode Theme Using CSS Variables](https://www.digitalocean.com/community/tutorials/css-theming-custom-properties)
  - 本示例通过在最外层元素添加带css变量主题值的类名覆盖原值
