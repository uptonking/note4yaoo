---
title: web-style-css-sass-dev
tags: [css, sass, styling, web]
created: 2020-10-31T06:56:52.341Z
modified: 2021-02-25T17:50:04.640Z
---

# web-style-css-sass-dev

# guide

- SASS variables are replaced with their values as the preprocessor produces its CSS output long before the browser interprets the code, 
  - while CSS custom properties are evaluated by the browser at runtime.

- **sass vs css variables**
- sass pros
  - There are no inherit browser support considerations. They compile down into normal CSS.
  - Little stuff: Like you can strip units from a value if you had to.
  - sass除了提供变量，还提供了样式值计算工具函数
- sass cons
  - 难以实现让用户随意修改变量值来更新样式，因为预编译了
  - node-sass下载安装对墙内不友好，但dart-sass很好用
  - sass内置函数有限，没有充分利用js灵活计算的优势，参考treat.js和polished
- css vars pros
  - 易于实现让用户随意修改变量值来更新样式
- css vars cons
  - 浏览器的兼容性不够完美
  - 样式计算工具函数不多，如calc，标准还会继续扩充

- ## hard
- comment注释
  - @import其他文件的含嵌套样式时，难以添加#region/#endregion来方便折叠浏览
  - 可以定义一个用来生成comment的mixin

``` SCSS
@mixin region($text){
  /* #region #{$text} */
}

@include region('hello');
```

- ## [SASS VARIABLES VS. CSS CUSTOM PROPERTIES](https://intu.io/blog/sass-css-custom-properties/)
  - If your project requires dynamic theming, CSS custom properties will be the way to go very shortly. 
  - Otherwise, SASS variables are still a good choice, because they give you access to the power of a wide range of SASS functions. 

- ## sass vs postcss
- postcss优点
  - 插件非常丰富
- postcss缺点
  - 有时配置会优点繁琐，但很适合给构建工具开发postcss插件
  - 如果将postcss作为预处理器使用，如在css中引入嵌套、插值，则会提示css文件语法错误，能用但不友好

- tips
  - 若scss变量值为null，而书写类样式时只有1个属性且属性值为该变量，那么构建输出时该类名不会被输出

# sass-pieces

- `@mixin` vs `@extend`
  - Unlike mixins, which copy styles into the current style rule, @extend updates style rules that contain the extended selector so that they contain the extending selector as well. 
  - When extending selectors, Sass does intelligent unification

- `@mixin` vs `%placeholder-selector`
  - 最好的建议是：如果你需要参数变量，使用mixin。否则，继承一个placehodler
  - 第一，在placeholder里面，不能像mixin那样传递使用参数变量。但是可以使用全局变量。
  - 第二，当你使用mixin时，Sass会重复输出这个mixin的属性规则内容，不会让CSS选择器公用这个mixin。这样的话，样式表将会变得很大。
    - mixin会输出重复样式，而%placeholder常输出`selector1,selector2{}`

- sass的文件名为什么要加前缀_
  - 若你不加，其他人使用你的源文件或非官方编译器转换时，可能在原目录直接生成输出文件，造成污染和不方便
  - 参考主流sass项目的选择，大多数都加了_

- [Is it possible to use Sass variables in the comments?](https://stackoverflow.com/questions/21180452)
  - https://sass-lang.com/documentation/syntax/comments
  - comment can contain interpolation
  - When the first letter of a comment is !, the comment will be interpolated and always rendered into css output even in compressed output modes. 

- map-get vs map.get
  - [map.get() doesn't work. map-get() does. What gives?](https://stackoverflow.com/questions/64210390)
  - The documentation doesn't seem to be very clear on this, but the (Sass Module System: Draft 6) document on Github explains it better.
  - It seems like Sass is moving on to using `@use` in favour of `@import` for better compatibility with native CSS, and in order to get access to `map.get` you now must explicitly import the map module using the @use keyword `@use "sass:map";`.

# theming-examples 切换主题方案示例

- ## 若多个theme所有样式在同一css文件中(都预加载也行)
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

- ## 若每个theme的样式书写在单独的css文件
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

- ## alternative style sheets(incompatible)
  - You can include all the stylesheets in the document and then activate/deactivate them as needed.
  - you should be able to activate an `alternate` stylesheet by changing its `disabled` property from true to false, 
  - but only Firefox seems to do this correctly.
  - chrome不直接支持，但可通过手动安装扩展支持
  - Avoid the nonstandard `<link disabled>`. Setting HTMLLinkElement#disabled is fine though.
  - alternative style sheets
    - Style sheets linked without a title attribute are always applied.
    - (rel="alternate stylesheet", title="..." must be specified): disabled by default, can be selected.
    - The alternate stylesheets are commonly specified using a `<link>` element with `rel="alternate stylesheet"` and `title="..."` attributes.

# pieces

- I'd suggest you to generate multiple CSS files based on the _variables.scss file. 
  - All you have to do is build new theme with different variable file.
- Other way would be to use CSS custom variables (called as custom properties). 

- It would always be safe to combine the files. 
  - It is considered best practice by today's standards. 
  - It is quite common to minify and bundle the js and css files together to reduce requests to the server.
  - Anytime you load a css file or change properties on elements, the css is parsed and re-renders the necessary styling.
  - NOTE: I feel obligated to make sure you take order of selectivity into account when bundling your css files.

- [Node-sass does not understand tilde](https://stackoverflow.com/questions/37106230/node-sass-does-not-understand-tilde)
  - Tilde path resolving is something that webpack does, node-sass doesn't have such a resolver built in. sass-loader for webpack has this.
    - You can write your own import resolution alternatively.
  - the new version of Sass has this new importer option, where every "import" you do on your Sass file will go first through this method
  - You can add another `includePaths` to your `render` options.

# ref

- [switch theme in javascript](https://stackoverflow.com/questions/26304798/switch-theme-in-javascript)
- [Replacing css file on the fly (and apply the new style to the page)](https://stackoverflow.com/questions/19844545/replacing-css-file-on-the-fly-and-apply-the-new-style-to-the-page)

- [Switchable custom bootstrap themes with sass](https://stackoverflow.com/questions/54252245/switchable-custom-bootstrap-themes-with-sass)
- [Bootstrap 4 Sass - changing theme dynamically](https://stackoverflow.com/questions/45486572/bootstrap-4-sass-changing-theme-dynamically)

- [Is Sass Worth Learning In 2020?](https://scalablecss.com/sass-in-2020/)
