---
title: docs-web-html-elements-dom
tags: [docs, dom, html, web]
favorited: true
created: '2020-07-17T09:39:12.042Z'
modified: '2020-07-17T09:49:09.076Z'
---

# docs-web-html-elements-dom

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
