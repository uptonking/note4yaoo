---
title: docs-web-html-elements-common
tags: [docs, dom, html, web]
created: '2020-07-17T09:39:12.042Z'
modified: '2020-12-08T13:14:07.354Z'
---

# docs-web-html-elements-common

# guide

# [Empty element](https://developer.mozilla.org/en-US/docs/Glossary/empty_element)

- The empty elements in HTML are as follows:
  - area, base, br, col, embed, hr, img, input, keygen, link, meta, param, source, track, wbr
  - 不是empty elements: script, style

- An empty element is an element from HTML, SVG, or MathML that cannot have any child nodes (i.e., nested elements or text nodes).
- The HTML, SVG, and MathML specifications define very precisely what each element can contain. 
  - Many combinations have no semantic meaning, for example an `<audio>` element nested inside an `<hr>` element.
- In HTML, using a closing tag on an empty element is usually invalid. 
  - `<input type="text"></input>` is invalid HTML.

- There is no such thing as a self-closing tag in HTML5 syntax.
  - Self-closing tags on non-void elements like `<p/>, <div/>` will not work at all. 
    - The trailing slash will be ignored, and these will be treated as opening tags. 
    - This is likely to lead to nesting problems.
    - This is true regardless of whether there is whitespace in front of the slash: `<p /> and <div />` also won't work for the same reason.
  - Self-closing tags on void elements like `<br/> or <img src="" alt=""/>` will work, 
    - but only because the trailing slash is ignored, and in this case that happens to result in the correct behaviour.

- In HTML5, the meaning of `<foo />` depends on the type of element.
  - On HTML elements that are designated as void elements (essentially "An element that existed before HTML5 and which was forbidden to have any content"), end tags are simply forbidden. 
    - The slash at the end of the start tag is allowed, but has no meaning. 
    - It is just syntactic sugar for people (and syntax highlighters) that are addicted to XML.
  - On other HTML elements, the slash is an error, but error recovery will cause browsers to ignore it and treat the tag as a regular start tag. 
    - This will usually end up with a missing end tag causing subsequent elements to be children instead of siblings.
  - Foreign elements (imported from XML applications such as SVG) treat it as self-closing syntax.

# [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

- Below listed are all the HTML elements, which are created using tags
- In HTML, a tag is used for creating an element. 
  - The name of an HTML element is the name used in angle brackets such as `<a>`
- elements by group
  - html: root element of html document
  - metadata
    - head: contains machine-readable information (metadata) about the document, like title
    - base: specifies the base URL to use for all relative URLs in a document
    - link: specifies relationships between the current document and an external resource
    - meta: represents metadata that cannot be represented by other HTML meta-related elements
    - style
    - title
  - body: represents the content of an HTML document. 
    - There can be only one body element in a document.
  - content section
    - main,nav,footer,header
    - address,article,aside
    - section
    - h1~h6
    - hgroup: has been removed from the HTML5 spec
  - text content block
    - blockquote,q(quote inline),cite
    - div,
    - dl,dt,dd
    - figure,figcaption
    - hr
    - ol,ul,li
    - p
    - pre
  - text inline
    - a,abbr,b
    - bdi: tells the browser's bidirectional algorithm to treat the text it contains in isolation from its surrounding text
    - bdo: overrides the current directionality of text, so that the text within is rendered in a different direction.
    - cite,q
    - code
    - data, time
    - dfn:to indicate the term being defined within the context of a definition phrase or sentence.
    - em,i,kbd,
    - mark
    - ruby: rb,rp,rtc
    - s: renders text with a strikethrough, or a line through it. use del and ins for editing
    - samp: typically rendered using the browser's default monospaced font
    - small:  renders text within it one font-size smaller
    - span
    - strong,sub,sup
    - time
    - u: rendered by default as a simple solid underline，如错误提示下划线
    - var: represents the name of a variable in a mathematical expression or a programming context.
    - wbr: represents a word break opportunity
  - image and multimedia
    - map,area: define an image map, a clickable link area
    - img
    - audio
    - video
    - track: a child of audio or video
  - embedded content
    - embed: embeds external content at the specified point in the document.
    - iframe: represents a nested browsing context
    - object: represents a: n external resource
      - param: defines parameters for an object element
    - picture: offer alternative versions of an image for different display/device scenarios
      - source: specifies multiple media resources for the picture, audio, video
  - script
    - canvas: with either the canvas scripting API or the WebGL API to draw graphics and animations.
    - script: embed executable code or data
    - noscript: defines a section of HTML to be inserted if a script type on the page is unsupported
  - editing
    - del
    - ins
  - table content
    - table: represents tabular data
    - thead: defines a set of rows defining the head of the columns of the table
    - tbody
    - tfoot: defines a set of rows summarizing the columns of the table
    - col: defines a column, generally within a colgroup
    - colgroup: defines a group of columns within a table
    - caption: specifies the caption (or title) of a table.
    - tr
    - td
    - th: defines a cell as header of a group of table cells
  - form
    - button
    - datalist: contains a set of option elements
    - fieldset: group several controls as well as labels within a web form.
    - form: represents a document section containing interactive controls for submitting information.
    - input: to create interactive controls for web-based forms in order to accept data from the user
    - label
    - legend
    - meter: represents either a scalar value within a known range or a fractional value. 类似温度计
    - optgroup
    - option: define an item contained in a select, an optgroup, or a datalist
    - output
    - progress: displays an indicator showing the completion progress of a task, typically displayed as a progress bar.
    - select
    - textarea
  - interactive elements
    - details: creates a disclosure widget in which information is visible only when the widget is toggled into an "open" state.
      - summary: specifies a summary, caption, or legend for a details 
    - dialog: represents a dialog box or other interactive component, such as a dismissable alert, inspector, or subwindow.
    - menu: represents a group of commands that a user can perform or activate
  - web components
    - slot: a placeholder inside a web component that you can fill with your own markup
    - template: a mechanism for holding HTML that is not to be rendered immediately when a page is loaded but may be instantiated subsequently during runtime using JavaScript.
  - obsolete and deprecated
    - acronym: 首字母缩写，use abbr
    - applet: deprecated in favor of object
    - center: a block-level element that displays its block-level or inline contents centered horizontally 
      - use text-align
    - spacer: allowed insertion of empty spaces on pages
      - use css
    - strike: if it represents deleted content, use del instead. 
      - In all other cases use s

