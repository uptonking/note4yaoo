---
title: docs-web-html-elements-dom
tags: [docs, dom, html, web]
favorited: true
created: '2020-07-17T09:39:12.042Z'
modified: '2020-07-17T09:49:09.076Z'
---

# docs-web-html-elements-dom

## guide

- [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
  - list all the HTML elements, which are created using tags
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

## `<a>` : The Anchor element

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

## details

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

## time

- represents a specific period in time. 
- It may include the `datetime` attribute to translate dates into machine-readable format, allowing for better search engine results or custom features such as reminders.
- It may represent one of the following:
  - A time on a 24-hour clock.
  - A precise date (with optional time and timezone info).
  - A valid time duration.

## blockquote

- cite属性
  - 该属性可能会对搜索引擎有用
  - 也可以便于其他应用程序获取引用文本内容的来源信息；

## img

- The HTML `<img>` element embeds an image into the document.
- [guide to image formats supported by web browsers](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/Image_types)
  - 支持的类型有 jpg, png, svg, gif, tif, webp

## elements-misc

- The HTML `<pre>` element represents preformatted text which is to be presented exactly as written in the HTML file. 
- The text is typically rendered using a non-proportional ("monospace") font. 
- Whitespace inside this element is displayed as written.

- The HTML Abbreviation element ( `<abbr>` ) represents an abbreviation or acronym; 
  - the optional `title` attribute can provide an expansion or description for the abbreviation. 
  - If present, title must contain this full description and nothing else.
