---
title: thread-web-css
tags: [css, thread, ux, web]
created: '2021-01-08T17:14:57.157Z'
modified: '2021-01-08T17:15:13.906Z'
---

# thread-web-css

# compatibility

- [Is Houdini ready yet？](https://ishoudinireadyyet.com/)
  - 各浏览器兼容性表格，标准状态、支持时间
- [WebKit Feature Status](https://webkit.org/status/)
  - CSS Typed OM Level 1: under dev
  - web animations api: supported since 14.0
  - CSS Animation Worklet API: under consideration
  - [WebKit CSS Feature Status](https://webkit.org/css-status/#)
  - [Features in Safari](https://developer.apple.com/safari/features/)

- clipboard only fully supported by Safari
- Typed OM & CSS Paint API only fully supported in Chrome
- bitmaprenderer, feature policy, & web locks experimental
# pieces
- ## 

- ## CSS trick to dynamically reduce the line-height as the font-size grows, large texts need condensed line-height
- https://twitter.com/hihayk/status/1280979972258172928
  - line-height: calc(0.25rem + 1em)
- or use doppler to fine-tune it
  - https://hihayk.github.io/doppler/

- ## z-index Tip: When creating a reusable component that declares a z-Iindex, add this style to the root element: isolation: isolate
- https://twitter.com/housecor/status/1432346434356060162
  - Why? This creates a “stacking context”, which means your z-index won’t “leak out” and override surrounding components.
- My proposed solution was using React context to create the stacking. This is much simpler.

- ## Before building dark mode for your component library, build "dark context." 
- https://twitter.com/markdalgleish/status/1432601569069916165
  - Even in light mode, setting a dark background on a container should flip the foreground elements. 
  - This forces you to decouple the concept of contrast from the idea that your app has two design modes.
- I’ve always worked with split concept. A ‘theme’ and a context. Your theme is the over all concept and the context is the specific variations over the theme, such as focus areas. Both should be able to be set independently throughout the DOM tree. Dark mode is just a theme.
- How do you execute this technically?
  - CSS variables and/or React context.

- ## Other than Next.js/styled-jsx, what other CSS libraries clean up their rules when they're no longer used? E.g. when all components using them unmount.
- https://twitter.com/sebmarkbage/status/1422278240866078725
  - I meant dynamically on a long running page. Not statically removing rules that are never used but removing rules that were used on one page but not another.
- We had this in react-jss since the very first version.
- @remix_run does this per route. When your routes unload, so does the CSS file used on that route.
  - That can be quite expensive, depending on the kinds of rules you're writing it may be cheaper to leave them in the DOM.
- **Removing unused CSS is expensive?**
  - Yes, browsers don't really track what selectors match in a sheet, if you're lucky they walk the entire page and find noting to recalc. If you're unlucky they recompute the style of the entire page. It depends on the browser and the selectors you removed.
  - Looking at the blink code I think if most of the page turns over on routes it's fine, though I wonder what you're optimizing for removing sheets? If you have a page where a route change swaps the sidebar but the main content doesn't it's probably slightly slower than leaving it
- To anyone wondering what are the benefits of [“unmounting CSS” ](https://kremling.js.org/concepts/unmounting-css.html)
  - And so it seems they create style tags with specific attributes, that serve as ids to remove them from the `<head>` upon unmounting
- Shadow DOM naturally does this
  - The advantages of Shadow DOM, especially when used with @buildWithLit , handle CSS brilliantly, and was a top reason why I moved to #WebComponents. There's always som use case that doesn't fit nicely, but I can't think of one.
  - I've been using shadow dom for over a year a half, and I still don't see many real world use cases for it. For most situations it introduces more problems than it solves

- ## CSS `filter: hue-rotate(-120deg)` can help to change emoji color
- https://twitter.com/DasSurma/status/1420831971828195328
  - filter属性除了ie支持度很成熟了
  - https://codepen.io/bramus/pen/dyWevRe
- colorize-filter: JS Module to apply a hex color to an image through css filters

- ## When you need a #CSS 'display: block' element that takes only the content size, you can now use the 'width: fit-content' instead of the 'inline-block' value.
- https://twitter.com/eladsc/status/1420411183547432970
  - And has full browser support! 

- ## a pseudo selector either needs to be pointing from the root or a child, cannot be used in case of a direct child
- https://twitter.com/adamwathan/status/1418882038082453506
  - 伪类不能用作直接子元素
  - ❌️ .prose > :where(ul > li > p)

- ## Prevent unwanted Layout Shifts caused by Scrollbars with the `scrollbar-gutter` CSS property
- https://www.bram.us/2021/07/23/prevent-unwanted-layout-shifts-caused-by-scrollbars-with-the-scrollbar-gutter-css-property/
- there’s a distinction between two types of scrollbars
- Overlay Scrollbars are those iOS/macOS-style scrollbars which are placed over the content. 
  - They are not shown by default, but only while the user is scrolling. 
  - To keep the content underneath visible they are semi-transparent, but that’s totally up to the user-agent (browser) to determine. 
  - While interacting with them, their size may also vary.
- Classic Scrollbars are scrollbars that are placed in the so-called “Scrollbar Gutter”. 
  - The Scrollbar Gutter is the space between the inner border edge and the outer padding edge. 
  - With classic scrollbars, the size of the Scrollbar Gutter is the same as the width of the scrollbar. These scrollbars are usually opaque (not transparent) and take away some space from the adjacent content.

- When the content of a box becomes too big (e.g. when it is overflowing), the browser will — by default — show a scrollbar. 
- In case of a classic scrollbar this has a nasty side-effect: as the scrollbar needs some space, the available width for the content shrinks — thus the layout shifts.
- In case of Overlay Scrollbars there’s no layout shift, as those scrollbars get rendered over the content.
- By setting `scrollbar-gutter` to `stable` we can have the UA always show the Scrollbar Gutter, even if the box is not overflowing and no scrollbar is shown. 
  - This way we have a visually stable layout: when the box starts to overflow the scrollbar will be rendered but no layout shift will happen as space for it was already reserved.

- ## user in data saver mode? skip the media, save loads!
- https://twitter.com/argyleink/status/1389244232641089537
  - @media (prefers-reduced-data: reduce) 

- ## Easy way to tell if your CSS variables are maintainable or not—comment out one of your variable definitions. Did it break the build?
- https://twitter.com/markdalgleish/status/1416276184409645056
  - Another quick test—simulate a typo in one of your `var` expressions by deleting a random letter from the variable name. Did *that* break the build?
  - The slow way to guard against this: screenshot tests.
  - The fast way to guard against this: hashed variable names (e.g. vanilla-extract)
- I prefer scss variables because css vars let my build pass even if they don’t exist..

- ## We're considering removing a few CSS variables from our design system. 
- https://twitter.com/markdalgleish/status/1416282722108989440
  - Normally this would be a breaking change, but luckily they're hashed (via vanilla-extract) 
  - and we never exported them to consumers, making them private CSS variables—something the web doesn't natively support.

- ## Use `<datalist>` to enhance your forms with suggested values – not only for text inputs, but also 🧮 numbers, 📏 ranges, ✉️ emails, and even 🚦 colors!
- https://twitter.com/stackblitz/status/1409493323660857348
  - https://stackblitz.com/edit/datalists?file=index.html

- ## Designers, use buttons with a larger tap area.
- https://twitter.com/darylginn/status/1408335654237335554
  - Around 50% of Internet traffic is mobile, you have to be taking it seriously. Those tiny buttons need to go.
  - 40px is the sweet spot.
- Are people setting fixed heights for buttons instead of using padding?
  - In our case, the text in our buttons will never be on multiple lines - so you gotta consider that
  - Also great for size variants (small, medium, large, etc.) and for keeping heights consistent with inputs and dropdowns.
  - You should have an aversion(厌恶) to fixed heights. It’s not accessible. Button heights should only be defined with min-heights. If you have fixed height buttons and the user jacks their font size by 200% it won’t be able to compensate. Very few scenarios require fixed height buttons
  - Yeah, I prefer to let sizes adjust based on their children, and make them grow to the size of their parents with flex.
- using em or better yet rem  (based on root em) units would be more ideal for responsive design.  Another option would be percentages. Zooming in might make for a bad UX. A good mobile design should not make the user feel the need to zoom in on any important element.

- ##  `img {max-width: 100%}` is a must have in css reset
- https://twitter.com/eladsc/status/1408042880283914242

- ## With `box-shadow` , one sibling's shadow can cast over another, breaking the 3D illusion. 
- https://twitter.com/JoshWComeau/status/1407811337984647169
  - By putting `drop-shadow` on the parent, we avoid this problem 
  - https://codepen.io/joshwcomeau/pen/KKWjxMv
- drop-shadow also produces a more “realistic” shadow, since it looks like it’s darker where the item shadows overlap
- There is one weird bug in Safari when you apply drop-shadow with transform. 
- I wouldn't recommend drop-shadow for cards. It causes issues with positioning items inside. It's best for single elements, like images.

- ## Custom Scrollbars In CSS
- https://twitter.com/shadeed9/status/1407412821990776833
  - [Custom Scrollbars In CSS](https://ishadeed.com/article/custom-scrollbars-css/)

- ##  `touch-action: manipulation;` make taps 300ms faster
- https://twitter.com/argyleink/status/1405881231695302659
  - element doesn't want double-tap to zoom
  - browser *immediately* responds to taps instead of waiting 300ms for a "potential" 2nd tap 
- If you've got a mobile viewport set, the 300ms tap delay is already gone (since 2013)
  - Seems like that's not true for Safari, which is a huge percentage of (my) mobile traffic?
  - yeah I was pretty sure they fixed the delay like 5+ years ago
- 

- ## Hey CSS Grid people, how would you go about center-aligning grid items so that orphans are centered? 
- https://twitter.com/brad_frost/status/1403441552467185664
  - Or if only two items are defined they are center-aligned? 
- I’ve tried VERY HARD to make this happen with Grid (think Quantity Queries), but ultimately went back to Flexbox for this specific lay-out class. 
  - The rule of thumb I’ve been using is: if you know how many items will be in the grid → CSS Grid. Otherwise, if you don’t → Flexbox
- I'd straight up go to flex land for this but maybe a quantity query plus grid-column: 2/3 or whatnot?
- Flexbox grid layouts seem more flexible than CSS Grid when it comes to horiz centering items. While our flexbox grids only need a justify-content: center applied to them to achieve that, that unfortunately doesn’t work with CSS Grid.

- ## Learn About Aspect Ratio In CSS
- https://ishadeed.com/article/css-aspect-ratio/

- ## How much does minifying CSS files really help I wonder.
- https://twitter.com/kentcdodds/status/1402396259688665089
  - You can't mangle selectors, property names, or values. You can only really get rid of comments and whitespace (which gzips away anyway).
  - And with HTTP/2, concatenating probably doesn't matter much either
- well, if your site gets a million visits a month, a million requests to that CSS file, if you save 5kb by compressing it, that's 5M kb => 5GB of bandwidth and depending on your hosting that could be a couple of bucks a month. Also, a tiny speed boost for every user and page load.
- As always, it depends on the scale. Sometimes it isn't worth it to uglify JavaScript either. You can always do the math to figure out how many bytes you'll save. But how much will it cost in debugability and developer time? It's good to think it through.
- you can make structural changes and minify properties & values
  - https://github.com/css/csso

- ## not-yet: Why would the exact same settings produce so many absurdly wrong radio buttons?
- https://twitter.com/Elijah_Meeks/status/1402097012875554822
- My best guess is that whichever styles you're using, they're getting rounded to the nearest screen pixel. Border & box widths do this to avoid fuzzy edges.
  - And maybe the device and browser are somehow miscommunicating how bit those pixels are??? Unless this is really small text.

- ## justify-content vs align-items vs align-content
- https://twitter.com/JoshWComeau/status/1394394504283758599
  - https://courses.joshwcomeau.com/office-hours/004

- ## We all agree JSON-in-CSS is the future.
- https://twitter.com/jon_neal/status/1392600862703378433
  - CSS respects quotes, & bracket groups like (), [], or {}.
  - Ergo, CSS can syntactically support "JSON".
  - Custom Properties support syntactically valid values.
  - Ergo, Custom Properties can be "JSON".
  - CSS doesn’t know it’s JSON.
  - But CSSOM can see it.
  - And JS can parse it.
- incredible. the future of the internet rests in your hands

- ## Web container layout syntax guide:
- https://twitter.com/argyleink/status/1388490388755865600

1️⃣ `justify-*` the axis/direction letters and words travel along
2️⃣ `align-*` the axis/direction paragraphs travel along
3️⃣ `*-content` align/distribute cells
4️⃣ `*-items` align/distribute children within their cell

- ## If you could use a parent() function in CSS to return the parent value of *any* CSS property (e.g. parent(background-color) returns the parent background color, and parent(--foo) returns the parent value of var(--foo)) what would you use it for?
- https://twitter.com/LeaVerou/status/1377062738472603650
- Recently was using CSS grid with a 2nd grid inside the grid items. Wanted to use 5% of parent grid width as the gap for both, but 5% of the grid-item is different than 5% of the parent. parent() sounds like the perfect solution.

- ## Used the :in-range or :out-of-range CSS selector?
- https://twitter.com/jh3yy/status/1384766096511733762
  - Use them to select an input whose value is in/out of the min/max range
  - `<input type="number" min="0" max="5"/>` .
  - https://codepen.io/jh3y/pen/MWWowEb

- ## Enhanced `:not()` can take a selector list, and refer to the base selector with `*` .
- https://twitter.com/5t3ph/status/1383803482310807557
  - https://codepen.io/5t3ph/pen/OJWoJrE

- ## typography tip: word break with `<wbr>` and/or `&shy;` .
- https://twitter.com/argyleink/status/1382685891613712387
  - https://codepen.io/argyleink/pen/vYgjVVx?editors=1100
  - wbr会换行，&shy; 换行时还会显示短横连字符
- Good way to show the hyphen difference between `<wbr>` and `&shy; `

- ## What does `min-width: 0` have to do with anything?
- https://twitter.com/ryanflorence/status/1382116922678861826
  - Spent 3 hours until I figured out to put `min-width: 0;` on some containers to fix some flex children from being too wide because of `<pre>` s.
- This happens with Grid as well. By default it's "auto", which will use the intrinsic content size. Put that ish next to your global box-sizing selector
- The magic min-width. Also useful when you use ellipsised text inside flex-box.
- Min-width defines the same value as flex-basis. They both define the inicial width before any flex is applied. By default is auto, which means: look at my width.
- `flex-basis: 0;` might work too
- I had to do exactly the same thing some days ago to correctly truncate text with ellipsis.
  - [Flexbox and Truncated Text](https://css-tricks.com/flexbox-truncated-text/)
- min-width: 0 is not some hacky workaround, it’s actually the suggested behavior right from the spec.

- ## Just found out that window.getComputedStyle() won't list out all custom properties for a given element. 
- https://twitter.com/markdalgleish/status/1381105674260684800
  - You can request specific properties by name, but there's no way to get a complete list. 
  - I was hoping to automatically detect and forward all CSS Variables through a React portal, but this means I can't. Sad about it.
- [How to list all css variables names/values pairs from element](https://stackoverflow.com/questions/54004635/how-to-list-all-css-variables-names-values-pairs-from-element)
  - It's using a browser API that's been removed (getMatchedCSSRules), and their polyfill looks pretty expensive

- ## We just deprecated setting `body` properties with the expectation that they "propagate" to the viewport. 
- https://twitter.com/MiriSuzanne/status/1380310383588646916
  - This currently works with things like overflow, & will continue to work forever, because: The Web.
- Trust me, your life (or at least, the parts of it spent debugging CSS) will be easier if you get in the habit of distinguishing between styles on `<html>` (which fills the viewport) and styles on `<body>` (which might not).
- [viewport propagation of scrollbar-gutter](https://github.com/w3c/csswg-drafts/issues/6079)

- ## Over the past decade, writing cross-browser CSS has gotten easier
- https://twitter.com/JoshWComeau/status/1379101677589037062
  - browser vendors implement the spec without many custom flourishes.
  - This thread shares some scarcely-known browser differences.
- Starting in Firefox 88, CSS outlines will match the radius of their elements.
  - This even works with `outline-offset` — outlines that are further away will be more rounded!
- On MacOS, both Chrome and Safari will "soften" colours, making them less bright and vibrant. 
- A while ago, grid and transitions only worked well on Firefox, was that already fixed?

- ## Any hardcore CSS geeks able to confirm if `backdrop-filter: drop-shadow(...)` actually *does* anything in any browser?
- https://twitter.com/adamwathan/status/1378817428839407617
  - Same question for `backdrop-filter: opacity(...)` too.
- Okay so it seems like `backdrop-filter: opacity(...)` does actually do something — it changes the opacity of any other backdrop-filters that are applied, which I suppose makes sense 
  - Still pretty sure drop-shadow(...) does absolutely nothing as a backdrop-filter.
- It most likely will, but only in Chromium (AFK right now, so can't test).

- ## What are the most common things you use CSS filters/backdrop filters for? 
- https://twitter.com/adamwathan/status/1378423163185463301
  - Trying to figure out which values should exist for each filter function in Tailwind by default — always the absolute hardest part of building any new feature 
  - Making a bit of progress on some sensible default constraints here 
- Gray scale the page on slow page transitions.

1. grayscale() for disabled items.
2.  blur() mostly for modal backgrounds.
3. drop-shadow() for non-rectangular shapes (e.g. icons).

- ## Use "clip-path: polygon()" to create shapes with CSS 
- https://twitter.com/jh3yy/status/1377782704285097986
  - Need a drop shadow? Apply the "clip" to a pseudo-element 
  - Check this demo that's a "clip-path" version of the famous [The Shapes of CSS](https://css-tricks.com/the-shapes-of-css/) article
  - https://codepen.io/jh3y/pen/RwKpLYg
  - the demo is created with @reactjs && @prismjs
- How does that "drop-shadow" trick work? 
1. Create an element.
2. Create a pseudo-element.
3. Clip the pseudo-element.
4. Apply filters to the parent.
- For hollow polygons, you can use the zero-width tunnel technique

- ## An epoch-making new feature of CSS container queries are here! Now enable Flag in Chrome Canary to preview
- https://twitter.com/jieorlin/status/1376395220812619776

- ## Didn't realise CSS support and a plugin architecture was coming to esbuild. That's super exciting—and great news for vanilla-extract.
- https://twitter.com/markdalgleish/status/1375580423602888707
- Unfortunately, it is just a bundler, it does not provide the same rich API as babel, and we cannot operate AST.
  - Haven't looked into it, but we have pretty straightforward requirements and could probably get away without access to the AST.
- Esbuild provides a plugin API. The ast can be used from a separate library. 

- ## If you need to style multiple elements in a pseudo selector state (focus, hover, active...) you can use :is() to select them all at once!
- https://twitter.com/wesbos/status/1374771569852043269
  - Before you go all-in on :is(), there's three interesting things to know about it:
  - The selector list of :is() is forgiving
  - The specificity of :is() is that of its most specific argument (!!)
  - :is() does not work with pseudo-elements (for now)

- ## If you don’t want your background image to show underneath your padding space, you can use `background-clip` to prevent this
- https://twitter.com/Vanaf1979/status/1374341846021894148
- https://codepen.io/Since1979/pen/NWbQZYr

- ## Have you used `display: inline-block` to adjust visual width?
- https://twitter.com/5t3ph/status/1374376280146120709
  - What if you still want a different `display` type for that element, like grid or flex?
  - Upgrade to `fit-content` - retain block behavior but limit visual width!
- [Smol css Visited Styles](https://smolcss.dev/#smol-visited-styles)
  - The `:visited` pseudo class is very unique because of the potential to be exploited in terms of user's privacy. 
  - To resolve this, browser makers have limited which CSS styles are allowed to be applied using :visited.
  - A key gotcha is that styles applied via :visited will always use the parent's alpha channel - meaning, you cannot use rgba to go from invisible to visible, you must change the whole color value. 
  - So, to hide the initial state, you need to be able to use a solid color

- ## In terms of #CSS low specificity selectors, it's better to use the pseudo-class selector of ':not()' within the ':where()' pseudo-class.
  - :not会增加特指度，:where不会
  - Everything in the where brackets isn't counted in the specific, include the :where pseudo-class itself

- ## If you use low-level CSS Variables for theming, how do you declare your themes?
- https://twitter.com/markdalgleish/status/1373153810516877312
  - 1 theme via ":root"
  - 1 theme via class
  - 2+ themes, all classes 
- Each theme defined for the class, noy using root at all. Dark mode is just another theme with some special treatment that is used for invertef components like Tooltip in light mode and vice versa. So at least 2 themes at all times.

- ##  `color-contrast()` will automatically pick a color that passes contrast ratios, just give it a list to choose from. aka: throw colors at it!
- https://twitter.com/argyleink/status/1372634187866378243
- Ooh, it's only in Safari TP! That's not very obvious from this tweet. 

- ## In 2021 #CSS Specificity can be confusing with the new ":is()" and "where()" pseudo-classes.
- https://twitter.com/eladsc/status/1372445466709868545
  - https://codepen.io/elad2412/pen/72c460c264a736692b1a72733c390195
- As @dannievinther noted :is() takes over the specificity of the most specific selector contained inside it. I took the liberty to adjust the visualisation. Think this conveys the message better.

- ## CSS resets don't have to be globally scoped! Here's an example where I've taken the famous Eric Meyer reset and locally scoped it using @emotioncss .
- https://twitter.com/markdalgleish/status/1371047244095365122
  - This is obviously a bit tedious to use in this form, but you could make it more ergonomic by wiring it up to a primitive `<Box>` component or something similar, e.g. `<Box as="h1">` will apply the reset.h1 class.
  - This is particularly useful if you're building a component library and don't want to leak your reset into the global scope.
- mmh, you have to add className to every single element?

- ## Foldables, grid and custom props make a nice team don't ya think?
- https://twitter.com/argyleink/status/1370383578488442884
- https://github.com/foldable-devices/spanning-css-polyfill
  - This is a polyfill for the proposed CSS Foldable Display extensions.
  - Web developers targeting foldable devices want to be able to effectively lay out the content in a window that spans multiple displays. 
  - CSS Foldable Display extensions provides a mean to do that using stylesheets.

- ## I haven't seen any memory difference between overflow:hidden and overflow:clip.
- https://twitter.com/jaffathecake/status/1370320900025892868
  - overflow:scroll creates a new compositing layer and does a load more painting, 
  - but overflow:hidden and overflow:clip seem to behave the same in terms of GPU memory at least.
- The problem is that the two have different layout semantics, so it's likely to cause cross-browser issues

- https://twitter.com/argyleink/status/1371586954878275590
  - TIL: at least in Chromium, savings for `overflow: clip` are so negligible/small or would only exist under extreme use cases, that "less memory" has been removed from its list of benefits.

- ## Digging Into CSS Logical Properties
- https://ishadeed.com/article/css-logical-properties/
- https://caniuse.com/css-logical-props
- The basic idea of CSS logical properties is that we won’t use physical directions in CSS properties.
  - Instead, we will use properties that depend on the direction of the HTML document. 
  - Those properties are called logical properties.
  - 多使用start/end，而不是left/right

- ## Has anyone tried a CSS strategy where media queries can only change custom properties? 
- https://twitter.com/argyleink/status/1369887233700892677
  - no styles in media queries style
  - https://github.com/propjockey/css-media-vars
  - https://github.com/limitlessloop/typolize
- [CSS native variables not working in media queries](https://stackoverflow.com/questions/40722882)
- It really depends on the case, and in a lot of cases, when it acts well as params, I do.
- I do that all the time now. Very useful in case of :focus/:hover too.
  - I work with BEM. All my blocks have custom properties that can be set from "outside" the block. This to prevent nesting blocks. Resembles a how web components and ShadowDOM work too. Every block is standalone.
- I think I've experimenteel with typography and space scaling this way, by setting a var to be used with calc, and changing the var per viewport width

- ## How do I apply opacity to a CSS color variable?
- https://stackoverflow.com/questions/40010597
- You can't take an existing color value and apply an alpha channel to it. 
  - `--color: 240, 240, 240;` ; `color: rgba(var(--color), 0.8);` .
- The magic lies in the fact that the values of custom properties are substituted as is when replacing var() references in a property value, before that property's value is computed. 
  - This means that as far as custom properties are concerned, the value of --color in your example isn't a color value at all until a var(--color) expression appears somewhere that expects a color value (and only in that context).

- ## Your explanation of margin collapse is really good. 
- https://twitter.com/aalkz/status/1369168913309765634
- I return to that article from time to time when my css margins are acting up and I don't remember exactly why (which is often because it's an inherently confusing concept IMO).
- honestly I often work around this by only applying bottom margin on my elements.
  - Once flexbox `gap` support lands, I suspect I'll use margin way less!

- ## Have you used the :is() pseudo-class selector yet? 
- https://twitter.com/kilianvalkhof/status/1369605618068242434
  - It saves you from having to duplicate the entire selector just to set (for example) both hover and focus styles.

- ## I prepared a quick CSS Units Cheat Sheet for you.
- https://twitter.com/denicmarko/status/1368882923978579975
- [CSS Units Best Practices](https://gist.github.com/basham/2175a16ab7c60ce8e001)
- 1ch = width of 0 in font.
  - 1em = width of m in font.
  - 1ex = height of x in font.

- ## is there already a plugin for GIFs that does lazy-loading/Twitter style load (load animation on click)?
- https://twitter.com/allafarce/status/1368615483709091843
  - The goal here is to allow GIFs on the page but only pay the performance cost when the user wants to.
- Do you have the option to covert the gifs to video? If it's any help we have a short post on it
  - I could be wrong but I thought that twitter was secretly converting gifs to videos under the hood.
  - [Replace animated GIFs with video for faster page loads](https://web.dev/replace-gifs-with-videos/)
- Not a solution but don’t use gifs, use videos. Compression is much much better.

- ## CSS "content-visibility:auto" is amazing: skip rendering & painting offscreen content until needed. 
- https://twitter.com/addyosmani/status/1368479029683122180
  - I got a ~1s faster render on a long HTML document on desktop, ~3s on mobile.
- This property has an impact on screen-readers though as they end up not being able to discover the content until effectively rendered (which might be too late), so it's important not to use that on landmarks or elements containing landmarks.
  - Thank you for the reminder. I’d concur with the guidance to try keeping headings & landmark elements outside of areas using content-visibility:auto.
- I've played with that somewhat in an Electron app but it felt broken at best 🤔 Performance was affected negatively and I got weird glitches here and there. Maybe I should give it another try.

- ## How Spotify makes text on images more readable: a CSS linear-gradient overlay.
- https://twitter.com/addyosmani/status/1365735686838493187
  - More common these days, but still an effective technique for better color contrast.
- This tool right here can help you determine the opacity to use for the overlay
- Another technique from google.

- ## :focus only works on the exact input element. But, if you stick the element you want to style on focus immediately after the input in the HTML, you can do this
- https://twitter.com/jarredsumner/status/1365403128632238080
  - `input:focus + .FocusContainer {` .
  - Often this is to make `<label>` more prominent – you probably want it to visually appear before the `<input>` .
- `:focus-within` can also be used for this

- ## TIL CSS `background-repeat: round` repeats background images without clipping Scissors
- https://twitter.com/addyosmani/status/1275322697933881344
- repeat间距不变，直接重复，会截取只显示可见部分
- round会缩放间距，只显示完整图案
- space类似round
- https://twitter.com/anatudor/status/1099921793614336000
  - use `background-repeat: round` when you want your background to repeat n (integer) times AND have a size around a certain value
  - if you don't want any background stretching/ distortion, but you're ok with a bit of extra space in between background repetitions, go for `background-repeat: space`

- ## There are *lots* of different ways to hide stuff on the web
- https://hugogiraudel.com/2021/02/17/hiding-content-responsibly/
  - https://codepen.io/vincent-valentin/full/JjGmxzV

- ## Does the world need another CSS-in-JS library?
- https://twitter.com/markdalgleish/status/1365201894457679873
  - 使用postcss插件可以转换最新的css特性，类似babel
- Yes, something that can keep Lighthouse happy. I use one styled-component and Lighthouse screams at me to "REMOVE UNUSED JAVASCRIPT".
- What the world needs is CSS Variables-based zero-runtime library
  - CSS Variables are so much more suitable for themes and allow for the theme to be referenced from any context.
  - The only downside is that one can't use variables in a media query (for now?).
  - Custom Media Queries is in works
  - You can substitute it with "postcss-custom-media" for now.
  - What is really exciting is logical functions and constant variables
- Only if it outputs atomic CSS

- ## The css prop, as it was implemented, was a mistake.
- https://twitter.com/threepointone/status/1364696794005921801
  - it changes the type signature of every component 
  - the prop that's passed in is never available in the props received
  - the passed prop can't be examined
  - when composing, it has to be deserialised and serialised again
- How it should (could?) be
  - only 'host' elements (div, span, etc) should accept it and convert to className
  - other components could accept the object, but not convert to a className
- The css prop makes tracing CSS infinitely harder. It had/has great benefits, but that continues to be my biggest heartache about it.
- How does this compare to the styled syntax?
  - Dunno, never used it. I like the css() function.

- ## In general, items with bigger z-index values rise to the top, but that's not always true.
- https://twitter.com/JoshWComeau/status/1364569420325150722
  - Here, our tooltip (z-index 999999) renders under the header (z-index 2).
  - [What the heck, z-index?](https://www.joshwcomeau.com/css/stacking-contexts/)

- ##  For some reason, the blur is much more saturated on Firefox than Chrome. Not sure why, but ultimately both look good to me!
- https://twitter.com/JoshWComeau/status/1364313758584213504
  - Safari struggles with animating blurred elements. So be cautious with this one!
- Blurred pngs tend to be REALLY heavy (like, hundreds of kbs even after optimization), and jpegs don’t support transparency. 
  - Maybe some of the newer image formats are better, but yeah I’ve found it easier to do it in-browser.
- So apparently browsers don’t always agree on color space and it’s caused a number of bugs in the past. My guess is filter is new enough that the color handling in it either has bugs in one browser or wasn’t well specced for this usecase and it’s the Wild West.

- ## Avoid fixed dimensions! Layout should be fluid to cater for folks with different screens, preferences, and accessibility needs.
- https://twitter.com/jaffathecake/status/1364474359944007680
  - An indent must be exactly two spaces wide 
  - and prose must hard wrap at 100 chars.
- A viewer can choose how wide they want their tabs tab to render. 1.337 characters wide?
- 100 chars? Heresy! 80 or GTFO.
- 60 is my personal preference.  Ref https://baymard.com/blog/line-length-readability . Not just in design rendered but in code. Surprisingly helps keep things easy to parse. Yea, I’m totally crazy for doing this to myself.

- ## TIL that SVGs should almost always be sized with viewBox instead of width/height, and constrained by height (not width) via CSS when inlined into HTML.
- https://twitter.com/kripod97/status/1364319449306775554
  - Also, inputs and buttons should have a fixed height so they can follow a spacing scale without using weird paddings.
- How do you handle constrained-height buttons with user-defined text (thinking word-wrap ; )? 
  - I use Tailwind’s `inline-flex items-center justify-center text-center leading-tight` utility classes to make sure that even an anchor element behaves like a button would do.

- ## Does styled-components offer any lower level APIs for generating styles *without* generating a component? 
- https://twitter.com/markdalgleish/status/1364350921317097477
  - Something like Emotion's css function
- There’s an alternative solution called CSS Modules, have you heard of it?
  - I know you're kidding—but yeah, CSS Modules aren't great for super dynamic libraries. This is where CSS-in-JS really shines.
  - I’ve found that the most compelling solutions for your use case are CSS Modules + Tailwind + classnames to add dynamism or emotion with its css function.
  - You could give Twind a try. It is a tailwind-first CSS-in-JS solution
- css prop generates a styled component under the hood. I'm just wanting to generate class names without the component.
- My approach is to use a classes prop
  - https://twitter.com/pomber/status/1362125599607820290
  - https://github.com/code-hike/codehike/tree/v0.3/packages/classer
  - to make React component libraries interoperable with most styling solutions

- ## Braid uses arrays for responsive props, but I've realised objects are much better:
- https://twitter.com/markdalgleish/status/1362779695683543041
  - No need to plug holes with null, e.g. ['small', null, 'large']
  - Adding new breakpoints between existing ones isn't a breaking change
  - Types are simpler, e.g. `Partial<Record<Breakpoint, Space>>`

- Once you add it all up, I feel like it's tough to argue for responsive prop arrays over objects.
- I've been leaning on a more CSS approach recently either through a mediaQueries/variants prop:

```jsx
<Stack
  direction="column"
  mediaQueries={{ 'medium': { direction: 'row'  } }}
/>
```

  - More typing, but when you have a lot going on it's easier to discern IMO.

- Yeah, I believe Chakra supports both so you get the simplicity of the array for simple cases and the advantages you mention for the more complex ones. 
  - Loses some of the typing simplicity benefit though.
- We use them in our custom component system.
  - Btw braid inspired us a lot when we started to draft layout components API, so thank you very much
- Agreed. We swapped early on and never looked back.
  - Objects are much easier to parse and read too imp
- A related question: Do you define those breakpoints in Braid, or do consumers define those? Or I suppose you could provide defaults they override in the theme.
  - They're defined in Braid.

- ## CSS question, for folks with a deeper understanding of browser mechanics than me: Is there a difference between “layers” and “stacking contexts”?
- https://twitter.com/JoshWComeau/status/1362073864495370240
  - As far as I can tell, they're synonyms used in different contexts — layers are mentioned in terms of animation performance, stacking contexts in terms of layout and z-index. But are they actually discrete concepts? If so, what's the distinction?
- Yes, any transform (or non-0 opacity) (i.e. on the h1) creates a stacking context which would normally stack above the list. 
  - However `position: relative` explicitly stacks the list above the in-flow content (including that implicit context).
- I think stacking contexts don't get browser's GPU acceleration like composite layers
- it seems like if there is a difference, stacking contexts could refer to more rules than just layers. 

- ## The lesson: only use comma-separated selectors when those selectors have broad browser support. 
- https://twitter.com/JoshWComeau/status/1359213597331763200
  - When using browser-prefixed things, or cutting-edge stuff like `:focus-within` , you should repeat the rules instead.
- Here's what's going on: 
  - the comma operator is used to apply the same CSS rule to multiple selectors, but in order for it to work, *all selectors must be valid*.
  - When Chrome sees `-moz-range-track` , it doesn't recognize it, and it invalidates the *entire rule*.
- Firefox ignored but not fails on `-webkit-*` for compatibility reasons, since devs are/were littering their CSS with it and it was breaking sites in Firefox.

- ## print-to-pdf is almost good enough. Are there CSS tricks you can use to improve page breaks?
- https://twitter.com/Swizec/status/1358589201495728129
- There are a few things, you can force page breaks or try to prevent them inside specific elements (if possible) with "page-break-after" and "page-break-before"
- There is also "widows" and "orphans", which might come in handy
  - [Orphans and Widows in CSS](https://tosbourn.com/orphans-widows-css/)
  - Orphans are the lines of text that get left behind on an old page should a paragraph of text get split onto a new page.

- ## For an LTR layout, positioning an element outside its parent on the left side does not cause a horizontal scroll. 
- https://twitter.com/shadeed9/status/1358664786867798017
  - However, positioning the element on the right side does.

- ## Browsers have a built-in Dark Mode color scheme. 
- https://twitter.com/bramus/status/1358093784001740801
  - If you don’t change any of the default colors, you can have Dark Mode support by adding only this little piece of CSS:
  - `:root { color-scheme: dark light; }` .
  - To prevent a FOUC(flash of unstyled content), its recommended to use a meta tag for it though.
- [Improved dark mode default styling with the color-scheme CSS property](https://web.dev/color-scheme/)

- ## I got a question asking what I thought about CSS frameworks like Bootstrap.
- https://twitter.com/JoshWComeau/status/1357709670325059592
  - My answer: I do not suggest using them. Nor do I suggest using fully-styled component libraries like Material UI.
  - TL; DR — unless you’re building a short-term project (prototype, hackathon), CSS frameworks can be harmful, *increasing* the amount of time you need to spend on the UI. 
  - I recommend using a style-agnostic tool like Reach UI instead. 
  - Use third-party functionality, not styles.
  - A design is more than the sum of its parts. I can take a bunch of really-nicely-designed components and still wind up with a poorly-designed product. 
  - It’s been said that only Google can produce nice-looking Material Design apps, since their designers understand how to use it.
  - I teach at a bootcamp, and we strongly discouraged students from using fully-styled component libraries. 
  - Invariably, students would hit a point where they’d spend longer trying to override the styles/get it to work than they would have spent building it from scratch
  - Now there is one HUGE caveat here. I’m talking specifically about “styled” component libraries. 
  - Style-agnostic libraries like Reach UI, which focus purely on functionality, are a godsend and you should absolutely use them. 
  - Please don’t build your own modal from scratch.
  - I think if you’re a solo dev maker, investing in your design skills is the best thing you can do.
- 100 % agree. I think this is exactly why Material-UI is working on Unstyled Components in v5.
  - [[RFC] Material-UI v5:  Unstyled components](https://github.com/mui-org/material-ui/issues/20012)

- ## Today I looked into the performance of different layout modes in CSS. 
- https://twitter.com/JoshWComeau/status/1356377422925541377
  - I was curious if it takes the browser longer to lay out elements in a grid vs. Flexbox vs. flow layout.
  - TL: DR; they're all plenty fast, but there are small differences.
- For the benchmark, I created an app that renders 1000 random items, with a couple HTML tags in each one. I trigger a re-render, and measure how long it takes to recalculate layout.
- Regular flow layout. No CSS on the container.
  - I imagine this is the lowest it could be, since each element fills the available width. No "interplay" between children.
  - This will be our baseline!
- A flex column.
  - Very similar layout to the last element, except that margins don't collapse anymore.
- A flex row, with `flex-wrap: wrap` , and min/max sizes on children
  - This one requires a bit more computation, since the browser has to decide where the lines wrap.
- A 5-column grid.
  - I remember reading that CSS Grid could be slower in some circumstances, but it doesn't make a HUGE difference.
- I've seen a couple "CSS Grid is slow, use Flexbox instead" takes, 
  - and I feel much more comfortable now saying that you should ignore them Smiling face with open mouth and cold sweat the folks working on browsers are super smart 
  - and they wouldn't ship a layout method with huge performance problems.
- My takeaway: there is a cost when it comes to using dynamic layouts, but that cost is quite small in absolute terms.
  - Even on a low-end device, using Grid layout probably won't increase render times by a noticeable amount

- ## I'm working on a UI for a client project and wanted to share some CSS and SVG goodness.
- https://twitter.com/shadeed9/status/1353047713256882177
  - The requirement is to implement a dynamic tape element that can be colored, rotated, and sized. 
  - This is a very good use case for CSS and SVG. Isn't it?
  - https://codepen.io/shadeed/pen/OJRYaZK
- (1) I used Adobe Illustrator to group the tape into three layers. The base, white areas, and black areas. All of the layers have a semi-transparent background. This will help in making them *blend* with elements underneath them.
- (2) Then, I exported the SVG and placed the content within an `<def>` . This will help me in reusing the SVG in other pages without duplicating the code each time. Also, I used `fill: currentColor` to pass a custom color to each tape.
- (3) To make it easy to customize the tapes, I will use CSS variables as inline styles.
- (4) That's it. We created a dynamic tape that can be colored, sized, and rotated very easily. Thanks to CSS and SVG!

- ##  `--bg: ; /* with a space */` vs `--bg:; /* no space */` .
- https://twitter.com/MiriSuzanne/status/1352055999771787264
  - for `body { background: var(—bg, green); }` .
  1. A value of ‘ ‘ is valid but not a color, no background
  2. No value (eg ‘guaranteed-invalid’), fallback to green
- `--bg:;` is not a valid declaration, and is *ignored*

- ## CSS conic-gradient borders 
- https://twitter.com/argyleink/status/1282889809782927360
- https://codepen.io/argyleink/pen/pogZxaZ

- ## Did you know that you can make any element resizable, just like `<textarea>` ?
- https://twitter.com/denicmarko/status/1351431494733062145
- it won't work without `p {overflow: auto; }`

- ## I remember hearing that it was safer to use numbered font-weights (eg. font-weight: 700 instead of font-weight: bold) because of a browser rendering bug.
- https://twitter.com/JoshWComeau/status/1351179391938813963
  - Does anyone remember what this was? Has it been fixed?
- That's because if a bold variant is not part of the font-face, the browser will try to make it bold by itself (Sometimes making the text look really ugly). 
  - But if the browser cannot find a numbered variant, it will just skip it and render the text at normal weight.
- Both tachyons and tailwind still use numbers for font-weights. I do, too.

- ## You can use the `:target` pseudo-class to create modals with zero JavaScript.
- https://twitter.com/denicmarko/status/1350761109360414721
- Only problem is accessibility. 
  - You still need JavaScript (I believe) to close the modal by pressing escape or clicking outside of it.
- you can't use anchors inside modals and you don't have control on it. 
  - For example updating aria attributes or activating the focus trap, because you don't know when it's open/closed
  - I made this long time ago to test this approach.
