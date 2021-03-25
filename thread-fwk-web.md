---
title: thread-fwk-web
tags: [framework, frontend, thread, web]
created: '2020-12-05T17:52:28.808Z'
modified: '2021-01-08T17:13:53.965Z'
---

# thread-fwk-web

# pieces

- ## 


- ## I wonder how many people realize that React Hooks is really just disconnected, less declarative reactive programming.
- https://twitter.com/BenLesh/status/1374755992378953730
- Comments immediately go towards RxJS (Streams) but hooks syntactically more resemble MobX (Signals/Behaviors). In that light this description is dead on. I'd go as far as saying almost all JS UI Frameworks land here to anyone wanting to beat that tired React isn't reactive drum.
- This relationship is muddled in my mind because AFAICT most reactive frameworks put _events_ and _time_ as front-and-center concepts, and Hooks seems more about dataflow - which feels extremely related to event systems, often implemented via events, but don't quite seem the same.
- Now, I am confused. Are hooks good or bad? This really got me thinking because I am having horrible time in build meaningful observable abstractions with hooks.
  - I think they were a step in the right direction and there was reason to be excited about that. But there are caveats and a lot of people have been bitten by them. Hooks are essentially limited reactivity. The reactive part is awesome, but the limitations aren’t.
- RxJS makes react much cleaner imho. In fact, imho RxJS (the reactive paradigm, really) makes working in an event driven env like the frontend of web apps much easier after the initial learning curve, results in much cleaner code, and encourages better data como/flow
  - RxJS was absolutely the worst thing I ever had to maintain.


- ## To make nostalgie.dev's SSR pipeline extensible, I've been trying to figure out how to give plugins the ability to customize the wrapper markup.
- https://twitter.com/filearts/status/1374342826318761992
  - "Why not give them a mutable HTML AST?", I thought. Then I wondered if npm.im/linkedom would be fast enough
  - Plugins will get a per-request, high-fidelity HTMLDocument instance that can be modified in an idiomatic way before being stringified and served.
- If you think about doing SSR, the patterns for rendering the app itself are pretty solid; you call your framework's renderToString() equivalent and dump it in #root of your html template.
  - But what if Plugins want to customize that html template in a _general_ way?

- ## Anyone know if Angular, Ember, or Svelte have a hooks or composition type API?
- https://twitter.com/justinfagnani/status/1372967430025142272
  - Looking to enable reusable, stateful, reactive units of code across frameworks.
- We're working on a decorators/class based API for providing the same reactive composition that hooks provides. 
  - I would say the result ends up being a bit less granular, but a bit more clear IMO

- ## Very good picture, it's from @MarkoDevTeam , explaining streaming SSR.
- https://twitter.com/dogetoge/status/1372440505200504833
- I love this visual. I used to try to explain this with Chrome timelines. @mlrawlings nailed it with this one.

- ## I’ve been talking lately how Vercel isn’t good for fullstack, but wow do I love the simplicity of their api/folder with regular node req/res handlers.
- https://twitter.com/flybayer/status/1372007899418013697
  - So much nicer and more portable than the lambda event api
- server codesharing DX. The lack of an arbitrarily nestable way to share layout was too painful so I use React Router and client-side render everything. It's been great.

- ## Event bubbling causes so many problems. It breaks component encapsulation. Events shouldn't leak out of a component just like styles shouldn't.
- https://twitter.com/devongovett/status/1371549410245640195
  - When you handle an event in a component, you should usually stop propagation so parent components don't also try to handle it.
  - example: you could have row selection in a table. Clicking anywhere on the row selects it, but if you had a button inside a cell, you would want the button to handle this event rather than selecting the row.
- In React Aria we treat this as a general rule. 
  - All of our interaction hooks stop propagation on all events once they've been handled. 
  - This means application developers don't need to worry about these problems and in general things work as expected out of the box.
  - Obviously there are cases where bubbling is useful, but often times these can also be handled by using capture phase listeners instead. 
  - We also support a `continuePropagation` method on some events that allows opting into propagation rather than opting out.
- We had to add this for Headless UI, because while I was working on an example with a Menu inside a Modal, guess what happened when you pressed "escape" 
- What if you want to extend a behavior ? If your event isn't bubbling you can't do it
  - Usually there are better ways to do this. For example adding an event handler on the element you want to handle events for rather than a parent. But of course there's always capturing events you can use too.
- Agree. I like the concept of custom events in @vuejs -  they propagate only one level up. 
  - Hence you don't have such a problem there at least with custom events. 
  - On the other hand, for native events, Vue has a nice syntaxis to stop event propagation