# picture ie都不支持

- `<picture>` element contains zero or more `<source>` elements and one `<img>` element to offer alternative versions of an image for different display/device scenarios.
  - The browser will consider each child `<source>` element and choose the best match among them. 
  - If no matches are found—or the browser doesn't support the `<picture>` element—the URL of the `<img>` element's `src` attribute is selected.
- The `<img>` element serves two purposes:
  - It describes the size and other attributes of the image and its presentation.
  - It provides a fallback in case none of the offered `<source>` elements are able to provide a usable image.
- Common use cases for `<picture>`:
  - Art direction. 
    - Cropping or modifying images for different media conditions 
    - (for example, loading a simpler version of an image which has too many details, on smaller displays).
  - Offering alternative image formats, for cases where certain formats are not supported
    - For example, newer formats like AVIF or WEBP have many advantages, but  might not be supported by the browser.

# form-select-option

``` HTML
<label for="pet-select">Choose a pet:</label>

<select name="pets" id="pet-select">
  <option value="">--Please choose an option--</option>
  <option value="dog" selected>Dog</option>
  <option value="cat">Cat</option>
  <option value="parrot">Parrot</option>
  <option value="spider">Spider</option>
</select>
```

- `<select>` is given an `id` attribute to enable it to be associated with a `<label>` for accessibility purposes, as well as a `name` attribute to represent the name of the associated data point submitted to the server
- Each `<option>` element should have a `value` attribute containing the data value to submit to the server when that option is selected. 
  - If no `value` attribute is included, the value defaults to the text contained inside the element. 
  - You can include a `selected` attribute on an `<option>` element to make it selected by default when the page first loads.
  - You can further nest `<option>` elements inside `<optgroup>` elements to create separate groups of options inside the dropdown.
- The `<select>` element is notoriously difficult to style productively with CSS. 
  - However, these properties don't produce a consistent result across browsers, 
  - and it is hard to do things like line different types of form element up with one another in a column
- The `<select>` element's internal structure is complex, and hard to control. 
  - If you want to get full control, you should consider using a library with good facilities for styling form widgets, or try rolling your own dropdown menu using non-semantic elements, JavaScript, and WAI-ARIA to provide semantics.
- react相关
  - The `selected` attribute is supported by `<option>` components. 
    - You can use it to set whether the component is selected. 
    - This is useful for building controlled components.
  - With a controlled component, the input’s value is always driven by the React state. While this means you have to type a bit more code, you can now pass the value to other UI elements too, or reset it from other event handlers.
  - React, instead of using the `selected` attribute, uses a `value` attribute on the root `select` tag.
  - Overall, this makes it so that `<input type="text">` `<textarea>` , and `<select>` all work very similarly - they all accept `value` and `onChange` attribute that you can use to implement a controlled component.
  - You can pass an array into the `value` attribute, allowing you to select multiple options in a `select` tag

## `<datalist>` 主流浏览器都支持

- `<datalist>` element contains a set of `<option>` elements that represent the permissible or recommended options available to choose from within other controls.

``` HTML
<label for="ice-cream-choice">Choose a flavor:</label>
<input list="ice-cream-flavors" id="ice-cream-choice" name="ice-cream-choice" />

<datalist id="ice-cream-flavors">
  <option value="Chocolate">
  <option value="Coconut">
  <option value="Mint">
  <option value="Strawberry">
  <option value="Vanilla">
</datalist>
```

# br: The Line Break element

- The HTML `<br>` element produces a line break in text (carriage-return). 
-  Do not use `<br>` to create margins between paragraphs; 
  - wrap them in `<p>` elements and use the CSS `margin` property to control their size.
