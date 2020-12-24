---
title: note-style-css-in-js-dev
tags: [css-in-js, style]
created: '2020-08-07T16:13:30.609Z'
modified: '2020-09-25T05:56:45.321Z'
---

# note-style-css-in-js-dev

## guide

- why use css in js
  - 维护方便
  - all-in-js的趋势
  - 标准化theme的趋势
  - 局部样式、动态样式、主题切换
  - 技术选型时，参考知名项目或大公司项目的选择
  - 灵活性
    - 书写的样式可编译成极短的唯一名，也可以编译成开发调试时的长样式名
    - 调试时编译成类似bootstrap的唯一类名，发布时编译成atomic css
    - ！！！ 甚至可以在发布时编译出使用css vars实现的theme

- I feel like we’re moving out of the CSS-in-JS era into something new. We’re moving more towards:
  - Static extraction
  - Zero-runtime
  - Types
  - Platform-agnostic: atomic/tailwind output, native
- Something we could perhaps call “TSS” (Typed/Token Style Sheets)

- [How to increase CSS-in-JS performance by 175x](https://itnext.io/how-to-increase-css-in-js-performance-by-175x-f30ddeac6bce)
  - Keep your CSS as static as possible for variations (the most important optimization)
  - Consider compile time libs like linaria, compiled
  - Use CSS Variables for theming

## theming

- While I love the API and DX of Theme-UI (and derivative libraries like Chakra), they are fatally flawed without static CSS extraction. 
  - https://twitter.com/jaredpalmer/status/1271482711132254210
  - Hooking every single component into that theme and calculating runtime styles is death by 1000 cuts. 
  - You pay a price for every single `<Box>`
  - Pinterest has a very fast `<Box>` component [implementation](https://github.com/pinterest/gestalt/blob/master/packages/gestalt/src/Box.js). it’s got Only 30 properties and mapped direct to css modules. No runtime theming.
  - It's been my experience as well with things like styled-components, etc. 
    - React is slow enough without having to double the number of components, parsing CSS strings, etc.
  - I think Linaria would work as a better foundation since theming is based on CSS variables. 
    - However, Tailwind and RNW's StyleSheet will still be more efficient in the long run as the app grows, because they have atomic classes.
  - Styletron is fine. 
    - Has good perf. Uber uses it. 
    - Any ThemeProvider is still a really really bad idea imho
    - How would you declare and access your theme? CSS variables only? Exported from a regular module?
    - Export from regular module. That’s how we do it.
  - Does what you're describing also apply to styled-components (using their ThemeProvider)? I know they support static extraction, but I specifically am not using it. Or is this a Theme-UI thing?
    - It's both, since both implement the "styled" API whereby CSS is a function of a components props and a global theme object is injected in to those props, which requires a Context Consumer wrapping every single styled component instance
  - I can’t say I’ve noticed any perf issues but this seems like something Theme UI could solve pretty easily with a plugin at build time for static sites or asynchronously when you initialize the theme provider
  - One thing I've learned from using Tailwind in a component-based framework (React/Vue) is that neither fully static or fully dynamic is perfect. 
    - You've gotta do a mix of static for things that can be extracted, and dynamic for other things.
    - Tailwind is a great example of fully static. But if you have more than a few design tokens, and you want to generate variant classes (screen size, hover, focus) you end up with _too_ much CSS. This is why most Tailwind users reach for PurgeCSS. But that causes its own problems..
    - If you want a component like this `<button color="blue">` to render `<button class="text-blue-500 hover:text-blue-700 focus:text-blue-800">`, there's no guarantee that those classes will exist because they may be purged.
    - All this to say, I totally agree that 90% of CSS can be static, but that 10% is a real problem that has to be dealt with.

- Is static extraction seems realistic?
  - Static extraction is realistic, at work we created library (something like Chakra but with some special features) and we try to generate theme for components to CSS and it looks promising
  - Static extraction is definitely realistic and something I plan on digging into in the near future.
    - Theme UI definitely can be improved performance-wise, we just wanted to make sure we nailed down a solid DX before investing time on optimization.
    - It's about that time
  - I agree it should be static, and with the current API I think it can eventually be transitioned to static calls. 
    - There's some current work glaze in this space 

- We really should stop using React Context for theming libraries when CSS Variables:
  - https://twitter.com/buildsghost/status/1251569049940537345
  - Are capable of everything you need for theming purposes
  - Can just as easily be the underlying implementation detail of these libraries instead of React Context
  - Are measurably more performant
- CSS-in-JS libraries have become Very Fast (enough at least). 
  - But the CSS-in-JS theming libraries that everyone is using have not.
  - And the performance problems they (eventually) cause are going to be much harder to refactor your way out of.
- I am very much with you on this. 
  - In fact I had a wip thing for my CSS in JS library style-sheet to add support for theme-ui via custom properties and extract em to static.
  - That said I think React Context shines when you want to subscribe selectively i.e. just a portion of the subtree or a few components. 
  - In that case you automatically get encapsulation i.e. upper and (important) lower boundaries without having to reset theme.
- Does reading from a theme file in context have a noticeable performance impact? 
  - I always assumed it’s pretty cheap as long as it’s not changed.
  - Using context thousands of times will eventually start having a performance impact. To be fair you can get away with it for a long time. But once you can't, now you have thousands of things to update
- Unfortunately that won't work if you need to make your lib cross platform with RNW. RN does not have css vars.
  - Context theming and core React code is more portable.
  - it's possible to compile to 2 targets - web & RN, which could use different theming solutions, or just have 2 flavors of the lib, depends on how do you author ur cross-platform code
  - it wouldn’t be that hard to build for the app level, slightly trickier when preparing such universal library but totally doable thanks to pkgJson["react-native"] support. All boils down to how you want to consume theme exactly and some work on top of that
- It'd be pretty easy to use progressive enhancement in those cases. 
  - Make every property: `background: ${theme.pageBackground};` to 

`background: #eee; 
background: var(--pageBackground); `

  - This is a pretty simple build-time transform, or at runtime with a stylis plugin using emotion
- Context is type safe and testable. CSS variables are not.
  - How do you prevent typos or name conflict with this?
  - Also, Context works on all browsers and doesn't need the browser to be tested (since it works with React-native too after-all)
  - There are polyfills that you can use and yes it is still experimental, however, there are benefits to using a future standardized API (i.e. eventually you'll end up shipping no code for that feature)
  - About the typos and name conflicts, take a look at the solution used in Linaria
  - Specifically `stylelint` lets you statically analyze your CSS-in-JS (zero runtime and built on CSS variables)

## pieces 

- css-in-js vs sass
  - Component Driven idealogy. Your CSS also is now a component. - This is pretty cool!
  - Total styling isolation
  - Load what you need and when you needed, kinda lazy CSS
  - Theme provider, skins, modularity and dynamic - This can be achieved by other libs too
  - Server side construction of your component DOM and its style.
  - Remove the need to manually handle class names
  - Easily use javascript variables within style
  - colocate css with jsx/html
  - 参考使用css-in-js的优点

- [Why Don’t I Sell the Idea of Static Extraction with CSS-in-JS?](https://medium.com/@tkh44/why-dont-i-sell-the-idea-of-static-extraction-with-css-in-js-df21f571503b)

- CSS has a dynamic nature, with one-off rules applicable to only a few pages per site. 
  - I think we should address this need first, and then generate a bundle of common styles upfront. 
  - Add the latter as a static `<link>`, based on spacing/color/etc. scales of a design system.
  - Utility CSS libs like tailwindcss do a marvelous job at defining classes upfront.
  - However, issues may arise after purging unused class names, especially when generating those dynamically.
  - I propose dynamic-first styling, replacing css(…) calls with static classes in a 2nd pass

- Right now our design system is a monolith with a global CSS file and a bunch of React components. 
  - While it is versioned, there’s not a safe way for a project to use multiple versions of the system (think micro-frontends).
  - Thinking again about how to break up into smaller packages that can truly be independent. 
  - Splitting React code out isn’t too complicated. 
  - What is complicated us how to handle the styling.
  - CSS Modules was surprisingly easy, once I got the tooling working. That was the hardest part.
  - Emotion was really not hard either. Took a bit of back and forth on using emotion/core vs emotion. 
    - Ended up with standard emotion because it takes less setup (didn't need babel junk) and was still able to use `cx` which is their fancy `classnames` package.
    - What sucked with Emotion was I was never able to figure out how set up a complex amount of variations for my button example. Multiple color, fill, and size options and all of them have unique CSS. 
  - Stitches was great to install. Almost zero config changes. The built-in theming and variables are super nice. I came up with an interesting way of composing the component that I was starting to like.

- [survey: styled-components vs SASS vs CSS, which one would win!](https://twitter.com/Ipenywis/status/1275091218905608192)
  - s-c:sass:css = 2:1:5
  - 仅8人投票

- It's funny how CSS-in-JS is controversial vs. external/extracted CSS files, but web components basically require inline CSS strings in JS. 
  - Due to the complete style isolation, you basically cannot bundle CSS to a separate file with shadow DOM in a performant way.

- The more I look at projects like tailwindcss and tachyons_css, the more I realise CSS-in-JS misses the boat(错失良机) on solving the important problems with large-scale CSS:
  - No specificity issues
  - No bloat(膨胀，过多)
  - No naming wars
  - No opinionated component-based architecture

- Wholeheartedly agree, BEM + ITCSS all the way as opposed to(相对于，而不是) sprinkling(撒在，使用少量) utility classes on top of everything. 
  - Tailwind creates a many to many maintenance problem that just makes large codebases unmaintainable. 
    - if you apply 4-7 CSS classes to style something out of let's say 100 available classes to 1000-10 000 lines of HTML, there are too many variations. 
    - If you ever want to get rid of a class it's going to be difficult, as the combinations are practically infinite.
    - Whereas if you scope CSS to a namespaced selector e.g. `.c-my-component-name` you will be able to see all instances of this component in use when you globally search your project and you have a clear route to refactoring
    - So... give it a few years and lots of team will be stuck loading Tailwind's 350kb forever because they just can't get it out of their codebase.
  - I imagine it’s popular because of CSS-in-JS.

- css in js style
  - Old way: Include this css import to get styles.
  - New way: Styles automagically added when you use the component.
  - Old way:
    - you control all your styles
  - New way:
    - those fucking styles appearing by themselves, your application contains at least 3 css-in-js libraries, some of them duplicated, your app looses half of styles during SSR, 
    - and you are looking at some AstroTurf, which ends as css.

- With our css-in-js lib(radix) and components, we have core layers and then framework-specific layers. 
  - We can build Svelte or Vue wrappers, so we're not necessarily tied to any particular framework.
  - The design tool just maps styles to components.
  - It's not inherently linked to React.

- I tend to stick to what I know that works at scale (BEM/ITCSS). But I also find that there is such a huge learning curve to BEM/ITCSS that it leads to problems in itself. Is scoped styling the answer? 
  - For a personal project, I'll generally go with BEM. For a project involving many developers and which will be used and maintained over years ? Scoped styles for sure.

- [Why write CSS-in-JS when vanilla CSS is just fine? ](https://twitter.com/saltnburnem/status/1290690315540717568)
  - The styling of a component is very linked to it's structure, so put them together.
  - The main element of reuse is the component. You won't ever need a .header CSS class when instead you'll reuse `<Header>`

## jss

## survey: css in js vs css

- ### [are there any cons to using regular CSS vs CSS-in-JS?_2018](https://twitter.com/ka11away/status/1014990019801411586)
  - css: css-in-js = 0.557: 0.443 /79votes
  - It’s depends on ur purposes. 
    - If u use dynamic generated styles (in runtime) a lot — css-in-js (styled-components) is a nice choice. 
    - If not, better use static css-in-js approach (emotion + extract, css-literal-loader) or classic

## ref

- [The Next Era of CSS in JavaScript - From CSS-in-JS to TSS_202008](https://joebell.co.uk/blog/the-next-era-of-css-in-js)
  - More and more libraries are choosing to focus on features such as:
    - Static extraction
      - to inline critical styles and CSS files.
    - Zero-runtime
    - First-class TypeScript support
    - Design Token-driven
    - Platform-agnostic
      - outputting atomic classes or config files (e.g. Tailwind)
      - native/multi-framework support
  - It's these fundamental changes that lead me to believe we're moving into a new era; one I like to think of as TSS.
    - TSS - Typed/Token-driven Style Sheets
- [CSS-in-JS and the death of traditional CSS_202007](https://www.diogorodrigues.dev/blog/css-in-js-and-the-death-of-traditional-css)
- [CSS-in-JS: An Investigation. An introductory comparison_202007](https://t.co/y5zfBsY9IY?amp=1)
- [Tailwind just keeps exceeding all expectations. I’m about to leave CSS-in-JS and go all in on Tailwind for any new projects I do](https://twitter.com/flybayer/status/1290016656299683840)
  - It’s nothing but great.
