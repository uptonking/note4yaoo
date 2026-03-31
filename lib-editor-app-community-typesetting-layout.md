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

- ## [Pretext: TypeScript library for multiline text measurement and layout | Hacker News _202603](https://news.ycombinator.com/item?id=47556290)
- The problem it solves is efficiently calculating the height of some wrapped text on a web page, without actually rendering that text to the page first (very expensive).
  - It does that by pre-calculating the width/height of individual segments - think words - and caching those. Then it implements the full algorithm for how browsers construct text strings by line-wrapping those segments using custom code.
  - This is absurdly hard because of the many different types of wrapping and characters (hyphenation, emoji, Chinese, etc) that need to be taken into account - plus the fact that different browsers (in particular Safari) have slight differences in their rendering algorithms.
  - It tests the resulting library against real browsers using a wide variety of long text documents

- Some details on how it works from a code comment:
  - Problem: DOM-based text measurement (getBoundingClientRect, offsetHeight) forces synchronous layout reflow. When components independently measure text, each measurement triggers a reflow of the entire document. This creates read/write interleaving that can cost 30ms+ per frame for 500 text blocks.
  - Solution: two-phase measurement centered around canvas measureText.
  - prepare(text, font) — segments text via Intl. Segmenter, measures each word via canvas, caches widths, and does one cached DOM calibration read per font when emoji correction is needed. Call once when text first appears.
  - layout(prepared, maxWidth, lineHeight) — walks cached word widths with pure arithmetic to count lines and compute height. Call on every resize. ~0.0002ms per text.

