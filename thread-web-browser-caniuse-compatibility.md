---
title: thread-web-browser-caniuse-compatibility
tags: [browser, compatibility, css, js, thread, web]
created: 2021-07-28T12:54:43.589Z
modified: 2021-07-29T11:15:44.100Z
---

# thread-web-browser-caniuse-compatibility

# guide

# chrome
- [Web Capabilities (Project Fugu 🐡)](https://www.chromium.org/teams/web-capabilities-fugu/)
  - https://github.com/GoogleChromeLabs/fugu-showcase
    - [Project Fugu API Showcase - Chrome Developers](https://developer.chrome.com/fugu-showcase/)
    - a collection of apps that make use of APIs that were conceived in the context of Project Fugu.
  - Project Fugu 🐡 is an effort to close gaps in the web's capabilities enabling new classes of applications to run on the web.
  - [Fugu API Tracker](https://fugu-tracker.web.app/)
  - [What Is Project Fugu — Google’s Initiative To Unlock All Native Device Features For The Web](https://medium.com/swlh/what-is-project-fugu-googles-initiative-to-unlock-all-native-device-features-for-the-web-892fafa726f9)
# caniuse-css
- [`:focus-visible` CSS pseudo-class](https://caniuse.com/css-focus-visible)
  - ❌️ safari 15仍然不支持
  - Previously drafted as `:focus-ring`
- [@supports()](https://caniuse.com/css-featurequeries)
  - ✅️ 除IE外都支持，很成熟
# caniuse-js

# discuss-ios-safari

- ## 

- ## 

- ## 

- ## 🚨 TIL: In Safari `navigator⁠.storage.persist` only works for "home screen apps".
- https://twitter.com/schickling/status/1753417758518173947
  - This means even with this API, every page you didn't visit for more than 7 day loses all of your data (localstorage, IDB, OPFS, ...)
- [Updates to Storage Policy | WebKit _202308](https://www.webkit.org/blog/14403/updates-to-storage-policy/)
  - [Full Third-Party Cookie Blocking and More | WebKit _202003](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/)
  - This post from 2020 spells out the 7 day policy more explicitly
- Here's a webkit bugzilla issue making a case for changing this behavior, with folks from 1Password and Simplenote chiming in. Unfortunately, the answer appears to be: save to home screen

- Are Chrome and Firefox any better?
  - Yes, works both in Chrome and Firefox.

- better to persist and sync localStorage with one of the https://0data.app protocols, @remotestorage_ even lets you connect dropbox and google drive
# discuss
- ## 

- ## TIL about `PointerEvent.getPredictedEvents()` . Apparently, web browsers can predict where the cursor could potentially move next
- https://x.com/sebastienlorber/status/1869083536185331772
  - It's now supported everywhere starting Safari 18.2

- ## 自从知道 Chrome 有能实时捕获网页内的媒体流的 tabCapture API 后，对我这个常年开发 iOS App 的良民来说受到了文化冲击，这个 API 简直是外挂
- https://x.com/kevinzhow/status/1818562695026950216
- 这个 API 的目的是…… 录制网页内的视频？
  - 比如截图
- 甚至不需要是浏览器插件，网页页可以
- 有一个叫 Fugu Plan 的计划，旨在为浏览器实现更多 native app 的能力

- ## Surprised to see browser support for Custom States ( `ElementInternals.states` ) already at 87%
- https://x.com/claviska/status/1800680936998076439
  - https://caniuse.com/mdn-api_customstateset

- ## 每日 CSS 一小坑：用了 container 后所有 position: fixed 的后代的坐标都会相对于该元素而不是 viewport。类似的属性还有 transform
- https://twitter.com/luinlee/status/1787325824661942741

- ## View Transitions are now in Safari Tech Preview 191
- https://twitter.com/dannymoerkerke/status/1773392919002525954
  - https://codepen.io/dannymoerkerke/pen/ExMEPaW

- ## From Chrome 124, scrollers are keyboard focusable by default if they have no keyboard focusable children.
- https://twitter.com/passle_/status/1771448139876118951
- I believe a variation of this has existed inside of Firefox for a bit too. Be nice if* it finally makes it to chrome stable. 

- ## 📏 fun fact: while chrome URL limit is 2, 083 characters the hash part of URL is not limited by this number, that's why I was able to put 100kb of code into typescript playground
- https://twitter.com/JLarky/status/1771603877676142666
  -  set your querystring to a buncha zeroes and send it to a willing httpd
- Yeah we use the same trick in sveltelab to get a whole repo in the url. I think it's not actually chrome the problem but rather the server receiving the url. Since the hash is not sent you can write whatever in it
- nope, Chrome's URL limit is absolutely not 2083 bytes — you're probably seeing a limit enforced by your `httpd` (which of course wouldn't include the hash) 
  - set your httpd to have unlimited request length and you can easily see Chrome put 100kb on the wire
  - set your querystring to a buncha zeroes and send it to a willing httpd
- Move away blockchain, new distributed database is on the way.

- ## new APIs to help make scroll-snap and overflow areas more feature rich and easier to work with:
- https://twitter.com/argyleink/status/1771320680417816818  
  - Experimental feature (from Canary) 

- JS
  - snapChanging
  - snapChanged
- CSS
  - scroll-start
  - scroll-start-target

- ## JSPI, which lets you use async JS APIs from sync WebAssembly without asyncifying the entire app, is going to origin trial in Chrome 123
- https://twitter.com/v8js/status/1768755661083701361

- ##  `ElementInternals.states` is coming in Safari 17.4, which means only Firefox is left — and it's already available behind a flag.
- https://twitter.com/claviska/status/1765707964692697564

- ## 🌊 `ReadableStream` async iteration is coming to a Chromium-based browser near you! 
- https://twitter.com/MattiasBuelens/status/1765655738095960191
  - In Chrome Canary, this now works: `for await (const chunk of response.body) {}`

- Also tastes great combined with WebSocketStream
  - `for await (const message of wss.readable) {}`

- ## popover ships in Firefox 125 _20240304
- https://twitter.com/hdv/status/1764577917093228813
  - [Dialogs and popovers seem similar. How are they different? _202309](https://hidde.blog/dialog-modal-popover-differences/)

- `popover` is available:
  - Chrome (116) and Edge (115)
  - Safari 17
  - Firefox from 114 (behind dom.element.popover.enabled flag)

- ## With Edge 121 supporting AVIF, it will soon cross the 90% adoption mark
- https://twitter.com/TimVereecke/status/1758983962792169702

- ## Perhaps one of the most pleasant surprises of 2023 was Safari going all-in on PWA. 
- https://twitter.com/dhh/status/1736081020393521620
  - Add To Dock in macOS Sonoma and full support for web push notifications has made it a joy to use and develop PWAs. 
  - Native still has a place, of course, but it's a smaller one than it was.

- iOS and iPadOS 16.4 beta 1 is now available with:
  • Web Push for Home Screen web apps 
  • Focus support for Web Push
  • Third-party browser support for Add to Home Screen
  • Badging API 
  • Manifest ID 

- ## You can reduce the number of DOM elements and DOM operations _by a lot_ and speed things up as a result by highlighting things with the CSS Custom Highlight API
- https://twitter.com/fabiospampinato/status/1653421306128334848
  - Sadly isn't supported in Firefox and Safari
- So are all of your debugging tools highlights?
  - No the thing that draws rectangles around elements does that on a transparent canvas, you can't implement something like that with highlights. There's only a limited set of CSS properties that they support (to stay super fast).
- Did anybody mention a text editor that uses this API?
  - There may be some problems in practice, like for example I think you can't make text bold just with highlights, and you may need some wrapping anyway to make like links clickable.
- TIL about the Custom Highlight API. Looks pretty useful to mark search results and that sort of thing. Great find!

- ## It is now 2023 and `display: contents` still breaks accessibility in Safari.
- https://twitter.com/devongovett/status/1628501529207402497
- Display contents was a complete mess. It doesn’t work right in any browser. Try using it in a contenteditable for comical effect.
  - I try to avoid anything related to content editable

- ## 🤔 [Does Safari and Google Chrome for macOS use the same rendering engine?](https://apple.stackexchange.com/questions/350671/does-safari-and-google-chrome-for-macos-use-the-same-rendering-engine)
- While Google Chrome used WebKit for macOS client at one point, that's no longer the case for current stable build.
  - WebKit was the original rendering engine, but Google eventually forked it to create the Blink engine; 
  - **all Chrome variants except iOS now use Blink**
- The restriction to use WebKit as the rendering engine for 3rd party Web browser apps exists solely on iOS. 

- ## Just confirmed: iOS 15 now supports the HTML5 drag and drop API on iPhone!
- https://twitter.com/devongovett/status/1441087776489807875

- ## A new feature-detecting function coming soon to a browser near you: HTMLScriptElement.supports("importmap")
- https://twitter.com/domenic/status/1433842051339243522
  - import.meta.supportsType("css")

- ## Safari joins Chrome, Firefox, Opera & IE in dropping the 300ms tap delay!__201603
- https://twitter.com/jaffathecake/status/712004058890915840
  - Safari 9.1 is also available today for OS X Yosemite and OS X Mavericks with the same great WebKit features from OS X El Capitan 10.11.4.

- ## The Safari onLoad event handler for the assets works differently from Chrome and Firefox. 
- https://twitter.com/bruno__quaresma/status/1428846800631435264
  - If the asset is already loaded on cache, the onLoad event will not 

- ## macOS Big Sur started hiding scrollbars. Here's why I think it's bad and what we can do about it.
- https://twitter.com/dluzar/status/1428758952389533700
  - Apple introduced automatic scrollbar hiding which is enabled by default when no mouse peripheral is connected. 
  - This not only applies to the system scrollbars, but to websites as well.
- Scrollbars serve two purposes. 
  - One is obviously to allow you to scroll content. 
  - The other is to indicate whether there is more content to be scrolled to.
  - Apple decided that since you can use a trackpad there's no need for scrollbars, completely ignoring the second aspect.
- The best thing about it is, the Mac OS scrollbar autohiding doesn't apply to custom scrollbars. It's unclear how long this will remain the case.
  - You can style it as you want, but there are couple of downsides.
  - First, you can't replicate the browser look because the scrollbar arrows are hidden when using these CSS rules.
  - Second, it doesn't work in Firefox (they instead implement `scrollbar-color` and `scrollbar-width` that in turn no one else does — and it doesn't fix the autohiding).
- Since most devs use macOS, they may not even be aware that their sites could have potentially broken layout on Windows where scrollbars are visible by default.
- Another problem is unnecessary layout changes when the scrollbar shows. 
  - Luckily `scrollbar-gutter` is on the horizon
  - 但所有浏览器都不支持 scrollbar-gutter (202108)

- ## We're experimenting with a page transition API in Chrome. 
- https://twitter.com/jaffathecake/status/1427656326172262400
  - It's just for SPAs right now, but you can use it on real sites via an origin trial.
  - [Smooth and simple page transitions with the shared element transition API](https://developer.chrome.com/blog/shared-element-transitions-for-spas/)
- I tried to come up with a fully featured CSS version and ended up with like 20 new properties and I wasn't even close.
  - There may be a CSS version of this, but it'd be a subset of the full capability.

- ## What's the difference between window.location and document.location in JavaScript?
- https://stackoverflow.com/questions/2430936
- According to the W3C, they are the same. 
  - In reality, for cross browser safety, you should use `window.location` rather than `document.location` .

- ## If you're a fan of alert(), you may have heard about a change that briefly hit Chrome Stable channel this week (it's been temporarily disabled at the moment while breakage is remediated)
- https://twitter.com/estark37/status/1422694856544059396
  - The change is to disable alert(), confirm(), etc. inside cross-origin iframes. Sorry if this broke you!
- if you're wondering why this change is happening, the tl; dr is: alert() and friends are often used for spoofing(电邮欺骗；滑稽模仿) and scams(欺诈骗钱) that take advantage of the fact that the message's provenance(来源，出处) is ambiguous.
  - It's very easy to use alert() to trick a user into thinking their browser is telling them something when in fact the message is coming from a malicious website.

- ## JS and CSS modules with no build in sight!
- https://twitter.com/justinfagnani/status/1403436100132110340
  - all built into the platform, no builds required, usable with `python -m SimpleHTTPServer 8000`

- CSS modules is a very simple idea: import a CSSStyleSheet from a CSS file. Apply it to the document, or a shadow root for scoped styles.
  - They're great with web components already and a good building block for future features like importing class names and such from CSS into JS.
- What is the production perf implications of this? It seems
  1. CSS imported this way only loads when the importing js module is parsed (nested import chain)
  2. An app written this way results in many small requests to many small CSS files
  - Import as Constructable StyleSheet also means the CSS cannot be extracted and merged into a single file (worse compression). A build time optimization can only inline the CSS in JS - which means style changes invalidate js cache.
- Short-term, to bundle you'll have to go into JS.
  - With top-level await you can compile to the async `CSSStyleSheet.replace()` call so CSS parsing is non-blocking.
  - Long term we really need Web Bundles for this and so many reasons. Bundling by mutating and actually merging file contents is really bad for caching and tooling complexity, and only works for file formats where you can encode multiple files. CSS isn't one of those.
- I think tools could insert preload hints in parent bundles similar to what we do today to solve the first problem. Combining is harder when shadow DOM is involved… another case for Resource Bundles I guess.

- ## Building upon "Import Assertions" we recently saw JSON Modules land in V8/Chromium 91__202104
- https://twitter.com/bramus/status/1421236658159112196
  - In Chromium 93 the same thing for CSS lands (“CSS Modules”)
  - [CSS Modules V1 Explainer](https://github.com/WICG/webcomponents/blob/gh-pages/proposals/css-modules-v1-explainer.md)

```JS
import json from './foo.json'
assert { type: 'json' };

import styles from "./styles.css"
assert { type: "css" };
```

- ## In new Chromium 92, PWAs can register themselves as handlers of custom URL protocols/ schemes using their installation manifest, making them all the more appy.
- https://twitter.com/brucel/status/1420775444287303680
  - [URL protocol handler registration for PWAs](https://web.dev/url-protocol-handler/)

- ## Safari quirk: when an element has pointerCapture, the event's movementX and movementY will always be zero. 
- https://twitter.com/steveruizok/status/1420844366617264132

- ## CSS Module scripts were just merged into the HTML spec! __20210715
- https://twitter.com/justinfagnani/status/1415383208359645184
  - [Feature: CSS module scripts: ](https://chromestatus.com/feature/5948572598009856)
  - import styleSheet from "./styles.css" assert { type: "css" }; 
- how will this work in webpack or other bundlers? currently we import "style.css" and it adds it automatically or it's configured as a css-module. will this interfere with that?
  - Bundlers will have to adapt to the ever-evolving web platform as they always do.
  - I'm this case there's a straightforward transform to a JS module that exports a CSSStyleSheet. Later there may be more options around Web Bundles or multi-sheet CSS files.
  - I think with the import assertions, bundlers can use those as flags to fairly skip or delegate this process and then generate a chunk for the target file. But who knows Man shrugging, I'm still yet unsure if bundlers right now supports assertions.
  - I think with the import assertions, bundlers can use those as flags to fairly skip or delegate this process and then generate a chunk for the target file. But who knows Man shrugging, I'm still yet unsure if bundlers right now supports assertions.

- To be brutally honest, I think the "native CSS modules" standardization is rushed and again shows arrogance of those involved in the process.
- https://twitter.com/youyuxi/status/1427406150463537152
- clashes in naming with an popular existing solution (making search results confusing for beginners)
- uses the same syntax with popular existing conventions (extract via build tools)
- requires JavaScript (can't avoid FOUC)
- doesn't play nice with SSR
- doesn't scale in production (can result in hundreds of requests)
- All of which are non-issues for existing conventions! And the solution for the problem is more specs.
- Which begs the question: why rush it into a standard before the whole category of problems are thought through? Why such a hurry to standardize something that collides with existing conventions, yet doesn't even offer feature parity?

- I completely disagree that minimally useful is half-baked.

- ## Things I didn't know are apparently impossible – positioning something exactly above the virtual keyboard on iOS Safari.
- https://twitter.com/tommoor/status/1420469267057844227
- You can use `window.visualViewport.height` .  (Try creating a new issue with a long description in linear for example)

- ## This week it was working around the fact that Safari dispatches two _mousemove_ events whenever you press a modifier key like Shift, Alt etc.
- https://twitter.com/brianskold/status/1420312185444601856
- whoa, is that per mouse move?
  - No, per key press. One on keydown, one on keyup.
- Safari fires a mousemove event on keydown/up if the key is shift, ctrl, alt, cmd etc, even if the mouse hasn't actually moved. 
  - Neither Chrome or Firefox do this. Safari doesn't do it for other keys.
- In Safari's defence, the MouseEvent objects have boolean properties for the state of those keys, so it's kinda sort-of reasonable to fire another event when that state changes.
  - But yeah, firing mousemove when the mouse didn't move feels weird.
