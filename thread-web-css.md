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

``` jsx
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
- it won't work without `p {overflow: auto;}`

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
