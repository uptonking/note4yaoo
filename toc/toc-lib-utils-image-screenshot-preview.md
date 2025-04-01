---
title: toc-lib-utils-image-screenshot-preview
tags: [image, preview, screenshot, toc, utils]
created: 2021-01-30T15:35:07.367Z
modified: 2023-04-16T13:34:33.706Z
---

# toc-lib-utils-image-screenshot-preview

# guide

- 基于`getDisplayMedia`的方案
  - 优点是主流pc浏览器都支持，移动端浏览器不支持
  - 缺点是会提醒用户选择tab/screen，截图体验不好

- tips
  - 在macos上，html2canvas的截图效果似乎比modern-screenshot要好
  - screenshot更适合静态内容
  - preview实时预览更适合直接展示dom，支持动态交互
# react-comp-screenshot
- https://github.com/fayeed/use-screenshot
  - https://use-screenshot.now.sh/
  - React hook to take screenshot for React components.
  - 依赖 html-to-image
- https://github.com/salman-monetate/react-component-export-image
  - https://codesandbox.io/s/nostalgic-poincare-7xfrl?file=/src/App.js
  - Export component as jpeg, png or pdf
  - 依赖html2Canvas、jspdf
# dom-screenshot
- https://github.com/niklasvh/html2canvas /30.8kStar/MIT/202201/ts/inactive
  - https://html2canvas.hertzen.com/
  - Screenshots with JavaScript
  - The script allows you to take "screenshots" of webpages or parts of it, directly on the users browser.
  - `html2canvas(element[, options])` 支持截图部分元素，🌹 且截图样式稳定
  - html2canvas支持非browser环境，数据源可以是json而无需打开页面
  - ❓ 对于无需交互的场景，html2canvas的速度是否比cloneNode更快
    - cloneNode在改变dom位置/层级/结构时，样式很可能会混乱
    - You may retrieve the current layout of every element using  getComputedStyle and apply it to the cloned elements
  - how it works
    - The script renders the current page as a canvas image, by reading the DOM and the different styles applied to the elements.
    - It does not require any rendering from the server, as the whole image is created on the client's browser. 
    - However, as it is heavily dependent on the browser, this library is not suitable to be used in nodejs.
    - The html2canvas library utilizes Promises and expects them to be available in the global context. 
  - 🍴 forks
  - https://github.com/html2canvas/html2canvas /202407/ts
    - a fork of niklasvh/html2canvas
  - https://github.com/cantoo-scribe/html2canvas
- https://github.com/johnnywang1994/jsPDF-html2canvas
  - A combine usage with jsPDF & html2canvas, which translating html content to PDF file.

- https://github.com/rsify/pico /2kStar/MIT/202004/ts/inactive
  - Pico's goal is to produce high precision screenshots of any viewport entirely client side.
  - This is different from simply capturing a webpage using Puppeteer or a similar tool in that the **screenshot taking happens entirely client side**.
  - This program renders whatever is displayed in the given `Window` into an image, thanks to svg's `<foreignObject>`.
  - **No server side code is required to produce the screenshot**.
  - Render the given `Window` to a PNG image and return it as an object URL.
  - Pico's selling point is representing the whole viewport as accurately as possible. If you want to render a single DOM node instead, consider using one of the above libraries.
  - Pico is built using `Fluture` and in addition to the Promise also provides a direct API to Fluture via functions suffixed with Fluture

- https://github.com/bubkoo/html-to-image /5.9kStar/MIT/202301/ts/inactive
  - Generates an image from a DOM node using HTML5 canvas and SVG.
  - Fork from `dom-to-image` with more maintainable code and some new features.

- https://github.com/1904labs/dom-to-image-more /526Star/MIT/202410/js/cpp
  - a library which can turn arbitrary DOM node, including same origin and blob iframes, into a vector (SVG) or raster (PNG or JPEG) image, written in JavaScript.
  - Anatolii's version was based on domvas by Paul Bakaus and has been completely rewritten
  - This fork of `dom-to-image`

