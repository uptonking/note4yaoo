---
title: toc-lib-utils-image
tags: [image, toc, utils]
created: 2023-04-04T22:39:34.498Z
modified: 2023-04-04T22:39:45.442Z
---

# toc-lib-utils-image

# guide

- tips
  - 对image/pdf/富文本编辑器的标注，通常流行产品都会有产品自身的实现，不必执着于标准

- pdf/image/canvas-tools, 主流语言是c/js/python
  - sharp(js/cpp/apache2)-基于 libvips(c/LGPL), jimp(ts/MIT)
  - ImageMagick(c/FreeWithAttribution)
  - scikit-image(py/BSD), Pillow(MIT/py/c)
  - imgproxy(go/MIT), imaginary(go/MIT), imaging(go/MIT), imagor(go/apache2)
  - lazy-image(MIT/rs), photon(apache2/rs)
  - OpenImageIO(apache2/cpp)

- resources
  - [PIXLS. US - Free/Open Source Photography](https://pixls.us/)
    - [Software projects that make open source imaging possible](https://pixls.us/software/)
# popular
- AI位图转矢量
  - https://vectorizer.ai/
    - 利用人工智能将 JPG、PNG 等位图转成矢量 SVG 格式。先用 MidJourney 生成插图，再用这个工具转成矢量略加修改，岂不美哉。

- tui.image-editor /5.9kStar/MIT/202210/js/fabricjs/简单编辑图片
  - https://github.com/nhn/tui.image-editor
  - http://ui.toast.com/tui-image-editor
  - Full-featured photo image editor using canvas. 
  - 偏向图片滤镜
  - Plain JavaScript component
  - 🍴 forks
  - https://github.com/cocomite/tui.image-editor /202405/js/inactive
  - https://github.com/parteekmalik/tui.image-editor /202509/js
  - https://github.com/arkotik/tui.image-editor /202508/js

- https://github.com/ikuaitu/vue-fabric-editor /7.5kStar/MIT/202512/ts/vue/偏向设计软件
  - https://ikuaitu.github.io/doc/#/
  - https://ikuaitu.github.io/vue-fabric-editor/#/
  - 快图设计- 基于 fabric.js 和 Vue 开发的插件化图片编辑器，可自定义字体、素材、设计模板、右键菜单、快捷键
  - 💰 开源版本仅前端代码，付费版本提供完整的前后端、管理后台，功能完整开箱即用，提供源码授权、支持二次开发
    - 支持通过 HTTP 接口、表格文件批量生成图片。
  - core不依赖vue
  - 插件化架构：可通过插件的进行扩展开发，支持右键菜单和快捷键。
  - 拖拽式设计：以轻量、简洁为主的图形编辑器，而非大而全的在线 PS 类的重行设计工具。
  - 功能完善：PSD 解析、辅助线、历史记录、渐变、自定义字体、裁剪等功能。
  - 导入 JSON、PSD 文件
  - 导出 PNG、SVG、JSON 文件
  - 撤销/重做
  - 组合/拆分组合
  - 图层功能
  - 外观属性/字体属性/描边/阴影
  - 多元素水平、垂直对齐方式
  - [你好，可以增加ppt导入功能吗？ _202407](https://github.com/ikuaitu/vue-fabric-editor/issues/465)
    - 将PPT转为 json 然后导入到画布中
  - [小建议：能否把每一步做成时间轴  ](https://github.com/ikuaitu/vue-fabric-editor/issues/395)
    - 像PS的历史记录一样，可以回退到指定节点就好了
  - [开源图片编辑器推荐-可用于海报编辑、商品设计、封面设计、标签设计等场景 _202406](https://www.v2ex.com/t/1052550)
    - 开源图片编辑器，更像一个开源在线设计工具，可用于海报设计、图文笔记、商品设计、封面设计、标签设计、logo 设计、等场景，自定义字体、素材、设计模板、右键菜单、快捷键，还提供插件化的方式扩展二次开发 
  - [图片分层 AI 模型都开源了， 5 天 800Star，不搞一把？ - V2EX](https://www.v2ex.com/t/1180830)
    - vue-fabric-editor ！这是一个基于 Vue 和 fabric.js 开发的、功能非常完善的开源图片编辑器。
    - 它本身就有图层管理、PSD 解析、历史记录、各种滤镜等专业功能，界面友好，插件化架构，特别适合二次开发
  - 🐛 [SVG导入时不规则路径剪切问题 _202404](https://github.com/ikuaitu/vue-fabric-editor/issues/325)
    - 不规则路径剪切考虑支持吗？
    - 暂时还没计划哈
  - [前端真有意思，又干了一年图片编辑器 - V2EX _202601](https://v2ex.com/t/1183304)
  - [开源了一个 web 版图片/海报编辑器，参考稿定设计和创客贴设计 _202302](https://hk.v2ex.com/t/917129)
  - 🏠 [开源图片编辑器的插件化架构 - V2EX _202408](https://v2ex.com/t/1063993)
  - [React版本，结合AI  ](https://github.com/ikuaitu/vue-fabric-editor/issues/510)
    - 其他伙伴根据 core 方法开发了 React 版本
  - https://github.com/x007xyz/r-fabric-editor /202406/ts/inactive
    - https://x007xyz.github.io/r-fabric-editor/
    - 开源项目vue-fabric-editor的React版。核心功能已经全部实现，部分样式和功能待添加
  - https://github.com/Qiu-Jun/element-fabric-editor /MIT/202512/ts/vue
    - https://qiu-jun.github.io/element-fabric-editor/#/
    - vue-fabric-editor的element plus版本
    - 由于一个单子甲方需要ElementPlus作为组件库，因此诞生而单独维护，Element Fabric Editor功能是和vue-fabric-editor上是一致的，但在组件划分上Element Fabric Editor会更细致，因为Element Fabric Editor不考虑SDK的打包，所以在组件抽离会更细致

- https://github.com/dromara/yft-design /1.5kStar/MIT/202508/ts/vue/inactive
  - https://yft.design/
  - https://demo.yft.design/
  - 基于fabric.js的开源版【稿定设计】。一款美观且功能强大的在线设计工具，具备海报设计和图片编辑功能。
  - 历史记录（撤销、重做）
  - 导入PDF(完美还原格式，不支持图片裁切导入)
  - 导入PSD(完美还原格式，支持部分特效还原，亮度，对比度，颜色覆盖)
  - 导入SVG(不支持tspan字体)
  - 多元素组合
  - [能封装成组件形式吗类似这样，便于项目中引用 _202404](https://github.com/dromara/yft-design/issues/73)
    - 我这个项目就是基于 `pptist` 改的，看你也提交了pptist组件代码，你可以自己封装哈
  - [本项目是否还在维护，当前还存在许多问题 _202503](https://github.com/dromara/yft-design/issues/114)
    - 图层不会同步，删除或添加了素材，图层里面的元素还是一样没有变化
    - 修改后不会保存，每次刷新页面都是上一次的内容
  - [大佬绘图还有很多bug _202503](https://github.com/dromara/yft-design/issues/115)
    - 修改图层后设计会被重置
    - 👷 欢迎PR哈
  - [考虑做导出pptx的功能吗  ](https://github.com/dromara/yft-design/issues/94)

- glightbox /1.6kStar/MIT/202203/js/inactive
  - https://github.com/biati-digital/glightbox
  - https://biati-digital.github.io/glightbox/
  - Pure Javascript lightbox with mobile support. 
  - It can handle images, videos with autoplay, inline content and iframes
  - All the animations are created with CSS and only the transform and opacity properties are animated. 

- https://github.com/jimp-dev/jimp /MIT/202409/ts/NoDeps
  - http://jimp-dev.github.io/jimp/
  - An image processing library written entirely in JavaScript for Node, with zero external or native dependencies.
  - 图片格式转换, 图片裁剪/改变大小, 自定义插件  

- https://github.com/cozmo/jsQR
  - A pure javascript QR code reading library. 
  - This library takes in raw images and will locate, extract and parse any QR code found within.

- https://github.com/ailon/markerjs2 /ts
  - https://markerjs.com/
  - Add image annotation to your web apps.
  - 效果类似在图片上的画板批注层
  - Linkware license for v2; MIT for v1
  - https://github.com/ailon/markerjs

- https://github.com/CyberTimon/RapidRAW /3.8kStar/AGPL/202512/rust/ts
  - A beautiful, non-destructive, and GPU-accelerated RAW image editor built with performance in mind
  - a modern, high-performance alternative to Adobe Lightroom®. It delivers a simple, beautiful editing experience in a lightweight package (under 20MB) for Windows, macOS, and Linux.
  - rawler: For the excellent Rust crate that provides the foundation for RAW file processing in this project.
  - I developed this project as a personal challenge at the age of 18. My goal was to create a high-performance tool for my own photography workflow
    - I am immensely grateful for Google's Gemini suite of AI models. 
    - As an 18-year-old without a formal background in advanced mathematics or image science, the AI Studio's free tier was an invaluable assistant, helping me research and implement concepts like the Menon demosaicing algorithm.
  - 👾 I've designed RapidRAW's AI features with flexibility in mind. You have three ways to use them
  - Built-in AI Tools (Local & Free): These features are integrated directly into RapidRAW and run entirely on your computer. 
    - AI Masking: Instantly detect and mask subjects, skies, and foregrounds. 
    - Automatic Tagging: The image library is automatically tagged with keywords using a local CLIP model, making your photos easy to search.
    - Automatic Tagging: The image library is automatically tagged with keywords using a local CLIP model, making your photos easy to search.
  - Self-Hosted Integration with ComfyUI (Local & Free)
    - For users with a capable GPU who want maximum control, I've made it so RapidRAW can connect to your own local ComfyUI server.
    - Full Control: Use your own hardware and any custom Stable Diffusion model or workflow you choose
    - Custom Workflow Selection: Import your own ComfyUI workflows and use your custom nodes.
  - Optional Cloud Service (Subscription)
    - To be clear, I won't lock features behind a paywall. All of RapidRAW's functionality is available for free if you use the built-in tools or self-host.
    - For those who want a simpler solution, I will be offering an optional $5/month subscription (pricing is not final).
  - [I built a open-source lightweight RAW editor in 2 weeks because Lightroom felt too heavy on my machine : r/photography _202506](https://www.reddit.com/r/photography/comments/1lnj348/i_built_a_opensource_lightweight_raw_editor_in_2/)

- https://github.com/immich-app/immich /61.9kstar/AGPLv3/202503/ts/dart/svelte
  - https://immich.app/
  - High performance self-hosted photo and video management solution.
  - server依赖@nestjs/bullmq、typeorm、handlebars、kysely-postgres-js
  - 🍴 forks
  - https://github.com/EinAeffchen/Omoide /NonCommercial/202511/python/ts
    - Self‑hosted, offline‑capable photo & video library with AI features. No cloud services required. 
    - Everything runs locally after an initial one‑time model setup.

- https://github.com/hsa00000/urocissa /MIT/202601/rust/ts/vue
  - https://hsa00000.github.io/urocissa/
  - https://demo.photoserver.tw/
  - a self-hosted photos gallery designed to serve massive collections, capable of handling millions of images and videos.
  - The goal of this project is to efficiently serve one million photos on a 4 GB RAM server, providing smooth scrubbable scrolling, infinite photo streams, and instant search and selection, without waiting for the entire database to load in the browser.
  - Memory Efficient: Even with the entire database cached in memory, both the standard demo and the one-million-photo demo can run seamlessly on a single server with just 4 GB of RAM.
  - Infinite Photo Stream: Experience endless scrolling without pagination. No lazy loading needed. Urocissa uses advanced virtual scrolling to serve one million photos, overcoming the DOM height limit of 33, 554, 400px (see TanStack/virtual#616).

- https://github.com/TeaM-TL/FotoKilof /424Star/MIT/202512/python
  - GUI for ImageMagick and Wand or Pillow
  - GUI for the most used (by me) ImageMagick functionality for processing pictures. If ImageMagick or Wand are unavailable, Pillow is in use. There are small limitation, but works in general.
  - apt-get install python3-pip python3-tk python3-wand imagemagick xclip
# image-editor
- https://github.com/ximing/fabric-photo /MIT/202003/js/inactive
  - https://ximing.github.io/fabric-photo/
  - 基于 canvas 的纯前端的图片编辑器，支持方形，圆形，箭头，缩放，拖拽，鹰眼，马赛克，涂鸦，线条，导出 png，剪切等

- https://github.com/scaleflex/filerobot-image-editor /1.7kStar/202412/js/inactive
  - Edit, resize, and filter any image
  - apply basic transformations like resize, crop, flip, finetune, annotate, watermark and various filters to any image.
  - History management (Undo/Redo/Reset).
  - Image Annotating & Drawing.
  - VanillaJS + Bridged to frameworks (React & More to support...).

- https://github.com/sleepy-zone/fabritor-web /1.2kStar/MIT/202408/ts/inactive
  - https://fabritor.surge.sh/
  - 基于 fabricjs 的开源创意图片编辑器，可应用于海报设计、小红书公众号封面设计、banner 设计等场景
  - [[开源图片编辑器] 为了让图片编辑器不那么卷，我开发了 fabritor - V2EX _202403](https://www.v2ex.com/t/1023314)

- https://github.com/cshum/imagor-studio /20Star/MIT/202509/go/ts
  - https://imagor.net/
  - Self-hosted image gallery and live editing web application
  - High-performance image gallery with virtual scrolling and live editing capabilities powered by imagor.
  - Advanced image editing with real-time preview, color adjustments, effects, cropping, and instant URL generation for transformed images.
  - Mounts your Photos directory as read-only for safe access 
  - Creates persistent storage for the app database (SQLite)
  - GraphQL API with gqlgen
  - Image Processing via imagor and libvips
  - Storage abstraction (filesystem/S3)
  - TanStack Router for type-safe routing with loaders
  - shadcn/ui component library
  - GraphQL client with code generation
  - [Imagor Studio: Self-hosted image gallery and live editing web application : r/selfhosted _202509](https://www.reddit.com/r/selfhosted/comments/1nnmgnb/imagor_studio_selfhosted_image_gallery_and_live/)
  - https://github.com/cshum/imagor /3.8kStar/apache2/202509/go
    - Fast, secure image processing server and Go library, using libvips
    - imagor uses one of the most efficient image processing library libvips with Go binding vipsgen.
    - It is typically 4-8x faster than using the quickest ImageMagick 
    - imagor implements libvips streaming that facilitates parallel processing pipelines, achieving high network throughput.
    - Alongside there is imagorvideo bringing video thumbnail capability through ffmpeg C bindings.
    - https://github.com/libvips/libvips /10.7kStar/LGPL/202509/c
      - https://libvips.github.io/libvips/
      - A fast image processing library with low memory needs
      - libvips is a demand-driven, horizontally threaded image processing library
      - Compared to similar libraries, libvips runs quickly and uses little memory

- https://github.com/sahandghavidel/ai-image-editor-saas-app /202509/ts
  - https://ai-image-editor.100jsprojects.com/
  - AI Image Editor SaaS app using Next.js, Tailwind CSS, Prisma, Neon, ImageKit and Better Auth

- https://github.com/MattKetmo/darkroomjs /201512/js/inactive
  - Extensible image editing tool in your browser
  - It is based on the awesome FabricJS library to handle images in HTML5 canvas.

- https://github.com/fengzhizi715/Monica /apache2/202512/kotlin
  - Cross-platform open-source image editor with AI features, RAW support, and a modern customizable UI
  - [Monica：开源、跨平台、桌面端图像编辑软件，提供丰富的图像编辑功能 - V2EX _202506](https://www.v2ex.com/t/1136906)
    - 磕磕绊绊地做了一年多，终于做了一款桌面端的图像编辑软件 
    - 支持 JPG/PNG/WebP/SVG/HDR/HEIC/RAW(CR2/CR3)
    - 图像放大预览、图像调色、滤镜支持（含参数调节）
    - 支持多种深度学习模型：人脸识别/替换、AI 漫画风、素描生成
    - Kotlin Compose Multiplatform 写的桌面应用，macOS/Windows/Linux 都能跑
    - 可用于验证 OpenCV 算法（目前内置一些基础调参）
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

- mirador /593Star/apache2/202512/js
  - https://github.com/projectmirador/mirador
  - https://projectmirador.org/
  - https://projectmirador.org/demo/
  - https://mirador-dev.netlify.app/__tests__/integration/mirador/
  - web based, multi-window image viewing platform with the ability to zoom, display, compare and annotate
  - 偏向于图片查看，标注功能少
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

- https://github.com/hst-Sunday/tubed /202512/ts
  - 一个图床服务、文件托管服务，适合在VPS上的简单存储服务
# images-apps

# images-utils
- https://github.com/sneas/img-comparison-slider /822Star/MIT/202406/ts/inactive
  - https://img-comparison-slider.sneas.io/examples.html
  - Image comparison slider. Compare images before and after. 
  - Supports React, Vue, Angular.
  - Mobile friendly

- https://github.com/kylewetton/image-compare-viewer /583Star/MIT/202410/js/NoDeps/inactive
  - https://image-compare-viewer.netlify.com/
  - A fully responsive slider to compare before and after images for grading, retouching and all else. 
  - Mobile and fluid container friendly

- https://github.com/nerdyman/react-compare-slider /MIT/202512/ts/NoDeps
  - https://react-compare-slider.js.org/
  - A slider component to compare any two React components in landscape or portrait orientation. 
  - It supports custom images, videos... and everything else.
  - Supports responsive images and any other React components (picture, video, canvas, iframe etc.)
  - Supports landscape and portrait orientations
  - Unopinionated & fully customizable – optionally use your own components and styles

- https://github.com/tam315/react-compare-image /MIT/202507/ts/inactive
  - https://react-compare-image.yuuniworks.com/
  - React component to compare two images with a slider
  - https://github.com/tam315/vue-compare-image /archived

- https://github.com/TonySpegel/image-comparison /MIT/202304/ts/lit/inactive
  - Compare two images using a slider, an overlay, or a side by side split view.
  - This webcomponent follows the open-wc recommendation

- https://github.com/jotform/before-after.js /MIT/202203/js/inactive
  - http://www.jotform.com/formscentral/
  - before-after is now a jquery plugin

- OpenSeadragon /3.1kStar/BSD/202503/js
  - https://github.com/openseadragon/openseadragon
  - http://openseadragon.github.io/
  - web-based viewer for high-resolution zoomable images, implemented in pure JavaScript, for desktop and mobile.
  - Supported Tile Sources: legacy image pyramids, osm, tms, iiif

- https://github.com/wojtekmaj/react-pdf /js
  - Display PDFs in your React app as easily as if they were images.
  - For React-PDF to work,  `PDF.js` worker needs to be provided.

- https://github.com/vercel/satori /MPLv2/202411/ts
  - https://og-playground.vercel.app/
  - Enlightened library to convert HTML and CSS to SVG
  - ✨ 提供了支持可视化配置的playground
  - 不支持html字符串渲染和dangerouslySetInnerHTML
  - What if there’s a `<Satori>` component that adds fluid layout & style transitions to your elements?
  - [Show HN: Satori – Convert HTML and CSS to SVG | Hacker News _202210](https://news.ycombinator.com/item?id=33156130)
  - https://github.com/natemoo-re/satori-html
    - satori is built on top of React's JSX and expects "React-elements-like objects". 
    - This library (satori-html) bridges that gap, generating the necessary VDOM object from a string of HTML.
    - Please use inline styles rather than class-based styling

- https://github.com/imgly/background-removal-js /GPLv3/ts
  - Remove backgrounds from images directly in the browser environment with ease and no additional costs or privacy concerns

- https://github.com/willnguyen1312/zoom-image /MIT/202404/ts
  - https://willnguyen1312.github.io/zoom-image/
  - powerful framework agnostic headless library to zoom images on the web
  - Examples are written with Preact, React, Svelte, Vanilla JS and Vue.
# codec
- https://github.com/GoogleChromeLabs/squoosh /apache2/202401/ts
  - https://squoosh.app/
  - Make images smaller using best-in-class codecs, right in the browser.
  - Squoosh does not send your image to a server. All image compression processes locally.

- https://github.com/addyosmani/squish /MIT/202501/ts
  - https://squish.addy.ie/
  - A modern, browser-based image compression tool that leverages WebAssembly for high-performance image optimization
  - Support formats: AVIF (AV1 Image Format), JPEG (using MozJPEG), JPEG XL, PNG (using OxiPNG), WebP
  - Browser-based compression (no server uploads needed)
  - Batch processing support
  - Smart queue for compressing large number of files
  - Format conversion
  - Real-time preview
  - Drag and drop interface
  - WebAssembly for native-speed image processing
  - jSquash for image codec implementations

- https://github.com/joye61/pic-smaller /MIT/202509/ts/inactive
  - https://picsmaller.com/
  - Compress JPEG, PNG, WEBP, AVIF, SVG and GIF images intelligently
  - [唉，一年了无人问津，开源算了 - V2EX _202405](https://fast.v2ex.com/t/1041478?p=1)
    - 图小小是一个图片压缩工具，基于 Vite+React 技术栈开发，它可以完全取代类似 TinyPNG 之类的在线图片压缩工具，且压缩之后视觉表现效果往往更好。但图小小有个更大的优势：通过图小小进行图片压缩完全是基于浏览器本地的，没有任何服务端交互
    - 目前图小小支持 JPEG/PNG/WebP/Gif 四种格式的图片压缩
    - 采用了大量的第三方开源项目，所以图小小本身是没什么技术含量的，我个人认为图小小优秀在于提供了良好的 UI 和使用体验，虽然是缝合怪，但鲜有人做出类似的产品
    - JPEG/WebP 压缩：利用了现代浏览器自带的功能，叫离屏渲染技术 OffscreenCanvas
    - PNG 压缩：采用了一个第三方的 Webassembly 实现，底层是 libPNG
    - Gif 压缩：采用了一个第三方的 Webassembly 实现，底层是 Gifsicle
    - 为了防止 UI 阻塞，运用了 Web Worker 技术进行编解码和压缩，同时为了防止同一时刻浏览器的内存占用过大（内存占用过大也会导致卡顿），用了一点小技巧在 Worker 端实现了一个简单的队列 Queue，这里不展开，有兴趣的自行研究源码

- https://github.com/nodeca/pica /202201/js
  - http://nodeca.github.io/pica/demo/
  - Resize image in browser with high quality and high speed

- https://github.com/Donaldcwl/browser-image-compression /202303/js
  - Javascript module to be run in the web browser for image compression.

- https://github.com/imgix/imgix.js /202310/js
  - https://imgix.com/
  - a dependency-free JavaScript library for the browser that allows for easy integration of imgix into websites.
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

- https://github.com/viliusle/miniPaint /MIT/202404/js/ps-alternative
  - http://viliusle.github.io/miniPaint/
  - Online image editor lets you create, edit images using HTML5 technologies.
  - miniPaint operates directly in the browser. Nothing will be sent to any server.

- https://github.com/1j01/jspaint /7.6kStar/MIT/202508/js/inactive
  - https://jspaint.app/about
  - JS Paint is a pixel-perfect remake of Microsoft Paint that runs in the browser.
  - 古老的像素风格

- https://github.com/chase-manning/react-photo-studio /MIT/202310/ts/inactive
  - https://reactphotostudio.app/
  - a free online photo editor for photography and design

- https://github.com/steffest/DPaint-js /MIT/202404/js/NoDeps/类似ps
  - https://www.stef.be/dpaint/
  - Webbased image editor, modeled after the legendary Deluxe Paint with a focus on retro Amiga file formats: read and write Amiga icon files and IFF ILBM images
  - It runs in your browser, works on any system and works fine on touch-screen devices like iPads. no data is sent to any server.
  - It is written in 100% plain JavaScript and has no dependencies.
  - The only part that is not included in this repository is the Amiga Emulator Files. (The emulator is based on the Scripted Amiga Emulator)
  - https://github.com/naTmeg/ScriptedAmigaEmulator
    - https://scriptedamigaemulator.net/
    - amiga emulator in pure HTML5 and JavaScript.
    - based on winuae and use the aros-kickstart replacement

- https://github.com/iyadahmed/AwesomeImageEditor3 /python
  - open-source, user friendly and high-performance image editor made from scratch with Python and Qt
# image-tiles/lod
- https://github.com/EddieMachete/em-ui-quadrant
  - Quadrant is a tile based, JavaScript web component which allows viewing an image in different levels of detail while optimizing the download process. 
  - Quadrant is based on my interpretation of Google Maps applied to image viewing over the web.
# image/cover-generator/open-graph
- https://github.com/PJijin/Cover-Image-Generator /js
  - Generate a cover image for your blog post online.

- https://github.com/daveearley/screenshot.rocks /ts
  - Screenshot.rocks is an online tool which allows you to create beautiful mobile & browser mockups from screenshots.
  - https://chrome.google.com/webstore/detail/screenshotrocks-one-click/oolmphedpohnagciifbnfpemadolahki

- https://github.com/alvarcarto/url-to-pdf-api /7.1kStar/MIT/202303/js/inactive
  - Converts any URL or HTML content to a PDF file or an image (PNG/JPEG)
  - Rendered with Headless Chrome, using Puppeteer. The PDFs should match to the ones generated with a desktop Chrome.
  - PDFs can be generated in many ways, but one of them is to convert HTML+CSS content to a PDF. This API does just that.

- https://github.com/spatie/browsershot /MIT/202511/php
  - https://spatie.be/docs/browsershot
  - Convert HTML to an image, PDF or string
# qrcode
- https://github.com/sz3/libcimbar /MPL/202407/cpp
  - https://cimbar.org/
  - Optimized implementation for color-icon-matrix barcodes
  - cimbar is a high-density 2D barcode format. Data is stored in a grid of colored tiles
  - 一般二维码只能容纳 2.9KB 的数据，用来放超链接和文本足够了。libcimbar 开发了一个特殊的压缩和解压算法。可以把小于 33MB 的文件直接压缩到特殊的二维码里，用他们提供的 App 扫码解压即可得到文件。
# image-ai 👾
- https://github.com/Tansuo2021/gemini-3-pro-image-preview /MIT/202601/js
  - https://tansuo2021.github.io/gemini-3-pro-image-preview/
  - 基于 Google Gemini 3 Pro 模型的现代化图像生成工作台
  - [【开源】并发自定义多渠道的gemini-3-pro-image-preview超强生图工具 _202511](https://linux.do/t/topic/1222546)

- https://github.com/Hi5v/UnderlayX /AGPL > closrc/202510/ts/inactive
  - https://www.underlayx.com/
  - UnderlayX is a creative image editing tool that lets you clone objects, change or remove backgrounds, and place text or shapes behind objects in an image, all in one place.
  - It uses https://github.com/imgly/background-removal-js for background removal.
  - [Built an all-in-one creative image editing tool—after thousands of visits and requests for the code, I made it open-source! : r/webdev _202501](https://www.reddit.com/r/webdev/comments/1i1aoxn/built_an_allinone_creative_image_editing/)
  - 🍴 forks
  - https://github.com/bytexposure/UnderlayX

- https://github.com/LuqP2/Image-MetaHub /153Star/MPL/202512/ts
  - https://imagemetahub.com/
  - A desktop application for browsing, searching, and organizing AI-generated images locally. 
  - It scans your folders, parses metadata from popular tools (Automatic1111, ComfyUI, Fooocus, SD. Next, Forge, SwarmUI, DrawThings) and online services like Midjourney / Nijijourney, whenever their metadata is present in the files. and lets you search, filter and organize your images by prompt, model, sampler, seed and more – all offline, on your machine.
  - Rich metadata parsing for Stable Diffusion / A1111 / ComfyUI and other tools
  - Powerful search & filters by prompt text, model, steps, CFG, sampler, seed, etc.
  - Compare tools to inspect variations side‑by‑side (Pro)
  - Analytics dashboard to see how you actually generate and use your models (Pro)
  - The core app is free and open‑source (MPL 2.0) – this repository.
  - Some advanced workflow features are Pro and require a license key to unlock in the desktop app.
  - Pro currently unlocks:
    - Automatic1111 integration (send prompts/settings back and forth)

- https://github.com/upscayl/upscayl /39.3kStar/AGPLv3/202508/ts
  - https://upscayl.org/
  - Upscayl lets you enlarge and enhance low-resolution images using advanced AI algorithms. Enlarge images without losing quality
  - You'll need a Vulkan compatible GPU (Graphics Card) to upscale images. Many iGPUs (integrated graphics) do not work but, no harm in trying
    - NCNN Vulkan requires a Vulkan-compatible GPU. Upscayl won't work with most iGPUs or CPUs.
    - @Wyrdgirn has contributed a workaround for Windows and Linux 
  - Upscayl uses AI models to enhance your images by guessing what the details could be. 
    - It uses Real-ESRGAN and Vulkan architecture to achieve this. 
    - Our backend is fully open-source under the AGPLv3 license.
  - https://github.com/upscayl/upscayl-ncnn /AGPL/202507/cpp/c/backend

- https://github.com/karant-dev/AutoRedact /GPL/202512/ts
  - Client-side, privacy-first image redaction tool. No server, no data leaks
  - Automatically detects and blurs PII (Emails, IPs, Keys) using local OCR. 
  - Tech Stack: React, Vite, Tesseract.js v6.

- https://github.com/Sanster/IOPaint /22.6kStar/apache2/202504/python/ts/inactive
  - https://www.iopaint.com/
  - A free and open-source inpainting & outpainting tool powered by SOTA AI model.
  - fully self-hosted, support CPU & GPU & Apple Silicon
  - FileManager: Browse your pictures conveniently and save them directly to the output directory.
  - https://huggingface.co/spaces/Sanster/iopaint-lama

- https://github.com/chunxiuxiamo/ai-image-edit /95Star/202512/js
  - AI图片生成编辑网站，可以框选图片局部区域进行编辑修改。
  - 通过画笔涂抹或框选图片局部区域进行编辑修改，可一次性修改多个区域。
  - 对复杂图形有概率会修改到原图其他元素
  - [【开源】：Nano-banana生图和画笔涂抹、框选局部区域进行编辑修改 _202512](https://linux.do/t/topic/1369893)
    - 优化模型选择功能，兼容其他绘图模型（OpenAI通用API格式），支持自定义模型
    - 直接框选就行右边会自动出现坐标和对应的指令输入框，输入指令之后 下面的设置提示词按钮就可以了 不用自己写坐标
    - 模型需要支持通用的OpenAI API格式 我测试gpt-image是可以的
    - 复刻了lovart的核心功能啊，大佬牛逼
    - 新增支持gemini官方API渠道 但是我没有官方api key测试不了 你拉下代码看看有没有问题
    - 可以用cliproxyapi反代antigravity，有pro的话使用gemini api格式，每五小时可以生成20张nano banana pro4K图

- https://github.com/markfulton/NanoBananaEditor /521Star/AGPL/202509/ts/inactive
  - https://nanobananaeditor.dev/
  - Nano Banana image generator and editor application.
  - Powered by Gemini 2.5 Flash images API.
  - Conversational Editing - Modify images using natural language instructions
  - Paint masks to target specific areas for editing
  - [I built the best Nano Banana AI Image Editor, and I'm open-sourcing it : r/SideProject _202509](https://www.reddit.com/r/SideProject/comments/1n5mzas/i_built_the_best_nano_banana_ai_image_editor_and/)
  - https://github.com/etranHOLI/NanoBananaEditor /AGPL/202512/ts
    - Nano Banana image generator and editor application. This tool provides a central hub for AI image generation and revisions.

- https://github.com/sapthesh/AI-Photo-Editor-Nano-Banana /MIT/202509/ts/inactive
  - web application allows you to transform your photos with simple text prompts
  - upload an image, select a region, and describe your vision in natural language.
  - Powered by the Google Gemini gemini-2.5-flash-image-preview model
  - Iterative Editing Workflow: Use the generated image as the new starting point for further edits, allowing you to stack multiple creative changes.
  - Prompt Suggestions: Get inspired with clickable example prompts
- https://github.com/aigem/aice_ps /apache2/202510/ts/inactive
  - 网页版 AI 照片编辑器，利用 Google aistudio 的先进能力
  - 智能修饰 (局部编辑): 在图片上轻松点击指定位置，通过简单的文字指令（如“移除这个物体”、“把衬衫变成红色”）进行精准、无缝的局部修改。
  - 创意滤镜与专业调整: 一键应用动漫、合成波、Lomo 等多种艺术风格滤镜，或进行背景虚化、增强细节、调整光效等专业级图像调整。
  - 一键抠图: 强大的人工智能可自动识别并移除图片背景，一键生成带透明通道的 PNG 图像，非常适合设计和合成。
  - AI 模型: Google Gemini API (gemini-2.5-flash-image-preview, imagen-4.0-generate-001, gemini-2.5-flash)

- https://github.com/yunshaochu/genai-image-patcher /202601/ts
  - 基于nano banana pro局部重绘图片，并回填原图
  - 允许用户在图片上框选特定区域，利用 Google Gemini 或 OpenAI (及兼容接口) 的多模态能力，根据文本提示词对该区域进行修改、增强或替换，并自动将生成的补丁无缝合成回原图。
  - 无论是去除水印、修改细节、批量编辑，还是通过局部框选绕过 AI 模型的安全过滤实现漫画翻译，这个工具都能轻松胜任。
  - [开源一个可以用banana pro翻译涩图的项目 _202601](https://linux.do/t/topic/1510546)
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

- https://github.com/andrii-kryvoviaz/slink /984Star/AGPL/202510/php/svelte
  - https://docs.slinkapp.io/
  - self-hosted image sharing platform designed to give users complete control over their media sharing experience. 
  - Built with Symfony and SvelteKit