- The `<br>` element has a single, well-defined purpose — to create a line break in a block of text. 
- As such, it has no dimensions or visual output of its own
- You can set a margin on `<br>` elements themselves to increase the spacing between the lines of text in the block, but this is a bad practice — you should use the `line-height` property that was designed for that purpose.

# `<a>` : The Anchor element

- The HTML `<a>` element (or anchor element), with its href attribute, creates a hyperlink to web pages, files, email addresses, locations in the same page, or anything else a URL can address. 
- Content within each `<a>` should indicate the link's destination.
- `<link>` is similar to `<a>` , but for metadata hyperlinks that are invisible to users.

``` CSS
/* a标签默认样式,color默认蓝色 */
a {
  color: -webkit-link;
  cursor: pointer;
  text-decoration: underline;
}
```

# details

- The HTML Details Element ( `<details>` ) creates a disclosure widget in which information is visible only when the widget is toggled into an "open" state. 
- A summary or label can be provided using the `<summary>` element.
- A disclosure widget is typically presented onscreen using a small triangle which rotates (or twists) to indicate open/closed status, with a label next to the triangle. 
- If the first child of the `<details>` element is a `<summary>` , the contents of the `<summary>` element are used as the label for the disclosure widget.
- A `<details>` widget can be in one of two states. 
- The default closed state displays only the triangle and the label inside `<summary>` (or a user agent-defined default string if no `<summary>` ). 
  - the browser has a default summary string (usually "Details")
- When the user clicks on the widget or focuses it then presses the space bar, it "twists" open, revealing its contents
- By default when closed, the widget is only tall enough to display the disclosure triangle and summary. When open, it expands to display the details contained within.
- Fully standards-compliant implementations automatically apply the CSS `display: list-item` to the `<summary>` element. 

- A `<summary>` element may only be used as the first child of a `<details>` element. 
  - When the user clicks on the summary, the parent `<details>` element is toggled open or closed, and then a toggle event is sent to the `<details>` element, which can be used to let you know when this state change occurs.

# time

- represents a specific period in time. 
- It may include the `datetime` attribute to translate dates into machine-readable format, allowing for better search engine results or custom features such as reminders.
- It may represent one of the following:
  - A time on a 24-hour clock.
  - A precise date (with optional time and timezone info).
  - A valid time duration.

# blockquote

- cite属性
  - 该属性可能会对搜索引擎有用
  - 也可以便于其他应用程序获取引用文本内容的来源信息；

# img

- The HTML `<img>` element embeds an image into the document.
- [guide to image formats supported by web browsers](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)
  - 支持的类型有 jpg, png, svg, gif, tif, webp

# iframe

- The HTML Inline Frame element ( `<iframe>` ) represents a nested browsing context, embedding another HTML page into the current one.
- Each embedded browsing context has its own `session history` and `document` . 
- The browsing context that embeds the others is called the parent browsing context. 
- The topmost browsing context — the one with no parent — is usually the browser window, represented by the `Window` object.
- Because each browsing context is a complete document environment, every `<iframe>` in a page requires increased memory and other computing resources. 
  - While theoretically you can use as many `<iframe>` s as you like, check for performance problems.

- Inline frames, like `<frame>` elements, are included in the `window.frames` pseudo-array.
- With the DOM `HTMLIFrameElement` object, scripts can access the `window` object of the framed resource via the `contentWindow` property. 
  - The `contentDocument` property refers to the document inside the `<iframe>`, same as `contentWindow.document`.
  - From the inside of a frame, a script can get a reference to its parent window with `window.parent`
- Script access to a frame's content is subject to the same-origin policy. 
- Cross-origin communication can be achieved using `Window.postMessage()`.
- As a replaced element, the position, alignment, and scaling of the embedded document within the `<iframe>` element's box, can be adjusted with the `object-position` and `object-fit` properties.

# frame

- `<frame>` is an HTML element which defines a particular area in which another HTML document can be displayed. 
- A frame should be used within a `<frameset>` .
- Using the `<frame>` element is not encouraged because of certain disadvantages such as performance problems and lack of accessibility for users with screen readers. 
- Instead of the `<frame>` element,  `<iframe>` may be preferred.

# object

- The HTML `<object>` element represents an external resource, which can be treated as an image, a nested browsing context, or a resource to be handled by a plugin.
- `data`
  - The address of the resource as a valid URL. 
  - At least one of data and type must be defined.
- `type`
  - The content type of the resource specified by `data` . 
  - At least one of data and type must be defined.

``` HTML
<!-- Embed a flash movie -->
<object data="movie.swf" type="application/x-shockwave-flash"></object>

<!-- Embed a flash movie with parameters -->
<object data="movie.swf" type="application/x-shockwave-flash">
  <param name="foo" value="bar">
</object>
```

# elements-misc

- The HTML `<pre>` element represents preformatted text which is to be presented exactly as written in the HTML file. 
- The text is typically rendered using a non-proportional ("monospace") font. 
- Whitespace inside this element is displayed as written.

- The HTML Abbreviation element ( `<abbr>` ) represents an abbreviation or acronym; 
  - the optional `title` attribute can provide an expansion or description for the abbreviation. 
  - If present, title must contain this full description and nothing else.
