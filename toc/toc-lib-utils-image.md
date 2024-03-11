---
title: toc-lib-utils-image
tags: [image, toc, utils]
created: 2023-04-04T22:39:34.498Z
modified: 2023-04-04T22:39:45.442Z
---

# toc-lib-utils-image

# guide

# popular
- AI位图转矢量
  - https://vectorizer.ai/
    - 利用人工智能将 JPG、PNG 等位图转成矢量 SVG 格式。先用 MidJourney 生成插图，再用这个工具转成矢量略加修改，岂不美哉。

- tui.image-editor /5.9kStar/MIT/202210/js
  - https://github.com/nhn/tui.image-editor
  - http://ui.toast.com/tui-image-editor
  - Full-featured photo image editor using canvas. 
  - 偏向图片滤镜
  - Plain JavaScript component

- glightbox /1.6kStar/MIT/202203/js/inactive
  - https://github.com/biati-digital/glightbox
  - https://biati-digital.github.io/glightbox/
  - Pure Javascript lightbox with mobile support. 
  - It can handle images, videos with autoplay, inline content and iframes
  - All the animations are created with CSS and only the transform and opacity properties are animated. 

- https://github.com/jimp-dev/jimp
  - An image processing library written entirely in JavaScript for Node, with zero external or native dependencies.

- https://github.com/cozmo/jsQR
  - A pure javascript QR code reading library. 
  - This library takes in raw images and will locate, extract and parse any QR code found within.

- https://github.com/ailon/markerjs2 /ts
  - https://markerjs.com/
  - Add image annotation to your web apps.
  - 效果类似在图片上的画板批注层
  - Linkware license for v2; MIT for v1
  - https://github.com/ailon/markerjs
# image-viewer
- https://github.com/xiaolin/react-image-gallery /js
  - http://linxtion.com/demo/react-image-gallery
  - carousel image gallery component with thumbnail support

- https://github.com/dimsemenov/PhotoSwipe /js
  - https://photoswipe.com/
  - JavaScript image gallery for mobile and desktop, modular, framework independent

- https://github.com/rpearce/react-medium-image-zoom /ts
  - https://rpearce.github.io/react-medium-image-zoom/
  - The original medium.com-inspired image zooming library for React.
  - 支持 img/picture/svg

- https://github.com/francoischalifour/medium-zoom /js
  - https://medium-zoom.francoischalifour.com/
  - JavaScript library for zooming images like Medium
  - Pluggable — add your own features to the zoom

## crop

- https://github.com/DominicTobias/react-image-crop
  - An image cropping tool for React with no dependencies.

- https://github.com/jwagner/smartcrop.js /js
  - Content aware image cropping
  - Smartcrop.js implements an algorithm to find good crops for images. It can be used in the browser, in node or via a CLI.

- https://github.com/fengyuanchen/cropperjs /js
  - JavaScript image cropper.
# iiif-spec
- https://github.com/UniversalViewer/universalviewer /MIT/202311/ts
  - http://universalviewer.io/
  - http://universalviewer.io/examples/#?c=&m=&s=&cv=&manifest=https%3A%2F%2Fedsilv.github.io%2Fbiiif-workshop%2Fcollection%2Findex.json
  - a community-developed open source project on a mission to help you share your content with the world
  - 由多个子项目组成，包括 OpenSeadragon

- https://github.com/DDMAL/diva.js /js
  - http://ddmal.github.io/diva.js
  - IIIF-compatible document image viewer
  - Diva.js (Document Image Viewer with AJAX) is a JavaScript book image viewer designed to present multi-page documents at multiple resolutions.
  - Compatibility with IIIF Presentation API version 2.1 and 3.

- https://github.com/IIIF-Commons/biiif /ts
  - Organise your files according to a simple naming convention to generate IIIF Presentation API json using nodejs (Dat and IPFS compatible)
  - Organise your files according to a simple naming convention to generate IIIF content/data using 100% node.js! IPFS compatible.
  - This uses the IIIF Presentation API v3, and is compatible with the Universal Viewer v3.
  - biiif will automatically generate IIIF image tiles for any image it finds and put them in a +tiles directory, along with an associated info.json
  - https://github.com/edsilv/biiif-workshop
    - Learn how to use biiif to generate IIIF data from static files and host it on github pages.