- i wrote something similar for this purpose, but much simpler and in 2kb, without AI, about a year ago.
  - [Show HN: uWrap.js – A faster and more accurate text wrapping util in < 2KB | Hacker News _202504](https://news.ycombinator.com/item?id=43583478)
  - https://github.com/leeoniya/uWrap /MIT/202508/ts
  - A 10x faster and more accurate text wrapping util in < 2KB (min)
- Looks like uWrap only handles latin characters and doesn't deal with things like soft hyphens or emoji correction, plus uWrap only handles `white-space: pre-line` while Pretext doesn't handle pre-line but does handle both normal and pre-wrap.
  - correct, it was meant for estimating row height for virtualizing a 100k row table with a latin-ish LTR charset (no emoji handling, etc). its scope is much narrower. still, the difference in perf is significant, which i have found to be true in general of AI-generated geenfield code.
- I've worked with text and in my experience all of these things (soft hyphens, emoji correction, non-latin languages, etc) are not exceptions you can easily incorporate later, but rather the rules that end up foundational parts of the codebase. That is to say, I wouldn't be so quick to call a library that only handles latin characters comparable to one that handles all this breath of things, and I also wouldn't be so quick to blame the performance delta on the assumption of greenfield AI-generated code.
  - no disagreement. i never claimed uWrap did anything more than it does. it was not meant for typography/text-layout but for line count estimation.however, for the use case of virtualization of data tables -- a use case pretext is also targeted at -- and in the common case of latin alphabets, right now pretext is significantly slower. 
- uWrap demo has text extending beyond text boxes all other the place on Safari, is that the price of simplicity?
  - Chrome is no different, for example, "RobertDowneyjr" is out of the box, so does "enthusiastic" in a couple of places.

- prepare uses measure text, if it is in a for loop, it won't be fast. This library is meant to do prepare once and then layout many times. layout calls should be sub-1 ms.

- It's a library that allows to "do stuff" before the browser renders the actual text, but by still having the browser render, eventually, the actual text?
  - Yes the browser still renders the text at the end - but you can now do fancy calculations in advance to decide where you're going to ask the browser to draw it.
- I suspect exposing the browser's text layout measurer is going to become a Web API in the future, much like exposing the HTML parser via setHTML().

- Previously if you want to layout text on the web, you have to use canvas.measureText API and implement line-breaking / segmentation / RTL yourself.
  - Pretext makes this easier. Just pass the text and text properties (font, color, size, etc) into a pure JS API and it layouts the content into given viewport dimension.
- I have one question though: how is this different from Skia-wasm / Canvaskit? Skia already has sophisticated API to layout multiline text and it also is a pure algorithmic API.
  - It’s not wasm?

- the demos all render wrong on my system (Fedora, Firefox). The torus for example is completely distorted.
  - I think it goes to show, if you try to make something like this you'll be chasing a long tail of edge cases ~forever.

- The FontMetrics API solves this, hopefully browsers will ship it someday. https://drafts.css-houdini.org/font-metrics-api-1/

- Yeah, that's definitely needed. That's why I've added `Graphics.Text` (https://docs.sciter.com/docs/Graphics/Text) in Sciter. Graphics. Text is basically a detached `<p>` element that can be rendered on canvas with all CSS bells and whistles.

- Has someone ever found a good solution for long / infinite lists / grids virtualization not breaking browsers native text search?
  - Native search only sees the DOM. Once you virtualize a list or grid, offscreen rows do not exist as nodes, so Ctrl-F cannot match them unless you keep enough hidden text around to erase most of the win from virtualization.
  - A browser API could help, but it would need to hook into selection, focus, scroll position, and match navigation across content the page has not rendered yet. That is a much bigger contract than 'search this string', and I would not bet on sites using it consistently.

- This is awesome! I had this problem when building a datagrid where cells would dynamically render textarea. IIRC I ended up doing a simple canvas measurement, but I had all the text and font properties static, and even then it was hellish to get it right.

- I get the feeling this is an AI hallucination. It uses the canvas to render the text to be measured, which doesn't bypass the browser layouting. The only potential performance to be gained here is rendering straight to a canvas instead of building a dom node, but it's not clear that it's actually faster.
  - What you're missing is that each segment (typically a word) only needs to be measured once, in the setup phase. The canvas gets thrown away after that, and subsequent layout passes all reuse the cached measurements. If you only perform layout once, it doesn't save any work. If you need to reflow many times, it saves a lot.

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

- https://x.com/_chenglou/status/2038486958708851074
  - just a parser and a cache
- the edge cases with bidi, grapheme clusters, etc. are enough to make anyone go insane

- In pure typescript? Why? Do you parse ttfs on your own? Or using canvas? If latter it’s completely obsolete, because parsing ttf from wasm is incredibly cheap and then kerning is also solved
  - Those don’t have line breaking & segmentation heuristics, nor cross-browser line break differences (the calculated measurements would be wrong)
  - Also, licensing and payload issues
- But you’re just wrapping HarfBuzz?

- Bold approach. Reminds me of canvas-based UIs challenging DOM assumptions. Key question: consistent cross-browser results?
  - It currently has two sets of APIs. One that accurately calculates multiline text on the big 3 browser engines (they lay out text differently), and one that instead lets you manually lay out each line and bypass native layout. So either way you can get consistency

- https://x.com/_chenglou/status/2038505059923968014
  - It's time to use Pretext's expressive controls to improve text readability.
  - @Somnai_dreams implemented the Knuth-Plass algorithm to reduce reading churn on long paragraphs of text
- This is actual Knuth-Plass (global optimization, not greedy) running in the browser? 
  - It is! It's not the full TeX impl with glue/penalty, but the core is DP
  - TeX’s full line-breaking system includes extra concepts like glue and penalties. But the part being used here is the core Knuth-Plass algorithm, which is a dynamic programming (DP) method for choosing the best line breaks globally instead of greedily line by line.
  - Standard web browsers use a "greedy" algorithm for text: they fit as many words as possible on line 1, break the line, fit as many as possible on line 2, and so on. This often results in rivers of white space and ugly typography.
  - Dynamic Programming (DP), on the other hand, evaluates the entire paragraph at once. It calculates the mathematical cost of thousands of different possible line breaks, balancing the spacing of line 1 against line 2, line 3, etc., to find the absolute mathematically optimal layout for the whole paragraph.
- KaTeX already does its own DOM-free rendering (it outputs static HTML/CSS, no reflow needed). If Pretext could consume KaTeX's output dimensions as pre-measured inline boxes, we'd essentially have a full DOM-free document layout engine for scientific content. Is that the direction you're thinking, or is the LaTeX connection more limited?
  - It's whichever direction you wanna code up! I'm only trying to give control back to userland
- That's the right mindset. Giving control back to userland is exactly what frontend has been missing.

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

- https://x.com/yisibl/status/2038475725465071922
  - Pretext’s enthusiasm is unusual. Text wrap in CSS is nothing new(CSS Exclusions)—Adobe even implemented it in Chrome, but it was later removed over differences in vision. 
  - The fact that browsers never kept pushing it suggests there is very little real demand for this feature.

- 
- 
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

- https://x.com/xicilion/status/2038507745067077636
  - 需要精确布局的场景是不能容忍这种误差的，稍不留神就换行了。
  - 它的核心逻辑是先分词，只要保证“不在不应该断开的地方断开”即可，这里用的是浏览器提供的分词api。分词完了就把分词作为一个簇去排版，每个簇都是最小的布局单位，中间不换行，用测量api去算宽度。 这个误差大概 1~2 像素。
  - 最后就是巨大的特殊情况列表。标点不在开头，各种语言特例等等。

- https://x.com/winter_cn/status/2038290733204201863
  - 这不是对measureText的简单封装，而是基于这个API写的一个排版引擎
  - 往多了说，也就做到了10%的css文本排版能力，却碰瓷css搞宣传，这让我觉得非常不真诚
  - 排版这个事情的难度其实是随着特性增加指数级增长的，把别的特性砍光多做个环绕排版并不能说明技术有多强
  - 环绕排版在css中迟迟不能推进，一方面是实现难，另一方面真的是用的场景太窄，大概也就能“把网页变得更有趣”了

- ### [I dug into Pretext codebase. Lessons we can learn. _202603](https://tigerabrodi.blog/i-dug-into-pretext-codebase-lessons-we-can-learn)
1. Separate what you know once from what changes
2. Canvas measureText as a cheap side door
3. Binary search over a cheap function
4. Parallel arrays instead of arrays of objects
5. Collect platform quirks into a profile object.(Pretext puts all platform differences in one typed object, computed once at startup. The rest of the code reads engineProfile.lineFitEpsilon. It does not know which browser it is on. The algorithm is clean. The quirks are in one place.)
6. Measure the error once. Correct for it forever.
7. Answer questions about results without building the results(Build a cheap path that answers questions about output without producing the output. Offer both paths. Let the caller choose.)
8. Check if already solved(Instead of reimplementing Unicode word boundary rules, it lets the browser handle that and applies its own merging and splitting on top.)

- ### 其实几年前有个库用 wasm 实现了一个类似 flexbox 的布局系统。
- https://x.com/unixzii/status/2038458974501314951
  - 仍然使用 DOM 渲染（就像 pretext 的 shaping 和 rasterizing 仍然还在用浏览器能力），但绕过了 CSS 布局计算，性能好很多。
  - https://github.com/nicbarker/clay /zlib/202603/cpp

- ### 我整理了 8 个非常炸裂的脑洞大开的案例
- https://x.com/axiaisacat/status/2038233070709436617

- ### 🌰 cursor now truncates file paths in the middle w pretext
- https://x.com/fredrikalindh/status/2039009480625754409
- middle truncation with pretext is such a small detail and such a big quality of life fix for anyone who lives in cursor all day

- this doesnt require pretext lol

- this is easily doable without pretext or canvas ??? what do you gain by adding that

- [javascript - Ellipsis in the middle of a text (Mac style) - Stack Overflow _202604](https://stackoverflow.com/questions/831552/ellipsis-in-the-middle-of-a-text-mac-style)
  - 很多js方案
  - 纯css方案: https://codepen.io/editor/uptonking/pen/019d4539-8f59-7fc4-be14-077eba66cc42

- ### 🌰 was playing with a similar idea a week ago. 
- https://x.com/vamsibatchuk/status/2037924109049311702
  - link/image元素在点击时, 通过环绕的布局展示图片/卡片

- https://x.com/lucas__crespo/status/2038312815249817653
  - intercepts pinch-to-zoom and resizes text instead of the page. Only two lines of code built on top of @_chenglou ’s pretext.
  - https://pinch-type.surge.sh/

- ### besides all the cool typography demos i have seen on here, one of the real-world use cases is unrestricted generative ui with dynamic spatial awareness
- https://x.com/_proteuss_/status/2038424238214824198
  - so i made a small demo comparing traditional DOM based generative ui vs pretext based rendering
  - traditional: render the streaming text inside a standard div with a fixed width. use getBoundingClientRect() inside a useEffect on every new token to calculate the current height of the text block so the 'whiteboard' can auto-expand and push other ui elements out of the way
  - pretext: use the pretext library. use prepare() and layout() to calculate the exact height of the incoming text stream in pure js (arithmetic) as tokens arrive. adjust the whiteboard container height based on these calculations without ever touching the DOM for measurements
  - https://github.com/protimroy/spatial-ai-lab
  - http://www.protimroy.com/spatial-ai-lab/

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
- we have had this with `shape-outside` .
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

# discuss-solutions
- ## 

- ## 

- ## 

- ## [Show HN: uWrap.js – A faster and more accurate text wrapping util in < 2KB | Hacker News _202504](https://news.ycombinator.com/item?id=43583478)
- https://github.com/leeoniya/uWrap /MIT/202508/ts
  - A 10x faster and more accurate text wrapping util in < 2KB (min)

- Looks like uWrap only handles latin characters and doesn't deal with things like soft hyphens or emoji correction, plus uWrap only handles `white-space: pre-line` while Pretext doesn't handle pre-line but does handle both normal and pre-wrap.
  - correct, it was meant for estimating row height for virtualizing a 100k row table with a latin-ish LTR charset (no emoji handling, etc). its scope is much narrower. still, the difference in perf is significant, which i have found to be true in general of AI-generated geenfield code.
- I've worked with text and in my experience all of these things (soft hyphens, emoji correction, non-latin languages, etc) are not exceptions you can easily incorporate later, but rather the rules that end up foundational parts of the codebase. That is to say, I wouldn't be so quick to call a library that only handles latin characters comparable to one that handles all this breath of things, and I also wouldn't be so quick to blame the performance delta on the assumption of greenfield AI-generated code.
  - no disagreement. i never claimed uWrap did anything more than it does. it was not meant for typography/text-layout but for line count estimation.however, for the use case of virtualization of data tables -- a use case pretext is also targeted at -- and in the common case of latin alphabets, right now pretext is significantly slower. 
- uWrap demo has text extending beyond text boxes all other the place on Safari, is that the price of simplicity?
  - Chrome is no different, for example, "RobertDowneyjr" is out of the box, so does "enthusiastic" in a couple of places.

- I plan to use this tool to pre-calculate the letter size ratios for all my fonts, then bake those into my non-JS server code as constants and use a similar wrapping algorithm. Now there's no runtime canvassing. Thanks for this code
  - You'd need more than just letter widths because of kerning and ligatures, for 100% accuracy. Anyway, fontkit can work on the server and can get individual glyph metrics as well as metrics for a run of glyphs.
- yep, uWrap internally builds a lookup table for char pairs that differ significantly in width together from just adding their raw widths.

- the use case of this is anything where I have lots of text on a canvas? Like, a canvas based game with thought bubbles or something like that?
  - it's where you need to know the wrap points of some text given a width of the container. since Canvas does not offer text wrapping, that is one use case, because you have to wrap manually.
  - my use case is determining the height of a table cell given a specific column width and text that needs to be rendered inside.

- we needed something like this for virtualization of the Table panel, data-heavy dropdowns, and long list views in Grafana. so i guess that's a three-in-one?
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
