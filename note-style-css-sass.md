---
title: note-style-css-sass
tags: [css, sass, style, theming]
created: '2020-10-31T06:56:52.341Z'
modified: '2020-10-31T06:57:33.840Z'
---

# note-style-css-sass

## sass-theming

- 3 easy steps:
  - Compile all themes into different files upon deploy. This will take care of timestamping, zipping, etc.
  - Render page with default theme.
  - Use javascript to load alternate theme CSS.
- No need to mess with dynamic compilation and all that.
- To load a CSS dynamically you can use something like this:

``` JS
function loadCSS(url) {
  var cssfile = document.createElement("link");
  cssfile.setAttribute("rel", "stylesheet");
  cssfile.setAttribute("type", "text/css");
  cssfile.setAttribute("href", url);
}
```

- Unless you're trying to do something extreme like CSSZenGarden with hundreds of themes, or each theme is thousands of lines, I'd recommend setting each theme as it's own CSS class rather than it's own file.
  - It's straightforward to switch theme classes with JQuery
  - you will have to tag the elements you want the update with the ThemedElement class
- If you think you can manage your themes with classes rather than files, here's how we generate them with SASS. 
  - SASS doesn't support json style objects, so we have to reach way back and set up a bunch of parallel arrays with the theme properties. 
  - Then we iterate over each theme, substitute the dynamic properties into the auto generated theme class, and you're off to the races
  - 写theme样式时多用scss变量，然后通过循环逻辑编译出不同theme的样式类

- 基于scss变量和mixin编译出themes

``` SCSS
$themes: (
  darkTheme: (
    'text-color': white,
    'bg-color': #424242
  ),
  lightTheme: (
    'text-color': black,
    'bg-color': #f5f5f5
  )
);

@mixin theme() {
  @each $theme, $map in $themes {
    // $theme: darkTheme, lightTheme
    // $map: ('text-color': ..., 'bg-color': ...)

    // make the $map globally accessible, so that theme-get() can access it
    $theme-map: $map !global;

    // make a class for each theme using interpolation -> #{}
    // use & for making the theme class ancestor of the class
    // from which you use @include theme() {...}
    .#{$theme} & {
      @content;    // the content inside @include theme() {...}
    }
  }
  // no use of the variable $theme-map now
  $theme-map: null !global;
}

@function theme-get($key) {
  @return map-get($theme-map, $key);
}

```

``` CSS
.content {
  padding: 32px;
}

.darkTheme .content {
  color: white;
  background-color: #424242;
}

.lightTheme .content {
  color: black;
  background-color: #f5f5f5;
}
```

## Theming with CSS Variables