- https://github.com/jbaiter/pdiiif /ts/svelte
  - https://pdiiif.jbaiter.de/
  - a JavaScript library to create PDFs from IIIF Manifests, completely client-side (with server-based fallback for unsupported browsers)
  -  PDF Page for every single-image Canvas in a Manifest

- https://github.com/glenrobson/SimpleAnnotationServer /js/java
  - This is an Annotation Server which is compatible with IIIF and Mirador
  - This Annotation Server includes a copy of Mirador so you can get started creating annotations straight away. 
  - The annotations are stored as linked data in an Apache Jena triple store by default. 
  - It is also possible to store the annotations in SOLR.
  - Now supports IIIF Search API in both the Universal Viewer and Mirador
# image-upload
- https://github.com/charlzyx/rush
  - 图片压缩 & 直传图床工具
  - 拖拽批量压缩图片, 支持格式 jpg/png/gif
  - 拖拽批量上传图片到对象存储, 并默认开启图片压缩
  - 支持 阿里云 OSS、 腾讯云 COS、 七牛云 Qiniu、 Github

- https://github.com/elninotech/uppload /MIT/202308/ts
  - https://uppload.js.org/
  - JavaScript image uploader and editor, no backend required
  - It's highly customizable with 30+ plugins
# images-utils
- https://github.com/TonySpegel/image-comparison /lit
  - Compare two images using a slider, an overlay, or a side by side split view.
  - This webcomponent follows the open-wc recommendation

- OpenSeadragon /2.1kStar/BSD/202304/js
  - https://github.com/openseadragon/openseadragon
  - http://openseadragon.github.io/
  - web-based viewer for high-resolution zoomable images, implemented in pure JavaScript, for desktop and mobile.
  - Supported Tile Sources: legacy image pyramids, osm, tms, iiif

- https://github.com/wojtekmaj/react-pdf /js
  - Display PDFs in your React app as easily as if they were images.
  - For React-PDF to work,  `PDF.js` worker needs to be provided.

- https://github.com/vercel/satori /ts
  - Enlightened library to convert HTML and CSS to SVG
  - What if there’s a `<Satori>` component that adds fluid layout & style transitions to your elements?
  - https://github.com/natemoo-re/satori-html
    - satori is built on top of React's JSX and expects "React-elements-like objects". 
    - This library (satori-html) bridges that gap, generating the necessary VDOM object from a string of HTML.
    - Please use inline styles rather than class-based styling

- https://github.com/imgly/background-removal-js /GPLv3/ts
  - Remove backgrounds from images directly in the browser environment with ease and no additional costs or privacy concerns

## annotation/labelling

- mirador /400Star/Apache2/202105/js
  - https://github.com/projectmirador/mirador
  - https://projectmirador.org/
  - https://mirador-dev.netlify.app/__tests__/integration/mirador/
  - web based, multi-window image viewing platform with the ability to zoom, display, compare and annotate

- https://github.com/ZitySpace/react-annotate /ts
  - https://react-annotate-demo.vercel.app/
  - React component for computer vision dataset annotation
  - 依赖fabric、react-draggable、use-gesture

- https://github.com/labelflow/labelflow /ts
  - https://labelflow.ai/
  - an open platform for image labeling. 
# codec
- https://github.com/GoogleChromeLabs/squoosh /apache2/202401/ts
  - https://squoosh.app/
  - Make images smaller using best-in-class codecs, right in the browser.
  - Squoosh does not send your image to a server. All image compression processes locally.

- https://github.com/nodeca/pica /202201/js
  - http://nodeca.github.io/pica/demo/
  - Resize image in browser with high quality and high speed

- https://github.com/Donaldcwl/browser-image-compression /202303/js
  - Javascript module to be run in the web browser for image compression.

