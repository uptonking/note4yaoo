---
title: lib-media-image-community
tags: [community, image]
created: 2024-09-16T11:11:04.287Z
modified: 2024-09-16T11:11:14.989Z
---

# lib-media-image-community

# discuss-stars
- ## 

- ## 

- ## [Should I generate images on the client or server side ? : r/django](https://www.reddit.com/r/django/comments/1piidtl/should_i_generate_images_on_the_client_or_server/)
  - My business flow is as follows : The user uploads a picture I open the background picture I paste the user 's picture on it I then paste the overlay picture
  - So I use pillow in the backend , but I feel this might be doing unnecessary and causing me too much memory and time . When I could just use the user 's browser and render the images .
  - After I changes my code to do this on the client side using canvas , I noticed my memory usage went down by 10 MB , due to me not opening the background picture in memory and then pasting imag3s in it.

- Are you charing them for the service? If so use it on the backend. If not, just let their computer do it. Although what youre describing SHOULDNT be expensive for either the server or client

- I prefer rendering such things on the server, because on the client a user can manipulate it (ie. add a custom frame on their linkedin profile image if it would be done in js)
# discuss-image-css
- ## 

- ## 

- ## Image zoom hover effect is one of my favourite simple ways to enhance your project
- https://x.com/davidm_ml/status/1842187323435593944

# discuss-image-ai
- ## 

- ## 

- ## Pika 新活，将你的照片变成任何图片中的人物，感觉是首尾帧加 ID 保持
- https://x.com/op7418/status/1900477755416056007
- 可灵快跟上
- 换脸加首尾帧合成动画好像就可以

- ## 给产品和网站配图 line art 是一个很好的表现形式，但 AI 生成的这种line art drawing 都没法生成透明的背景。
- https://x.com/leeoxiang/status/1858321793691623515
  - 实验下来 http://recraft.ai 效果是最好的，line art + remove bg 生成透明背景的 line art 效果图。

# discuss-tools
- ## 

- ## 

- ## 最近新知道了一个 Web API: HTMLImageElement.decode() 。
- https://x.com/wsygc/status/1833673933624901853
  - 如果动态地将已有图像替换为新图像，这会特别有用，而且还可以防止在图像解码时因代码以外的不相关绘制而挂起。
  - 以前预加载图像常用的方式就是捕捉image onload事件，遇到需要写async/await的情况，还得用Promise包裹处理一层，现在有了decode，一个 await img.decode() 完事，简单方便

# discuss-html2canvas
- ## 

- ## 

- ## 🤔 [when iframe cross-origin , how to sreenshot · Issue #1532 · niklasvh/html2canvas](https://github.com/niklasvh/html2canvas/issues/1532)
- After digging this issue for hours. I solved it by using
  - start a reverse proxy ( e.g. http-proxy) which proxy remote-host to localhost:8888.
  - add `document.domain = document.domain` on both container page and iframe content. According to MDN, this will cause the port number to be overwritten with null. If you can't change iframe content source directly, consider modify the HTTP(s) response. (MitM)
  - Since container & iframe now have the same domain localhost, Javascript API is working on iframe! ( So does html2canvas)

- ## [Iframe is not working · Issue #3095 · niklasvh/html2canvas](https://github.com/niklasvh/html2canvas/issues/3095)
- you can get your iframe content by `iframeElement.contentWindow.document.body` , then create an image of that and replace it with the iframe element when you create main image

- ## [IFrame with no width/height fails · Issue #1892 · niklasvh/html2canvas](https://github.com/niklasvh/html2canvas/issues/1892)
- A possible fix is to use getComputedStyle(iframe).width here instead of iframe.width (and same for height)

- ## 🌰 [Bug canvas iframe · Issue #2120 · niklasvh/html2canvas](https://github.com/niklasvh/html2canvas/issues/2120)
- adding width and height attributes seems to work but an other bug when i set a margin-left for example