- [CodePen demo，这个示例样式过多](https://codepen.io/BarthyB/pen/EBzxje)
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

## theming-examples 切换主题方案示例

- ### 若多个theme所有样式在同一css文件中(都预加载也行)
  - 检查body或最外层元素样式名是否等于themeName
    - `element.classList.contains('themeName')`
    - 若不等于，则添加themeName到样式名
  - 优点
    - 组件上的类名不必修改，只需将themeName添加到最外层元素的类名上
    - 计算任务只是切换样式名，性能较高
  - 缺点
    - 不一定能准确选中要覆盖样式的元素，可能有部分元素样式没改变

``` CSS
.myDefault {
  color: green;
}

.themeName .myDefault {
  color: blue;
}
```

- I would suggest an approach which is not mentioned here, in which you will include both the CSS files in the HTML
  - basicall every selector in `dark.css` will be a child of `.dark_layout`
  - Then all you need to do is to change the class of body element if someone selects to change the theme of the website.
  - You can also add CSS animations for backgrounds and colors which makes the transition highly smooth.

``` CSS
/*** light.css ***/
p.main {
  color: #222;
}

/*** dark.css ***/
.dark_layout p.main {
  color: #fff;
  background-color: #222;
}
```

``` JS
$("#changetheme").click(function() {
  $("body").toggleClass("dark_layout");
});
```

- ### 若每个theme的样式书写在单独的css文件
  - 通过事件修改head部分link节点的href
  - 优点
    - 组件上的类名不必修改
  - 缺点
    - 需要额外下载css，消耗性能多

``` typescript
// 示例1
<link id="themeLink" href="script/easyui/themes/dark/easyui.css?v=20130913" rel="stylesheet" type="text/css" />

var options = $('#themeOptions'),
    dir = 'script/easyui/themes/',
    file = 'easyui.css?v=',
    link = $('#themeLink');

options.change(function(){
    var selected = $(this).find(':selected').val(),
        time = new Date().getTime(); // optionally include time to avoid caching

    file = selected.length ? '/' + file : file;
    link.prop('href', dir + selected + file + time);
}).change(); // optional trigger onload
```

``` JS
// 示例2
<link rel="stylesheet" href="dark.css" id="theme">
<button id="switch">Switch Theme</button>

document.getElementById('switch').onclick = function() {
  if (document.getElementById('theme').href == "dark.css") {
    document.getElementById('theme').href = "light.css";
  } else {
    document.getElementById('theme').href = "dark.css";
  }
};

// dark.css
body{
    background: #000;
}
// light.css
body{
    background: #fff;
}
```

- You can create a new link, and replace the old one with the new one. 
  - `oldlink.href = cssFile;`也行
  - This replaces the whole link node in the DOM.
  - If you're wanting to pull a live-reload type of thing, this is probably the way to go since the href may be the same 
    - and the browser may not actually do anything if the href hasn't actually changed. 
  - while switching css files, the gap in downloading the file and rendering the styles leaves the html without styles. 
    - I guess, there should be a default stylesheet, which adds basic styles, always there. 
    - Mobile browsers may take much time to replace the css style sheet. 
    - Also the index of link might vary in different pages, given a static website generated by jekyll 

``` html
<html>

<head>
  <title>Changing CSS</title>
  <link rel="stylesheet" type="text/css" href="positive.css" />
</head>

<body>
  <a href="#" onclick="changeCSS('positive.css', 0);">STYLE 1</a>
  <a href="#" onclick="changeCSS('negative.css', 0);">STYLE 2</a>
</body>

</html>
```

``` JS
function changeCSS(cssFile, cssLinkIndex) {

  var oldlink = document.getElementsByTagName("link").item(cssLinkIndex);

  var newlink = document.createElement("link");
  newlink.setAttribute("rel", "stylesheet");
  newlink.setAttribute("type", "text/css");
  newlink.setAttribute("href", cssFile);

  document.getElementsByTagName("head").item(0).replaceChild(newlink, oldlink);
}

// 另一种
document.getElementsByTagName('head')[0].href = 'stylesheet2.css';
```

- ### alternative style sheets(incompatible)
  - You can include all the stylesheets in the document and then activate/deactivate them as needed.
  - you should be able to activate an `alternate` stylesheet by changing its `disabled` property from true to false, 
  - but only Firefox seems to do this correctly.
  - chrome不直接支持，但可通过手动安装扩展支持
  - Avoid the nonstandard `<link disabled>`. Setting HTMLLinkElement#disabled is fine though.
  - alternative style sheets
    - Style sheets linked without a title attribute are always applied.
    - (rel="alternate stylesheet", title="..." must be specified): disabled by default, can be selected.
    - The alternate stylesheets are commonly specified using a `<link>` element with `rel="alternate stylesheet"` and `title="..."` attributes.

## pieces

- I'd suggest you to generate multiple CSS files based on the _variables.scss file. 
  - All you have to do is build new theme with different variable file.
- Other way would be to use CSS custom variables (called as custom properties). 

- It would always be safe to combine the files. 
  - It is considered best practice by today's standards. 
  - It is quite common to minify and bundle the js and css files together to reduce requests to the server.
  - Anytime you load a css file or change properties on elements, the css is parsed and re-renders the necessary styling.
  - NOTE: I feel obligated to make sure you take order of selectivity into account when bundling your css files.

## ref

- [switch theme in javascript](https://stackoverflow.com/questions/26304798/switch-theme-in-javascript)
- [Replacing css file on the fly (and apply the new style to the page)](https://stackoverflow.com/questions/19844545/replacing-css-file-on-the-fly-and-apply-the-new-style-to-the-page)
- [User theme switching with SASS - Ruby on Rails](https://stackoverflow.com/questions/8744941/user-theme-switching-with-sass-ruby-on-rails)
- [Switchable custom bootstrap themes with sass](https://stackoverflow.com/questions/54252245/switchable-custom-bootstrap-themes-with-sass)
- [Bootstrap 4 Sass - changing theme dynamically](https://stackoverflow.com/questions/45486572/bootstrap-4-sass-changing-theme-dynamically)
- [Is there a way to add dark mode to my application with SCSS?](https://stackoverflow.com/questions/57017955/is-there-a-way-to-add-dark-mode-to-my-application-with-scss)