- https://github.com/tsayen/dom-to-image /10.4kStar/MIT/201706/js/inactive
  - turn arbitrary DOM node into a vector (SVG) or raster (PNG or JPEG) image, written in JavaScript.
  - It's based on domvas
- https://github.com/pbakaus/domvas /370Star/MIT/201307/js/inactive
  - Domvas implements the missing piece that connects the DOM and Canvas.
  - It gives to the ability to take arbitrary DOM content and paint it to a Canvas of your choice.
  - Domvas uses a feature of SVG that allows you to embed XHTML content into the SVG 
  - the actual SVG can be used as a data uri, and therefore behaves like a standard image.
  - I brought CSS transforms to browsers that did not have them.
    - HTML content needs to be serialized to XML, and all styles have to be inlined.
  - The DOM object is not linked, but copied 
  - Content outside the bounding box of the element will be cut of per default if painted to Canvas. Don't worry though, simply pass a more comfortable offset to the toImage function

- https://github.com/cburgmer/rasterizeHTML.js /2.5kStar/MIT/202201/js/inactive
  - http://cburgmer.github.io/rasterizeHTML.js
  - Renders HTML into the browser's canvas
  - it is possible by embedding the HTML into an SVG image as a `<foreignObject>` and then drawing the resulting image via `ctx.drawImage()`.
  - SVG is not allowed to link to external resources and so rasterizeHTML.js will load external images, fonts and stylesheets and store them inline via data: URIs (or inline style elements respectively).

## capture-utils

- https://github.com/likaia/js-screen-shot /MIT/202401/ts
  - https://www.kaisir.cn/js-screen-shot/
  - web端自定义截屏插件(原生JS版)
  - 支持electron环境下使用插件

- https://github.com/xataio/screenshot /MIT/202202/ts/inactive
  - zero-dependency browser-native way to take screenshots powered by the native web MediaDevices API.

- https://github.com/sindresorhus/pageres /MIT/202311/ts
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
- https://github.com/riccardoperra/codeimage /MIT/202405/ts
  - https://codeimage.dev/
  - A tool to beautify your code screenshots. Built with SolidJS
  - SSG+Partial hydration
  - a fork of html-to-image
  - https://x.com/riccardoperra0/status/1603412081054810112
    - lazy load @codemirror and motion without blocking rendering and losing performance.

- https://github.com/carbon-app/carbon /MIT/202403/js
  - https://carbon.now.sh/
  - Create and share beautiful images of your source code
  - 对源码生成截图时支持多种theme
  - 依赖codemirror5、puppeteer-core、morphmorph

- https://github.com/raycast/ray-so /MIT/202407/ts
  - https://ray.so/
  - Create code snippets, browse AI prompts, create extension icons and more.
  - Code Images: Create beautiful images of your code.
  - Snippet Explorer: Browse and import Raycast Snippets.
  - Built with @nextjs , @tailwindcss , @dubdotco and obviously @radix_ui

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
# google-photos-like
- https://github.com/ente-io/ente /AGPLv3/202403/ts/dart
  - https://ente.io/
  - open source, End to End Encrypted alternative to Google Photos and Apple Photos
  - Ente is a service that provides a fully open source, end-to-end encrypted platform for you to store your data in the cloud without needing to trust the service provider. 
  - On top of this platform, we have built two apps so far: Ente Photos and Ente Auth
  - This monorepo contains all our source code - the client apps (iOS / Android / F-Droid / Web / Linux / macOS / Windows) for both the products, and the server 
  - Ente Photos is a paid service, but we offer a free trial. You can also clone this repository and choose to self host.
  - Two years ago, while building Ente Photos, we realized that there was no open source end-to-end encrypted authenticator app. We already had the building blocks, so we built one.

