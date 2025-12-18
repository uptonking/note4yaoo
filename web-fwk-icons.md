---
title: web-fwk-icons
tags: [icon, web]
created: 2021-04-17T15:27:54.454Z
modified: 2021-07-28T19:22:07.339Z
---

# web-fwk-icons

# guide

# popular-icons-solutions
- ## heroicons
- https://github.com/tailwindlabs/heroicons
- @heroicons/react
# discuss-figma-icon
- ## 

- ## 

- ## 

- ## What's the best practice in 2024 to get SVG icons from a Figma design into a Vite web app with minimal impact on app bundle size?
- https://x.com/schickling/status/1825836159244599452

# discuss-tools-icon
- ## 

- ## 

- ## Meet http://draw.supply — an open-source illustration library, updated weekly for personal and commercial use.
- https://x.com/talktogoutham/status/1885335252274733275
  - Free to use in any project without restrictions. Just no reselling as illustration pack or an a illustration paid library.
  - Handmade by my partner @KikiDoodoo & designed by me.
  - Font is Made Gentle

# discuss
- ## 

- ## 

- ## 
# discuss-svg-icons
- ## 

- ## 

- ## 💡🔡 SVG icons have been "solved" myriad ways, but I find them all lacking.
- https://x.com/fractaledmind/status/2001372075559391595
  - Inline SVGs? Bloated DOM.
  - `<img>` tags? Can't change colors.
  - Icon fonts? Blurry at certain sizes, a11y issues.
  - CSS background-image? Still can't change colors.
  - But, today there's actually a perfect solution...
  - CSS `mask-image` + `background-color: currentColor` .
  - This technique was elegantly explained by @rikschennink back in 2022
  - The key insight: instead of changing the SVG's fill, you mask the element and change its background-color. Simple, but powerful.
  - @joeldrapper and I have talked about how to perfect the concept in that post for months. And we have a new NPM package / Tailwind plugin that is truly the *perfect* way to work with icons on the web.
- https://github.com/joeldrapper/maskicons /MIT/202512/ts
  - Tailwind CSS v4 utilities for popular icon sets. This lets you include icons with Tailwind LSP auto-complete and thanks to Tailwind’s tree-shaking, your output CSS will only include the icons you actually use.
  - Supported icon sets: Bootstrap, tabler
  - The icon inherits currentColor by default, or you can override it. Plus, the icon scales with font-size.
  - The killer feature: Tailwind's tree-shaking means you only ship the icons you actually use. No icon sprite containing 2000 icons you'll never need. No runtime JS to load icons. No extra HTTP requests. Just the CSS for the icons in your markup.
  - maskicons ships with Bootstrap Icons, Tabler, and Flag Icons—but the technique works with ANY icon set. 
  - The utilities use `:where()` selectors, giving them zero specificity. This means ANY utility class overrides the defaults. 
  - the  browser support? ~95% global coverage. Full support in Chrome 120+, Safari 15.4+, Firefox 53+, Edge 120+.

- Sprites were my go-to approach previously, but you sent down the full icon set when you only will use 10-20% of the icons. The tree-shaking with the TW utilities is just lovely. And the simple accessible descriptions via text content is a cherry on top.
- You just pick the ones you need in the sprite, c'mon.
  - But you send the sprite sheet down over the wire I mean. Leveraging TW’s tree shaking means your CSS file only includes the icons you use out if the whole icon set. But again, I’m a fan of the svg sprite sheet approach. It does have a perf hit relative to inline SVGs or masks tho
- Yeah but you craft the sprite by hand. 
  - For sure, if you manually “tree shake” them you get lots of the benefits from the spritesheet. I need to find the details on the perf hit, but when dealing with a larger number of icons on a page, there is a perf difference. 

- I would still use sprite instead of inlining svgs when dealing with many icons. Inlining them results in redownloading them every pagehit + chunked HTML = potentially delayed discovery of other (typically image) resources. All while sprite svg is cached after first pagehit

- fwiw that's what we do on tldraw
  - https://github.com/tldraw/tldraw/blob/main/packages/tldraw/src/lib/ui/components/primitives/TldrawUiIcon.tsx

