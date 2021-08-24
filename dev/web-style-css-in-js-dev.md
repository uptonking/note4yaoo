---
title: web-style-css-in-js-dev
tags: [css-in-js, style]
created: '2020-08-07T16:13:30.609Z'
modified: '2021-01-01T20:06:19.327Z'
---

# web-style-css-in-js-dev

# guide

- why use css in js
  - 维护方便
  - all-in-js的趋势
  - 标准化theme的趋势
  - 局部样式、动态样式、主题切换
  - 技术选型时，参考知名项目或大公司项目的选择
  - 灵活性
    - 书写的样式可编译成极短的唯一名，也可以编译成开发调试时的长样式名
    - 开发调试时编译成类似bootstrap的唯一类名，发布时编译成atomic css
    - ！！！ 甚至可以在发布时编译出使用css vars实现的theme

- css-in-js-cons
  - styled形式的css in js，跨项目复用css难
    - 不方便将一套css用在多个项目，可考虑实现一套css和一套css in js

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
# pieces 
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
# discuss-stars
- ## Speaking of style recalculations: I’d strongly suggest migrating to Linaria
- https://twitter.com/iamakulov/status/1430106459983945730
- Here’s a pattern I see a lot:
  — the app has an `<Input>` that opens an `<Autocomplete>` on keypress
  — the first time the `<Autocomplete>` mounts, styled-components adds it styles to DOM
  — that causes the browser to spend 100-200 ms recalculating the page styles. Whoops, slowness!
- I love styled-components. 
  - They are a pleasure to use, they extract Critical CSS, they are (generally) fast.
  - But the way s-c work leads to frequent 100+ ms style recalcs. And you can’t control them – they happen all around the place. Which is bad if you care about input latency.

- ## Has anyone had to deal with styles being mixed up in prod with Next & Styled Components?
- https://twitter.com/mattgperry/status/1420257223155060736
- yeah. i think disabling minification of classnames solved the issue for me
- Yep, I couldn't wrap my head around it and ended up switching to SCSS.
  - Yeah it's weird. Dev is fine, SSR is fine, and then hydration happens and it all explodes. Even seems to happen on random deploys
  - Same thing happened to me when mixing scss+tailwind. Dev was fine but build would break.

- ## Super happy that someone dug into real life css-in-js performance. 
- https://twitter.com/Vjeux/status/1402352889469673473
  - In theory, css-in-js should be faster because we remove all the rule selection part of css, but that doesn't seem to be realized in this case.
- Many CSS-in-JS libraries do not compile to stylesheets at build time. The main reason is that this would be very difficult to do statically while still allowing styles to be assembled using arbitrary JS, depend on runtime props, etc.
- I think most of styles css-in-js build is static, is it possible only dynamically assigned style resources  to be built in runtime?
  - It's not simple, one big problem is that you can't change the order of rules, or it might break things. So somehow the static extraction part needs to make sure that the order stays the same with dynamic styles, which won't be possible, or determine what's safe to extract.
  - It's not just rules, sometimes we use multiple classes on same element, and for that to work properly, the order of the styles needs to be the same in the output. It can be very complex to do with combination of both dynamic and static styles, I'm not even sure if it's possible.
- **Libraries like a Linaria extract everything to static styles, so the order is always preserved**. Dynamic styles are applied using CSS custom properties. But this approach has limitations, you can only have dynamic values for style properties, not whole rulesets.
  - It's also not simple, to make sure that everything static can be extracted, Linaria needs to evaluate the JavaScript in a VM so that you can have actual logic in JavaScript, import values from other files etc. It also needs to make sure to evaluate as little as needed for perf.
  - Of course there are other simpler approaches, but the simpler the approach, the more limitations you'll have on what you can do in the styles.
- I've had a similar experience. This is why a really important part of jsxstyle was the webpack plugin to extract static css files and remove the runtime.

