---
title: docs-web-mozilla
tags: [docs, web]
created: '2020-07-18T12:22:41.248Z'
modified: '2021-01-04T16:19:02.355Z'
---

# docs-web-mozilla

# [w3c html5 editing](https://www.w3.org/TR/2008/WD-html5-20080610/editing.html )

- The `contenteditable` attribute is an enumerated attribute whose keywords are the empty string, true, and false. 
  - The empty string and the `true` keyword map to the true state. The `false` keyword maps to the false state. 
  - In addition, there is a third state, the `inherit` state, which is the missing value default (and the invalid value default).
  - `contenteditable` 属性默认继承
- If an element is editable and its parent element is not, or if an element is editable and it has no parent element, then the element is an editing host. 
  - Editable elements can be nested. 
  - User agents must make editing hosts focusable (which typically means they enter the tab order). 
  - An editing host can contain non-editable sections, these are handled as described below. 
  - An editing host can contain non-editable sections that contain further editing hosts.
- When an editing host has focus, it must have a caret position that specifies where the current editing position is. It may also have a selection.
  - How the caret and selection are represented depends entirely on the UA.
# contenteditable vs contentEditable
- `contenteditable` global attribute is an enumerated attribute indicating if the element should be editable by the user.
  - 作为html的属性
  - If so, the browser modifies its widget to allow editing.
  - `true` or an empty string, which indicates that the element is editable.
  - `false`, which indicates that the element is not editable.
  - If the attribute is given without a value, like `<label contenteditable>Example Label</label>`, its value is treated as an empty string.
  - If this attribute is missing or its value is invalid, its value is inherited from its parent element: so the element is editable if its parent is editable.

- `HTMLElement.contentEditable` property
  - 用在js中读写该属性
# Preloading content with `rel="preload"`

- The preload value of the `<link>` element's `rel` attribute lets you declare fetch requests in the HTML's `<head>`, specifying resources that your page will need very soon, 
  - which you want to start loading early in the page lifecycle, 
  - **before browsers' main rendering machinery kicks in**. 
  - This ensures they are available earlier and are less likely to block the page's render, improving performance.

```html
<head>
  <meta charset="utf-8">
  <title>JS and CSS preload example</title>

  <link rel="preload" href="style.css" as="style">
  <link rel="preload" href="main.js" as="script">

  <link rel="stylesheet" href="style.css">
</head>

<body>
  <h1>bouncing balls</h1>
  <canvas></canvas>

  <script src="main.js" defer></script>
</body>
```

- Here we preload our CSS and JavaScript files, so they will be available as soon as they are required for the rendering of the page later on.
- This example is trivial, as the browser probably discovers the `<link rel="stylesheet">` and `<script>` elements in the same chunk of HTML as the preloads, 
  - but the benefits can be seen much more clearly the later resources are discovered and the larger they are. 
  - For example:
    - Resources that are pointed to from inside CSS, like fonts or images.
    - Resources that JavaScript can request, like JSON, imported scripts, or web workers.
    - Larger images and video files.
- preload has other advantages too. 
- Using `as` to specify the type of content to be preloaded allows the browser to
  - Prioritize resource loading more accurately.
  - Store in the cache for future requests, reusing the resource if appropriate.
  - Apply the correct content security policy to the resource.
  - Set the correct `Accept` request headers for it.
- Many different content types can be preloaded.

- Other preloading features exist, but none are quite as fit for purpose as `<link rel="preload">`
  - In it's most basic form it sets the link that has `rel="preload"` to a high priority, 
  - Unlike prefetching, which the browser can decide whether it's a good idea or not, preload will force the browser to do so.

- `<link rel="preload" href="main.js" as="script">`
  - preload提供了一种声明式的命令，让浏览器提前加载指定资源(加载后并不执行)，在需要执行的时候再执行
  - 将加载和执行分离开，可不阻塞渲染和 document 的 onload 事件
  - 提前加载指定资源，不再出现依赖的font字体隔了一段时间才刷出
  - 在不支持 preload 的浏览器环境中，会忽略对应的 link 标签
  - preload 是告诉浏览器页面必定需要的资源，浏览器一定会加载这些资源；
  - prefetch 是告诉浏览器页面可能需要的资源，浏览器不一定会加载这些资源。
  - preload 和 prefetch 混用的话，并不会复用资源，而是会重复加载。

