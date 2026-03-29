---
title: lib-editor-app-community-typesetting-layout
tags: [comunity, editor, latex, layout, typesetting, typst]
created: 2026-03-29T13:03:09.145Z
modified: 2026-03-29T13:03:35.455Z
---

# lib-editor-app-community-typesetting-layout

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🚀👷 pertext: Fast, accurate and comprehensive userland text measurement algorithm in pure TypeScript, usable for laying out entire web pages without CSS, bypassing DOM measurements and reflow
- https://x.com/_chenglou/status/2037713766205608234
  - Occlusion (virtualization) of hundreds of thousands of text boxes, each with differing height, without DOM measurement, therefore simplifying the visibility check to a single linear cache-less traversal of heights, scrolling & resizing at 120fps
  - Shrinkwrapped chat bubbles
  - Multi-columns magazine layout, but _responsive_ and dynamic
  - Variable font width ASCII art, because why not, it's easy now
  - Your typical auto-growing text area, accordion, multi-line text centering, pure canvas multiline text, and all other things that used be real CSS challenges, now reduced to a boring footnote 
  - The engine’s tiny (few kbs), aware of browser quirks, supports all the languages you’ll need, including Korean mixed with RTL Arabic and platform-specific emojis
  - This was achieved through showing Claude Code and Codex the browsers ground truth, and have them measure & iterate against those at every significant container width, running over weeks
  - This paradigm is significantly more performant (~500x, but it's an unfair comparison; read on) than laying out text and messily crawl out the measurements through getBoundingClientRect(), which causes DOM read/write interleaving, one of the most expensive operations on the web
  - In the past, such measurement also had to be batched, which wrecked the programming model of having UI components boundaries in the first place. The best perf gains come from architectural shifts! Measurements are actively tracked in the repo

- [Rich Text Demo](https://chenglou.me/pretext/rich-note/)
  - https://x.com/_chenglou/status/2037964564072210899
  - here's the standard rich text demo! But ofc, manually laid out, with full awareness of box height, so you can do occlusion (virtualization) easily without observers and other mess

- In pure typescript? Why? Do you parse ttfs on your own? Or using canvas? If latter it’s completely obsolete, because parsing ttf from wasm is incredibly cheap and then kerning is also solved
  - Those don’t have line breaking & segmentation heuristics, nor cross-browser line break differences (the calculated measurements would be wrong)
  - Also, licensing and payload issues
- But you’re just wrapping HarfBuzz?

- Bold approach. Reminds me of canvas-based UIs challenging DOM assumptions. Key question: consistent cross-browser results?
  - It currently has two sets of APIs. One that accurately calculates multiline text on the big 3 browser engines (they lay out text differently), and one that instead lets you manually lay out each line and bypass native layout. So either way you can get consistency

- This is really cool! I'm working on a library to render TSX on GPU using shaders. I'd love to port this to Rust+WGSL as the layout engine.
  - Pretext only does layout, not rendering, though yes it has enough layout heuristics that you should just extract all that!
- I think I just unlocked another superpower. I've always wanted to build a UI that treated data like another component, flowing it, mapping it, graphing it, etc. With https://github.com/chenglou/pretext and https://github.com/tmzt/matter-stream I think I've figured out how to do it. Then another superpower emerged. What if I could incorporate voice interaction directly with feedback and affordances right in the UI. This is going to be awesome. It will probably go into Continuo first, there's more screen real estate than is possible with Personal OS on a mobile device. Think Figma + interaction + Tufte-style graphics all in one flowing markdown document (with TSX wrappers).

- is this basically doing latex's algorithms in the browser on whatever objects exist in the scene?
  - It has 2 modes, one is replicating almost exactly various browsers' algorithm (greedy). 
  - Second mode is free-for-all measure-and-layout each line yourself, which lets you build latex' alg on top of it

- Nice! I worked on something like this 10 years ago or so for rendering PDFs. It’s a fantastically hard problem, especially if you handle Unicode properly. Luckily OffscreenCanvas and Intl. Segmenter exist now - I had to implement font parsing and line breaking from scratch back then. I think react-pdf still uses a version of it
  - https://github.com/diegomura/react-pdf/tree/master/packages/textkit /MIT
  - https://github.com/foliojs/textkit

- The masonry virtualization demo alone is worth the entire project — doing variable-height virtualization without measuring the DOM has been one of those "unsolvable" problems for years.

- I have used the canvas measureText API a couple of times for ellipsis calculations but holy moly brother this is amazing!

- why not do this in c++ or something
  - Because that’s not where the perf bottleneck is, and doing it in C++ means carrying wasm modules where you end up having to batch send the calculations to wasm since communication is expensive (strings). So you end up with a similar-shaped bottleneck than DOM measurement

- https://sebland.com/textflow/

- 🐛 As long as we don't want text selection to work right. Look, I'm all for better text layout on the web, but shouldn't we drive this by enhancing browsers, not by doing ever-more work in janky client-side JS?

- Of note, Intl. Segmenter is not great in several important languages, there are better approaches out there that you could use 

- unfortunately virtualization breaks native browser text search. have you found a solution for it?

- May be better to have the actual content appear in the markup rather than in the JS so that it's more accessible?

- why can't browser vendors not take these principles and bake this into the browser engines themselves?
  - They have been, but critically (imo), in the wrong place
  - I do wish this could be exposed by the platform, but I'm not sure CSS is the right way to go. In fact this was created to avoid more CSS bloat, which impacts all other web systems indirectly if you know how these rendering engines work
- I wonder if more css hooks like Houdini could help find a middle ground, where a js (or wasm) library module extends layouting while the consumer just uses it like css
  - Houdini's most interesting stuff got blocked. Wasm was supposed to be the way to go, but then the interop story kinda turned into this: doing it in C++ means carrying wasm modules where you end up having to batch send the calculations to wasm since communication is expensive (strings). 
  - What we _actually_ need is an accessibility API that's not tied to DOM, plus the scrolling logic. Then userland can recreate everything. But certain committee folks, esp at Apple, disagree
  - We've been robbed of the ThreeJS for 2D web due to bad platform API decisions.
    - Currently, if you want to build a 2D interface on the web, you are largely forced to use the DOM (HTML) and CSS. You are constrained by the browser's built-in layout engines (Flexbox, Grid, etc.). A "ThreeJS for the 2D Web" would be a revolutionary, community-built rendering engine that completely bypasses CSS. 
    - standard committees (W3C) and browser vendors (like Apple) have made decisions that prevent developers from building this "2D ThreeJS". the most powerful parts of Houdini (like the Layout API) were stalled or blocked by browser committees due to complexity and security/performance concerns. 
    - If a developer decides to just say "Forget the DOM, I'll draw my UI on a 2D canvas" (which is what Google Docs and Flutter Web currently do), they face a massive problem: Accessibility (Screen Readers) and Native Scrolling.
- That’s a valid approach, personally I’m in favor of keeping the DOM and extending it to allow programmatic control of rendering and layout, I think Houdini was the right idea we just need to keep pushing on it. I don’t like the idea of recreating the Flash-site era

- https://x.com/antonioeloi98/status/2037927058764964191
- The reason the web doesn’t use this style it’s because it’s not the best layout for reading in screens.
  - Someone reinvented the wheel, available 25+ years before but forgot that everyone uses adaptive layouts so that the page will be rendered ok on both mobile and desktop. 2 text columns on a smartphone screen will make me cringe.

- 
- 

- ### pretext 仅依赖 canvas.measureText 和 Intl. Segmenter。
- https://x.com/ewind_dev/status/2038226134882832434
  - 后者 bun 和 node 都内置，前者可用 @Brooooook_lyn 的 skia canvas 来实现。
  - 这意味着仅靠 bun + yoga + pretext + skia canvas 就够完整渲染 headless UI 了
  - 记得 measureText API 当时也是我接的，但域名邮箱过期导致贡献者里我失踪了……

- https://x.com/_justineo/status/2038110463943389415
  - 这个项目的核心并不是文本测量算法，文本测量本身只是调用了 canvas 的 measureText API，就一行 
  - 如何把测量结果变成和浏览器一致的断行决策，这个才是这个项目主要做的事情。
- https://x.com/xicilion/status/2038270226467623188
  - 用 canvas 检测尺寸有风险，canvas 检测出来的尺寸和 DOM 有细微差别，精确布局的时候，有时候会导致实际渲染时容器尺寸不足而换行。
- 只能说 It works for some cases

- https://x.com/KKaWSB/status/2038053741757399095
  - 完全绕过了浏览器的DOM排版系统。以前网页要知道一段文字多高多宽，必须把它塞进DOM让浏览器算一遍，这个过程极其昂贵。Pretext用纯数学自己算，快了500倍。
- CSS text wrap + shape-outside 組合終於能實現這個效果了，但瀏覽器兼容性一直是個問題。能做到120幀絲滑說明底層渲染優化也到位了，這才是真正的挑戰所在。前端排版這個領域確實被低估太久了。
- 挺棒的，不过浏览器 layout 计算时间的开销，在整个产品生命周期里的价值有限，这是一个很棒的提升，谈不上跨时代
- 从技术上说，确实很牛；但它解决的问题，并不重要，可以说并不是问题
- AI编程，让过去很多望而却步的实现变得唾手可得
- 用浏览器做出版物排版，这方向是不是就错了？

- https://x.com/tvytlx/status/2038269309269741785
  - 让Codex帮我重新实现了一下pretext的demo，然后看了一下它的代码，大概过程是这样的：
  1. pretext 先测量文字，内部用浏览器的canvas.measureText()。
  2. pretext 再做排版决策。layoutNextLine() / layoutWithLines() 返回“这一行是什么文本、宽度多少”。
  3. 最后的绘制是，在 div 里，把 line.text 填进 textContent，然后浏览器用原生 DOM 文本渲染把它画出来。
  - 球的物理碰撞也是先在外面算完了然后在做排版决策之前告诉它。
  - 感觉这个API应该由浏览器提供，没想到以这种外挂的方式实现了。

- https://x.com/7id/status/2038291698946838557
  - 回到 pretext 本身。 它想解决的问题是，DOM计算文本尺寸需要触发重排，会中断渲染导致性能问题。它给的解决方案是，绕开DOM直接走Canvas模拟，然后将布局结果写死。
  - 它解决性能问题了吗？解决了。能用吗？不能。或者说能用的场景非常有限。
  - 因为代价是连续文字失去了内在关联，变成了孤立的元素。
- 看了下 div 划分/canvas 渲染好像对 AI 来说更难读了

- https://x.com/geniusvczh/status/2038191870195757359
  - Chrome在windows下用的direct write ，也不是自己做的，而是每个平台用最好的方法做一次。决定文字大小最终是看native api的实现方式，而这个结果在不同的渲染器+不同的系统下面肯定是会变得不确定。所以对于实现layout的这么个具体的事情，反正不可能去用他的

- ### 我整理了 8 个非常炸裂的脑洞大开的案例
- https://x.com/axiaisacat/status/2038233070709436617

- ### 🌰 was playing with a similar idea a week ago. 
- https://x.com/vamsibatchuk/status/2037924109049311702
  - link/image元素在点击时, 通过环绕的布局展示图片/卡片

- https://x.com/lucas__crespo/status/2038312815249817653
  - intercepts pinch-to-zoom and resizes text instead of the page. Only two lines of code built on top of @_chenglou ’s pretext.
  - https://pinch-type.surge.sh/

- ### Pretext快速而且精准的文本测量算法，可以实现类似报纸的动态图文环绕效果。
- https://x.com/op7418/status/2038095651234627600
  - 有了这个以后，AI 就能清楚地知道每个字符的宽度和总宽度，不会出现闪烁、超出范围和抖动等问题。

- 如果这个方案最后能跨字体、跨语言、跨渲染环境都保持一致，那价值会非常夸张。 尤其是中文、日文、emoji、混排场景，才是真正的压力测试。做到了的话，很多 AI Native 编辑器都会直接受益。

- ### Pretext is awesome for other reasons, but seeing all the comments on "editorial design being finally possible on the web" makes it clear most people don't know that ˋshape-outsideˋ does the job natively in CSS for DOM layouts in all browsers.
- https://x.com/bdc/status/2038002901033845178
  - shape-outside cannot enable this: 图标在段落任意位置移动

- CSS is amazing, but i too have hit many performance ceilings where i hit the ceiling due to layout + repainting (even with CSS containments and such). 

- does it support re-flowing of the text across columns? or are the columns hard defined?

- ### A Midjourney engineer finally just fixed it. It’s called Pretext
- https://x.com/JoshKale/status/2037900758750761053
- we have had this with `shape-outside`.
- been in chrome since 2014, safari 2017 & firefox 2018

- apparently, this can wrap text around randomly positioned objects on the screen, but i never had any instance where i needed that. either you have a picture at a certain position in text or you don't, you don't wrap text around random objects on screen...

- ### a cartoon girl dancing in text
- https://x.com/EsotericCofe/status/2038076140661932273
- I won't prefer this constantly changing layout, too distracting. Tell me if i am wrong
  - It's just a demonstration of performance, what it actually does is solving a problem that is awful since the beginning of the web that is weird whitespace. This new equation brings InDesign editorial level to CSS. It is to make reading smoother instead of distracting.

- The web's layout engine has always been a compromise between the precision of print and the fluidity of the digital medium. We've spent decades building workarounds for a foundational gap. Cheng Lou's Pretext isn't just a library; it's a fundamental bridge that restores the aesthetic integrity of typography to the dynamic interface. We're finally moving from 'making it work' to 'making it beautiful' at scale.

- As but a lowly pleb I have to ask - every example I’ve seen looks cool af, but is essentially unreadable so… what’s the exact use case for this?

- ### This little illuminated dragon is very happy about Pretext. 
- https://x.com/Riyvir/status/2038093450139279426
- He replaces HTML with a canvas. So the problem in html css was not solved he used a self build ts script.  Correct me. Question is could this kind of text flow also be done on level of HTML and css javascript

- The problem was solved 30 years ago; it’s been there in the word processor algorithms. We can look ahead if things are simple. But what if the paragraph is composed of multiple fonts and sizes? Then we need something like a DOM structure. This little cute trick can be applied to the CSS standard as an advanced ‘pre’ tag, but anyway, it’s just a cute little gimmick.
  - that's doable too as rich text

- Place it in strategic places just like any illustration in a good illustrated book and you get a really good anchor for long term memory.

- ### Your browser re-layouts the entire page every time an image loads. So what if the layout engine was just math?
- https://x.com/davidbyttow/status/2038056071265476845
  - Left: native CSS Grid. Images load one by one without preset dimensions. Each one triggers a cascade of layout shifts. Red outlines = every element that moved.
  - Right: boxmath, a pure JS layout engine I built this morning. Same images, same timing. Positions are pre-computed with arithmetic, applied in one batch write. Nothing moves. Zero layout shifts.
  - Inspired by @_chenglou 's pretext (http://github.com/chenglou/pretext), which figured out that text measurement doesn't need the DOM. Canvas gives you widths, and from there it's just arithmetic. boxmath takes that same idea and applies it to layout: Box, Stack, Row, Text, Image. Five primitives, pure math, no reflow.
  - The browser's layout engine isn't slow because the algorithm is hard. It's slow because every measurement read forces a synchronous recalc of the entire document. Decouple the computation from the DOM and re-solving a full layout tree costs ~0.1ms.
  - tbc: css grid handles card grids fine and you can set aspect-ratio/etc to get zero layouts.
  - the interesting part to me is layout as a pure function you can call anywhere: before rendering, in a worker, against a canvas, etc.

- You're overstating the CSS situation, right? Many developers building the thing on the left would nail down the image dimensions in CSS, and possibly also the area allotted for the descriptions, allowing it all to be laid out just once. A few dozen lines of CSS, a browser which is extremely good at handling HTML and CSS, no JavaScript layout machinery needed. There are likely valuable designs that benefit from taking control of the layout and code, but I don't think this is a good example of that.
  - yep fair. when setting aspect-ratio on the images the CSS version is stable too.
- reality is non deterministic image and text dimensions

- ## Seems like a good opportunity to share a trick I used on the React Aria website to make headings scale to fit the viewport on mobile, even with SSR.
- https://x.com/devongovett/status/2038312787362087055
  - I used fontkit, a library I wrote 10 years ago to parse fonts and layout glyphs, to measure the width of the heading at build time in the "em" unit.
  - width = font.layout('DateRangePicker').advanceWidth / font.unitsPerEm
  - This is a size independent measurement using the font's internal metrics. When multiplied by any font size, you get the pixel width of the text.
  - To calculate the font size, set this as a CSS variable and divide the target width (100vw minus padding). Clamp to make sure it doesn't get too big or small.
  - font-size: clamp(35px, (100vw - 32px) / var(--text-width), 55px)
  - You have perfectly scaling text no matter the viewport size. 

# discuss-examples
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 