- https://github.com/gavinfitch/Pixel /202312/js/inactive
  - a photo-sharing application built on PostgreSQL, Express.js, React, and Redux
  - Logged in users can upload, view, edit, and delete photos. They can also create, view, edit, and delete albums. 
  - heavily inspired by Flickr and is meant to be seen as a loose clone
  - 依赖express、sequelize5、PostgreSQL
  - AWS is used for all storage of user uploaded files, and the React-AWS-S3 module is used for communication between React and the S3 bucket.
  - All user files are uploaded to an S3 bucket, AWS then sends back the location of the files to the backend, where they are stored, along with any other relevant information

- https://github.com/mustafaomousa/Rumblr /202201/js
  - A full stack application clone of Tumblr, but with cars.

- https://github.com/LibrePhotos/librephotos /MIT/202402/python
  - https://demo2.librephotos.com/
  - Self hosted alternative to Google Photos
  - 依赖django4、django-chunked-upload、django-extensions、djangorestframework、flask3、Flask-RESTful、Pillow
  - django用得比flask多，flask仅在7个文件中使用
  - Support for all types of photos including raw photos
  - Timeline view
  - Scans pictures on the file system
  - Multiuser support
  - Face recognition / Face classification
  - Search by metadata; Semantic image search
# screen-recording/sharing
- https://github.com/CapSoftware/Cap /AGPLv3/202403/rust/ts
  - https://cap.so/
  - instant screen sharing. Open source and cross-platform.
  - Cap is an open source alternative to Loom. It's a video messaging tool that allows you to record, edit and share videos in seconds.
  - 依赖Rust, React (Next.js), TypeScript, Tauri, Drizzle (ORM), MySQL, TailwindCSS, Turborepo
  - Download for macOS · Windows · Linux

- https://github.com/hughfenghen/bloom-shadow /202401/ts
  - https://hughfenghen.github.io/bloom-shadow/
  - 在浏览器中运行的录屏工具，可用于视频课程制作、直播推流工作台；
  - 基于 WebAV 实现

- https://github.com/thenickdude/webm-writer-js /202110/js/inactive
  - This is a JavaScript-based WebM video encoder based on the ideas from Whammy. 
  - It allows you to turn a series of Canvas frames into a WebM video.
  - This implementation allows you to create very large video files (exceeding the size of available memory), because when running in a privileged context like a Chrome extension or Electron app, it can stream chunks immediately to a file on disk using Chrome's FileWriter while the video is being constructed, instead of needing to buffer the entire video in memory before saving can begin. 
  - Video sizes in excess of 4GB can be written. The implementation currently tops out at 32GB, but this could be extended.
# thumbnail/preview-image
- https://github.com/wei/socialify /MIT/202412/ts
  - Socialify helps you showcase your project to the world by generating a beautiful project image 
  - Social Image as a Service
# more
- https://github.com/antfu/broz
  - A simple, frameless browser for screenshots
# discuss
- ## 

- ## 

- ## Hackreels —— 代码动画制作工具 (非开源)
- https://x.com/ftium4/status/1807508945071964607
  - https://www.hackreels.com/
  - 支持多种语言和字体格式，让你的代码展示效果更炫酷。

- ## Here's a lovely trick for getting all the event handlers from a component's props.
- https://x.com/mattpocockuk/status/1804100225964855644
  - 类型示例使用代码动画展示
- [How are you doing those animations?](https://gist.github.com/mattpocock/ce7cf1d0df62c72aa3b58bb7e4e4fdce)
  - building in a private repo, based on Remotion and Code Hike
- Any reason why intersection instead of Extract?
  - Fewer characters

- ## React tip: Use a custom hook to handle array states in your components 
- https://twitter.com/_georgemoller/status/1734738304698884575
  - 代码动画效果

- ## 💫 How do you create the animations for that video? (demo source code)
- https://twitter.com/elie2222/status/1708888899685433410
- 👉🏻 Learn how to animate code (and more) using Apple Keynote by using magic move!
