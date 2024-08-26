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

# discuss
- ## 

- ## 

- ## 

- ## 

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
