---
title: thread-web-dev
tags: [frontend, thread, web]
created: 2020-12-05T07:43:47.005Z
modified: 2021-01-08T17:13:43.392Z
---

# thread-web-dev

# repeat

- ## This Pagination component might be a good test for a technical interview
- https://twitter.com/WebReflection/status/1484558920660262913
  - [Can You Recreate this Web Component?](https://hackernoon.com/developer-challenge-can-you-recreate-this-web-component)

- ## Is there any reason not to use HTTP PUT and DELETE in a web application?
- https://stackoverflow.com/questions/1101888
- Quite simply, the HTML 4.01 `form` element only allows the values "POST" and "GET" in its `method` attribute
  - an HTML document must conform to the HTML spec.
  - it explicitly disallows any `<form>` method except for POST and GET.
  - But this doesn't apply to Ajax requests
  - For example jQuery supports all HTTP methods
- Actually a fair amount of people use PUT and DELETE, mostly for non-browser APIs. Some examples are the Atom Publishing Protocol and the Google Data APIs
  - Beyond that, you don't see PUT/DELETE in common usage because most browsers don't support PUT and DELETE through Forms. HTML5 seems to be fixing this
  - The way it works for browser applications is: people design RESTful applications with PUT and DELETE in mind, then "tunnel" those requests through POSTs from the browser. 
- There are some comments on whether AJAX libraries support all the methods. 
  - It does come down to the actual browser implementation of `XMLHttpRequest`

- [http中的put、delete等请求为什么不安全？](https://www.zhihu.com/question/38770182)
- HTTP中那些method的真正区别只有那个单词拼写不一样。其他部分没有任何区别。
  - 各种Method的区别是语义上的。是为了让你的应用程序能够清晰简化的进行通信。对于HTTP本身来讲没有任何区别。当然安全性也没有任何区别。
  - 当然也有可能是一些其他的客观因素。比如公司斥巨资买了一个防火墙，发现只能拦截过滤POST和GET请求。
# discuss
- ## 

- ## 

- ## 

- ## A URL is a URI, but a URI is not always a URL.
- https://x.com/sergiodxa/status/1928582537003118593
  - e.g. a torrent magnet link is a URI, but not a URL, it identifies a resource (the torrent) but doesn't locate it via a protocol like HTTP or FTP.

- ## Use the `<datalist>` element to create native HTML autocomplete.
- https://x.com/denicmarko/status/1903431486335803801
  - <input list="items" /> ` + ` <datalist id="items"><option value="aa" /></datalist>`
- It used to have a horrible browser default design which was terrible to style. Don’t if there are better ways for its styling now.

- ## Each element remembers where it was scrolled to, even the virtualized element list, which is WAY dynamic and only rendered after the DOM has been measured.
- https://x.com/tannerlinsley/status/1880404505260617978
- how is this implemented?
  - It’s custom. Low overhead scroll tracking, session storage, location state keys.

- ## chrome 选定 dom 可以直接 ask ai
- https://x.com/hylarucoder/status/1870064803533967670
- 没有context, 不在runtime, 甚至都不是源代码，试了几次暂时弃置了

- ## I ran into something interesting: a "mouseenter" event will be re-triggered on a parent element if the user is over a child element, and that child is replaced with a new element
- https://x.com/alexandereardon/status/1853234614007128488

- ## 💡 I knew elements with IDs became global variables, but any child elements with a `name` attribute become properties on that global variable
- https://x.com/kilianvalkhof/status/1840739327354998987
  - `idElem.namedInput.onclick=()=>{}`

- But it applies *only for form* and its elements. These "form elements" are not necessarily direct form children. And even not necessarily children at all, since there is the "form" attribute we can use to link the "detached" element.
- Give the input a name of attributes and watch things break 
  - Sure there's a lot of footguns here, but it's nice for some quick little form stuff.

- ## Why is `cloneNode(true)` so broken in browsers today compared to `importNode(true)` ?
- https://x.com/trueadm/status/1792590536777375841
  - cloneNode doesn't work with lazy `<img>` elements in FF/Webkit
  - cloneNode doesn't work with pointer events in Chrome
  - cloneNode doesn't work properly with custom elements
  - Yet, `cloneNode` is still around 30% faster than `importNode` in our testing.

- In both the standard and in WebKit these end up calling the same underlying algorithm. Would be interesting to see some tests.
- It’s faster because it’s missing a bunch of features

- ## 看起来单个 observer会更快。 这不性能优化的点就来了，以后面试官问你就可以说你是怎么优化曝光组件的了
- https://twitter.com/wulianwen1/status/1788244518044852243
  - 我看大家写曝光组件的时候，一般会在组件中注册一个 intersectionObserver, 这样的话有多少个曝光的地方就会 new 多少个实例。但实际上一个 intersectionObserver 就可以观察多个元素，只需要一个单例就行了。但是这样会让代码变得复杂，而且不知道性能会不会比 new 多个要强

- ## Quick HTML tip: ordered lists come with a "start" property.
- https://twitter.com/stefanjudis/status/1780140328487727597
- My favorite is the `reversed` attribute

- ## TIL the `<option>` element has a "label" attribute.
- https://twitter.com/RogersKonnor/status/1769034451370082344
- What’s the difference between label and the innerHTML?
  - If label attribute isn't specifically set, reading it returns the element's text content.

- ## if you guys remember, Cloudflare moved away from NGINX to build their own proxy named Pingora
- https://twitter.com/hnasr/status/1762868114675687793
- I wonder if it performs better than NGINX for Wordpress installations that also uses cloudflare as a cdn 
  - my thoughts too, this was built for Cloudflare scale, I wonder the overhead is (for multi-pool connection for example) for smaller installations.

- ## IIRC at Nokia times, we developed Nokia Maps with Offline Navigation (RIP WebSQL) and all mobile browsers (Android 2 at that time or iOS 5) 
- https://twitter.com/WebReflection/status/1760950919779270758
  - and it was less than 100K & no framework used, it worked wonderfully well too

- ## Learn concepts instead of implementations/frameworks
- https://twitter.com/sseraphini/status/1760262122129207442
  - babel -> compilers
  - webpack -> bundlers
  - javascript -> programming logic
  - sql -> databases
  - redis -> cache
  - serverless, k8s, aws -> containers, linux, vm, DNS, IP
  - express -> HTTP/TCP/UDP
  - react -> html, css, js

- ## 整理了一份独立开发者出海工具库
- https://twitter.com/weijunext/status/1759857266646282394
- 可以多看看cloudflare，其服务包括了 数据库，邮件和网站分析。 最重要的，免费额度特别大。

- 推荐nextjs只是个人观点：vue与react切换的学习成本不算高，但是前端理解服务端的成本、了解生态技术栈的成本比较高，而且国外nextjs开源项目比nuxt多太多了，所以我认为一名熟悉vue的程序员学全栈框架，学nextjs成本不会比nuxt高，既然如此，学nextjs可以进入一个更大的社区、多一项技能，何乐而不为

- ## 昨天在为 Django 项目添加 Telegram 登录时，遇到了一个神奇的前端问题，花了足足一天半的时间进行调试
- https://twitter.com/Ehco1996/status/1746077907972403670
  - 大部分浏览器会默认打开 `noopener` ，需要配置特定的header才能让popup页面访问到opener

- ## I'm not sure any 100% spec-compliant programs for matching paths against ".gitignore" files exist, not even git probably. The problem:
- https://twitter.com/fabiospampinato/status/1733170282196500755
  1. Globs are meant to be case-insensitive.
  2. A filesystem could be case-insensitive or not.
  3. You could mount any filesystem at ~any path.
  - So basically if you have "/path/to/some/random/file.js" each segment of it could be the mount point of a filesystem with a different case sensitivity than its parent, which presumably(据推测; 大概, 可能) is such a weird scenario that nobody is actually accounting for it

- ## 8 Essential Internet Protocols You Must Know
- https://twitter.com/AmigosCode/status/1730204104838832135
  - 协议示例动画

- ## I still see people using `<script type="text/javascript">` and `<link type="text/css">` all the time 
- https://twitter.com/matthewcp/status/1729872010921328786
  - Why are you doing this, it hasn't been necessary in like 10 years!
- Lighthouse actually warns about this. Removing attribute will improve performance

- ## script标签会不会阻塞html加载
- https://twitter.com/wulianwen1/status/1724699387300069380
  - async支持html-parse时下载js，但js执行会阻塞html-parse
  - defer支持延迟下载和执行js，js在html-parse完成后才会执行

- ## 🤔 is importNode any better or different than cloneNode ?
- https://twitter.com/WebReflection/status/1721837891276431706
  - well, importNode for fragments uses a nodeType check + isShadowRoot check
  - cloneNode just clones the node
  - if you create nodes via template then: content.cloneNode(true) 👍

- I have observed that templates whose content is not imported/adopted but only cloned, if they have web components within them, those WCs will exhibit different upgrade timing behavior, often undesired behavior, such as elements not being upgraded when you would expect them to be. This could be browser specific. I can't recall if I observed this in only Chromium-based browsers or not.
  - Dunno but code speaks … in WebKit they end up doing the exact same thing, and as WebKit passes same W3C compat tests Chromium does, I expect Chromium or Firefox to be aligned there too. adoptNode is irrelevant in this thread as well + it does something completely different too.

- ## You can use `<hr />` in `<select>` now for chrome 119+
- https://twitter.com/zhaojinjiang/status/1718549113594376206

- ## People sometimes to to replicate lit-html with a system that returns an HTML strings and replaces the whole DOM each render.
- https://twitter.com/justinfagnani/status/1687119365001592832
  - Yes, that's simpler and a lot less code.
  - No, it's not good. Making minimal DOM changes is the whole game.
  - I do with you could write a good 10 line lit-html replacement. That's why we're working on the Template Instantiation proposal. But it *has* to handle updates, attributes, properties, events, lists, and composition. That's the MVP.

- Why so? Doing diffs in JavaScript is likely much slower than browser does.
  - The browser doesn't do diffs. If you set `innerHTML` it recreates all of the DOM.
  - lit-html also doesn't do diffs, because yes, diffs are too slow.
  - Don't do: el.innerHTML= html`contentString`; 
- How do you know? Browsers have many optimizations that are invisible.
  - It's specified and empirically provable that browsers don't do diffs.
  - The spec will be the DOM spec for innerHTML.

- You're saying that if I set the `innerHTML` of a div with a string that generates 5, 000 nodes, and it only differs from the existing 5, 000 nodes by a single class name, that it would be impossible for a browser to optimize that and reuse the existing nodes?
  - Yes
- You'd also realize that if browser's retained some elements and recreated some on assigning to innerHTML, it would terribly break expectation! They don't even have the right to make assumptions there.

- Recreating all the DOM is slow or quick? Why would it be slow, surely it has fast memory allocation, it is designed to be fast even with rubbish JS, aren’t we over optimising? Is there a benchmark showing the actual difference? You guys at Google should do such benchmark please
  - It can be very slow if you do it the root of the page, and maybe more importantly it destroys all of the DOM state. Focus, scroll, input state, state of components. It's not viable.

- ## Apparently, the JavaScript URL parser will omit the default port for a protocol (80 for HTTP and 443 for HTTPS) even if it was explicitly specified.
- https://twitter.com/ZoltanKochan/status/1684531065019416578
  - `new URL('http://localhost:80').port` 结果为空字符串

- ## DOMParser and innerHTML deactivate inline event handlers (except Chrome’s DOMParser does not deactivate `<img src=* onerror=“alert(‘evil’)”>` ).
- https://twitter.com/dfkaye/status/1682848179270606848
  - XHR.response doesn’t deactivate any. 
  - It’s best to define a CSP header for ‘script-src’ that at minimum excludes ‘unsafe-inline’.

- ## I learned that the `EventTarget` interface is a web-native event emitter. 
- https://twitter.com/stefanjudis/status/1673033968583581699
  - [How to use EventTarget as a web-native event emitter | Stefan Judis Web Development](https://www.stefanjudis.com/today-i-learned/how-to-use-eventtarget-as-a-web-native-event-emitter/)
- it has some downsides if you decide to implement the event contract supporting both browser and Node.js. EventTarget is also heavily DOM-oriented and operates with Events primarily.

- ## 通过 `<datalist>` 可以为 `<input>` 定义一个数据列表，实现类似 React Select 的下拉选择和过滤功能。
- https://twitter.com/novoreorx/status/1658531596818063361
  - 可惜交互太少了，不能 tab 补全之类的

- ## There are two DOM APIs that I'd love to exist today. 
- https://twitter.com/trueadm/status/1659679705862209536
  - `reconcileChildNodes(arrOfNodes)` ; 
  - `createDocumentFragment({persistent: true})` ; 
  - Their usage would be primarily by frameworks and libraries, resulting in less code and fewer bugs and more consistent performance

- ## Two types of issues I've seen in every web app I ever needed to work on: timezones and scrollbars. I dread them both equally.
- https://twitter.com/TkDodo/status/1645859388014448661

- Timezones I often feel pretty comfy with storing UTC in the db and then date-fns-tz based on other needs. 
  - It *does* suck if I need to store timezone separately, as for some reason storing timezones is just not done very often, but still.

- Timezones are kinda simple, 
  - On server: store everything and do all date calcs on UTC, return those dates as ISO strings to the front end.
  - On frontend: use date-fns and initialize the timezone according to the users timezone, show format the dates given that timezone. Voiala! 
- Agree. We did the same on the last project I’ve worked on
- What’s your plan for avoiding the flash of unstyled content before the date renders client side?

- Internationalization on top of per-user timezones. It's an abyss fractal of pain.

- 4 facets to the timezone challenge.
  - The domain itself.
  - People who think libs solve the problems (they don't do much these days...)
  - Engineers who don't understand them.
  - PMs who don't understand them.
- Fighting with people about it is harder than fighting the domain.

- I just refuse to modify scrollbars; leave user's workspace alone!

- Getting the scroll bar of a virtualised table (just a bunch of divs) to work consistent between all browsers is the stuff nightmares are made of

- I usually use the ScrollArea component from @radix_ui instead of the built-in scrollbars. 
  - It offers cross-platform styling + other niceties.

- ## sunday webdev challenge: can you think of a way to test network connectivity that *does not* print an error to dev tools?
- https://twitter.com/aboodman/status/1632071181749862401
  - For Replicache we want to periodically test connectivity while offline. It's *not* an error for us to be offline, so don't want to spam console though.
- And first prize goes to @msnegurski with the idea to use a web worker.
  - Actually the error still goes to the network tab though
- Maybe you could abuse OPTIONS preflight requsts for this
  - Sadly no, Chrome is too clever. It only treats the actual preflight request this way, not any old OPTIONS request.
- Navigator.onLine exists, but AFAIK only tests for "hard lack of connectivity" (no network iface), not "soft lack of connectivity" (LieFi, packet loss)

- ## Is there a DOM node that has no impact on visual/layout that can be used as a form of marker? 
- https://twitter.com/trueadm/status/1632136227892633603
  - Sort of like a comment node, but one that you can lookup via a query selector?
  - I also tried using an element with display: contents, but that doesn't seem to work well.
- If you don't want it to have children, you can use script or template.
- I did not try `<meta>` ! Let me look into it.
- script or style tags won’t do?
  - I tried that. It causes perf issues. I want to have a marker element that I can replace with some dynamic content.
- label? or `<blink>` ? `<object> or <input type=hidden>`

  - Causes issues with the accessibility tree.
- Depending on context,  `<wbr>` might work for you
  - We're using comments and a tree walker for what is probably a similar use case. Really wish there were such an element or that xpath selectors were faster.
  - Yeah. I saw Solid does something similar by inserting tree path into an attribute?
  - it does for both top-level elements (fr components) and use comments for Suspense boundaries (I guess there are other cases as well)
- I don't think so 🤔 I think about the best that can be done is a comment node with some id as the value, then using a TreeWalker with a SHOW_COMMENT filter, and manually finding the one with the value you are looking for.

- Should it have children? If so, try span/div with display:contents

- ## 8 modern browser APIs you might not know, but really should:
- https://twitter.com/Steve8708/status/1625516871633211393
- `structuredClone()` gives you browser native deep cloning that  supports a variety of types like Date, Set, Map, etc
- `Promise.allSettled` helps you await multiple promises concurrently to increase perceived performance, while still handling errors effectively
- CSS `:is(), :where(), :has()` gives you a handy way to clean up redundant selectors
- new `URL()` gives you a native interface for parsing and manipulating URLs
- `Intl` gives you browser native date, time, number (and more!) formatting
- `all: unset` can make styling a lot easier
- Are you using modern attributes to ensure your images load optimally?
  - Do you know how and when to use `decoding=async` , `loading=lazy` , fetchpriority, `<picture>` , `aspect-ratio` , or `srcset` ?
- JS `Map` s are wildly underutilized - refresh yourself on the performance, functionality, and ergonomic benefits

- The barcode detection API (experimental) 🧪 is one I learned this year. 
- Which ones does node implement?
  - structuredClone(), URL(), Map() and Promise.allSettled() if I am not mistaken.
- Any discussion of interesting browser APIs cannot be complete without mentioning HTMLMediaElement.canPlayType(), which can return the values: "probably", "maybe", and ""

- ## [You’ve Got Options for Removing Event Listeners](https://www.macarthur.me/posts/options-for-removing-event-listeners)
1. removeEventListener()
2. addEventListener(..., { once })
3. clone + replace the node
4. AbortController

- ## 前端调试 outline: 1px solid red; 
- https://twitter.com/_justineo/status/1620930072759902210
  - ProTip：建议改成半透明的，可以方便看出叠加；增加 outline-offset: -1px 避免被 clip。

- ## TIL FormData and query string both have only string value types.
- https://twitter.com/oleg008/status/1619808119349202945
  - Having typed data using these is fundamentally impossible without using additional encoding on top.
  - E.g. to send a boolean or a number over query you basically would use a JSON string.
- TRPC suggests to JSON.stringify that stuff and put it into query or body, which is ugly, but its not TRPC's fault.
- This is the motivation behind a fair amount of @tan_stack Router
- But it makes sense. FormData and query are meant to pass data from client to server, and in HTTP only text can be transferred. Everything else, including JSON, is an abstraction on top of plain text.

- ## TIL that Google Maps implements a scheduler in the browser main thread, similar to React!
- https://twitter.com/geoffreylitt/status/1615761940055212032
- I think any sufficiently large graphics app has a scheduler of some form, whether ad-hoc or not. You implement a scheduler the moment you abstract around `requestAnimationFrame`

- ## [Compress An Image Before Upload With JavaScript - PQINA](https://pqina.nl/blog/compress-image-before-upload/)
- Compress An Image Before Upload With JavaScript - without any external dependency. Neat trick! Did you know that browsers have built-in image compression features? 

- ## URLPattern is just a string matcher, like RegExp. React Router's route matching algorithm takes into account route nesting. It's a little more complex than a simple string pattern match.
- https://twitter.com/mjackson/status/1532972006471180288
- Unrelated: URLPattern shouldn’t have become a standard, imo. It’s slow by design because it encourages matching every route individually instead of all at once, and matching each route typically needs a regex
  - Yeah, agree. I took one look at it and thought “this isn’t going to help at all”. It’s a classic case of premature standardization.

- ## A few screens of JSON data
- https://twitter.com/iamakulov/status/1534617100471439361
  - (this is common with SSR when you’re inlining the initial data to load it on the client. it’s fine when it lives in the end of `<body>` – but if you put it into `<head>` , it will delay the First Paint)

- ## process.env. NODE_ENV in browser code needs to die a quick and painful death.
- https://twitter.com/justinfagnani/status/1532928015738363905
- How to make `globalThis.ENV` a thing though? Some big framework needs to just adopt the convention so others can copy...
  - Make a development build under the officially sanctioned(许可；准许) "development" export condition. Don't dynamically check anything.
  - At the *very* least write `globalThis?.process?.ENV` so you don't crash in browsers.
- The ENV branching usage pattern with dead code replacements may still not fall easily... so may benefit from both alternatives. `globalThis?.ENV` would be ideal IMO, we shouldn't have a `process` global created by every browser build....

- maybe javascript needs some bundler｜compiler spec to solve this
  - We already have it: It's called "export conditions"

- ## Is there a way to keep track of V8 releases and their features? AFAICT, the V8 blog (*) skips releases.
- https://twitter.com/rauschma/status/1532327360237797377
- I've been able to track V8 releases with releases of Chromium, but features I've really only been able to find on the blog.
- Not ideal, but I watch the kangax/compat-table repository and the maintainers/contributors usually open PRs for new supported features soon enough.

- ## Does anyone know how to hide/remove horizontal scroll bars on scrollable elements?
- https://twitter.com/samselikoff/status/1532013589703409664
  - I noticed the scrolling is built with css scroll-snap (scrolling still works without JS). 

```SCSS
& {
  scrollbar-width: none;
}

&::-webkit-scrollbar {
  display: none;
}
```

```CSS
.carousel {
  scroll-snap-type: x mandatory;
}

.carousel .item {
  scroll-snap-align: start;
}
```

- I have successfully used `scroll-snap-type` with `scrollbar-width: none` to get the scrolling without scrollbars. Seems Stripe does the same they have that on the `TestimonialCarousel__track` class.

- ## If your site has a dark theme, make sure to set: `:root { color-scheme: dark }` So scroll bars are also dark.
- https://twitter.com/diegohaz/status/1529543787311144961
  - If you need to set it programmatically with JavaScript:
  - document.documentElement.style.colorScheme = "dark"

- which is better this vs `<meta name="color-scheme" content="dark">` in head?
  - You can use both, but the CSS color-scheme is more flexible since you can add it to individual elements

- ## Does there exist a decent, modern boilerplate for creating browser devtools? 
- https://twitter.com/DavidKPiano/status/1512901804127830019
- In the past I basically just ripped off @tannerlinsley pattern, he just mounts a “panel” (absolute positioned Div) within the app :)

- ## 我在推微前端时，经常会被问： “为什么不用 iframe？”
- https://twitter.com/ThaddeusJiang/status/1514604744790376450
1. url 不同步。浏览器刷新 iframe url 状态丢失、后退前进按钮无法使用。
2. UI 不同步，DOM 结构不共享。想象一下屏幕右下角 1/4 的 iframe 里来一个带遮罩层的弹框，同时我们要求这个弹框要浏览器居中显示，还要浏览器 resize 时自动居中..
3. 全局上下文完全隔离，内存变量不共享。iframe 内外系统的通信、数据同步等需求，主应用的 cookie 要透传到根域名都不同的子应用中实现免登效果。
4. 慢。每次子应用进入都是一次浏览器上下文重建、资源重新加载的过程。
- 其中有的问题比较好解决(问题1)，有的问题我们可以睁一只眼闭一只眼(问题4)，但有的问题我们则很难解决(问题3)甚至无法解决(问题2)，
  - 而这些无法解决的问题恰恰又会给产品带来非常严重的体验问题， 最终导致我们舍弃了 iframe 方案。

- ## DOM diffing is surely one of the most discussed, explored, and implemented topics, 
- https://twitter.com/WebReflection/status/1515083477275877382
  - when it comes to Web development ... and the response from vendors is: counterproductive to keep repeating the same discussion every 2-3 years
  - That's how slow/bad Web is
  - That discussion tl; dr is like: It seems hard to even swap nodes w/o causing side effects like reloading an iframe

- ## 不知道这个行为是不是符合规范，如果某行 css 中出现了一个伪元素下带其他元素的选择器，那么这一行的全部选择器都是无效的，也没有任何错误提示，
- https://twitter.com/_Xheldon/status/1514994277100945408
  - 在 Devtools 中检查元素压根看不到这行的任何规则，Chrome 和 Safari 均如此

- ## I have found a cheap + simple way of generating custom drag previews with browser powered drag and drop
- https://twitter.com/alexandereardon/status/1510826920023248900

- ## Quick HTML tip: I just discovered that `li` elements support a `value` attribute to configure the start of an ordered list.
- https://twitter.com/stefanjudis/status/1510922335104245766
  - You can also use the `start` attribute for that.
- And to top things off: there’s the `type` attribute as well

- ## Unexpected token U in JSON at position 0 is a very common error that happens in JavaScript due to JSON.parse trying to parse an undefined value, always try-catch JSON.parse
- https://twitter.com/Andrei_Calazans/status/1511058521235746819

- ## I think my ideal learning path is 1) find good toy implementation, 2) port to a different language.
- https://twitter.com/geoffreylitt/status/1493410385168420868
  - Porting can be fast, efficient, methodical -- but also forces enough engagement to actually understand. 
  - Easily 10x more effective than just reading source
  - Recent example: had a hard time understanding Adapton, an incremental computation system. Luckily found miniAdapton, a beautiful small Scheme implementation. After porting that to Typescript, could go back and actually grok the original paper

- ## "Using Google Fonts is faster, as the font might already be in the browser's cache!"
- https://twitter.com/PixelAmbacht/status/1494272370076536840
  - ⚠️ This hasn't been true for over a year now: cross domain caching has been disabled in all major browsers. 
  - Using a CDN for fonts is NEVER faster than self-hosting!
- Totally correct thread, but Google Fonts supports self hosting and so this all only applies when using the Google Fonts CDN which really should only be used for quick hacks at this point.

- ## Been doing some prototyping lately. Turns out, JavaScript with no types is nice, actually!
- https://twitter.com/devongovett/status/1490729034803724289
- You can use tsc as a js linter...catches some things eslint doesn't, ime.3

- I have two prototyping workflows:
  1) TS with no types, everything `any` , then 'harden' until everything's strictly typed.
  2) TS types and function signatures, strictly typed, but with no code, then add the function bodies after all the types compile.
- ## Question for the #webperf folks, is `<script type="application/ld+json">` render blocking?
- https://twitter.com/TimVereecke/status/1490011729643945990
- TL; DR No.
  - Spec-wise, scripts that are not JS are not processed by the browser at all, and their src attribute is ignored. Naturally nothing will happen until the inline content is downloaded and the next tag is parsed, but otherwise there is no "render-blocking" operation AFAIK

- ## How to query a database from CSS
- https://twitter.com/argyleink/status/1489280746061631489
  - [Yes, I can connect to a DB in CSS](https://www.leemeichin.com/posts/yes-i-can-connect-to-a-db-in-css.html)

```CSS
.query-display {
  background: paint(sql-css);
}

main {
  --sql-query: SELECT * FROM genre;
  --sql-database: url(...);
}
```

- Sure you can, but …why?!?
  - "It's been a hell of a long time since I last embarked on a quality shitpost project, in fact it's been so long that back then I probably didn't even have the word shitpost in my vocabulary."

- ## We made a Chinese version of Wordle! 汉兜 - 汉字 Wordle 每天一词，汉字、声母、韵母、声调都会独立进行颜色判断，同时也支持繁体输入与注音，欢迎来玩
- https://twitter.com/antfu7/status/1487459883037634563
  - https://handle.antfu.me/

- ## did my best to condense all the lessons of processing files dragged & dropped onto a website into one module that you can use
- https://github.com/placemark/flat-drop-files

- ## New quick tip: CSS-only External Link Favicons
- https://www.zachleat.com/web/external-link-favicons/

- ## Working with my routes as arrays/objects instead of JSX is refreshing. 
- https://twitter.com/tannerlinsley/status/1459015713390092291
  - Many have have told me that JSX routes look "cleaner" to them, but at the end of the day, it's an abstraction that doesn't really give me much in return.
- What’s the difference? I just have a big array of objects that maps to a route component?
  - Yeah, that's the idea. I mean, that's what's happening under the hood with most routers either way.

- ## I am ONCE AGAIN reminding you: do not use heading elements unless they introduce a section of content!
- https://twitter.com/heydonworks/status/1466797867369177092
  - If the only content of your card component is a heading, it shouldn’t be a heading—it should just be big text. #a11y

- ## I can't believe devs still don't `document.querySelector(location.hash).scrollIntoView()` when content is ready!
- https://twitter.com/WebReflection/status/1470770711174262790
  - a constantly broken pattern:
  * a link with a name/id is shared
  * the SPA loads content for that link on demand
  * the whole intent of pin-pointing the link is lost
- that and styling :target

- ## Why are img tags inline elements? What's the rationale behind that?
- https://twitter.com/Andrei_Calazans/status/1471799716426010624
- I think it's closely related to RTF specification at time. Microsoft Word also makes images inline by default, and also, it appears to be heritage of RTF.

- ## there are developers writing articles about how great vanilla JS is compared to libraries, the same developers that then write stuff like: `removeEventListener(type, obj.fn.bind(obj))` as if that ever worked. these mistakes are the reasons most devs use libraries: they don't test
- https://twitter.com/WebReflection/status/1476088827831889927

- ## New Node module: "html-segmentator", a thing for splitting an HTML string into its top-level tags. 
- https://twitter.com/fabiospampinato/status/1444436271120752641
  - It can unlock some extra performance when you need to do some work on your HTML (parsing, sanitizing etc.) and you can cache the result for unchanged tags.
  - You should probably use DOMParser instead for this, but the thing is **DOMParser is synchronous** and the HTML string could be arbitrarily large, you can't just block the main thread indefinitely like that. 
  - Unfortunately **DOMParser can't run in a Web Worker**, but this module can.

- ## at work i need to change the cursor dynamically, tried to translate3d html but it's laggy.
- https://twitter.com/0xca0a/status/1441327362914742277
  - the idea is that you have a portal into the dom cursor: `<Cursor>` , and everything inside is svg. but it's just react, so you can form components, bind them to state, animate contents, use anything in the eco system, do whatever you want basically.
  - this is not moving a html fragment along though it literally renders the document.body.style.cursor. 
  - moving stuff along is too laggy because the browser is unable to keep up with the cursor and the events come in when it already miles away.
- you mean like rendering a whole ass svg into cursor: url(...)
  - const callback = () => (document.body.style.cursor = `url('data:image/svg+xml; base64, ${btoa(node.outerHTML)}'), auto` )
- css transforms tied to mouse in general are impossibly slow. that's why these fancy agency sites always smooth-lerp them. base64 svg can drop frames for all i care, it's not that i *need* to animate it 60fps, but it will cling to the cursor, it *is* the cursor
- addEventListener("pointermove", e => div.style.transform = `translate3d(${e.clientX}px, ${e.clientY}px, 0)` , { passive: true })
- Can’t you just change the same SVG instance programmatically vs re-rendering the whole thing?
  - thats what react does, only changes single props. but eventually you need to base64 it for it to be a cursor, so the little time that react saves is probably for nothing.

- ## Designing even simple websites is so hard these days! So many variables and constraints to consider:
- https://twitter.com/devongovett/status/1439362488995237889
  - Responsive design across 4+ breakpoints
  - Light + dark mode
  - Accessible color contrast
  - Animations, but also reduce motion setting
  - Touch and keyboard friendly interactivity
- [Prioritize optimization axes on the web](https://notebook.lachlanjc.com/2021-08-23_priotize_optimization_axes_on_the_web/)
- This is why it's pedantic to build with plain old javascript. You'll end up building a mini framework yourself.

- ## A lot of folks think serving JSON is more efficient than HTML, but once gzipped they're often the same. Sometimes HTML is smaller.
- https://twitter.com/jaffathecake/status/930836616779878401
- Important benefit of JSON over HTML
  - for SPAs that reside for a long time in a browser tomorrow's JSON is much more likely to still work with the loaded page than tomorrow's HTML.

- ## I remembered document.domain is a thing and ruined my day
- https://twitter.com/jaffathecake/status/1436340091098652692
- Forget about it by remembering the existence of the one falsy object: document.all.
- I have that with navigator.userAgent and navigator.onLine
- I recently used it to make communication with an iframe on a different subdomain work. Not aware of any alternatives
  - Websockets? Maybe webRTC? Window.postMessage?
  - True, but admittedly it was some marketing script. I was thinking more in the direction of CSP headers.
- And that's without having to worry about IE8. I've written posts on the topic. I think I even did a velocity talk on it once.

- ## I recently learned about Event.composedPath() that returns an array of objects (DOM up to a Window) on which listeners will be invoked
- https://twitter.com/maxkoretskyi/status/1434955497082441732
- Hm.. sounds like nice way to handle outside click
  - It is, but you only really need it if you are working with Shadow DOM. Otherwise plain `Element.contains()` is enough.

- ## 30+ HTML tags to consider before using a div; Why does using specific tags instead of divs matter? 
- https://twitter.com/housecor/status/1434168410364157965
  ✅ Accessible (used by screen readers)
  ✅ Machine parsable (SEO, metadata parsing, etc)
  ✅ Maintainable (easier for fellow devs to read and understand)
  ✅ Testable (target for tests)
- Also, this is why code reviews are so critical. Enforcing good semantic markup can’t be automated. It requires a human to consider the content and context.

- ## Improve the performance of your apps by lazy-loading iframes
- https://twitter.com/mgechev/status/1427125495292956675
  - Just specify the attribute "loading=lazy"
- [It's time to lazy-load offscreen iframes!](https://web.dev/iframe-lazy-loading/)

- ## Anyone found a good way to test for accurate scrollBehavior support?
- https://twitter.com/sebastienlorber/status/1420476101491630080
  - Getting some false positives on Windows+Chrome

- ## If you're working on a tool that writes files to disk (like a compiler, babel/postcss/etc), it would be cool if there were an option to say: "Don't write to disk if the file is unchanged."
- https://twitter.com/kentcdodds/status/1418719232271929346
  - Otherwise, filewatchers will trigger even when there weren't content changes
- I think this makes more sense to be the filewatcher’s responsibility? The watcher could be configured in one place and just compare file hashes, otherwise you’d have to configure every tool
- The filewatcher having the cache for what has changed or not makes more sense. From a tools perspective it is **always cheaper to write rather than keep a cache or read before write**.
- Having trouble seeing why this just wouldn’t always be the behavior?
  - I think it’s because writing straight to the fs is just easier to implement. To implement the correct behaviour you’d have to perform an atomic write (write to new file and rename).

- ## There are still users browsing with a Chrome 37 engine (7 years ago), 
- https://twitter.com/firt/status/1415645416276860929
  - not because they don't update their browsers 
  - but because it's Facebook Mobile Browser on Android 5 using a webview. 
  - Facebook does NOT honor user browser choice leaving that user with an old engine.
  - That user was navigating with Facebook 326 (launched last month), so she was updating her native apps; we can assume her browser was updated as well, and it can be Chrome 91, but the webview is still old, giving the user a bad experience, errors and probably security problems.
- Not arguing with your main point here but IIRC in 5.0 and above the system webview is an APK that can be updated just like Chrome can. Wonder if it’s a third party Android fork, Amazon or something?

- ##  I've seen a lot of examples of custom selects and comboboxes in various libraries relying on aria-activedescendant. 
- https://twitter.com/devongovett/status/1312150515220799489
  - I'd *highly* recommend avoiding this if possible. 
  - It does not work with mobile screen readers, and changes are often not announced. 
  - Use real DOM focus!
  - TL; DR: test your code with real devices and AT! 
- react-aria solves this?
  - Not yet! To clarify, we use real DOM focus for our select component and all other published components due to issues we've seen in the past. ComboBox is a work in progress.
- This is a major headache, especially for junior developers trying to write tests. Where is my Select component?  Yeah check the Dom, it’s outside the app’s root. Time to mock those. Feels very unnecessary...

- ## HCL Wizard is a perceptually uniform color selection tool based on the HCL color model.
- https://twitter.com/DataVizSociety/status/1412479722374770693
  - [Perceptual Uniformity with HCL Wizard](https://nightingaledvs.com/perceptual-uniformity-with-hcl-wizard/)

- ## I feel like it's at least monthly that I'm using @ryanflorence 's @reach/observe-rect package
- https://twitter.com/tannerlinsley/status/1412498450290077698
- Curious to know what's the difference with ResizeObserver
  - ResizeObserver won't notify if the element's rect moved but didn't resize.
- Just checked implementation for rect and oooof, it gonna kill application or two if used improperly or too much. I’ll better mix `ResizeObserver` and `onScroll` event.
  - You should write a new implementation with a similar api then.
  - Not possible without understanding WHY it is used. Right now I know only HOW it does work. tell me about your use case and the reasons to track element position relative to the screen
  - Tooltip or anchored panel positioning
- Getting the rect on animation frame shouldn’t be very performant. I’d stick with `ResizeObserver` by default, which has a very similar API as well.
  - I just mean that for 99% of the cases a ResizeObserver is a better tool. Tbh I can count on a single finger the number of times I’ve had to watch for rect changes due to scroll/resize/etc. 

- ## Number one accessibility tip: learn how to use the screen reader that’s built into your computer/phone. Then test every library you use yourself.
- https://twitter.com/devongovett/status/1410277820622802944
  - Unfortunately, many claim they are accessible because they have a few ARIA attributes, but it’s way more complicated than that.
  - The docs claimed it was accessible because it followed the ARIA authoring practices.
  - Unfortunately, ARIA authoring practices are not bullet proof. They’re just a guide. They assume perfect ARIA support (definitely does not exist) and any customizations you make can have drastic effects. Testing yourself with real assistive tech is the only way to verify.
- every screen reader is different, and even then different users have different settings. Accessibility is like design in that it can be quite subjective.
  - Different screen readers sound like different shots and the ability to holistically understand the whole picture. But how we can hook into those engines…

- ## How do you deal with exceptions in Node.js?
- https://twitter.com/hanspagel/status/1410192448601608198
  - When I don’t catch them, the whole process will exit. Bad, rigIht?
  - When I catch them, I have to make sure to log them somewhere, right?
- I typically just catch `process.on('uncaughtException')` and log it to sentry
- We use @getsentry for that
- move away from LogStash towards @fluentd or eventually @opentelemetry

- ## Loading new style tags into a page that only apply to the new content seems like it would be fast but it requires reapplying rules to all existing content. 
- https://twitter.com/sebmarkbage/status/1409884048185495562
  - Making it a factor of all the nodes on the page. This is counter intuitive but a huge perf consideration on larger pages.
- If you remove all existing content before, it might be less of an issue, but that preclude you from animating between two pages or subscreens. 
  - It also doesn't work well with progressively showing content if inserting styles change the previous content. You're repaying the cost.
- One way to solve this is by literally inlining styles. 
  - That's counter intuitively more expensive than you'd think because each one has to be converted to the internal representation which is way more expensive than looking up an existing value in a Map.
- These two things together lead a lot of perf sensitive people to conclude that "Atomic CSS" style solutions where you produce large reusable sheets with small rules are the way to go.
  - Tailwind is another way to do this. 
  - Statically extracting them using a compiler is another.

- ## There is an `<hr>` tag but there is no `<vr>` tag for vertical separator. I guess they never thought you may want to separate content vertically?
- https://twitter.com/oleg008/status/1407653485647126534
- [see Separator of Radix UI](https://radix-ui.com/primitives/docs/components/separator)

- ## TIL `ResizeObserver` & `IntersectionObserver` need to be manually disconnected, else they leak memory through their callback.
- https://twitter.com/jaffathecake/status/1405437361643790337
  - This happens in all browsers. 
  - `MutationObserver` and event listeners don't have this issue. 
  - Make sure you manually disconnect resize/intersection observers!
- Now you made me wonder which way `PerformanceObservers` go. How do MutationObservers not leak memory? Hold weak refs to the callbacks?
  - The other APIs are smart enough to realise the callback will never happen again, because the means to reconnect the element to the document (or manually dispatch an event) are gone. PerformanceObservers are always global, so they always need disconnecting/unobserving manually.
- I've made it a habit of manually unsubscribing(?) everything I do attach, be it IntersectionObserver or event listeners. It is a bit verbose at times but I've found that it forces me to think what happens when elements/components are torn down, which is quite easy to overlook.
- WebKit folks are working on this now

- ## when somebody asks "how would I do [x]", the answer is: Same basic strategy as with PHP, Rails, Laravel, express, etc. Then here are some clientside hooks to make the UX super fancy".
- https://twitter.com/ryanflorence/status/1406064047712210946
  - lots of folks have put a JWT in local storage but never "Set-Cookie" in HTTP headers.
  - I'm finding many web devs today don't know what the baseline behaviors are! We have to teach how the web works first

- ## Does anyone know if localStorage read/writes are synchronous between different tabs and windows?
- https://twitter.com/tannerlinsley/status/1402021739513597957
  - [Define how localStorage is synchronized between browser tabs/windows](https://github.com/whatwg/html/issues/403)
- Between tabs, localStorage is, sessionStorage isn't. Not sure about between windows
- I think it’s synchronous. And also persistent. Meaning that if you change it from a tab, it’ll also be changed on the other one. But I believe seeing the change in the other tab requires page refresh unless you have some sort of event listener on it.
- Wouldn’t that require LS updates to be subscribe-able? Or am I misunderstanding your question?

- ## 更好的做法：在if/else中处理差异，尽快结束分支，回到主线逻辑处理剩下相同/相似的部分。
- https://twitter.com/TooooooBug/status/1401718371947716609
  - 代码示例是为了说明，不要写if else，可以写多个if，在前面先处理else的逻辑

- ## Is there a reasonable way to get a list of all the html entities directly from the browser itself without shipping a whole damn list containing all of them?
- https://twitter.com/fabiospampinato/status/1400429400785555462
  - I can't stand shipping a ~12kb min+gzip list of all those damn entities, ~95% of which I guess pretty much nobody even knows about or uses.
- maybe I don't even need a list, I can just let the browser to its work:

```JS
const decode = entity => {
  const div = document.createElement('div');
  div.innerHTML = entity;
  return div.textContent;
};
decode('&#70;'); // => F
```

- In theory this is also more forward-compatible, it they'll extend the list of entities that function will always work without needing to be updated (assuming you are in a browser to being with though).

- ##  `addEventListener` could automatically clean up your listener if it would have to be invoked only once
- https://twitter.com/mgechev/status/1399584040815108098
  - additionally, you can specify `capture` rather than bubble and set the listener as `passive` , which is useful for improving scrolling performance

- ## Why are race conditions so tricky to prevent and debug? In my opinion, a couple of reasons:
- https://twitter.com/DavidKPiano/status/1396819218205655042
  - Time is one of the most neglected variables.
  - We tend to think of logic as a fixed sequence, and seldom consider that time can affect the order of events in the sequence.
  - And because of that, there's actually a combinatorial explosion of sequences in which events can occur, 
  - and it's difficult to predict and simulate all those possible sequences. Race conditions live in the unexpected sequences.

- ## The browser puts up new frames for every single motion on the page, even when scrolling.
  - To provide a smooth experience, it has to prepare each frame in 16.66 ms (60 fps)
  - To help the browser with that, we need to have our JS callbacks run FAST & at the RIGHT TIME (during each frame)
  - If a callback runs near the end of a frame, the frame might exceed its 16.66 ms deadline (causing it to be delayed/dropped)
  - `requestAnimationFrame` helps with timing
- It's best to do DOM manipulations or style changes (even when not doing animations) via requestAnimationFrame, as it schedules the callback to run at the start of the next frame

- ## Is there an open source implementation of http://vectormagic.com / http://vectorizer.io? That takes a png and outputs a svg.
- https://twitter.com/Vjeux/status/1387828983522234370
- Often times these sorts of vectorization tools are based on the Potrace algorithm. There’s a port of it in node, but it’s not great performance wise.
  - https://github.com/tooolbox/node-potrace#readme

- ## new image codecs this generation: AVIF, JPEG-XL, WebPv2.
- https://twitter.com/jaffathecake/status/1387715305112211457
- Remember, for most images on the web, you're aiming for "not bad" rather than "almost lossless".
- JPEG-XL and WebPv2 aren't ready yet, so they're not 100% representative. Also, how the images look as they load is something we'll only really know as they land in browsers.

- ## Safari really is the new IE
- https://twitter.com/MarijnJH/status/1387049528927289346
  - my users keep bringing me new obscure bugs, they never get fixed, 
  - and one doesn't really get the impression that the company in control cares all that much anymore.
- As a bonus, debugging Mobile Safari is a giant pain when you're not developing on a Mac. 
  - When a new issue with iOS in the title is reported, my stomach sinks.
- They(Apple) are also essentially using their position to block consensus on platform progress in a similar manner
- What’s the reasoning again for MS having to allow users a choice of browser during os onboarding while Apple gets away blocking everything thats not Safari from iOS?
  - MS was forced to do so after an anti-monopoly ruling. Apple also deserves the same fate.
- Apple uses their position on iOS to hobble other browsers -- requiring them to use JavaScriptCore or pure interpretation (no JIT).
  - Actually, JavaScriptCore is a quite good JavaScript engine. 
  - The bigger problem is Apple's restriction that browsers *must* use WebKit, not their own rendering engine, letting Apple control how good web apps can be -- some say to force people to build apps and give Apple 30%.
- It(Safari) might be the new IE regarding compatibility, but Chrome is the new IE regarding monopoly and making up their own standards
  - I'm not advocating for Chrome as a whole. I am simply defending their aggressive web standards development. 

- ## How to handle reloading pages created with POST
- https://github.com/whatwg/html/issues/6600
- What to spec
- Manually refreshing a page where the top-level was submitted via POST should show a prompt. I'm not sure about location.reload(). I think it should either downgrade to GET, or show a prompt.
- Using pushState means reloads of that document will be GET, even if the pushState doesn't change the URL, or only the hash of the URL changes.
- Changing the hash of the URL by other means doesn't change anything in terms of refreshes. Refreshes will still show a prompt and use POST.
- Traversing to a page previously fetched with POST will show an error page. If it's top-level, the error page can invite the user to refresh, which will prompt and re-POST. If it's nested, the error is not recoverable.

- ## I hate to be the one to tell you this, but serviceworker didn't make offline-first any easier.
- https://twitter.com/aboodman/status/1383157955248283649
- we ended up removing it entirely, it was too expensive to keep trying to debug the issues
  - [Goodbye Offline Page](https://dev.to/devteam/goodbye-offline-page-5d98)
  - the TLDR; : we weren't sure about what was actually going on and were tired of threading in the dark and had related tech debt, by removing it we put a stop to it all.
  - Aggressive edge caching plus InstantClick plus not enough service worker related expertise in the team doomed it
- Strong disagree

- ## I've been trying to persuade AVIF folks to allow a 'preview' frame at the start of the stream.
- https://twitter.com/jaffathecake/status/1382608978400702465
- I can confirm that some people (🤚) hate this “feature”, mostly because the LQIP is often not replaced with the final image 
  - I guess it would be much better with a native support, without relying on additional JS.
  - The alternative for the "failure to fully load" case is just empty space.
  - I prefer empty space over useless LQIP. At least I know something better is supposed to load.
  - As I said, a native solution would have less issues, at least on the JS side.
  - With JS-based LQIP, "straight away" is not the main goal (for me), I can wait a little. But the final image often doesn't load at all (even if I wait for it) when I go on Medium.
- Why an area of the page might not load straight away
  - Dependent on JS
  - In an iframe
  - In the cell of a grid that hasn't been parsed yet
  - Dependent on web fonts that haven't loaded yet

- ## Little pro-tip: Firefox is *so* much smoother than Chrome when it comes to window resizing, at least on the sites I've tested with.
- https://twitter.com/JoshWComeau/status/1379849269692207108
  - I switch to FF whenever I need to record a GIF of a window resize for my CSS course.
- I've noticed Chrome is only janky if devtools is open and you resize
- What I do is keep the devtools narrow and turn on mobile emulation with the "Responsive" option instead of a device 
- In Firefox you can also close the dev tools but keep the resizer. In Chrome you have to move the dev tools to the side or pop it out to get it out of the way
- Firefox is my go-to browser for debugging layout issues as well

- ## If you had to choose one browser API that’s the most frustrating to work with, what would it be?
- https://twitter.com/devongovett/status/1372215804318613510
  - I’ll go first: the drag and drop/clipboard APIs. OMG they are so so so bad. 
  - Not only is the API bad, but the implementations in browsers are incredibly buggy and inconsistent.
  - The dnd API was first implemented in IE 5, and then subsequently copied by other browsers and standardized in HTML5. It's honestly astonishing that it basically hasn't been touched since then. Here's an article from 2009 that explains how bad it is.
- "If you had to choose one" - Immediately lists two
  -  They are really the same API. They both use the DataTransfer API, which is really what I'm talking about. But I thought people wouldn't know that specifically, and understand dnd/clipboard better. 
- We should differentiate between bad design and low level capabilities... 
  - mostly nobody likes IndexedDB but it gives us a lot of features 
  - document.cookies gives us only error prone, string based, shenanigan approach 
  - One is over engineered for basic use but powerful
  - What do you find bad about document.cookie?
  - You have to properly escape concatenated strings with various options, as opposite of passing a `setCookie({...options})` ... and you can't read options at all unless parsing explicitly once the whole string is out ...
- tabindex is broken too, of course. Focus management could be easy but instead it’s always a pain
  - And mostly for backwards compatibility with the positive number api we all agree shouldn’t be used anyway
- I’d have to say video and audio, there are teams of ours at Canva trying to really push the envelope and the support for the type of primitives you need are just not there
- Seriously except localStorage, document.querySelector, fetch, and classList, the whole DOM/Browser API is pure shit.
  - LS can't sore rich types and doesn't convert rich types to strings for you. Its that great. Its actually more on the inconvenient side. Talking just in terms of API. Having the LS feature itself is of course nice.
  - It's simple and efficient enough, the kind of thing we need in this context. It has limitations, arguably dumb, but working with strings is ok when you have native JSON support.
- Push notifications are super complicated too
- WebRTC

- ## I have a form (in our SPA), but every time I save data, the page reloads!
- https://twitter.com/acemarke/status/1371826468263763970
  - My psychic debugging skills say, add `type="button"` to your 'Save' button in the form, because it's auto-POST-ing to the server
- But wouldn't you want to keep it as type submit so that Enter key still works. I guess preventDefault in submit handler can fix it too
  - for accessibility purposes I think one can mimic the button type submit with button `type="button" role="submit"` .
- Wouldn't doing prevent default in the on submit handler be a better option ?

- ## When implementing file uploads in your app, do you have a File model in your database to store attributes like s3 id, bucket, image width, height, etc?
- https://twitter.com/flybayer/status/1371865319271239680
- Always. I usually call it a Media. 
  - Each record contains the metadata and paths to all versions/sizes of a file. 
  - Every other table points to Media records and never to any paths directly. 
  - This makes it trivial to resize media/migrate/alter metadata in the future
  - Also, I never include the hostname in any of the paths. Makes it easier for move things between per-environments buckets
- Also allows arbitrary data to be stored along side the file, which can come in really useful. E.g. you could store a blurhash string of images.
- Yeah, I usually store only the key in S3 then a reference + everything else in the db so I have more data access patterns for querying
  - Yeah same. I try and keep DJ table data to a minimum as I’ve found doc tables are one of those things that are easy to add a ton of fields, most of which you find aren’t really needed
- I personally prefer to add some metadata inside of a db, even if S3 and other providers allows us to store image attributes. It makes things easier once you need to query the images for any reason
- I think you should make a separate storage layer, so that we could have many adapters, like FileStoreAdapter, S3StoreAdapter, ..
- I usually have a File model/entity with these properties: id, bucket key, mime type, and URL (computed).
  - All S3 details coming from ENV variables, so objects can be migrated between buckets with no DB changes needed.

- ## Use "translate" attribute and set it value to "no" for your company name.
- https://twitter.com/Prathkum/status/1370910146059190279
  - So that in case, the webpage is translated into another language, your brand name will remain intact
- To prevent #Google translate in a  text, use 𝘁𝗿𝗮𝗻𝘀𝗹𝗮𝘁𝗲="𝗻𝗼" for that tag. 

- ## Did you know that HTML has a native lazy `loading` ?
- https://twitter.com/eligarlo/status/1370315477982019588
- This works for all major browsers except Safari (desktop and mobile). 
  - If you have a lot of mac/iPhone visitors then a JS-based solution is still recommended for lazyloading

- ## How to drop IE11 support while keeping your site accessible (including from IE)
- https://twitter.com/_developit/status/1369384447557140481
  - Build your site to work properly without JavaScript.
  - Load JS via `<script type=module>` , which IE ignores
  - Think about it: bogging IE11 down with 2mb of polyfilled JS reduces accessibility.
- In case it's been forgotten:
  - IE11 was half as fast as Chrome M44
  - current browsers are all >2x faster than M44
  - this is for ES5 - ~ES2017 widens the gap (+10%)
- I don't think this is a helpful suggestion. Telling developers to build their site to "work properly" without JavaScript just leads people to do dodgy things with CSS that harms accessibility. It's also unrealistic in an agency world.

- ## what's the standard local dev setup for HTTPS-only worklets?
- https://twitter.com/mattgperry/status/1367514986944335872
- Caddy + self signed certificate + dnsmasq entries for me. I address my services using .localhost or .dev top level domain
- Alternatively you can create a local cert. authority (CA). 
  - This repo is not maintained anymore but I added a short README with documentation on how to create a CA and work through https using Caddy and dnsmasq on localhost. Maybe it can help!
- Highly recommend mkcert
- [How to use HTTPS for local development](https://web.dev/how-to-use-local-https/)

- ## if you want to build a URL, or just get the parts of a URL, the `URL` object isn't half bad.
- https://twitter.com/BenLesh/status/1366776104942452737
  - and it exists in both the DOM and Node
- Its not in IE11 which has burned me so hard multiple times. 
- It's unfortunately quite broken in React Native Pensive face

- ## Do you use "window." when accessing lowercase properties of the global object?
- https://twitter.com/NicoloRibaudo/status/1365771610981085202
- I always use `window` because many vars share identical names. 
  - Makes it easier to know if I'm accessing window.location or location from useLocation()
- I use `globalThis` usually

- ## Theming with design tokens. Let’s say we have color-primary-100 through 900.
- https://twitter.com/claviska/status/1365672928868712452
  - Would you assume 100 is always dark and 900 is always light? Or would you find it OK if, for example, a dark theme more or less inverted the values so 100 is light and 900 is dark?
  - The benefit is you can restyle all components (even ones that don’t exist yet) purely with tokens.
  - If color values aren’t allowed to change, you’d need to explicitly style each component for every theme.
  - I’m torn but starting to lean towards this approach
- Tailwind CSS 
  - The dark mode just sits as a media query, but they also use statically named colors like: text-red-300

- ## The modern `.avif` image format is small and mighty: it produces images that are *20-90% smaller* than png/jpg!
- https://twitter.com/JoshWComeau/status/1365347703107031041
  - But it's only supported in Chrome and Firefox
  - Fortunately, we can use the `<picture>` HTML tag to support *all* browsers, by providing fallbacks in other formats
  -  I found, a web-based .avif file converter that does its work *in the browser*
- the decoding speed of this format can be pretty slow, since the compression is so advanced. 
  - This can mean that while it saves time/bandwidth downloading, it can still be bad for performance 
  - As always, do your own testing! 

- ## What if you could tell the browser about a JWT, and then it would automatically send it with any future requests to the server that authorized it?
- https://twitter.com/ryanflorence/status/1365451878075572228
- Oooh! We can call them cookies!
  - And make them just one giant string that’s a pain to parse!!!!
- And what if you didn't use JWTs at all and made your app reasonably secure instead with server-side sessions. Where the libraries automatically use httpOnly cookies by default.
  - What if you did use jwt with httpOnly so you can have best of both? Secure and no tie to a server architecture
- I like how the Firebase library works - any time you have Firebase authenticate (it receives a JWT), any further use of Functions/Firestore automatically include the JWT in the request. it's necessary for Firestore access rules
  - would be cool to see this for any jwt/fetch request
- Exactly, you can store the JWT in a cookie, just make sure it’s a local only and secure cookie

- ## Use the `start` attribute to change the starting point for your ordered lists.
- https://twitter.com/denicmarko/status/1364480932955238401
  - `<ol start="2">`

- ##  TIL about the "ping" attribute on `<a>` tags, which will send a POST request to the given URLs when the anchor is clicked.
- https://twitter.com/svenluijten/status/1363245229533507585
  - https://caniuse.com/ping
  - Disabled by default in Firefox
- Here's a great article about how the `ping` attribute is used to DDOS.

- ## TIL about the Visual Viewport API
- https://twitter.com/rikschennink/status/1361598959828037633
  - When opening a soft keyboard `window.innerHeight` will stay the same but `visualViewport.height` won't!
  - Even better, you can listen for `resize` and `scroll` events on the `visualViewport` object.

- ## Unpopular opinion: ESM was a bad idea.
- https://twitter.com/devongovett/status/1356258095949885442
  - It has caused half a decade of churn in the JS ecosystem, broken almost every tool, caused maintenance nightmares for library authors, and for what? A different syntax? CJS was fine. 
- CJS is not perfect too. Resolving algo is a nightmare. It would never be compatible with web.
- As someone who has written a few Babel plugins that analyze dependencies etc, I will say that it is an advantage for toolability that ESM syntax is more constrained than what CJS allows. 
  - I believe Sasha is correct about sync vs async and the web being the main driver.
  - Wasn’t the reasoning behind this something along the lines of “node modules are FS-based and sync and web cannot work like this”?
- The main benefit of ESM is not in features it adds over CJS, it is the features it removes. 
  - The inability to specify dynamic synchronous dependencies comes to mind.
  - To my "we haven't capitalized on it yet" point though: CJS exports mix realms, whereas ES Module instances preserve the potential for future cross-realm dependencies (JS<->WASM, between threads, etc)
  - ES Modules feel like they will be more than just JavaScript, whereas CJS was obviously a JavaScript-first approach. e.g. Import assertions

- ## HTML(performance) tip: You can use the `loading=lazy` attribute to defer the loading of the image until the user scrolls to them
- https://twitter.com/denicmarko/status/1355439705853194241
- Here's how it works. 
  - When the user comes to your page, the browser will load all images you used. 
  - But, if you use this attribute, the images will be loaded only until (and if) the user scrolls to them. 
  - It will boost the performance of your page significantly.
- How can we do this for a whole section, not just image.
  - The `content-visibility` CSS property controls whether or not an element renders its contents at all

- ##  you no longer have to write <a target=“_blank” rel=“noopener”> to make external links secure!
- https://twitter.com/swyx/status/1354743782701375488
  - The HTML standard was changed in 2019 so that `rel=“noopener”` is always implied
- also worth noting that we cant drop rel=noopener right this second, bc this change only JUST landed (Chrome 88) and will take time to roll out. but will be soon!

- ## The MS-Edge/Blink folks are working on adding a <popup> HTML element, for tooltips/menus
- https://twitter.com/JoshWComeau/status/1354529361031024640
  - Handles all the hard stuff (layering, positioning, focus management, accessibility)
  - Built-in “light dismiss”
  - Can be fully styled
- This is super exciting! We've all spent too many hours fussing with popovers
- That would be really nice. No more Popper.js or libraries for custom dropdowns, date pickers, tooltips and menus.
- How is this different from `<dialog>` ?
  - I see it can be directly tied to a parent element.
- Nice but that means the popup will be native and different across browsers
- That smells of new IE6 in the making.

- ## If you ever looked inside a non-minified bundle, you might’ve seen a lot of automatically generated comments that look like this `/*#​__PURE__*/ `

- https://twitter.com/iamakulov/status/1353650608750825472
- In 2016, folks noticed that when you transpile a JS class with Babel, the class isn’t removed during tree-shaking. 
  - Even if it’s not used anywhere.
  - React was heavily relying on classes back then, so this was a pretty huge deal for React apps.
- Back then, classes were just a syntactic sugar around functions. 
  - So, to transpile a class, Babel was converting it into a function – and wrapping that function into an IIFE (immediately invoked function expression)
  - a problem with an IIFE is that UglifyJS (which did tree shaking in webpack back then) doesn’t know whether it’s safe to remove it.
  - An IIFE may simply create a class and do nothing else, like above. But it also may send a request to the server. UglifyJS doesn’t know
  - To solve this `/*#​__PURE__*/` was born.
  - Babel started to add /*#​__PURE__*/ comments in front of IIFEs it generates (as it knows they don’t have any side effects).
  - And UglifyJS started to recognize these comments – and dropping pure function calls if their result isn’t used.
- Fast forward to 2021:
  - Terser replaced UglifyJS in webpack (and is still responsible for most of tree shaking)
  - A lot of other tools adopted /*#​__PURE__*/ comments (eg babel-preset-react – for React.createElement – or babel-plugin-styled-components – for styled.whatever)
  - /*#​__PURE__*/ annotations were documented on the Terser website, along with a couple others

- ## The "hidden" cost of webfonts: you need to test everything twice. 
- https://twitter.com/rauchg/status/1352730054950703104
  - Blocking webfonts are a no-go, so you need to consider every page in 2 dimensions (font-display: optional).
  - Similar problem as light/dark mode. Not bad per se, but you need to be aware of the complexity space.
- Yup, dark mode isn’t just swapping color and background color. 
  - It’s an entire new color scheme, basically double the work in terms of color styles on the website.
- CSS is NP-Hard Problem. 
  - That's why it's so hard to automatize it. 
  - But there are ways to get optimal enough solutions. If I understand it correctly

- ## How to get the best image performance (Updated 2021)
- https://twitter.com/leeerob/status/1352264153411497993
1. Use `width` and `height` to prevent layout shift
2. Lazy-load images as they enter the viewport
3. Use modern image formats (WebP, AVIF)
4. Serve correctly sized images using `srcset` .
5. Provide blur-up placeholders

- ## using Intersection Observer on a handful of elements on a page
- https://twitter.com/ChrisFerdinandi/status/1352040366548135937
  - is it better to create a new observer for each one, or use the observer.observe() method to attach multiple elements to one observer?
- Group by callback.
  - If your callback will include a bunch of if else matches to parse through  the results each time to filter which elements intersectionality to act on, you better have different observers.
- Also note that the callback is called immediately on the observer being instantiated, with initial status on all matching elements

- [Should IntersectionObserver represent the observation of a single target Element?](https://github.com/w3c/IntersectionObserver/issues/81)

- ## The JavaScript story for protobufs is SO painful.
- https://twitter.com/BenLesh/status/1351618444286976000
- I gave up on protobufs long time ago for the same reasons. 
  - For me the most productive way to do that is to wrap/augment my transportable objects with a discriminator using `.toJSON` impl and revive them upon reception with `JSON.parse` . 
  - This does not cover binary data use case though
- Going from "I have a .proto file" to "I have a client that can communicate with a server" or "I have a Node.js server" is, frankly, an awful experience. 
  - Nothing is straightforward, there's a lot of half-baked libraries that try to help, but aren't well supported.
  - When you do finally generate JavaScript via the blessed libraries, what you end up with looks like something dreamed up by Java developers in 1999, rather than anything resembling what you could do with plain HTTP or WebSockets given modern JS and Node.
  - There's so much more. Network tab debuggability, etc. etc.
  - That one is definitely true, but isn't that a general problem with protobuffs, not limited to JavaScript implementation per se?
- Not just painfully. 
  - If you want to use it from browser there is no good option. 
  - Large amount of code is generated if you went the grpc-web route. 
  - I find ts-proto and grpc-gateway a middle ground. 
  - But with this client deals with json not protos, but no extra client side code.
- I'd thought that TypedArrays and DataViews made it simpler. 
  - Support for binary data on the web is quite solid by now.

- ## It might be a "Hot take". But. You need a really good reason to be mocking API requests in @storybookjs
- https://twitter.com/jh3yy/status/1351288120881385479
  - It's a tool for building UI components in ISOLATION 
  - If your UI components are coupled to API requests, something can likely be designed better 
- There's usually a way to design and architect your UI in a way that gets around this
  - The ideal scenario is that you're able to drop in as out components without things falling apart 
  - Only place I can see where this can be tricky is things like widgets
- Mocks can be useful for page-level components and side-loaded data. 
  - In these cases, a components inherent complexity can be more awkward to abstract away.
  - Even if it's more verbose to create "container" components for pages it challenges the design process
  - That's one thing I really appreciate about Storybook. 
  - Especially when you develop Storybook first
- Thinking more on it. 
  - I guess this comes more from a "Because you can, doesn't mean you necessarily should" mindset.
  - Where I've used this in the bigger projects. 
  - The joy has been where things are kept "simple". 
  - Purely presentational. Because coupling isn't fun to maintain.
  - For sure, that's how we build UIs internally. 
  - Presentational all the way to the page and then hydrate data down
- I don't like seeing nested arrays or objects in storybook at all if I can help it!
  - Often that means there's something else to extract, which can then be imported into the parent test.
  - (Obviously this isn't a hard rule, sometimes they're needed)

- ## I was going to work on removing the outlines around buttons when you click on them but I'm having trouble focusing.
- https://twitter.com/markdalgleish/status/1350999134631768069
- No outlines? You know I care deeply about a11y. Seems like you guys are just pressing my buttons.
- Bug Report: Can't focus while PMs are hovering
  - `.markDalgleish:not(:focus) { }`

- ## Two of my most- and first-used checks when doing a performance audit are surprisingly old school:
- https://twitter.com/csswizardry/status/1349400099647090694
  - Validate HTML 
  - Disable JS.

- ## Pages opened with `target="_blank"` allow the new page to access the original's `window.opener` . 
- https://twitter.com/denicmarko/status/1349247474083508224
  - This can have security and performance implications. 
  - Include `rel="noopener"` or `rel="noreferrer"` to prevent this.
  - `noopener` sets `window.opener` to `null` on the new page, so it's good for the security and performance. 
  - `noreferrer` does the same but also omit the `Referer` header, which can have SEO implications, because all traffic to the targeted website will be registered as direct clicks.
- One of the obvious issues is that the original page can be redirected.

- ## Google's Web Vitals site doesn't pass Google's Core Web Vitals assessment 🤔 irony?
- https://twitter.com/toddmotto/status/1349128843928477704
- I get a different view. 
  - Tried in incognito mode in order to not run extensions.
- That looks like Desktop, try mobile over [here](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fweb.dev%2Fvitals%2F&tab=mobile)

- ## Avoid layout shifts on long pages by adding a scrollbar
- https://twitter.com/JoshWComeau/status/1349374805418635264
  - `overflow-y: scroll; `

  - Improves CLS score
- this is indeed annoying.
  - what's your solution for modals opening and hiding that scrollbar, producing a content shift on opening?

- ## url state
- https://twitter.com/kentcdodds/status/1349173470567964673
  - If you find yourself synchronizing some local component state with the URL (for example, query parameters), you'd be better off treating the URL as the source of truth 

    - and ditching your local state in favor of getting the value from the URL (or your router) and updating the URL.

- Agreed almost always. 
  - There are a few cases where you want to sync state though, like an autocomplete that goes up to the url search params, you’ll want to throttle that user interaction (maybe not with CM though!)
  - Although you can also navigate inside of a throttle ... so maybe you’re right always.
- I’ve said same thing before 
  - but I’ve since changed my mind because of performance issues it causes in many cases. 
  - Instead I suggest making an abstraction that mirrors the state using what ever throttling or debouncing mechanism you need, and ideally testing that error-prone code.
  - Imagine a search component. 

    - Updating the url on each keypress is not awesome anyway because it fills the history with crap (ignoring replace here). 
    - Updating it if you click a button to run the new search is fine though.

- Unfortunately updating the URL is throttled by browsers, 
  - so this doesn't work for state that is updated a lot, 
  - e.g. a search query that updates as you type 

- ## A downside of modern SSG's (e.g. Next.js getStaticProps or Gatsby) is that builds are dirty.
- https://twitter.com/jaredpalmer/status/1349060733837963265
  - Same input != same output. 
  - Even with @turborepo cache, we need better incremental bundler caching + hosting providers (like @vercel ISSG/revalidate) to handle last mile for SSG workflow
- It's so, so hard. 
  - Most tools are just not designed for caching at all. 
  - We've had to do so much work in Parcel 2 to properly track all possible changes that could invalidate the cache. 
  - And in some cases we still have to bail
- In what scenario would the same input would give different outputs?
  - When you fetch blog posts from an external CMS at build time and then use that to generate a page for each post
- SSG could be pure if all you used was the filesystem data as a source. Same for Next.js. 
  - However, that's not guaranteed at all. 
  - Anything can be placed onto gatsby's graphql graph and any code can run in getStaticProps

- ## The three features of React that we are going to rely on most in Remix are (probably):
- https://twitter.com/mjackson/status/1348816271933014021
  - renderToString
  - error boundaries
  - react-refresh
  - I would have said `Suspense` a few months ago, but we are targeting stable React so Suspense is out for now.
- We actually have our own mini suspense inside Remix itself, built on top of current stable React and React Router
  -  It includes:

     - async data fetching (that works during server rendering too!)
     - dynamic code loading (both styles and components)
     - a “pending transition” hook

  - I’m particularly excited about the error handling work we are doing. You’ve never seen anything like it before, I promise
  - Remix error boundaries work both for render errors *and* errors that occur during data fetching. Handling errors has never been easier.
- `Suspense` does make some things nicer, like image pre-loading, 
  - but I'm increasingly doubtful it's worth the added complexity and CM breakage.

- ## Do any of you create raw web components? e.g. custom elements without Stencil, lit, or any other tooling?
- https://twitter.com/claviska/status/1348797980854378496
- Any convenience utilities you’ve created/are using for data binding and similar things?
  - I’m weird I guess but I like to use jQuery it already supports scope `$(this, ’.element’)`

  - The util functions I often end up using is a function to `queryselector(all)` in the shadowDOM; 

    - and a function to fire a custom event - that automatically sets `composed:true` etc as default

- Yes! I love to build #webcomponents from scratch and I used to do that quite often to learn the in’s and out’s of the API. 
  - I won’t recommend it for production apps though since libs like #stenciljs have a great set of build tools, linters and optimizers in place.
- Oh yes. Occasionally bring in lit-html when I need data binding in a performant manner. 
  - Outside of that though, the DOM has everything I need!
  - Things like a static getter for ‘tagName’ and also one called ‘register’ that contains the call to `customElements.define()` .
  - The tagName allows use in templates of other components, and the register helps with testability.
- Not anymore. Created myself a base class when I did, plus a few small utilities for creating DOM from template strings.
  - This is where I’d ended up too (more or less). 

    - I still use my own lil toolkit for side project stuff, but for work I use Lit now.
    - Every so often I do still write something for work that doesn’t use anything external, but those are unusual cases.

- Absolutely! For me one of the best features for raw web components is extending native HTML elements

- ## list: Data fetching in #reactjs
- https://twitter.com/cse_as/status/1349025492389613570
  - There are a lot of strong opinions about this in the community about what's the best method. 
  - Here's an overview of all the different methods available with pros and cons
- axios
  - In a small application with no routes, if you want to quickly put together something, 

    - you can use a regular fetch/axios inside a `useEffect()` hook and store the response in a `useState()` variable.

  - Pro: Quick setup
  - Con: No caching, your data disappears on new routes
- react-query
  - With this, you can stick your async API calling function inside a hook, 

    - give the API call a name and global caching will be automatically handled for you.

  - Pro: Beginner-friendly, each component can handle data on it's own
  - Con: Relatively new library
- redux-saga
  - This middleware helps you push your API call response to the redux store for storing into global state. 

    - You control everything from fetching the data to how it is stored & retrieved.

  - Pro: You'll find this used in many large applications
  - Con: Lot of boilerplate
- redux-thunk
  - Another redux middleware that can be used to perform async tasks.
  - Pro: Slightly easier to understand than redux-saga, great for new applications, built into ReduxToolkit
  - Con: Existing applications might've already setup redux-saga so you'll need to learn that too
-  Apollo Client
  - This is the go-to library if you've already decided that you want a GraphQL backend.
  - Pro: Has built-in caching, can be used for global state management, very popular
  - Con: You'll need to convert all your APIs to GraphQL
- Personal opinion:
  - Use react-query for handling all data coming from an API. 
  - Use ReduxToolkit for anything left needed in global state.
  - This setup is easy to learn & understand, scales well, minimises the code you need to write & you don't need to learn sagas, thunks or GraphQL.

- ## We can use the `unknown` type in TypeScript when we don't know the type of a variable. 
- https://twitter.com/benmvp/status/1348784718808899586
  - I've found it most useful for functions that are passing thru data to another function
- `unknown` is likely preferable to `any` cuz we can't reassign it, manipulate it or pass it to a function
  - it says to me: "this type is unknown"
  - `any` (which allows anything) says "I was unable/unwilling to determine the type"
  - Type narrowing does make `unknown` usable tho
  - Generics are another good alternative to `any` but that's a whole other topic  

- ## list: what's your favorite transactional email API and why?
- https://twitter.com/swyx/status/1349028510786994176
  - for nice-looking, simple, reliable, API-sent email for customer fulfilment. I've really only used nodemailer before!
- AWS SES - I wrote a blog post about using it
- @SendGrid *was* great, but recently their support has been absolutely non-existent since acquisition by @twilio
- I'm using @Mail_Gun . 
  - Affordable and reliable. 
  - You can send mails via SMTP and their API. 
  - For legal reasons it's also important for me that you can select EU (European Union) as a region.
  - I'm from Germany and it's about GDPR. Also, depending on your product and industry, customers expect you to use services with servers in Europe.
- Sendgrid API, at least from Python, is really simple. I prefer it to using SMTP directly.
- i think the IH favorite is @postmarkapp. they also recently added broadcasts. 
  - i use sendgrid and it's also fine for transactional emails, but i do not recommend their marketing email product.
- +1 for postmark. 
  - I've found it has significantly faster and better delivery than mailgun. 
  - This is super important if you're doing passwordless auth

- ## dilemma: 1.0 is pretty much beta but everyone jumps on the new hotness anyway. 
- https://twitter.com/devongovett/status/1349015005371506696
  - But no one will try 2.0 beta even if it’s more stable than 1.x because it says “beta”. 
  - Version numbers are hard
- A major version bump tells me things that were working before can stop working. 
  - If a release is only making things more stable why would you bump the version by a major version number?
- I didn't know at about Parcel 2 initially because the tooling in VSCode/CodeSandbox on hover only showed 1.x. 
  - A blind npm install gets you the same. 
  - When it isn't on the latest tag the numbers of people using will always be significantly smaller.
  - Would it be weird for the default installed tag to be a beta?

    - That's what vite does I think, although they never reach v1... They went from v1 alpha to v2 beta.

- If there are any breaking changes that will impact many users and/or are hard to migrate prioritize them in 2.0. 
  - Otherwise, they can be deferred to Parcel 3 ~1 year after Parcel 2.0 stable.
  - We are trying to do this for Babel 8, to avoid the Babel 7 situation.
  - If you manage to only defer small breaking changes to 3.0, there is nothing wrong with not waiting years before a new major since for most users it will be easy to upgrade anyway.

- ## Let's Bring Spacer GIFs Back!
- https://www.joshwcomeau.com/react/modern-spacer-gif/
- Instead of using margin, I create a new element explicitly to add some space between the icon and text!
- In the late 90s, if you were to pop open the source of a typical website, you'd likely encounter this curious fella
  - `<img alt="" src="spacer.gif" width="1" height="1" />`

- CSS didn't exist yet, and web layouts were built using HTML tables. 
  - GIFs were used because GIFs were the only image format that supported transparency (this is pre-PNG). 
  - Our spacer friend consisted of a single transparent pixel, a completely empty image.
- CSS was added to the browser to offer an alternative to styling. 
  - The language wasn't originally designed with layout in mind, 
  - but developers quickly realized that — through the use of some clever float hacks — it could entirely replace table layouts!
- By separating our concerns
  - HTML for structure, CSS for layout and presentation, JS for behaviour
  - we had a convention that would help us keep complexity down, ultimately making it easier to maintain things.
- In the original Jambalaya table-layout days, the spacer GIF was a tasty complementary ingredient. 
  - It didn't taste so good when we switched to making deconstructed sandwiches. 
  - But now that many of us are working with component-driven architectures, our code might benefit from a pinch of spacer GIF.
- Originally, my `<Spacer>` component rendered a `div` instead of a `span` , but I found it was a little limiting. 
  - According to the HTML spec `div` s aren't supposed to be put within certain elements, like `p` and `button` .

- ## Quiz time! for histroy back
- https://twitter.com/ryanflorence/status/1346562678869790720
  - No JavaScript on the page, normal document requests:

    - You land at http://example.com
    - You click a link to /page.html
    - Again, you click a link to /page.html
    - You click the browser back button

- Turns out when you go to the same URL, the browser still makes a document request to the server, still gets the a fresh page, 
  - but it *does not* push a new entry into the stack, it *replaces* the current one!
  - It's the same as clicking "refresh", and that makes sense.
  - 结果是回到example.com
- 实践测试
  - 在空标签页打开 a.html，然后按返回键，会回到空标签页
  - 在空标签页打开 a.html，再点刷新按钮，然后按返回键，也会回到空标签页

- ## To help me decide exactly what my media query tweak points should be.
- https://twitter.com/Malarkey/status/1345873190380253187
- If I had to print something for debug purpose, I'd prefer to show a different content, with the information of the media applied, on a `body::before` pseudo element absolutely positioned.
- I went with a `content:"XS";`  `content: "S"/"M" ` and so on. 
  - I've got this `debug.sass` file damn full of ways to figure out common gotchas behind html classes like debug_viewport debug_grids and so on. 
  - It's annoying to maintain but it has saved me tons of time @ the job at least twice
- [Custom properties for breakpoint debugging_201802](https://thatemil.com/blog/2018/02/23/custom-properties-breakpoint-debugging/)

- ## State machines are great, so why aren’t we rewriting all of our async/await code to them?
- https://twitter.com/dan_abramov/status/1344502932704788480
- the simple answer: async/await is easier. 
  - It leaves out edge cases. When you include the edge cases, async/await is more complex... So developers just hope for the best.
- state machines are great at representing systems that have cycles & many possible transitions between each state, 
  - async await is better for relatively linear paths with limited branching
  - its a little bit like how regular expressions work well for the state machines that represent string matching, since those also tend to have lots of sequential states with no branches
  - Indeed. And regexes are generally convertible to pointer bumping string scanning code, with loops replacing eager Kleene star. 
  - See how hand-written lexers implement regex matching in code where lex would use a state machine. Instruction pointer replaces state code.
  - Regexes and automata are isomorphic, a regex is literally a state machine
- This made me think of XHR’s `onreadystatechange` event and how devs were really really happy to use `$.get` instead of considering all of the possible ready states. 
- Babel rewrites your async/await code into small state machines
  - As well as any of your code is executed on hardware state machines
  - So here you go, exactly as you asked
- I'd much rather go the other way and remove state machines and caching layers from async/await
  - [callback based, simplified async/await](https://es.discourse.group/t/callback-based-simplified-async-await/343)

- ## What advice were you given for your career that turned out to be a complete waste of time and effort?
- https://twitter.com/buildsghost/status/1343650869904986112
- I was told to go take a bunch of night classes on computer science by two MIT grads if I ever wanted to be "serious" about programming.
  - I took some free student-taught classes, 
  - and we spent months learning languages I have not used since.
- This isn't about tech, but when I was in school to be a licensed massage therapist.
  - I had a teacher tell us that we should work our first year *for free* in order to build a client base.
  - Thankfully, I didn't, but I am sure some folks listened.
- You *need* to be good in math
- Go to conferences.
- I was told that how people feel in a moment is more important than the outcome of the work. 
  - Now, I couldn't be happier to work somewhere frank, timely, respectful feedback is foundational to the culture. 
  - Spoiler alert: great work outcomes _make people feel good_
- Was also told "PHP is dead, JSP is the future" in around 2006. They were very wrong.

- ## I want to *scale* a div and all of its contents to fully fit wall-to-wall inside its container div. 
- https://twitter.com/erikras/status/1343480294654046209
- Similar to what `background-size: contain;` can do for images. Possible in CSS only? JS ok, too.
- I think scaling is the wrong thing for my use case.

- ## A year ago I made a bet on full-stack JS and switched my focus from @laravelphp to Node.js. A year later, I found that Node mostly just slowed me down.
- https://twitter.com/tylerlwsmith/status/1341557868571422722
- Server-rendered React components look really exciting. 
  - I just wish the Node ecosystem was less fragmented and more productive so it would be easier to take full advantage of it.
  - Until then, I can continue to get a ton of productivity out of Laravel 
- React Router is the reason I love React. 
  - It also has the most innovative front-end libraries, and the front-end is the part that users interact with. 
  - React also works great with extremely complicated state management.

- ## [Reflecting on a year with Node.js and why I should have stuck with Laravel_202012](https://dev.to/tylerlwsmith/reflecting-on-a-year-with-node-js-and-why-i-should-have-stuck-with-laravel-e5a)
- Earlier this year, I was two months into building a full-stack JavaScript app. 
  - I used an Express server, set up Next.js for server-side rendering, added Chokidar for instant server reloading, used Next.js's Webpack config to compile my server's TypeScript code, hooked up cookie authentication with Argon2 encryption, found the perfect Node ORM, and had the app running in separate containers for Node, PostgreSQL and Redis.
- After two months of hard work, all I had built was a mediocre server-rendered CRUD app hacked together with two-dozen NPM libraries. 
  - If I had used Laravel and jQuery, I could have built this all in a weekend.
- After a year of building Node.js apps, I discovered I was spending more time piecing together tools than writing application code. 
  - 这是因为基于php的传统web开发框架laravel已经非常成熟，工具丰富

    - 基于nodejs作为服务端的web开发框架，还处于快速发展阶段，可选工具不够多，并且功能不够丰富

  - Laravel gives me 80% of my tooling out-of-the-box for 20% of the work. 
  - If moving fast is important to you, you should consider batteries-included frameworks like Laravel and Rails first.
- What I've learned is if you want to develop applications quickly, it isn't about staying in one language: 
  - it's about reaching for the tools that let you move quickly, whatever those are.
  - I use React for most of my front-end web applications, and Laravel gives me the tools I need to spin up the backend quickly. 
- Rather than sharing code between the front-end and back-end, I've learned to 
  - move almost all of my business and validation logic to the back-end, 
  - and I consume it on the front-end via API. 
  - Just because you're using two different languages doesn't mean you need to write the same code twice.
- I prefer Laravel over Node.js because it lets me move fast.

- discussion

- I like Adonis. And Sails.js. And Nest.js. Loopback also looks cool.
  - I've never adopted any of them for a few reasons though:
  - 总结：支持node的大公司少了，工具不多
  - Lack of adoption. 
    - None of the batteries-included Node.js frameworks have major adoption, so I have to figure out how to integrate other tools myself.
    - It also means if I run into a problem, there are far fewer resources available than Laravel.
  - Uncertain future. 
    - Adonis is mostly carried by one person. Sails is maintained by a company out of Texas. 
    - For long term projects, using Adonis feels like a risk.
  - Lack of first-party integrations
    - Laravel kills it with the amount of first party integrations they have. 
    - It's a compelling reason to choose Laravel over Node

- ## if I was building a CMS using MongoDB would you tell me to stop immediately? If so, why?
- https://twitter.com/JakeDohm/status/1341892219511459842
- Every developer build a CMS at some point in their career. 
  - Might as well check it off of your bucket list.
- I’m going to get technical and ask what type of content your CMS would be housing. 
- That would determine DB for me. 
- Mongo doesn’t seem appropriate for most content I’ve worked with, as CMS tends to be highly relational.
- Maker me: Build whatever you want with whatever tools you want.
- Developer me: Don't use MongoDB, most of your stuff with be relational, 
  - and in the event you cannot use relational, use JSONB data type in PostgreSQL.

# ref
- [Custom Properties as State](https://css-tricks.com/custom-properties-as-state/)
