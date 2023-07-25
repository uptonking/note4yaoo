---
title: web-style-css-in-js-lib-vanilla-extract-sprinkles
tags: [css-in-js, vanilla-extract]
created: 2021-08-22T16:07:00.096Z
modified: 2021-08-22T16:08:42.552Z
---

# web-style-css-in-js-lib-vanilla-extract-sprinkles

# guide

- 如何去掉未使用的类名，或放心删除未使用的类名
  - 可以间接通过ide的find references找引用的方式，去掉未被引用过的类名

- compiled-css-in-js会编译出atomic css
# examples
- online
  - https://codesandbox.io/s/vanilla-extract-esbuild-9h490m

- https://github.com/one-aalam/awesome-vanilla-extract-css
  - Early Adopters: shopify
- https://github.com/markdalgleish/nextjs-vanilla-extract-example
  - 官方示例，仅单文件

- https://github.com/samuelkraft/design-system
  - WIP design system starter repo.
  - Design system
    - Styling with Vanilla Extract (can easily be changed)
    - Theming with next-themes
  - Docs site
    - Powered by MDX (with contentlayer)
    - Live editable code
  - Playground
    - TBA
- https://github.com/huijiewei/agile-ui
  - http://agile-ui.vercel.app/
  - React + TypeScript + Tailwind CSS Components
- https://github.com/timoclsn/mauli-vanilla-extract
  - https://mauli-vanilla-extract.vercel.app/
  - Experimental design system exploration with React and Vanilla Extract.
- https://github.com/whoisryosuke/gelato-ui
  - React component library and design system powered by Vanilla Extract

- https://github.com/copiest/fronttigger-blog
  - [next.js + vanilla-extract + mdx] fronttigger's blog
  - 依赖 recoil、mdx-bundler

- https://github.com/lukin/vanilla-reset
  - A tiny modern CSS reset for vanilla-extract.

## eg-csb

- official-examples
  - https://codesandbox.io/s/github/seek-oss/vanilla-extract/tree/master/examples/webpack-react

- https://codesandbox.io/s/radix-ui-with-vanilla-extract-rnl9d

## utils

- https://github.com/TheMightyPenguin/dessert-box
  - An utility to create a Box component from your vanilla-extract + sprinkles tokens.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## Provide a way to prune unused css?
- https://github.com/seek-oss/vanilla-extract/discussions/91
  - 可以间接通过ide的find references找引用的方式，去掉未被引用过的类名

- ## I missed this React discussion from 2021. Looks like they're officially recommending moving away from runtime CSS-in-JS towards static extraction
- https://twitter.com/markdalgleish/status/1528948996706025472
  - vanilla-extract isn't the only library doing this, but it's great to see our direction being validated.

- I have been against css in js from day 0. Since we were putting work of html already in js and with css in js we had put all work in js bucket leaving css to wait for js to execute first. AFAIK css and js parsing can happen in parallel which was not leveraged in css in js.

- Is there any plans to add nesting? The only downside I  see with vanilla-extract is it's pretty verbose. It takes a lot longer to style elements.
  - Maybe he means targeting other descendant elements?

- what's the possibility vanilla extract gets static extraction without requiring the styles to be isolated in a separate file
  - It's something we've debated a lot amongst ourselves, but we find **we prefer the explicit boundary between the two execution environments**—similar to the way Server Components are handled.
- yeah that's fair I just really enjoy the Stitches API since where the style definition and component definition is one step
- pretty similar on how css modules are being handled in a lot of frameworks, right? `<Component>.module.css`

- does vanilla-extract give you a stylesheet you can `<link ... />` to? i was told it didn't?
  - Yep! It’s a build tool that takes all your .css.ts files and generates a stylesheet. Basically like Sass or CSS Modules except that you author the styles in TypeScript!

- ##  `background-color: var(--colors-brand);` Is this code valid? Is this variable defined anywhere? 
- https://twitter.com/markdalgleish/status/1487393650607034373
  - Unless you look at every other CSS file in your project, there's no way to know.
  - This is what we're addressing when we talk about "type safety" for CSS variables in vanilla-extract.
  - With vanilla-extract, you must explicitly import vars to use them, making your CSS much more traceable. 
  - You can also define entire theme types to validate that all required vars are defined.
  - This kind of structural type checking is something we take for granted when working with TypeScript, and vanilla-extract brings this to static CSS.

- I can’t imagine working with an untyped theme ever again! I would like to use Vanilla Extract - but the randomized CSS variable names makes themes difficult to reuse across technologies, like styling third party widgets, cookie banners and such
  - There's a global theming API to deal with this
- How can your typing tell if the call-site is in the context of the provider though? Say you have multiple providers in an app with competing, overlapping, and extra vars, how do you type hint to the developer? Actually had a working session on Friday about this problem.
  - Can't type that part, unfortunately.

- ## First look at Vanilla Extract
- https://twitter.com/kylemathews/status/1382212439538761732?lang=en
- Does Vanilla Extract support to react-native?
  - No, it's specifically designed to target CSS.

- ## Are CSS Modules or Vanilla Extract suitable for a reusable component library?
- https://twitter.com/housecor/status/1429043686478909443
  - My concern: It would be difficult to override the styles as a consumer, right? (since generated classname hash may change if the parent DOM elements change)
- If you're trying to create an opinionated look and feel I would try and avoid class overrides all together. It removes your ability to make changes to the library as everything is now public API. Props and CSS variables make a much better API in my experience
  - With vanilla-extract specifically, the hashes are based on the .css.ts file location and the order of styles within it. DOM structure doesn't affect it.
-  In my experience, allowing style overrides removes your control as a maintainer. 
   - If you want style overrides, then copying the source code is often a better long term option as the consumer is taking ownership of the change.
   - Guess I see similar to create react app having the eject command. If you want to change the core system then you need to own it.
- Absolutely. You can still allow style overrides if desired, but you have to make an explicit API for it. 
  - I think this is a huge improvement over traditional CSS overrides—especially when you factor in static type checking—since it leads to a much stronger contract.
- Yup, primitive unstyled components that only handle logic, then style with any methodology you want, even plain old CSS. See @radix_ui
- I am building opinionated, styled components that implement the company design system. I'm currently just using BEM with Sass so consumers can easily override (because the class names are static and follow a clear convention)
  - In this particular case, I think @mattcompiles has the right approach -- it's appropriate to restrict style overrides. One additional reason this might be a good choice is that you want to encourage developers to raise inconsistencies up to the DS maintainers.
- Those tools encourage a closed design system where you customise the component with high level props and css variables.
  - If you wanna give some more control to consumer you can take `className` props for specific Dom nodes and merge it with internal classes.
  - One additional could be that you expose Base components which allows lot of overrides using above techniques. But then make variant components on top of it which only allow customisation via high level props. If consumer can't get something done with variant, they can copy it
- One way to do this is have your primitives be unstyled and use `data` attributes as selectors. Another could be an override API like Material UI.
