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
- https://github.com/niklasvh/html2canvas /ts
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
  - Fork from `dom-to-image` with more maintainable code and some new features.

- https://github.com/rsify/pico /ts
  - Pico's goal is to produce high precision screenshots of any viewport entirely client side.
  - This is different from simply capturing a webpage using Puppeteer or a similar tool in that the screenshot taking happens entirely client side.
  - how it works
    - This program renders whatever is displayed in the given Window into an image, thanks to svg's `<foreignObject>`.
    - **No server side code is required to produce the screenshot**.

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

## capture-utils

- https://github.com/likaia/js-screen-shot /ts
  - web端自定义截屏插件(原生JS版)
  - 支持electron环境下使用插件

- https://github.com/xataio/screenshot /ts
  - zero-dependency browser-native way to take screenshots powered by the native web MediaDevices API.

- https://github.com/sindresorhus/pageres
  - Capture screenshots of websites in various resolutions. 
  - It can also be used to render SVG images.
  - 基于puppeter

- https://github.com/premieroctet/screen-guru
  - Take clean screenshot of any websites
  - 基于puppeter

- https://github.com/flowko/website-shot /vue
  - 基于puppeter
# screenshot-browser-extensions
- https://github.com/Chromo-lib/screenshot /202210/js
  - Screenshot tool for making a full page or partial screen capture with further edit, download.
  - 只支持firefox和edge，不支持chrome
  - built with Chrome DevTools Protocol 

- note-it /16Star/Apache2/202208/ts/tiptap
  - https://github.com/MuhametSmaili/note-it
  - 支持截图及批注
  - NoteIt is a feature-packed, note-taking extension with OCR support for chrome.
  - 依赖React、Tiptap、tesseract.js、pdfmake、html-to-pdfmake
  - You can take notes, convert images to text, download notes to pdf, and more.

- https://github.com/felixfbecker/svg-screenshots /726Star/MIT/202105/ts
  - Browser extension to take scalable, semantic, accessible screenshots of websites in SVG format.
  - The SVG will not run any JavaScript.
  - 截图某些动态元素时，可能会变颜色
  - 依赖dom-to-svg、svgo
  - https://github.com/felixfbecker/dom-to-svg

- https://github.com/lxieyang/screenshot-extension /202011/ts
  - browser extension that takes full-page or partial screenshots!
  - 仅截图全屏，无滚动和编辑
  - https://chrome.google.com/webstore/detail/screenshot-extension-open/hmkbkbpdnembpeadgpcmjekihjmckdjh

- https://github.com/mrcoles/full-page-screen-capture-chrome-extension /js
  - Go FullPage
  - takes a screen capture of a full web page.
  - 提供了付费版-未开源

- https://github.com/timii/Snapper /202207/js
  - An easy-to-use extension for taking screenshots in your browser

- https://github.com/simov/screenshot-capture /202212/js/功能简单
  - Screenshot Capture / Browser Extension
  - https://chrome.google.com/webstore/detail/screenshot-capture/giabbpobpebjfegnpcclkocepcgockkc

- https://github.com/Aminadav/1click-webpage-screenshot /201902/js/功能丰富
  - Entire page Screenshot extension for Google Chrome
  - Annotate it with rectangles, circles, arrows, lines and text.

- https://github.com/folletto/Blipshot /202108/js
  - simple one-click full-page screenshots with drag and drop.
  - [This plugin isn't in development anymore](https://github.com/folletto/Blipshot/issues/28)

- https://github.com/ashrene-roy/blackboard /202107/js
  - annotate webpages, capture and save full page screenshots

- https://github.com/CamilleCharp/browsershot
  - take a screenshot and put it in a browser-like window, it is inspired by code-snapshot on VsCode.
  - Use the chrome extension api to capture the tab and html2canvas to download the final image.

- https://github.com/balduvian/ebetshot
  - A video screenshot extension for Chrome.

- https://github.com/williamemir/driveshot
  - takes screenshots and uploads to google drive, only for testing of manifest v3 

- web-clipper /4.7kStar/GPLv2/202208/ts
  - https://github.com/webclipper/web-clipper
  - https://clipper.website/
  - use Web Clipper to save anything on the web to anywhere.
  - 支持收藏链接、选区文字
  - 支持
    - flowus、wolai、语雀、有道、flomo
    - notion、github、onenote、joplin
  - https://chrome.google.com/webstore/detail/web-clipper/mhfbofiokmppgdliakminbgdgcmbhbac
# source-code-screenshot
- https://github.com/riccardoperra/codeimage /ts
  - https://codeimage.dev/
  - A tool to beautify your code screenshots. Built with SolidJS

- https://github.com/carbon-app/carbon /js
  - https://carbon.now.sh/
  - Create and share beautiful images of your source code
  - 对源码生成截图时支持多种theme

- https://github.com/Idered/chalk.ist /ts/vue
  - https://chalk.ist/
  - Create beautiful images of your source code

- https://unhtml.com/code
  - unhtml for code/markdown/picture
  - https://unhtml.404.ms/code

- https://ray.so/
  - code screenshot

## vscode

- https://github.com/jeffersonlicet/snipped /ts
  - Save SVG or PNG screenshots of code selection or all lines of your file.

- https://github.com/kufii/CodeSnap /js
  - Take beautiful screenshots of your code in VS Code

- https://github.com/octref/polacode /js
  - Polaroid for your code
  - Resize the snippet / container by dragging the lowerright corner
# more
- https://github.com/antfu/broz
  - A simple, frameless browser for screenshots