- [Real-world CSS vs. CSS-in-JS performance comparison](https://pustelto.com/blog/css-vs-css-in-js-perf/)
- tldr: Don’t use runtime CSS-in-JS if you care about the load performance of your site. 
  - Simply less JS = Faster Site. 
  - There isn’t much we can do about it. 
- Run test:
  - Network (size of the JS and CSS assets, coverage, number of requests)
  - Lighthouse audits (performance audit with mobile preset).
  - Performance profiling (tests for page load, one for drag and drop interaction)
- Conclusion
  - As you can see runtime CSS-in-JS can have a noticeable impact on your webpage.
  - I think build-time CSS-in-JS libs will be the next big thing in the CSS ecosystem 

- ## [Why Don’t I Sell the Idea of Static Extraction with CSS-in-JS?](https://medium.com/@tkh44/why-dont-i-sell-the-idea-of-static-extraction-with-css-in-js-df21f571503b)

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

- ## [survey: styled-components vs SASS vs CSS, which one would win!](https://twitter.com/Ipenywis/status/1275091218905608192)
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

- ## [Why write CSS-in-JS when vanilla CSS is just fine? ](https://twitter.com/saltnburnem/status/1290690315540717568)
  - The styling of a component is very linked to it's structure, so put them together.
  - The main element of reuse is the component. You won't ever need a .header CSS class when instead you'll reuse `<Header>`

- ## is possible to compile styled-components at build time in nextjs? 
- https://twitter.com/gipsterya/status/1381391459723530243
- As far as I know, styled-components requires runtime JS. 
  - You might consider another CSS-in-JS solution with zero runtime.
- I used styled-components, but switched to emotion because it does ssr without configuration. 
  - Then I switched to linaria, it drops 6kb from bundle and no runtime. 
  - Going forward I'll explore linaria+tailwind. 
  - I think tailwind will be a more powerful now because its jit compiler.
# survey: css in js vs css
- ## [are there any cons to using regular CSS vs CSS-in-JS?_2018](https://twitter.com/ka11away/status/1014990019801411586)
- css: css-in-js = 0.557: 0.443 /79votes
- It’s depends on ur purposes. 
  - If u use dynamic generated styles (in runtime) a lot — css-in-js (styled-components) is a nice choice. 
  - If not, better use static css-in-js approach (emotion + extract, css-literal-loader) or classic
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Working with vanilla-extract and treat for the last few years has me thinking compile time execution of code is a pretty unexplored space
- https://twitter.com/mattcompiles/status/1422535524535869442
  - We originally set out to see how powerful a CSS-in-JS library could be with zero runtime. 
  - But we ended up creating an excellent compile time execution system that happens to generate CSS.
- AST transforms have traditionally solved these kinds of issues, but you can never really guarantee they work in all situations.
  - Also you can't debug them when they don't work as expected. I don't to want to fallback to slow mode because I wrote some "edge-case" code.
- **Having a custom file extension is probably vanilla-extract's most common criticism**. 
  - However, I actually think it's one of its best features. 
  - A clear runtime/compile-time boundary that seamlessly fits into your codebase. 
  - React server-components are using a very similar idea.

- ## NEW ATOMIC CSS FRAMEWORK: Sprinkles
- https://twitter.com/markdalgleish/status/1387293525256007682
  - Zero-runtime CSS-in-TS
  - Compose atoms at build time — or at runtime
  - Type-safe functional API to access atoms
  - Configure properties, values, shorthands + conditions
  - Themed atoms via CSS Variables
- What's especially cool here is that Sprinkles is just leveraging the power of vanilla-extract. Anyone could write this library. You don't need to wait for us to put new abstractions into the core library—you can come up with your own.
- The idea is that 80% of your styles are the same over and over. Sprinkles solves this issue. Then compose the atoms up with the more specific stuff. That's how we architect braid.
  - Also sprinkles generates highly cacheable and compression friendly styles which mitigates the size issue.

- ## the initial version of @stitchesjs was based on atomic CSS. Lots of specificity issues to look out for
- https://twitter.com/giuseppegurgone/status/1385926007283138561
- What's the problem you saw with atomic and specificity? I am assuming one never has to "override" a property with a rule and each property-value combination exists only once. I am sure I am forgetting something...
  - You need to sort pseudo classes and at rules in a particular order otherwise the result would be non deterministic and depending on which component uses a declaration first. Of course this is not an issue if state is managed with JS and styles are just fn(state)
- So in case of a media query an atomic rule for the same property can be global and as a media child. If one uses both classes, specificity algorithm is involved. Is that the case you are talking about? When would one have both classes applied to one element?
  - If you have global styles then chances is that they are going to mess with yours - this is the case with any CSS in JS library.
  - If you have two classes one for the plan declaration and the other with a media query you need to sort them because the @media rule doesn't have any impact on specificity

- Is critical CSS even such a problem? I realize that loading all atomic classes like tailwind can lead to some delays but in a real life there much less such classes so why even care about extraction? @markdalgleish any comparison of your lib to tailwind?
- imo critical CSS extraction is not necessary when using a solution that produces atomic CSS classes. In tailwind it is (was?) necessary because you’d start from a bundle with the entire universe in it. With JIT compilation this shouldn’t be a problem
- Critical CSS optimizes initial paint for empty cache user by removing the need to wait for a blocking css request. It has nothing to do with atomic, cssinjs, static or client-side. Not everybody needs to have this optimized.

- ### Almost any CSS ordering suffer from code splitting, and almost nobody talking about it
- I was having a play with this in @compiledcss , where I'd move all "unsafe" styles to the primary chunk, but then leave everything else alone. Seems to work ok.
- yeah, also css-modules has the same problem, there was an issue like 10 years ago
  - Yes CSS Modules suffer from this issue as well: it happens when you import from multiple (shared) modules or pass scoped classnames as props.
- Well, this is not about CSS Modules, but a very nature of CSS and the bundling process. 
  - MiniCSSPlugin actually detects and reports some of such “race conditions”, (mostly false positives) but not able to solve.
  - indeed. CSS Modules additionally gives you that false sense confidence - people think that since styles are scoped they are good. I think that with some strict linter rules the issue I mentioned can be avoided
# ref
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