- https://github.com/imgix/imgix.js /202310/js
  - https://imgix.com/
  - a dependency-free JavaScript library for the browser that allows for easy integration of imgix into websites.

- https://github.com/MattKetmo/darkroomjs /201512/js
  - Extensible image editing tool in your browser
# gif/animated
- https://github.com/yahoo/gifshot
  - JavaScript library that can create animated GIFs from media streams, videos, or images.
# ps-online
- https://github.com/photopea/photopea
  - Photopea is not fully open-source
- https://github.com/sclang007/Open-Photopea /201811/js/inactive
  - Photopea is the best Photoshop alternative. Their program runs as a web app. Photopea is capable of running PSD, XCF and Sketch files.
  - Photopea is a closed source software. So I decide to extract the code and Open Source it, but if they ask me to remove it I will be 100% fine with their decition.
- https://github.com/vikdevelop/photopea_app
  - Photopea Desktop App for Flatpak (Electron + WebKitGTK wrapper)

- https://github.com/viliusle/miniPaint /js/Photoshop-alternative
  - http://viliusle.github.io/miniPaint/
  - Online image editor lets you create, edit images using HTML5 technologies.
  - miniPaint operates directly in the browser. Nothing will be sent to any server.

- https://github.com/iyadahmed/AwesomeImageEditor3 /python
  - open-source, user friendly and high-performance image editor made from scratch with Python and Qt
# image-tiles/lod
- https://github.com/EddieMachete/em-ui-quadrant
  - Quadrant is a tile based, JavaScript web component which allows viewing an image in different levels of detail while optimizing the download process. 
  - Quadrant is based on my interpretation of Google Maps applied to image viewing over the web.
# image/cover-generator
- https://github.com/PJijin/Cover-Image-Generator /js
  - Generate a cover image for your blog post online.

- https://github.com/daveearley/screenshot.rocks /ts
  - Screenshot.rocks is an online tool which allows you to create beautiful mobile & browser mockups from screenshots.
  - https://chrome.google.com/webstore/detail/screenshotrocks-one-click/oolmphedpohnagciifbnfpemadolahki
# ocr
- https://github.com/naptha/tesseract.js /js
  - a javascript library that gets words in almost any language out of images.

- https://github.com/jbaiter/ocr-parser /MIT/202309/ts
  - This library provides a simple interface to parse OCR data from a stream, buffer or string. 
  - It does not rely on any DOM APIs and can therefore be used in contexts where there is no built-in support for XML parsing, most notably in Web Workers and Service Workers.
  - Currently the library supports hOCR and ALTO OCR markup.

## ocr-apps

- https://github.com/hiroi-sora/Umi-OCR /MIT/202403/python/qml
  - 开源、免费的离线OCR软件。
  - 支持截屏/批量导入图片，PDF文档识别，排除水印/页眉页脚，扫描/生成二维码。内置多国语言库。
# more
- https://github.com/ascorbic/unpic-img
  - This library uses unpic to detect the image CDN, and then uses the CDN's URL API to resize and format images. 
  - It then generates the correct srcset and sizes attributes for the image. 
  - It uses new features built into modern browsers to handle lazy loading, fetch priority and decoding. 
  - It also uses pure CSS to handle responsive resizing of images, preserving aspect ratio and avoiding layout shift.
  - Unlike most other image components, it does not use any client-side JavaScript by default, and generates just a single `<img>` tag without any wrapper divs or padding elements.

- https://github.com/jiechud/fast-image-editor
  - 一款开源图片编辑器，采用React + Typescript + React-knova 框架开发.

- lazy-loaded images need all the CSS to be loaded before it can decide if the image is needed. 
  - https://twitter.com/tunetheweb/status/1664224241879769089
  - If you add `loading=lazy` to an `<img>` the browser won’t load the image until it KNOWS it needs it. 
  - It can’t know it needs it until it’s got all the CSS and completed the page layout. 
  - So don’t use it unless it’s going to be off screen. 
  - Particularly don’t use on LCP images.