- ## 🤔 [Support for iframe capture · Issue · niklasvh/html2canvas _202109](https://github.com/niklasvh/html2canvas/issues/2692)
- is there any plan to support iframe capture in the same origin?
  - It's definitely supported. Try setting a height and width on the iframe.
  - Iframe element must set width and height through attributes. eg: `<iframe src="./child.html" width="400" height="400"></iframe>` . Because html2canvas iframe clone initialize by `iframe.width and iframe.height`

- ## [html2canvas failing when trying to capture embedded SVG · niklasvh/html2canvas · Discussion _202204](https://github.com/niklasvh/html2canvas/discussions/2855)
- I think you can't capture an iframe from a different origin without running into CORS problems unless you use a CORS proxy. If you aren't already using some kind of CORS proxy I would suggest it because html2canvas by itself does not bypass CORS restrictions. In the html2canvas documentation it suggest using the html2canvas-proxy.

- ## [why does it render the page inside an iframe · niklasvh/html2canvas · Discussion _202211](https://github.com/niklasvh/html2canvas/discussions/2987)
  - can't we just render it on the canvas?

- I have this question too. I notice that if I hack the code a little to avoid the iframe and generate the canvas directly from the element on the page it still works, and is about a second faster. 
  - I assume there was some corner case that required the use of the iframe. It would be interesting to know what it was.
# discuss-screenshot-dom
- ## 

- ## 

- ## 

- ## Built this animation entirely in Remotion
- https://x.com/JNYBGR/status/1902632839239074217
  - 源码显示在三维表面的效果
- Do you have HDR support? Specifically rec2020/bt2084?
  - Not to a satisfactory degree. We rely on Chrome screenshots that are only available in sRGB. 
  - We do however tonemap HDR videos so they look okay in sRGB. You can also export videos in BT.2020, but to be honest you should probably not use this option

- ## 💡🤔 TIL you can turn HTML elements into screenshots in JavaScript with modern-screenshot
- https://x.com/aidenybai/status/1883934244390724026
- idk if you’ve ever looked at the source of one of these, but it is a master class in obscure web hacks. IIRC most of them work by embedding the html in an svg foreign object and inlining stuff like fonts where possible. there are a lot of foot guns that can cause them to break (by tainting the canvas). still incredible none the less
  - 💡💡 That is sadly the most effective way of doing it, though it definitely does not work reliably. The browser intentionally prevents grabbing node textures, even though they’re obviously in memory, for security reasons. 
  - It’s more reasonable to have servers running your app, loading client data, and taking/sending back screenshots
- i literally went through this exact process a few years ago. start with dom2img -> puppeteer on a server
  - It’s sad but the only way (unless you have an electron app or something where you can access more of the browser APIs)

- How do you render it server side to create the image?
  - Run a headless chrome browser (via Playwright or Puppeteer) and generate screenshots.

- Pretty sure you can just get capture a video stream of DOM elements nowadays just fine, no hacks needed.
  - Pretty intrusive UX though

- ya, until it tries loading fonts and icons off the wrong paths.  they need a native HTML API for this that can just read out of the frame buffer like the Screen Capture API does

- I’ve used `html2canvas` previously. I’ll check this out. I need to ship something using this
  - `modern-screenshot` has better Safari support
- html2canva does not support all css
- All of them suck tbh. They all block the main thread during the conversion process and can't run on service worker as they are all required to access the dom. What does it mean? It mean they can't be used in anything serious/complex as it halts the UI.
  - That's why people still end up using something like puppeteer.js from a separated server/service to do simple screenshots

- https://x.com/_justineo/status/1885272602362732689
  - domvas ➡️ dom-to-html ➡️ html-to-image ➡️ modern-screenshot，这个事情每隔一段时间就会被 fork 一下，JS 社区接力了十几年了，浏览器到现在还没有实现
  - 有一个相关的 DOM proposal

- ## [Show HN: Satori – Convert HTML and CSS to SVG | Hacker News _202210](https://news.ycombinator.com/item?id=33156130)
- You can do something like this via the browser by printing the page to PDF then using Inkscape to convert that to SVG

