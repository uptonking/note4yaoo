---
title: note-style-css-sass
tags: [css, sass, style, theming]
created: '2020-10-31T06:56:52.341Z'
modified: '2020-10-31T06:57:33.840Z'
---

# note-style-css-sass

## theming-examples 切换主题方案示例

- ### 若多个theme所有样式书写在同一个css文件中
  - 检查body或最外层元素样式名是否等于themeName
  - `element.classList.contains('themeName')`
  - 若不等于，则添加themeName到样式名
  - 优点
    - 组件上的类名不必修改，只需将themeName添加到最外层元素的类名上
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

- ### 若每个theme的样式书写在单独的css文件
  - 通过事件修改head部分link的href
  - 优点
    - 组件上的类名不必修改
  - 缺点
    - 需要额外下载解析css

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
  - `oldlink.href = cssFile;`也work。
  - This replaces the whole link node in the DOM.
  - If you're wanting to pull a live-reload type of thing, this is probably the way to go since the href may be the same 
    - and the browser may not actually do anything if the href hasn't actually changed. 

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
```

## ref

- [switch theme in javascript](https://stackoverflow.com/questions/26304798/switch-theme-in-javascript)
- [Replacing css file on the fly (and apply the new style to the page)](https://stackoverflow.com/questions/19844545/replacing-css-file-on-the-fly-and-apply-the-new-style-to-the-page)
