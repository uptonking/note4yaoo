---
title: thread-web-browser-caniuse-compatibility
tags: [browser, compatibility, css, js, thread, web]
created: '2021-07-28T12:54:43.589Z'
modified: '2021-07-29T11:15:44.100Z'
---

# thread-web-browser-caniuse-compatibility

# caniuse-css
- [`:focus-visible` CSS pseudo-class](https://caniuse.com/css-focus-visible)
  - ❌️ safari 15仍然不支持
  - Previously drafted as `:focus-ring`
- [@supports()](https://caniuse.com/css-featurequeries)
  - ✅️ 除IE外都支持，很成熟
# caniuse-js

# discuss

- ## 

- ## 

- ## What's the difference between window.location and document.location in JavaScript?
- https://stackoverflow.com/questions/2430936
- According to the W3C, they are the same. 
  - In reality, for cross browser safety, you should use `window.location` rather than `document.location`.

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
