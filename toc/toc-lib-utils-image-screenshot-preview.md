---
title: toc-lib-utils-image-screenshot-preview
tags: [image, preview, screenshot, toc, utils]
created: 2021-01-30T15:35:07.367Z
modified: 2023-04-16T13:34:33.706Z
---

# toc-lib-utils-image-screenshot-preview
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

- https://github.com/rsify/pico /ts
  - Pico's goal is to produce high precision screenshots of any viewport entirely client side.
  - This is different from simply capturing a webpage using Puppeteer or a similar tool in that the screenshot taking happens entirely client side.
  - how it works
    - This program renders whatever is displayed in the given Window into an image, thanks to svg's `<foreignObject>`.
    - No server side code is required to produce the screenshot.

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
# page-screenshot-browser-extensions
- https://github.com/mrcoles/full-page-screen-capture-chrome-extension
  - Go FullPage
  - takes a screen capture of a full web page.

- note-it /16Star/Apache2/202208/ts/tiptap
  - https://github.com/MuhametSmaili/note-it
  - 支持截图及批注
  - NoteIt is a feature-packed, note-taking extension with OCR support for chrome.
  - 依赖React、Tiptap、tesseract.js、pdfmake、html-to-pdfmake
  - You can take notes, convert images to text, download notes to pdf, and more.

- https://github.com/lxieyang/screenshot-extension /202011/ts
  - browser extension that takes full-page or partial screenshots!
  - 仅截图全屏，无滚动和编辑

- https://github.com/Chromo-lib/screenshot-fullpage-extension /202210/js
  - Screenshot tool for making a full page or partial screen capture with further edit, download.
  - 只支持firefox和edge，不支持chrome
  - built with Chrome DevTools Protocol 

- https://github.com/timii/Snapper /202207/js
  - An easy-to-use extension for taking screenshots in your browser

- https://github.com/Aminadav/1click-webpage-screenshot /201902/js
  - Entire page Screenshot extension for Google Chrome
  - Annotate it with rectangles, circles, arrows, lines and text.

- https://github.com/folletto/Blipshot /202108/js
  - simple one-click full-page screenshots with drag and drop.

- https://github.com/ashrene-roy/blackboard /202107/js
  - annotate webpages, capture and save full page screenshots

- https://github.com/felixfbecker/svg-screenshots
  - Browser extension to take scalable, semantic, accessible screenshots of websites in SVG format.
  - The SVG will not run any JavaScript.
  - 截图某些动态元素时，可能会变颜色

- https://github.com/simov/screenshot-capture /202012/js
  - Screenshot Capture / Browser Extension

- https://github.com/CamilleCharp/browsershot
  - take a screenshot and put it in a browser-like window, it is inspired by code-snapshot on VsCode.
  - Use the chrome extension api to capture the tab and html2canvas to download the final image.

- https://github.com/balduvian/ebetshot
  - A video screenshot extension for Chrome.

- https://github.com/williamemir/driveshot
  - takes screenshots and uploads to google drive, only for testing of manifest v3 

## screenshot-for-vscode

- https://github.com/jeffersonlicet/snipped
  - Save SVG or PNG screenshots of code selection or all lines of your file.

- https://github.com/kufii/CodeSnap
  - Take beautiful screenshots of your code in VS Code
# source-code-screenshot
- https://github.com/carbon-app/carbon
  - https://carbon.now.sh/
  - Create and share beautiful images of your source code
  - 对源码生成截图时支持多种theme

- https://unhtml.com/code
  - unhtml for code/markdown/picture
  - https://unhtml.404.ms/code

- https://ray.so/
  - code screenshot

- https://github.com/Idered/chalk.ist
  - https://chalk.ist/
  - Create beautiful images of your source code
# more
- https://github.com/antfu/broz
  - A simple, frameless browser for screenshots