- ref
  - [用 preload 预加载页面资源](https://juejin.cn/post/6844903562070196237)
  - [HTML - Why is my preloaded resource loading again?](https://stackoverflow.com/questions/59353686/html-why-is-my-preloaded-resource-loading-again)
# Replaced elements
- In CSS, a replaced element is an element whose representation is outside the scope of CSS; 
  - they're external objects whose representation is independent of the CSS formatting model.
- Put in simpler terms, they're elements whose contents are not affected by the current document's styles. 
  - The position of the replaced element can be affected using CSS, but not the contents of the replaced element itself. 
  - Some replaced elements, such as `<iframe>` elements, may have stylesheets of their own, but they don't inherit the styles of the parent document.
- The only other impact CSS can have on a replaced element is that there are properties which support controlling the positioning of the element's content within its box
- Typical replaced elements are:
  - `<iframe>`
  - `<video>`
  - `<embed>`
  - `<img>`
- Some elements are treated as replaced elements only in specific cases:
  - `<option>`
  - `<audio>`
  - `<canvas>`
  - `<object>`
  - `<applet>`
- HTML spec also says that an `<input>` element can be replaced, because `<input>` elements of the `image` type are replaced elements similar to `<img>` . 
  - However, other form controls, including other types of `<input>` elements, are explicitly listed as non-replaced elements (the spec describes their default platform-specific rendering with the term "Widgets").
- Objects inserted using the CSS `content` property are anonymous(匿名的) replaced elements. They are "anonymous" because they don't exist in the HTML markup.
- CSS handles replaced elements specifically in some cases, like when calculating margins and some `auto` values.
  - Note that some replaced elements, but not all, have intrinsic(自身的) dimensions or a defined baseline, which is used by some CSS properties, such as vertical-align. 
  - Only replaced elements can ever have intrinsic dimensions.
# User agent
- A user agent is a computer program representing a person, for example, a browser in a Web context.
- Besides a browser, a user agent could be a bot scraping webpages, a download manager, or another app accessing the Web. 
- Along with each request they make to the server, browsers include a self-identifying `User-Agent` HTTP header called a user agent (UA) string. 
- This string often identifies the browser, its version number, and its host operating system.
- Spam bots, download managers, and some browsers often send a fake UA string to announce themselves as a different client. This is known as user agent spoofing.
- The user agent string can be accessed with JavaScript on the client side using the navigator.userAgent property.
- A typical user agent string looks like this
  - `Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:35.0) Gecko/20100101 Firefox/35.0`
  - `Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36`
# `<length>` css data type
- represents a distance value. 
- Lengths can be used in numerous CSS properties, such as width, height, margin, padding, border-width, font-size, and text-shadow.
- The `<length>` data type consists of a `<number>` followed by one of the units listed below. 
- As with all CSS dimensions, there is no space between the unit literal and the number. The length unit is optional after the number 0.
- Absolute lengths can cause accessibility problems, since they are fixed and do not scale according to user settings. 
- For this reason, prefer relative lengths (such as em or rem) when setting font-size.

- **Relative length units**
  - Font-relative lengths
  - Viewport-percentage lengths
- em
  - Represents the calculated `font-size` of the element. 
  - If used on the `font-size` property itself, it represents the inherited `font-size` of the element.
- rem 
  - Represents the `font-size` of the root element (typically `<html>` ). 
  - When used within the root element `font-size` , it represents its initial value (**a common browser default is 16px**, but user-defined preferences may modify this).
- cap
  - Represents the "cap height" (nominal height of capital letters) of the element’s font 
- lh
  - Equal to the computed value of the line-height property of the element on which it is used, converted to an absolute length
- vh/vw
  - Equal to 1% of the height/width of the viewport's initial containing block.

- **Absolute length units**
- Absolute length units represent a physical measurement when the physical properties of the output medium are known, such as for print layout.   
  - This is done by anchoring one of the units to a physical unit, and then defining the others relative to it. 
  - The anchor is done differently for low-resolution devices, such as screens, versus high-resolution devices, such as printers.
- For **low-dpi** devices, the unit `px` represents the physical reference pixel; other units are defined relative to it. 
  - Thus, **1in is defined as 96px, which equals 72pt**. 
  - The consequence of this definition is that on such devices, dimensions described in inches (in), centimeters (cm), or millimeters (mm) don't necessary match the size of the physical unit with the same name.
- For **high-dpi** devices, inches (in), centimeters (cm), and millimeters (mm) are the same as their physical counterparts. 
  - Therefore, **the px unit is defined relative to them (1/96 of 1 inch)**.
- px
  - For screen displays, it traditionally represents one device pixel (dot). 
  - However, for printers and high-resolution screens, one CSS pixel implies multiple device pixels. 1px = 1/96th of 1in.
- cm
  - One centimeter. 1cm = 96px/2.54.
- in
  - One inch. 1in = 2.54cm = 96px.
- pt
  - One point. 1pt = 1/72nd of 1in.
- pc
  - One pica. 1pc = 12pt = 1/6th of 1in.

- When animated, values of the `<length>` data type are interpolated as real, floating-point numbers. 
  - The interpolation happens on the calculated value. 
  - The speed of the interpolation is determined by the timing function associated with the animation.

- ref
  - [length CSS data type](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
  - [CSS像素、物理像素、逻辑像素、设备像素比、PPI、Viewport](https://zhuanlan.zhihu.com/p/91636704)
# `<number>` css data type 
- represents a number, being either an integer or a number with a fractional component.
- The syntax of `<number>` extends the syntax of `<integer>` . 
  - A fractional value is represented by a `.` followed by one or more decimal digits, and may be appended to an integer. 
  - There is no unit associated with numbers.
- When animated, values of the `<number>` CSS data type are interpolated as real, floating-point numbers. 
- The speed of the interpolation is determined by the timing function associated with the animation.