- So much code (and people's mental models) assumes that events will bubble, that I've found this can lead to subtle, hard to find/debug problems. I use it sparingly and deliberately, but not universally for the above reason.
- I've been toying with an Overrides pattern that allows controlled bubbling. Still need to experiment more, but the idea was you could always stopPropagation and then use overrides where needed.

- ## Angular 的 NgModule 是为了解决什么问题？
- https://www.zhihu.com/question/376817427
- 像命名空间一样提供一种方式支持组件之间的引用。这个可以对比vue和react。
  - vue没有提供类似的功能，所以组件要么是全局注册的，要么就得给每个组件单独声明依赖（也就是对应组件的components和directives成员）。
  - react则与js原声处理依赖的方式一致，非常的简单也可以说是精妙。
  - angular的依赖就是以module为单位的，省去给每个组件声明一次依赖的步骤又避免了全局注册带来的代码chunk分割问题。实际上module之间的引用还是要手动声明的。
- 为依赖注入独立出了一条"查找路径"。
  - 因为组件本身也是有注入器的，组件注入器之间也有层级关系，当前注入器找不到会再去父注入器递归的查找。
  - 所以这里就有了一个策略，我没必要去每次都走一遍组件注入器树，我先通过某种方法判断我要的服务在不在组件注入器树里，不在就直接找module注入器树。这就是angular的nodeinjector引入bloom filter的原因。
- 并不是必须用module才能达到目的，只是angular选择了这样的设计。即使angular没有module的概念，也可以采取类似的策略：组件注入器树找不到就直接找一个全局的顶级的注入器。
  - 这点也可以对比下vue和react是怎么处理全局依赖的。
  - vue有的是直接附着在了全局Vue对象上(如vue.router$)，也有采取js全局变量的。
  - react就不用说了，js怎么做react就怎么做。
  - 相比之下angular确实是要规范不少，不止是在代码上有更多约束，结构设计上也是有一定规划的。

- ## Idea: a Next.js plugin that takes typed `api/` routes and codegens React hooks (with SWR / react-query) for reads/writes
- https://twitter.com/rauchg/status/1368283797280550912
  - Never deal with `fetch` and `res.ok` and `body` and `.json()` and AbortControllers ever again in your life
- I think @blitz_js is doing something like that
  - Yep! Plus tons of other awesome features and conventions that make you super productive for building fullstack apps
- Tougher than it sounds. Codegen thrives when it can target a static schema-style language (like GraphQL). Any codegen that targets actual code will need to either actually run that code (horrible side effects possible) or enforce conventions on that code.

- ## If we let go of the dream of running @blitz_js solely on lambdas, then we can fully embrace websockets and bake awesome real-time features into Blitz.
- https://twitter.com/flybayer/status/1370463255429275654
  - Serverless is AWESOME for queues and background processing, but less awesome for user facing requests.
- If we were to support websockets, we could also use websockets as transport layer for the RPC calls. Something like the deepkit framework by @MarcJSchmidt is using. This would also allow us to do streaming of data (think pagination, etc.)
- I say drop it. I think most people who praise serverless with Next are people who host on Vercel because they develop purely in monolith app style, but Vercel takes over on deployment and makes it serverless.
  - I personally don’t see Blitz as the type of app I’d deploy to Vercel either. Databases are an important aspect of the Blitz model, Vercel tells you to use a 3rd party service that adds latency to that.
  - Yeah I’m no longer recommending people to deploy to Vercel for these reasons. As they say, it’s for “frontend” apps
- You can use lambdas with websockets
  - Conceptually, how is that possible? Aren't Lambda's stateless? Isn't a web socket by definition a persistent http connection?
  - You can connect to lambda via socket a couple different ways. API gateway sockets, Appsync sockets, or older school MQTT sockets APIgateway/appsync are most common today

- ## Svelte Kit is now open source
- https://twitter.com/SvelteSociety/status/1370157702144348164
  - https://github.com/sveltejs/kit
- Q: What's the big deal about SvelteKit? 
  - A: The official recommended way to build apps with @Sveltejs . 
  - Superfast development with @vite_js , deployed with static or serverless adapters.

- ## Web platform support: Flutter or ReactNative? TLDR: React-Native for websites, Flutter for web-apps
- https://twitter.com/sebastienlorber/status/1367424075619049474
- Flutter 2 web has 2 possible backends:
  - HTML renderer: using web-components for better compatibility
  - CanvasKit: WebGL + canvas for performant apps but adds 2mb of size
  - In practice, it seems that all the major demos are using CanvasKit (> 10mb)
- Flutter Plasma is a cool Flutter demo.
  - It seems based on CanvasKit and seems like nice use-case for Flutter web.
  - However it downloads 12mb to show the first frame, so you'd rather have a good connexion.
- Flutter Folio looks more like a real-world business/consumer app.
  - But right from the login screen, you can feel it is not the native web platform. 
  - Also > 10mb
- Rive looks like the most interesting one.
  - It seems able to embed a very interactive canvas in existing pages in a lightweight way (like Lottie?).
  - The homepage is 3mb and impressive.
  - However, it's using React and NextJS from @vercel , not Flutter
- Flutter web is progressing:
  - a11y
  - password autofill
  - SPA
  - PWA
  - ...
- However, to succeed for content-centric websites, it also needs:
  - lightweight, code splitting
  - Jamstack, pre-rendering, SSR
  - SEO
  - ...
  - Very hard things to handle for CanvasKit
- Once the flutter.dev and rive.app landing pages are implemented in Flutter, it could be a huge success.
  - But it's not the case today, for good reasons, and I think this will be hard to achieve in the short term.
- In comparison, React-Native is a good fit to implement such landing pages.
  - The Twitter UI you read this thread on is based on React-Native-Web for years now. Many companies use this already in production.
- React-Native-Web:
  - Renders regular accessible HTML elements using React and atomic CSS-in-JS in a performant way
  - Is compatible with the existing frontend tooling (Webpack, code splitting...)
  - Is compatible with the Jamstack, SEO, server-side-rendering (Gatsby, NextJS...)
- React-Native does not hide platform differences, does not try to produce a single uniform UI result by default, but uses the target platform primitives.
  - It can require more work than Flutter, but can be worth it, particularly for websites.
  - React-Native is full of escape hatches.
  - You can basically add Flutter widgets, canvas, WebGL or whatever vanilla JS or JQuery in the middle of a React-Native-Web app without any friction.
- For critical interactive things, you can get as close to the platform as you need to be.
  - For simpler things, you can share 99% of the code.
- I still think Flutter is a very good solution for many use-cases, and show good progress to tackle some a11y concerns
  - But it is still far away from building the kind of websites that React-Native can build today.
- I would rather use :
  - Flutter for UI intensive web-apps that can download 10mb upfront
  - React-Native for content-centric websites
  - I believe React-Native is a less risky choice for the web, but it might require a bit more work.
- Why not just plain React and ionic @capacitorjs , possibly even with Next.js? 
  - Next.js + @capacitorjs for web, mobile, desktop, etc. would be a winning combo and we're seeing a lot of interest in that lately.
  - In the end we want a native app, not a WebView in a mobile/desktop shell. It definitively can improve but I don't think today WebView has the same level of experience as being close to the platform
  - You're certainly entitled to that view! Pointing out it's a valid option that has been resonating with React devs. Especially if you want true web platform support and the standard react dev experience and compatibility with all the React libs used today
  - I want true web platform support AND true mobile platform support AND true desktop platform support, which RN brings to the table.
  - Using the web everywhere has its advantages but also its limits, until WebViews become as good as native

- ## Flutter 2 announced last week to show off the cross platform power.
- https://twitter.com/kudochien/status/1369491495892316160
  - However, for the web support, since it's based on skia. It should be difficult to use SSR or prerender for SEO.
  - For embedded Linux, we also has an ongoing plan by react-native-skia.
  - By react-native-skia, we could extend react-native to other platforms like Flutter.
  - Although I didn't have much time on this project, but people from NAGRA OpenTV invested a lot.

- ## favorite coding trend lately: removing the code needed to connect frontend to backend (api calls)
- https://twitter.com/chris__sev/status/1368283798518050830
  - [blitz.js](https://github.com/blitz-js/blitz)
  - [inertia.js](https://github.com/inertiajs/inertia)
  - [livewire](https://github.com/livewire/livewire)
  - [Alpine](https://github.com/alpinejs/alpine)

- ## Hot @angular take: "core" and "shared" modules are bad practices
- https://twitter.com/gc_psk/status/1368143538853191681
  - I dislike core and shared modules used in multiple places. Adds too much overlapping and leads to bloated bundles.
- I use "core" to free all imports that should have been declared in app module because I want app module to be as simple as possible. Never use "shared".
- Never was a fan of core module... App module is core module already. Shared is a nice place to put things which are used in most other modules
  - The problem I see with SharedModule is that often you end up with lots of unused modules just for the convenience of using a few.
  - I mean the giant ones with just about everything (99% out there)
  - Smaller, local shared modules of things that are used often in combination are OK

- ## Why does it take GTA online so long to to load? Great investigation, and the answer is… a JSON parser??
- https://twitter.com/jaffathecake/status/1366275005185728512
  - [How I cut GTA Online loading times by 70%](https://nee.lv/2021/02/28/How-I-cut-GTA-Online-loading-times-by-70/)
- I can imagine how this happened; 'simple' task given to a junior team member, and 7 years ago the list of items was a lot smaller than 10MB. Too busy to be reviewed properly as it 'works'.

- ## JSX Lite is now the first and only framework you can edit visually right in your IDE 
- https://twitter.com/Steve8708/status/1365356598441308162
- At Vaadin we are working on something similar for those who prefer lit-html tagged literals to JSX.
- I think the coolest thing about JSX here is using it to map to compiled frameworks as well. 
  - Like there are Svelte and Solid outputs. 
  - One of the challenge I've seen with tagged template literals (and I do have a version for Solid) is that you can't bury the reactivity easily.
  - I'm stoked how JSX-Lite looked at common templating patterns--I'm biased since it basically reflects Solid's API--came up with something that should work regardless of top-down, reactive, or fine-grained rendering paradigms. As someone constantly fighting tooling it is refreshing
- Solid's API was such a huge unlock and inspiration for JSX Lite, and the highest performing output target! 
  - Solid is such an amazing project on so many levels everyone should check out

- ## Replace Type Component with Subcomponents. Tip: replace ReactNode by ComponentType
- https://twitter.com/sebastienlorber/status/1363891104194699269
  - Describe a pattern I often use in React, where you have some kind of "router" component that dispatch to subcomponents by reading a "configuration map".
- [Replace Type Component with Subcomponents](https://altrim.io/posts/replace-type-component-with-subcomponents)
  - At this point it was time to refactor the component and clean up the code so that even if we add additional themes in future we won't have to deal with all the conditionals and specific function behaviors depending on the theme type.
  - For the refactoring I thought to use a similar technique to Replace Type Code with Subclasses. 
  - The idea with this technique is to remove the type from the main class and replace it with specific type sub classes.

``` JSX
// Refactor this 👇
<InvoiceDetails invoice={invoice} theme={Theme.Simple} />
<InvoiceDetails invoice={invoice} theme={Theme.Modern} />
<InvoiceDetails invoice={invoice} theme={Theme.Classic} />

// Into this 👇
const Details: Record<Theme, ReactNode> = {
  [Theme.Simple]: <SimpleTheme invoice={invoice} />,
  [Theme.Modern]: <ModernTheme invoice={invoice} />,
  [Theme.Classic]: <ClassicTheme invoice={invoice} />,
};

```

- ## What is your favorite web server port?
- https://twitter.com/jbrancha/status/1363155210521243649
- 8000 of course, python -m http.server
- Parcel’s 1234 always appealed to me.
- also like Redwood's :8910

- ## More and more I’m realizing that there are two very different ideas of the web. 
- https://twitter.com/devongovett/status/1363194220635426817
  - One group thinks the web is for content sites, marketing pages, and mainly server rendered apps. 
  - The other is trying to build native-like apps using web technology.
  - The first group cares way more about loading performance, bundle sizes, server side rendering, progressive enhancement, etc.
  - The other group cares more about rich interactivity, keyboard navigation, touch gestures, rendering performance, animations, offline support, etc
  - One group wants to get rid of all build tooling and load their source code directly in the browser.
  - The other embraces build tools for the DX and UX benefits they provide, and capabilities they enable. (Seriously, do you know how much better web tooling is than native?)
  - This is the source of many disagreements on this website. It comes from each group seeing everything only from one perspective.
  - In reality, both are equally valid, and in fact there is often a great deal of overlap. The web is for all types of apps, not just one or the other!
  - Your priorities should change from project to project. Are new users constantly coming to your site for a short time? 
  - Maybe loading perf is your top priority. Do users keep your app open all day? Maybe great interactions at the cost of bundle size is the right trade off.
  - Of course, we should always aim for all of the above, but it’s not always possible to achieve. 
  - There are always trade offs. That’s why they are priorities, not exclusive.
  - You should prioritize what’s most important for *your* users. Everything else is secondary. 
- And here is my dumb self trying to do both at the same time.
- that's why I am a supporter of creating:
  - Document context (light browser view for content - this is what Google is trying to do with AMP)
  - Application context (there are many things here, it treats the screen window as a canvas, we can mess things up and create a new API which is exactly to the benefit of building web applications)
  - Legacy Context (the current browser, which we will give up in 10 years, downgrading websites to the document model or upgrading them to the application model)

- ## [I was impressed by @pmndrs valtio, so I decided to figure out how to implement a proxy state like valtio, using valtio's test cases.](https://twitter.com/lihautan/status/1361481299970592770)
  - Tips on get a deeper understanding of the library you are using
  - Try implement the library based on the public API and test cases, figure out how it might be implemented.
  - Peek into the source code if you are stucked.
  - https://www.youtube.com/watch?v=uZnO2G8pqn0
  - It's very interesting to see someone like you got interested in the vanilla version. I heard someone else is using it in vanilla. I had no idea if it's useful in vanilla when I started, as its goal was to implement an API that is compatible with React's useMutableSource.

- ## Running web apps from archives (think cross-platform executables) would be an important complement to hosted PWAs.
- https://twitter.com/rauschma/status/1362440337705365504 
  - Does anyone know why there is so little progress in this area (AFAICT)?
  - https://github.com/WICG/webpackage 
  - Web packaging format
- I think a big problem is the origin of a bundle: it's not HTTP, and it doesn't have a domain. 
  - That breaks a lot of assumptions about security and privacy on the web. 
  - Still would be interested in seeing this developed though.
- [Dynamic bundle serving with WebBundles](https://docs.google.com/document/d/11t4Ix2bvF1_ZCV9HKfafGfWu82zbOD7aUhZ_FyDAgmA/edit#)

- ## When you set an `id` to an HTML element it... becomes a global JavaScript variable referencing that element
- https://twitter.com/stackblitz/status/1359525093601382406
  - Beware of relying on globals!
- always name your id with - in between，example layout-version
- Global variables should not be here. They should be in a seperated js file that is used as global. And also not in any dom element.

- ## creating framework-agnostic components with @stitchesjs core
- https://twitter.com/peduarte/status/1358125279303065602
- Im so happy with this API so far. One thing is spec'ing it and the other is actually using it.
- Love it! Hear me out, I'm not drunk. Variants look like state machines 
  - Now you can create finite css styles with #xstate
  - Would be cool to have stitches dev tools to visualise components variants like that 
  - Question: Are there any limitations for variants? Obviously, I can't put variants inside variants. But besides that, is there anything else? Can I use pseudo selectors, media queries etc.?
  - No limitations like that apart from obvious stuff like you mentioned
  - The cool thing about variants is that they can be “immutable”, meaning instead of changing its styles on different conditions (breakpoints), they can be *applied conditionally*
- Framework-agnostic in 2019: React, Vue, Angular
  - Framework-agnostic in 2021: different flavors of React
  - stitches supports svelte too.

- ## The existing history API (window.history, popstate, etc.) is bad for building web apps. We've been working on a proposal for a new history API, and would love your feedback
- https://twitter.com/domenic/status/1356656668222885889
- I think it should be possible to iterate on top of what window.history already provides, and just fix the problems with it instead of introducing something entirely new.

- ## After all these years there really are still only 2 types of frontend JS UI Framework. Angular(React) and KnockoutJS. 
- https://twitter.com/RyanCarniato/status/1356655576420282371
  - Work has gone into optimization, and borrowing the benefits of the other's approach, sometimes producing a hybrid. 
  - The basics haven't changed for nearly a decade.
- Thnx for putting this into words @RyanCarniato - for me as well we've got 2 fundamental patterns:
  - pull: "ask for changes" (Angular, React etc.)
  - push: "tell me that sth changed" (KnockoutJS, Solid, Svelte etc.)
  - There are  toons of hybrids and nuances of course.
  - Still can't decide if "hybrids" trying to add push-based change detection on top of a framework written with a top-down pull mentality (ex. NgRx with Angular) are a good thing or not. 
  - Having a framework designed with a push-based model from the ground-up feels so much "cleaner"
  - Yeah, Vue is another example of this. Their reactive system sits on top of a VDOM. The types of optimizations it does are not unlike Solid or Svelte, but uses them to generate VDOM nodes and then goes diff them.
- 计算机研究的问题，很多都可以总结为经典问题，但具体业务的应用场景需要修改

- ## What are folks using to split their CSS bundles to only load the CSS used by the current page?
- https://twitter.com/rob_dodson/status/1355575341696204801
- is there some system that creates shared chunks for css files? 
  - globally (80%+ pages) shared styles as a file
  - inlined page specific styles above the fold 
  - page specific styles as a file
- MiniCssExtractPlugin seems to work OOTB if you lazyload / import() page JS, though that assumes your pages have JS
  - I use that for all my apps but only lazyload pages in big apps

- ## Does any Node.js serverless function providers optimize cold start time with V8 heap snapshots?
- https://twitter.com/youyuxi/status/1353853045520674817
- Don’t think so, 
  - because node itself doesn’t support v8 snapshotting, even for node’s internals. 
  - There’s some scary blockers still remaining, so unless the clouds figured them out but didn’t tell anyone we’re all waiting for that! Docker snapshots though maybe
- Cloudflare workers are your best bet if you want to minimize cold start (was they don’t have any) but they don’t run Node.js. 
  - They have a custom runtime that’s a thin layer atop v8.
- Cloudflare is closest.

- ## My Monday off has primarily gone towards a Babel/Webpack upgrade on a public sector code-base 
- https://twitter.com/slightlylate/status/1351346159869050880
  - and my prior that all of this is suspect and complexity-for-promotion's sake has never been more strongly reinforced.
- Finally upgraded a legacy react app to webpack v4 over the summer, not fun researching every new plugin and config option.
  - 6 months later I go to spin up a new project and now here’s v5 and everything I thought I knew is a lie
- If your tool comes with a transpiler in the default toolchain, it's a distributed liability whose costs you are externalizing onto unsuspecting teams that probably can't afford it.
  - this is why I think Lit should always have CDN-loadable binaries, whatever else is possible. The common path shouldn't require any of this.
- As a once-and-likely-future vendor of transpilers, I think about this a lot. 
  - The TypeScript's and JSX's of the world are not chained to the back-compat firmaments the way languages and platforms are, 
  - and taking bets on them is something we should _culturally_ discourage.
  - The ethical thing for transpiler vendors to do is to work themselves out of a job; 
  - to find the standard or platform vendor they can influence and get their improvements written into the system such that they can fade away.  
  - It's a dual failure when those bodies don't listen.
- I think Babel has done better than most here. 
  - It's hewing a close line to the spec...the problem is its prevalence, rather than its qualities.
- After almost a decade of using various js frameworks and acquiring transient knowledge that's superseded in a few years by whatever n framework(s), I've come to appreciate the value of learning standardised APIs. 
  - They won't last forever, but they will last much longer.

- ## Maybe you don’t need that SPA
- https://twitter.com/RyanCarniato/status/1334732629808009216
- @_developit's Island Architecture keeps getting brought up as if it's this new thing, despite this being the default in Marko for over 5 years.  Maybe "Island" is just catchier?
- I've seen people talk about this stuff in other frameworks like Vue and Svelte, and theorizing how to do this. 
  - But this takes those approaches already in Marko, and explains how even better partial hydration can be done.
- I think it is also worth tinkering about this problem from a different angle too: 
  - Island Architecture in a way is solving a problem of slow js rendering on the web, what if the rendering thing was 3x faster? 
  - Would it still make sense to invest in IA?
  - You mean in the browser? Really this is mostly initial load consideration. Sans cache, the server can start doing async data fetching earlier than the browser which has to wait for the page to be rendered.
- How does Marko resolve state for the hydrated components?
  - We look at what components have state in them (have classes). 
  - From there we can determine hierarchically which stateless components are never used in a stateful context and not bundle them in the client. 
  - And then push all static data above it to the hydrate call for that island.
- It's been always like that. 
  - People follow the projects based on the hype(促销广告、促销讨论). 
  - If a big company uses technology, everyone just blindly follows that. 
  - No one really notices the other better projects if they do not have enough hype around them.

- ## Which frontend frameworks support UIs that mostly work without JS?
- https://twitter.com/rauschma/status/1274737114794659842
- E.g.: Initially, there is server-rendered HTML that links to other pages. JS is injected into that HTML, but the URLs remain. Benefit: You can open links in new tabs.
- I faintly remember Ember supporting this.
- This has always been th default in preact-cli, 
  - but I'll be th first to admit there's a ton of progressive enhancement we don't do that we could be doing.
  - Preact team has a couple things underway that I think will help shift the status-quo in this area.
- Gatsby is built with the idea that JS enhances the experience, 
  - but Gatsby outputs plain HTML, all the links work. 
  - Many Gatsby sites work with JS disabled. So I think it qualifies
