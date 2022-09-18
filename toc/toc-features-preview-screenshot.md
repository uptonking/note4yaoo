---
title: toc-features-preview-screenshot
tags: [features, preview, screenshot, toc]
created: 2021-01-30T15:35:07.367Z
modified: 2021-01-30T16:05:48.466Z
---

# toc-features-preview-screenshot
- guide
  - preview实时预览更适合直接展示dom，支持动态交互
  - screenshot更适合静态内容
# react-comp-screenshot
- https://github.com/fayeed/use-screenshot
  - https://use-screenshot.now.sh/
  - React hook to take screenshot for React components.
  - 依赖 html-to-image
- https://github.com/salman-monetate/react-component-export-image
  - https://codesandbox.io/s/nostalgic-poincare-7xfrl?file=/src/App.js
  - Export component as jpeg, png or pdf
  - 依赖html2Canvas、jspdf
# js-screenshot
- https://github.com/niklasvh/html2canvas
  - https://html2canvas.hertzen.com/
  - Screenshots with JavaScript
  - The script allows you to take "screenshots" of webpages or parts of it, directly on the users browser.
  - how it works
    - The script renders the current page as a canvas image, by reading the DOM and the different styles applied to the elements.
    - It does not require any rendering from the server, as the whole image is created on the client's browser. 
    - However, as it is heavily dependent on the browser, this library is not suitable to be used in nodejs.
    - The html2canvas library utilizes Promises and expects them to be available in the global context. 
- https://github.com/johnnywang1994/jsPDF-html2canvas
  - A combine usage with jsPDF & html2canvas, which translating html content to PDF file.

- https://github.com/bubkoo/html-to-image /540Star/MIT/202101/ts
  - Generates an image from a DOM node using HTML5 canvas and SVG.
  - Fork from dom-to-image with more maintainable code and some new features.

- https://github.com/tsayen/dom-to-image /7kStar/201706
  - turn arbitrary DOM node into a vector (SVG) or raster (PNG or JPEG) image, written in JavaScript.
  - It's based on domvas
- https://github.com/pbakaus/domvas /370Star/201307
  - Domvas implements the missing piece that connects the DOM and Canvas.
  - It gives to the ability to take arbitrary DOM content and paint it to a Canvas of your choice.
  - how it works
    - Domvas uses a feature of SVG that allows you to embed XHTML content into the SVG 
    - the actual SVG can be used as a data uri, and therefore behaves like a standard image.
    - I brought CSS transforms to browsers that did not have them.
      - HTML content needs to be serialized to XML, and all styles have to be inlined.
    - The DOM object is not linked, but copied 
    - Content outside the bounding box of the element will be cut of per default if painted to Canvas. Don't worry though, simply pass a more comfortable offset to the toImage function 
# source-code-screenshot
- https://github.com/carbon-app/carbon
  - https://carbon.now.sh/
  - Create and share beautiful images of your source code
  - 对源码生成截图时支持多种theme

- https://unhtml.com/code
  - unhtml for code/markdown/picture

- https://ray.so/
  - code screenshot
# more
- https://github.com/antfu/broz
  - A simple, frameless browser for screenshots