- Note that `html2canvas` has a lot of limitations, since everything that needs to be rendered has to be implemented from scratch using canvas primitives. 
  - If you have (IIRC) shadows, more advanced CSS features, certain SVG icons, etc., your output will be pretty broken. 
  - I usually have to do DOM cloning and modify/hide the problematic parts before using html2canvas to generate an image.

- I look a little closer it appears the layout work is farmed out to yoga (not trying to take away anything from the effort here). So this project is almost a wrapper around running yoga as a renderer and using SVG as a form of backend target?

- Satori does not guarantee that the SVG will 100% match the browser-rendered HTML output. That's because Satori implements its own layout engine based on the SVG 1.1 spec. However, Satori generated result (SVG) is stable on all browsers.

- The SVG -> PNG part is handled by @vercel/og. Specifically, it uses Vercel Edge Functions + WebAssembly to handle generating images at the edge.
  - it appears to wrap Chromium to do the PNG generation.
- [Investigate replacing puppeteer with smaller alternative · Issue · vercel/og-image](https://github.com/vercel/og-image/issues/148)
  - 202210: We decided that embedding a browser is not a sustainable solution. So we built an alternative solution to convert HTML/CSS to PNG.

- Converting text to SVG is super hard. Flowing English text is easy enough, but when it comes to Unicode text, with languages such as Arabic and Indian languages, that's when it gets hard. I tried Satori, and it doesn't handle Unicode very well, particularly, combining characters.
  - Advanced text shaping isn’t implemented yet, where we plan to use Harfbuzz in the future.

- Some of what looks challenging here is handling fonts. SVG would be so much better if there was a way to do font embedding. Even a minimal set of fonts would be amazing. Or if operating systems or libraries for SVG support could all commit to supporting a common set of fonts, like browsers did for web safe fonts. Think of how clunky the web would have been without those.
- You can embed fonts in SVG
  - In my experience, embedded fonts are handled very inconsistently (and often poorly) by different rendering engines.
  - In particular: if you load an SVG in Chrome via an img tag, the webfont is not run because the environment tries to execute as little as possible. It'll instead use whatever fallback font is present on the system.
- I think you can safely embed data URLs because they’re known to be static. What you can’t generally do is trigger a network waterfall or dynamic evaluation from an img tag’s SVG resource.

- ## [Taking screenshots with js the smart way - DEV Community](https://dev.to/shubhambakhal/taking-screenshots-with-js-the-smart-way-5die)
- Alternative 1: HTML to Canvas
- Alternative 2: Dom to Image
- Paid Screenshot APIs
- Using WebRTC’s getDisplayMedia Method
- My Approach: Puppeteer Power Unleashed

- ## 📰 [Show HN: Dropflow, a CSS layout engine for node or <canvas> | Hacker News _202403](https://news.ycombinator.com/item?id=39778570)
  - For the last 5 years I've been working on a layout engine that targets CSS2 and some more modern properties.
  - We currently use it in CellEngine for our new canvas-based spreadsheet library to layout text in hundreds of thousands of cells, and will be using it soon to render PDFs with thousands of pages in a few seconds.
- The default way of generating beautiful PDFs in the backend these days is, running a headless browser and using browser APIs to turn HTML/CSS into PDFs. And apparently, it's a bit costly running instances of browser in the server and scale it properly for huge workloads.
  - This is literally a game changer. Now it's possible to design PDFs using HTML/css and generate them without the browser overhead!

- I needed to transform a 12MB HTML file into a PDF document and headless Chrome quickly ran out of memory (4GB+).
  - We are now using a commercial alternative that seems be be using a custom engine that implements the HTML and CSS specs. The result is reduced memory usage (below 512MB during my tests) and the resulting PDF is much smaller, 3.3MB vs 42MB.
- Did you try Weasyprint?
  - Yes, I’ve tried all the open source projects I could find. Including Weasyprint and wkhtmltopdf. 
  - Weasyprint was much slower than headless Chrome and also required a lot of memory to process the HTML. 
  - And wkhtmltopdf is no longer maintained and crashed while processing.

- Have you tried Typst? It's like a modern version of LaTeX and allows to generate nice looking documents quickly. Can be called from the console and makes it easy to create templates and import resources like images, fonts and data (csv, json, toml, yaml, raw files, ...). Of course it is its own language instead of HTML/CSS but so far I found it quite pleasant to use.

- layout-via-code for arbitrary documents is a humblingly complex problem, so leveraging existing layout engines is preferred.
  - This impressive effort looks far better than what I'd achieve, but when this approach has been tried before, it is eventually discovered that few organizations have the resources to maintain a rendering engine long-term.
- I don't agree that a layout engine is too difficult to maintain. More of the issue is that CSS layout (and maybe layout in general) is not widely well-understood. 

- 🤔 I've been building PDF renderers for a few clients. The biggest request in PDFs has been accessibility. Everyone needs to be ADA compliant. I sadly don't see myself switching to a canvas renderer because then there is no accessibility.

- I wondered whether using instead something like LaTeX wouldn't be faster and easier to scale.

- I don't think rasterized output makes a good pdf.

- You can make PDF client-side by html2canvas or webkit.js

- > wondering if css and svg could be used as abstraction over graphics and UI libraries
  - There's another project called Sciter that uses CSS to target native graphics libraries: https://sciter.com
- > I wonder how hard it was to implement css. I've heard it can be pretty complex.
  - It was hard, but the biggest barrier is the obscurity(晦涩, 费解) of the knowledge.
  - Text layout is the hardest, because working with glyphs and iterating them in reverse for RTL is brain-breaking. And line wrapping gets really complicated. It's also the most obscure because nobody has written down everything you need to know in one place. After I finished block layout early on, I had to stop for a couple of years (only working a few hours a week though) and learn all of the ins, outs, dos, and don'ts around shaping and itemizing text. 
  - A lot of that I learned by reading Pango's(gnome) source code, and a lot I pieced together from Google searches.

- did you ever find out what algorithm the various browsers are using to calculate how many words can fit on a given line?
  - Not sure if I understood the question correctly, but they use a greedy algorithm where the break points in the string are the choices. If your glyphs are scaling and so is the available width, you might have a float precision problem? Browsers use integers for that reason. I'm still using floats.

- I’m curious if you’ve implemented a rich text editor with this
  - Google Docs uses canvas, yeah, and last I looked it used an empty contentEditable just to receive [rich text] input. 
- Sciter is using its own implementation (obviously).
  - contentEdtiable thing is indeed quite limited for general purpose WYSIWYG editor.
  - For example Web platform is missing transactional update mechanism that allows to put custom DOM mutation groups into unified undo/redo stack.
  - Sciter's `<htmlarea>` element ( implement behavior:richtext - WYSIWYG ) allows to build specialized editors.

- Yoga is great but only really supports flexbox. 
  - For most cases that can be enough but inline content (as shown in the Dropflow demo) is difficult with only flexbox layouts available.

- This reminds me of flying saucer, a CSS render written in pure Java. Successfully used it in multiple projects for rendering PDFs in the past. 

- There is also HTML/CSS layout engine litehtml (https://github.com/litehtml/litehtml) and even a full-blown web engine in JS: WebKit.js 

- As you mention PDF, do you plan to support the various @page properties that add pagination? For example like pagedjs but native? Major usecases are books and invoices
  - Yes, this is pretty high up on my list. I've already done a little bit of work on pagination/fragmentation, but it will take me some time.

- the idea of using html for text styling has stuck, Swing UI do text styling with html (and rudimentary css!) to this day. Html would not be a lingua franca if its use was limited to the equivalent of native speakers (browsers).

- This looks great. I've been using html2canvas but it doesn't support the 'filter' property yet. This will be an awesome alternative.

- Are you planning to add support for the missing standard tags like img and table (both very useful for pdf rendering)?
  - Yes, definitely. In the meantime, you can still use this to get the intrinsic sizes of cells to create rows and columns, and you can use an empty inline-block and paint the image where it's laid out. I'll put something in the examples/ directory soon.

- Does anyone have a similar solution for drawing graphs / charts in a Node environment without a browser dependency? 
  - You could use https://github.com/vercel/satori
  - Unfortunately not for nested inline nodes, like spans of text with formatting. For a lot of uses, that will be OK - but for rendering say, markdown text, Satori won't work.
  - The upstream layout engine handles flexbox layout, and it's unclear if Facebook needs inline layout or if Vercel would pick it up and close the gap
  - Then again, for the main purpose Satori is advertised for - generating URL unfurl previews - Dropflow looks like it might be the answer.
- Thanks. I've tried using Satori but I'm curious if you've used it to draw graphs specifically. E.g. Satori expects JSX / doesn't support HTML strings from d3-node with dangerouslySetInnerHTML.

- 🤔 why can't we render HTML directly onto the canvas in the browser? The parser is there, the layout engine is already implemented, and the calculation of box layout is already done.
  - If you want to do any kind of text or diegetic UI in webgl, you are begging for DOM rendering to canvas (which is then sent to a texture)
- As far as I remember, it's down to security concerns. You can actually insert your HTML into a SVG `foreignObject`, and then `drawImage()` that onto your canvas. But your HTML-in-SVG document will need to load all its own resources, fonts, CSS etc.. which makes this process rather tedious.

- I've used satori on the backend with TypeScript/Deno to render React JSX + tailwind CSS as an SVG (which is then rendered to a PNG). 
  - Of course you could use another flavor of JSX (or even plain HTML) or omit tailwind, but it's really cool that you can use the same stack as a typical frontend and render it as an image.
  - Satori is meant for rendering Open Graph images, but I found that it works well for rendering arbitrary images. Satori has no native dependencies, so it kinda "just works" on the backend. It supports a subset of modern CSS, including flexbox.

- It's neat, but CSS layout is a small part of the overall problem. 
  - Even setting side accessibility, which is a massive undertaking in and of itself, you have text rendering.
  - To get an idea of what you'd have to emulate, here are some (not even all) issues related to rendering text: https://faultlore.com/blah/text-hates-you/

- I think there has to be something compilable to WebAssembly. https://github.com/DioxusLabs/taffy

- ## [Html2canvas - Webpages Screenshots with JavaScript | Hacker News _201107](https://news.ycombinator.com/item?id=2812559)
- basically, it is a browser rendering engine written in JS and output to canvas. It is a browser implementation in JS at some extent. This is truly inspiring.

- I noticed that Google+ allowed something similar when sending bug reports. Do they use a similar method?
  - I could with quite high certainty say that they have a very similar approach to doing this. 
  - One major advantage they have, which works for their favor is that they use the script on pages they control, where as my approach is trying to get this working on any page
  - If you aren't gonna be using z-index positioning, no letter-spacing, no CSS3 properties, no HTML5 form elements etc. it can be very easy to make matching screenshot to the page.

- paraschopra mentioned PhantomJS for doing the same thing at couple of days ago
  - PhantomJS is great, although there are some bugs in the WebKit embedded inside QT because it's a bit old, it has the advantage of supporting flash plugins and it can do screen caps. I'm using it for a project now.

- The problem with server side is you're limited to things that are not behind a login.
  - BugMuncher founder/developer here - BugMuncher takes the entire DOM tree from the client and recreates it for the screenshot, so as long as any external CSS/images aren't behind authentication, it works fine on authenticated pages. In fact, most of our users use BugMuncher specifically on auth protected areas.
# discuss
- ## 

- ## 

- ## 

- ## RMBG-2.0：最佳一键去背景模型
- https://x.com/Gorden_Sun/status/1856711137028608292
  - 模型开源但不可商用：https://huggingface.co/briaai/RMBG-2.0