- I believe @antfu7 has brought this up back in 2021:  
  - [Icons in Pure CSS](https://antfu.me/posts/icons-in-pure-css)

- And the DX is just lovely. The tree-shaking, the accessible icon name/description, and the color control all together has been such a quality of life improvement over the other approaches I’ve tried over the years
  - Yeah, svg->jsx with props that modify stroke are incredibly finicky. This solution sounds super, also in regards to tailwind treeshaking!

- Only possible for mono colored svg
  - yes
  - 但是可支持css渐变色
- You can even attain multicolor icons with stacked masks and animation!

- Or just use SVG sprites, and you can do whatever you want with them via CSS.

- svg容易支持react-native

- That's how I use remote icons from iconify on web. Here's my cross-platform solution (react native + web)
  - You don't need this with the official Iconify react library, but I don't use it, as it will only load on demand. I have a custom one for bundled icons so there is no FoC when an icon is rendered. But this is useful icons for icons you don't expect (user solicited)
  - Looking back at it now would probably replace useEffect and useState with use. And ofc add an AbortController. But you get the idea.
  - [Icon.base.tsx](https://gist.github.com/TheUltDev/cbd3fa36bb9df407e0e3041d83b0d66d)

- Sprite svg might be a solution, but there are also “svg-use” package and “svgr” and Astro has its built-in icons management tool which allow to maintain each icon by storing its own svg file and everything is cached and has awesome developer experience as well. Typesafe too

- I've been using SVG mask images for years with the -webkit- prefix 🤓 Which is even more exciting is that you can use those masks with gradients to fade the content or regular background images to get some fancy shapes.

- 🐛 Potential issue with this approach is that you’re now front-loading potentially 10-100s of icon definitions inside your root css file, which blocks render. I seem to remember a noticeable LCP increase when we tried this approach on a project with tons of icons.
  - There’s also the downside of more frequent cache misses. Especially with Tailwind, your root css shouldn’t change that often, if ever. This means you’re able to cache it for months. By adding icons to it, you’re increasing the likelyhood of it changing, thus invalidating cache.
  - These reasons lead us in the direction of spritesheets, which lessened both of these issues. The issue with these however, was the lack of tooling around generating them.
  - I’ve tried solving that issue with react-icons-sprite package. It automatically detects imports from popular icon packages, extracts them in to a spritesheet and replaces your inline icons with leaner `<svg>` + `<use>`. Result is the benefits you described + less issues we noticed.
- https://github.com/jurerotar/react-icons-sprite /MIT/202512/ts
  - a lightweight plugin for Vite and Webpack that turns React icon components into a single SVG spritesheet and rewrites your code to reference those symbols via `<use>`.

- gradient fill on SVG icons has been a great pain. masked icon techniques looks neat.

- ## what is the best performant and DX approach to import icons?
- https://x.com/peer_rich/status/1868635934822138237
  - at @calcom we currently have a build-process to turn all icons into a massive `sprite.svg` (introduced here: https://github.com/calcom/cal.com/pull/16135).
  - but while performance is great, developer experience is poor and we run into more edge cases than we would like
- I'm working on a vite plugin to generate sprites based on an input path. When I finish it I'll let you know.

- unplugin-icons is great. You can make a wrapper around it to use a single Icon component controlled by props

- if you are not styling them much and have close to non-interactivity, I would rather keep them as assets. On the contrary, if they are small and reusable, I would have them inline. but I am facing performance issues with this approach as well, even if I use tools to minify them.

- I made something for this that solved my problems with SVG in React. It’s using a reference file to all your icons and then loads them on demand depending on the renderer you need; 

- ## 🆚️ Article greatly explains strategies to load SVGs + tradeoffs. Then introduce a toolchain to make SVG use convenient
- https://x.com/sebastienlorber/status/1831291514070122593
- [Introducing @svg-use | Fotis _202408](https://fotis.xyz/posts/introducing-svg-use/)
  - This post introduces @svg-use, a set of tools and bundler plugins, to ergonomically load SVG files as components, via SVG’s `<use href>` mechanism.

- ## How to add 500kb+ of JS to all pages? 
- https://twitter.com/TkDodo/status/1729806516893389155
  - Easy: Have an un-optimized PNG (3k pixels wide), inline it into an SVG with base64 encoding, then render it as a React Component (svgr), which will inline it into the shared JS bundle
- Just use svg sprites instead of svgr and decrease it to 0

- ## Rendering lots of SVGs in React Native (especially Android) is surprisingly terrible for performance. You're better off with PNGs
- https://twitter.com/kadikraman/status/1720502412077580603
- This is a known issue, due to how android handles rendering svg. Each has to be rendered as a component, whereas ios offers native svg handling last I knew. The solution is to use font icons for svgs and pngs for anything over 50x50
- I found out this the hard way, thankfully  plain old views worked really well for my use case
- This seem more like a react native problem. Works fine in native android
- I’ve had this feeling as well (without digging deeper). Would be interesting to compare rendering performance with SVGs rendered through react-native-skia

- ## Your icons should be SVG sprites instead of JSX
- https://twitter.com/jacobmparis/status/1682904429366857732
  - make a component like `<Icon name="trash" />` (referenced by string)
  - get autocomplete for icon names
  - auto build the spritesheet when new svgs are added
  - [Use svg sprite icons in React](https://www.jacobparis.com/content/svg-icons)
- Good writeup! One suggestion I have would be that if you're going to write a JSON file to disk as part of the SVG generation script, you might as well just write out a Typescript type definition instead to simplify things. Same goes for the Icon component itself!

- ## 🚫💡 Please don't import SVGs as JSX. _202104
- https://twitter.com/_developit/status/1382838799420514317
  - It's the most expensive form of sprite sheet: costs a minimum of 3x more than other techniques, and hurts both runtime (rendering) performance and memory usage.
  - This bundle from a popular site is almost 50% SVG icons (250kb), and most are unused.

- If importing an SVG is the best thing for you ergonomically, choose a solution that returns a URL for use with `<img>` , or extracts them into `<defs>` for use with `<use href="#">` . 
  - Unlike JS, SVGs inlined into HTML are pretty cheap.
- Inline SVG often allows for more accessibility though, works well. Seems like a client side JSX problem instead.
  - No difference between inline and `<use>` for accessibility. Plus for icons there isn't really anything valuable to be set within the svg thst can't just go on the root.
- If you define them in `<defs>` do all the SVGs have to be defined inline? One for the defs and then one for each usage?
  - You can define them in many different hidden SVGs, or you can use `<svg src="">` within the defs. 
  - There are actually some solutions that do this automatically with similar ergonomics to the more common "import as a component" solutions.
  - JetBrains/svg-sprite-loader: Extract SVG sprite as separate file with extract: true option; except of Safari (both desktop and mobile) and Android browser prior to 4.4.4.
  - `<img>` doesn't work with CSS and currentColor for fill. When using React putting it into JSX in React components is the easiest. With code splitting it's not as bad I guess. Is there an easy solution (e.g. bundler-based) for the `<use>` approach? That would probably be best.
- What about a web component that fetches them on request?
  - Or go completely out of the SVG box and don't import SVG at all. Let a `<svg-icon>` WebComponent create the SVG Client-Side (used in an `<svg>` or `<img>` tag) and fully stylable with attributes and CSS (properties)
- They are not cheap when they are 3000 elements (tried going this route with an emoji keyboard, font or png sprite is so much better)

- If you server rendered that check icon in a list with 1000 items, it'll be duplicated across 1000 html elements.
  - I don't know enough about svg, but can you put a full blown `<svg>` inside a def and reference it? `<def><svg /></def>`?
  - Yes. This is the best solution for performance.
  - too bad we don't have html imports and do the same thing there
- The problem is that icons are either used repeatedly, or there are many of them, or both. 
  - In both cases, rendering them in JS is far more expensive than using `<use>` or `<img>`.
  - A few "lines" of paths adds up, because path data does not compress well.

- Just want to know what would be the best way to use svg. 

```jsx
const icon from './icon.svg';
function Icon(props) {
  return <img src={icon} {...props} />
}
```

- what if i want to use animation on svg?? `</img>` can't do that.
  - You can use inline SVG without inlining the SVG into JS. Inline it into the HTML (that's what "inline SVG" means). 
  - Or you can use `<object>` , which supports animation.
- in practice this doesn’t work as often you need to be able to style SVGs with CSS
  - at Yelp I built it like this 5 years ago but you can control only one color (probably fine in most cases). **Ultimately inline SVGs are way more easy to work with**
  - [Yelpicons: A Cross-Platform Icon Build System_201605](https://engineeringblog.yelp.com/2016/05/yelpicons.html)

- I'm a bit lost as to *why* it costs 3x more and the performance is bad though. Care to explain?
  - normally, an SVG is download cost (rendering doesn't have any main thread cost).
  - SVGs inlined into bundles get downloaded as JS, then parsed & evaluated as JS function calls to create objects, then rendered by a UI library (often repeatedly).
  - There is also a hidden cost here we don't really talk much about, which is that it's more expensive to execute a bunch of JavaScript to build up static HTML trees than it is to let the browser parse them along with the rest of the HTML for a page.
  - Also the tiny little extra cost of it actually being a (p)react component instead of a primitive element. Even if pure, etc it's still there in the tree for no particular good reason.

- What if each SVG is a component? Wouldn't tree shaking (mostly) solve this?
  - That just spreads out the problem over time. The memory issue and performance impact are still there, just less up-front.
  - code-splitting these is better than nothing, but since there's no technical reason for inlining SVG into JS in the first place, we can do better.

- I'm guessing this is only an issue with frameworks where each DOM node is function call though (React, Preact, Mithril, Inferno, etc). I imagine Svelte for example wouldn't suffer from this.
  - there's still overhead. there's a cost to having _any_ data represented in code
  - indeed. unless the SVG ends up being fully extracted from bundles, something is doing the work of parsing it and generating imperative DOM calls (effectively an expensive emulation of what browsers already do for us).

- What about inlined as JS strings and created with innerHTML? I assume still more expensive than `<def>` directly in HTML, but cheaper than vdom render fns.
  - Considerably. But hard to do if the svg is a top level element, since you can't nuke the component's container, and you can't use innerHTML with the SVG element
  - FWIW Svelte will do exactly this where it *is* possible, but those cases are rare
  - Yeah, Vue 3 does this too but have similar bail out conditions
  - Cheaper yes, though mainly for large SVGs. The bundle in the screenshot is actually doing that to a small extent IIRC, but for tiny icons like this, the cost of invoking fragment parsing can end up being basically as bad as nested render functions.
- Just do some related optimizations on tiktok.com, define the global inlined svg in `<body>` and `<use>` them in svg component.

- would you recommend using SVGR?
  - NO. IIRC that is the exact solution that produced the bundle in js.
- AFAIK using the loader is different https://react-svgr.com/docs/webpack/. It's the same approach that CRA uses and the webpack loader does some more magic.
  - it's still the same principle. You get a component that is just the svg inlined. It's still big blobs of JS with lots of JSX svg elements inside.

- what about dynamic import the icons instead build it in the bundle? as @elastic/eui did
  - Thst just spreads the problem around, doesn't address it.

- Inline the SVGs into the HTML and reference them like this: `<svg><use href="#foo-icon"/></svg>` . 
  - It works exactly like an inline SVG, no flash.
  - https://github.com/Epimodev/svg-sprite-html-webpack

- https://github.com/ToniMaunde/react-svg-component
  - I'd recommend tweaking this to avoid importing the JSON in the icon component. Currently it embeds all icon path data into bundles and can't be tree-shaken.
  - [Blueprintjs](https://blueprintjs.com/docs/versions/4/#icons/loading-icons) follows the same approach. They solved the issue of bundling all icons in v4. It's a bit complicated solution but they went for it to keep the nice DX they had. 

- What about if you have loads of icons, it's quite common to want to modulate the color of the svg icon. Having it as jsx is super convenient! Doing this with URLs would be annoying?
  - I've used CSS filters as a solution to this problem in my projects. As long as the icons are monochrome, it works quite well

- yes! also with css, why would you have css inside the javascript file if you can use an actual css file and let the browser cache it!

- I guess one thing that a lot of the replies don't take into account is dynamically changing SVGs, where you still probably want them in JSX

- how we can change color, size and ... of a svg programmatically if we don't use inline svg?
  - IIRC currentColor doesn’t work unless the svg is inlined. That being said, there are ways to inline other than using JSX
  - Exactly this. The only reason we aren't loading svgs through img tags is the currentColor problem. If you have basic svgs that never change color or style based on state, then an img tag might be fine.
  - If the svg must be inlined for styling, I think it’s a good compromise that maintains ergonomics and low complexity.
  - There’s room for a SVGR-like tool that makes inlining SVGs ergonomic and efficient, though 

- What about if you have loads of icons, it's quite common to want to modulate the color of the svg icon. Having it as jsx is super convenient! Doing this with URLs would be annoying?
  - Use `<use>` - it's the same functionality without the cost.
  - I remember having issues with not being able to target certain things which were possible with raw inlining. I think I wanted to target specific `<path>`s inside the icons for styling interaction feedback.
  - You probably can't access children because it's shadow DOM, but considering that they are just icons, it's quite an uncommon use case. Maybe you were placing more complex SVGs into the sprite, even those that you wanted to manipulate with CSS/JS?
  - I've used CSS filters as a solution to this problem in my projects. As long as the icons are monochrome, it works quite well Thumbs up
