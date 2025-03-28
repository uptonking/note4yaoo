---
title: thread-fwk-ssr
tags: [framework, ssr, thread]
created: 2021-04-24T08:28:46.667Z
modified: 2021-04-24T08:29:02.272Z
---

# thread-fwk-ssr

# guide

# repeat
- ## Do you use renderToStaticMarkup/renderToStaticNodeStream? 
- https://twitter.com/sebmarkbage/status/1385676708439904264
  - I.e. the form that just renders plain-HTML that can't be hydrated by React. 
  - If so, what do you use it for?
- Transactional email from the server in a user signup/checkout flow. The module already supports JSX because it's a Remix route and is compiled, so can slap out a quick email message with react!
  - Same thing with next JS, and other react server rendered frameworks
- Rendering e-mails on the backend before sending them. Instead of writing plain HTML, I can use @reactjs components to create awesome e-mails filled with complex data and good UI. That's also good because I can use @storybookjs on the backend to have e-mails previews.
  - How are you grabbing the data before rendering?
  - A @reactjs component is a function which expects props. All you have to do is to pass those props, and call that function inside renderToStaticMarkup. The data is in the backend context. It comes from anywhere, databases, APIs etc. Just pass as props
- renderToStaticMarkup to build html that's used for PDF generation
- I used to use it to render the shell of my HTML doc before hydrate() worked on the entire document. But now I just hydrate(el, document)
- Pure SSR that needs no client side code.
- for me
  - Error pages for scenarios severe enough that the app can’t load
  - no script markup to insert in the html page
- Rendering an SVG React element (that is also used elsewhere) to a base64 URL for CSS
- I’m working on an app that’s launched inside a new window (PayPal-like), and the library, provided to consumer, which open that window needs to be as lightweight as possible. So the small UI bits of that library are generated with renderToStaticMarkup
- using JSX as a templating language for emails and pages  that don't need much interactivity. traditional templating languages don't have great IDE support and doing complex rendering logic becomes a mess
- We have some components that are used dynamically on our CMS admin ui (here's what settings you picked will output) and then get rendered served as fragments from the rest service.
- Yes for visualizations that don't need interactivity. This is also done by the Nivo library I think.
  - https://github.com/plouc/nivo
- Notion uses it like this: `contentEditableElement.innerHTML = renderToStaticMarkup(toHtml(richText))`.
- I used it as an alternative to handlebars on some complicated pages in an older express-handlebars app
- No, I use renderToString even in cases where I don’t need hydration (e.g. static website generation without JS runtime)
- We use React to generate a template for PDFs. No need to hydrate!
- We use it to extract formatted data from a grid. The raw data is then used to export to pdf/xlsx.
  - https://github.com/adazzle/react-data-grid/blob/canary/stories/demos/exportUtils.tsx
- passing react components as column templates to a jquery datatable library
# discuss-stars
- ## 

- ## 

 

# discuss-ssr-architecture
- ## 

- ## 

- ## The Laravel team is officially taking over my Inertia.js project. _202502
- https://x.com/reinink/status/1886519391367598359
  - Almost exactly six years ago, I started a project inspired by Turbolinks that let developers using classic server-side frameworks like Laravel and Rails build rich client-side SPAs with libraries like React and Vue. That project became Inertia.js.
  - The goal was simple—I wanted to build apps using the classic monolith architecture while leveraging modern JavaScript frameworks as the templating layer.
  - At the time, there was no standard way to do this. Everyone told me the “right” approach was to turn my server-side app into a REST or GraphQL API and build a separate client-side app to consume it.
  - While that approach makes sense for some projects, it was total overkill for what I was building. I just wanted Laravel, but with React or Vue as my templating layer—yet, that meant adopting an entirely different architecture.
  - Back then, I used Turbolinks a lot to give my apps an SPA feel, but it didn't work well with React or Vue. That's when it hit me: what if I could create something like Turbolinks, but optimized for modern JavaScript frameworks?
  - The two key ideas that made Inertia work so well:
  01. Dynamic components – Modern JavaScript frameworks can dynamically swap one page component for another as you navigate.
  02. Reactivity – These frameworks automatically re-render when props change. So, simply visiting the same page with different data (props) updates it automatically—no manual handling required.
  - With the proof of concept in place, I kept building. We ended up with:
  - ✔️ A core client-side routing library
  - ✔️ Client-side adapters for React, Vue, and Svelte
  - ✔️ Server-side adapters for Laravel, Rails, and many other frameworks (thanks to community contributions)
  - Along this journey I got deeply involved in another project—Tailwind CSS. 
  - Thankfully, my friend Taylor Otwell stepped in. He dedicated Laravel staff to help with GitHub issues and bug fixes, including having Joe Tannenbaum effectively rewrite the entire library for v2.0. 
  - Recently, Taylor and I talked and decided that it was in the best interest of the project for Laravel to take it over officially.

# discuss
- ## 

- ## 

- ## Mark my word - @tan_stack /start  is going to be acquired by @Netlify , he is optimizing it for Netlify and not @Cloudflare worker/page for a reason.
- https://x.com/itspuru/status/1902620517581893852
- TanStack is not for sale, nor is it optimized for any deployment destination over another (this would currently mean Nitro is biased, which it's not) and it never will be.
- Netlify has cut its open-source involvement pretty heavily - Netlify CMS, Gatsby, and Netlify Identity are all dead.

- ## 一个经典问题：做 ssr ， js 在服务端怎么判断移动设备
- https://x.com/YuTengjing/status/1896031013396234611
- 根据 ua 来吧
- 怎么高效优雅拿到 UA 才是问题
  - headers 里面 取就完事了, 但是不同的框架可能做法不一样
- 确实，第一次可以直接根据 user-agent  大致判断是 xs/lg。用户客户端渲染后再在客户端往 cookie 写入准确的屏幕宽度，这样用户第二次访问的时候服务器端就可以准备的判断出 xs/sm/md/lg/xl 了。同理 ab 测试对用户做分组也可以使用在 middleware 中写 cookie，同时，实现 server 端识别用户分组

- ## Vercel 为了推 RSC 把 renderToString 直接就给禁了，还不给选项绕开。这吃相也太难看了吧
- https://x.com/unixzii/status/1893966604846674199
  - 用 import() 动态引入绕过了，希望后面别把这个路也堵了

- ## is there any meta framework that is CSR by default and opt-in SSR?
- https://x.com/hd_nvim/status/1890651898572591314
- Angular but it's not meta

- ## Technically isn’t server side rendering always gonna be more secure than any other approach, such as a rest API?
- https://x.com/webdevcody/status/1880724541837857210
- SSR still sends full data to the client, it’s just in the HTML instead of an XHR response. So the only solution either way is to manually limit the API  response fields or use smth like taint

- Not really. You are getting the same information in an HTML format or JSON format. Doesn't effect data leak vulnerabilities.
  - Both approaches and miles better than anything GraphQL or anything firebase has to offer.

- This question is a category error. cgi-bin had plenty of security issues and you don't get more SSR than that. Same with PHP.

- ## htmx is basically the same idea as the SSR stuff in React/NextJS/Remix of the last ~5 years, which is almost the same as the Rails 4 or 5 turbosomething approach to JS:
- https://x.com/Swizec/status/1868410384350380154
  - You render chunks of HTML on the server and your framework makes Ajax calls to inject these chunks into the page in response to user actions. Like a form submit or a navigation. 
  - The framework then hydrates these chunks so they can be interactive.
  - The reason this works now but didn’t 15 years ago is that you can now deploy those HTML rendering workers in a massively distributed CDN-like compute. This way a user from Australia doesn’t need to wait for ping times with us-west-2. Also frameworks make it nicer than when we tried to do this with jQuery back when Ajax was the new hot.
  - Ultimately the physical distance between your user and the data they’re accessing remains the core bottleneck.

- We have 2 super different use-cases. 
  - Parts of the app are standard multi-page stuff where htmx will be a good fit.
  - Parts of the app are more Figma-like and will need to be very client-side. Might even need wasm

- You can render HTML on an edge node, but for most apps this will be overkill and the actual perceptible delay will be either talking to the database from that edge node.

- ## Twitter(x) 的 web 端也做的很好，首次加载用 SSR 保 SEO、TTI、FCP，之后其他页面 router 用 CSR 保证切换流畅体验，客户端 API Request 减少 SSR 服务开销。
- https://x.com/zhdsuperman/status/1818660691710238878
  - 至今我还不知如何用 nextjs 实现类似体验，怎么做到只有首次加载是 RSC，但是之后切换为 CSR？
- 很简单啊后续的屏幕用layout套一下然后用react query的provider包住的在client side fetch

- ## ⌛️ History strikes back. HTMX, and Hotwire to add dynamic behavior are getting a lot of traction lately. 
- https://twitter.com/simas_ch/status/1768918127008477382
  - Something that Jakarta Faces (JSF) has already had for 15 years! AJAX was introduced in JSF 2.0 in May 2009
- The problem with JSF is that it tried to force a stateful model onto stateless technology in the most brutal way. If Bootstrap came a few years earlier JSF may have never gained traction. JSF has more exotic abstractions while bootstrap augments CSS and HTMX augments HTML.
- for ASP.net Web Forms via Ajax Extensions since 2007.

- ## Unless you have a really good reason to SSR apps behind auth, you're better off using CSR with a separate backend.
- https://twitter.com/ImSh4yy/status/1767608702587097325
- Separate backend is cool (I am even doing it in my current project), but having type safety from back to front is just so nice.

- "first page load" happens dozens of times a day even for internal tools

- ## Are we (Adonisers) the only one building traditional server rendered apps in Node.js?
- https://twitter.com/AmanVirk1/status/1757980175533306277
  - Folks using other frameworks like Fastify, Nest, or even Hono . Are you all building JSON API's?

- SPA and JSON API has been a standard for so long that the majority of devs are downright offended for suggesting traditional server apps.
- Almost every one these days is following Api trend, even if API is not required.
- I like the html first approach but personally find writing jsx easier in terms of composition. There should be a way to create html strings from it during build so it's not that heavy during runtime but I've not spent time finding an existing solution
  - [Use TSX for your template engine](https://adonisjs.com/blog/use-tsx-for-your-template-engine)
- Maybe there’s a dozen using express + ejs

- ## 💡 TLDR: morphing on the server to make smaller HTML payloads doesnt make as much difference as you think and introduces complexity
- https://twitter.com/RogersKonnor/status/1717185649839657168
  - Seems like they came to the same conclusion as the @stimulusreflex team did a few years ago about diffing on the server
  - [37signals Dev — Exploring server-side diffing in Turbo_202310](https://dev.37signals.com/exploring-server-side-diffing-in-turbo/)

- ## Just built another app that will probably never benefit from server components or streaming. 
- https://twitter.com/tannerlinsley/status/1657652038749265920
  - It’s an SPA, behind a login, with zero SEO concerns for users that will never care about or appreciate “It streams, baby” and instead immediately asked about offline support. 
  - It’s all trade offs, it just comes down to knowing what you can trade or not.

- server components 并不是必要的技术，除非 SEO 对于你至关重要。
  - BTW，如果 SEO 对你真的那么重要，推荐花钱投放一些广告，效果更明显。

- 首屏加载很快的话用户体验确实可以优化不少。
  - 有一种很古老的设计叫 application shell，用户体验也很快。

- 看场景。做 marketing 页面用 Server Component or SSG 真的很有必要 否则可以完全不用的

- ## [How single-page application works in SSR (React) - Stack Overflow](https://stackoverflow.com/questions/57243697/how-single-page-application-works-in-ssr-react)
- When implementing Server Side Rendering (SSR), the server knows how to generate a full page with markup so the user gets a fully rendered page and from that moment, when the js resources get downloaded, the application will be live (event listeners will be enabled, the react lifecycle will be active and so on).
01.              Get a request for a specific path
02.              Initiate a new store instance for the request
03.              In case of using react router (or other router solution), fill the state with the requested route
04.              Render the app, but instead of rendering and mounting the App, render the App to string (with renderToString)
05.              Dehydrate the state - take the latest state snapshot and append it to the result (after escaping it and wrapping it with script tag for example)
06.              Return the markup as a response. The markup can look similar to the following: 

```HTML
<html>

<body>
  <App markup />
  <!-- <div appMarkup /> -->
  <script>
    window.state = { state snapshot }
  </script>
</body>

</html>
```

07. The browser gets the html and renders it (before react), so the user already have something on the screen
08. The browser downloads the app bundle
09. The app bundle includes the App that initiate the state with the provided state snapshot (Rehydrate)
10. The App rendered into the DOM, if done correctly, no actual DOM rendering should happen since the result will be the same (app rendered according the same state as it was rendered in the server)
11. From this point the app behaves regular. Any route change doesn't trigger the SSR engine

- There are several frameworks (next.js for example) that comes out of the box with SSR solution along with code splitting according to routes. So when the user change route, a new backend request triggers the SSR flow again for the new route.
- SSR can be implemented in many different variations, but the basic stays the same

- ## [How is server-side rendering compatible with single-page applications? - Stack Overflow](https://stackoverflow.com/questions/66893389/how-is-server-side-rendering-compatible-with-single-page-applications)
- Do SSR SPAs always respond with full prerendered HTML, or only for first page loads?
  - Usually SSR is used for initial rendering of the page, so for the first question - for the first page load

- ## [vuejs3 - Why quassar with ssr mode behave like a SPA - Stack Overflow](https://stackoverflow.com/questions/74889396/why-quassar-with-ssr-mode-behave-like-a-spa)
- This is by design. Quasar is VueJS based, which (unlike e.g. PHP) focuses on delivering pages basically as SPAs, i.e. giving you data + JS to render it.
  - SSR only means that the first page is rendered on the server (e.g. for SEO purposes) and javascript takes over for fetching and rendering all subsequently loaded pages (or better the data + a recipe to render them) on the client. Thus, SSR will only get you server-side rendered pages upon initial load or page reload, all other renders are client-side.

- It is the same with NuxtJS, since it builds on VueJS and is in a sense just a higher order abstraction layer/framework that facilitates some common things that one frequently encounters when dealing with Vue. So take NuxtJS and Quasar like wrappers with a lot helper structures around VueJS. NuxtJS provides options to deploy the page via SSG as well

- ## The reason client rendering is still popular is that it is so much simpler than SSR. 
- https://twitter.com/devongovett/status/1648680262400704517
  - SSR can be a huge pain — dealing with hydration, environment differences, effects not running on the server, etc. 
  - For some apps, the DX of CSR outweighs the marginal UX benefits of SSR.
- Frameworks have simplified SSR a lot and I hope they continue to do so. But a lot of what’s hard is dealing with differences between the browser environment and the server environment. Missing APIs, different behavior, etc. It needs to be completely transparent.
  - My theory is that the simplest DX usually wins, even at the expense of UX (to a point). We see this play out over and over. If we want to make SSR the default choice for everyone, the best way to do that is to make it even easier than CSR. Eventually I think it’ll happen.

- At the startup I used to work at (6y ago) we did pure CSR.
  - We served everything static from S3 and it was super simple to understand and build for.
  - It did mean slower startup for users - but we knew our users only launched the app once a day - so startup didn't matter to them.
- It’s also just so much cheaper to host a client side app. Throw it on any blob storage provider and done

- ## Everyone is talking about server-side rendering. Why? SEO and page load speed.
- https://twitter.com/housecor/status/1532708512836505600
  - Yet many web apps are:
  - 1. Behind a login (so SEO doesn’t matter)
  - 2. Used only on fast connections (so minor page load time differences matter little)
  - Summary: Client-side rendering remains relevant
- That said, I’m a big fan of modern server-side rendered frameworks. But I recognize they’re overkill for many internal business apps. In such cases minor performance differences aren’t typically a big concern because the users are on fast connections with powerful machines.
- And a client-side app can actually be the fastest possible experience after initial load since everything is already loaded. 
  - A client-side app with one bundle can provide truly instant responses. Why? Because it was all loaded up front. This pays off on heavily used apps.

- This is very true. I've worked for 2 SAAS companies where the main persona is the dev (high end machine, at home/work with fiber connection).
Those front-end products started way before the era of Next & co. Very little incentive to invest for such migration. Context matters.

- ## I'm looking for a state of the art solution or architecture for loading external react components (basically js files) into an existing react app at runtime without rebuilding the app.
- https://twitter.com/code_punkt/status/1438132387301535750
- Dynamic import over http perhaps? Webpack module federation is one pf many ways to solve this

- ## how much trouble is it really to have client and server code live in the same file, only to be stripped out on either end during bundling? Is it complex? Needs dependency tracking? 
- https://twitter.com/tannerlinsley/status/1440306663299293191
- @vercel does this with Next. In page files `getStaticProps` , `getServersideProps` and `getStaticPaths` are stripped from the client bundle
- One way is to write a babel plugin that removes the server code from the file and then remove all unused imports so that node builtins are removed. But the way next does it is by tracking imports and variables and then removing the ones that were just used inside the server code.

- Reading about isomorphic architecture for web apps, looks promising.
  - Routes render on client or server depending on request 
  - React bootstraps to rendered HTML on data round trip
  - Once data is fetched, it is cached in client state

- ## How to do partial hydration in React, 2021 edition
- https://twitter.com/iamakulov/status/1437415799514271746
- Use https://github.com/hadeeb/react-lazy-hydration
- Build you own partial hydration
- Try out React 18’s selective hydration
- Check out the React’s Server Components proposal

- ## I really like what @astrodotbuild is doing by shipping less JS. 
- https://twitter.com/wardpeet/status/1429831663127863303
  - It comes close to the long-term vision I have for @gatsbyjs . 
  - Using React's Suspense, Server Components + a sprinkle of magic, we can get into a less JS heavy world. 
  - It's a long road ahead. I'm excited for the future!

- ## To help categorize different Server Rendering JS Frameworks and how they sit relative to each other I made a chart. 
- https://twitter.com/RyanCarniato/status/1428582141185597447
  - 横轴 spa -> mpa; 纵轴 ssg -> ssr
  - Some do extend out of their primary zones but I still think this is illustrative.
- Generally, all SSR frameworks support SSG even if it isn't their primary focus. 
  - And Quadrant 1 is way busier than the graphic shows as that is where the majority of Server Rendering JS frameworks sit. 
  - But there are few clear different types of frameworks here.
- I've written a few about this. More so focusing on JavaScript centric solutions. These frameworks all feel like you are writing client-side apps that happen to just render on the server. And techniques they use to minimize JS sent to the browser.

- ## Next.js has been doing SSR since October 2016. Plenty of successful SSR apps at scale like tiktok.com and trulia.com 
- https://twitter.com/rauchg/status/1424163068620075010
  - Sounds like @brillout had chosen to pre-render everything at build time which is optional

- ## Let me tell you a story of a library developer who wrote some 'isomorphic' code many years ago to run on node and web
- https://twitter.com/BenDelarre/status/1418005935025377284
- They merrily littered their library functions with checks to see which platform they were on...and all was well... But they didn't write tests that ran in the browser
  - Years later another developer enhances their library adding a call to an API from the first libs suite that they hadn't used before... But they too didn't write tests that ran in an actual browser
  - A month goes by, and an application developer updates the dependency on the second library... and all hell breaks loose! This third developer has tests which run in the browser!
  - Hours are spent trying to figure out why tests sometimes fail and sometimes pass, many heads are scratched.
  - Eventually we discover that someone forgot to include the platform check on a function many years ago but nobody had used it until now!
- Moral of the story...
  - Give up on web development, we're all doomed, go buy a farm and grow turnips. It'll be better for your health.

- ## Data fetching in Next.js can be a bit confusing. 
- https://twitter.com/theworstdev/status/1371915581100847107
  - This confusion stems from the fact that there are three ways to fetch and render data: static, server-side, and client-side. 
  - There are benefits and tradeoffs to each strategy so let's discuss what they are
- First up is data fetching for static rendering:
  - With static rendering, your pages are generated at build time and then served as static HTML files. 
  - This method provides speedy response times because the pages don’t need to be rendered for each request.
  - SEO also works as expected for statically rendered pages because the content is readily available for crawlers. 
  - However, statically rendered content can only be updated by deploying a new version of your app.
  - This means that relative to other methods, your content is more likely to become stale between deploys.
  - Static data if fetched in Next.js using the `getStaticProps` method
- Next up is data fetching for server-side rendering
  - With server-side rendering, pages are generated dynamically for each incoming request. 
  - This enables content to be updated between deploys (unlike static rendering), and SEO works as expected.
  - However, rendering on every request does add processing time that can noticeably increase response latency.
  - Server-side data is fetched using the `getServerSideProps` method
- Lastly, there is fetching data client-side rendering
  - With client-side rendering (the typical strategy for React apps), the browser requests the app, the page loads, then React requests the data to present to the user.
  - This strategy keeps pages fresh and responsive, but it isn’t compatible with SEO crawlers.
  - To fetch data client-side you use hooks in your React components
- it's worth mentioning that the delivery of files will be fast if you are using a CDN, but the cost of rendering is moved to the client.

- ## You might not need SSR
- https://twitter.com/devongovett/status/1388946950557372416
- Aside from SEO which is a bit tricky with client side data fetching, what is the point of SSR?
  - First page of app along with app-shell is statically generated and hosted on any CDN which hydrates on the client side. Navigating to different pages would only download the required data.
  - This is my favored approach, app shell + dynamic/on-demand module loading. SSR is a waste of time and energy for every project I've worked on. SSR introduces way too many problems for only solving one.
- Depends always on the app, I found if there is content, why should the user wait on JS to be downloaded and parsed, when it can be rendered as soon as the first byte comes?! For an app however, I tend to agree, if UX is not a white screen until JS comes!
  - And then next time the user needs to load some different content the JS will be cached and they just have to download the content. Instead of downloading the html and content. Which is pretty neat
  - Note that the JS is cached, but it still has to re-parse and run it, which can be a considerable cost on mobile.
- You probably want SSR for non static sites, it’s why 20 year old PHP forums can load in under 200ms backed by millions of live DB records, while Jamstack sites take seconds to show you a loading spinner.
  - API calls are faster in your VPC than over the internet so data fetching is faster in SSR, and browsers are optimized to show HTML as fast as possible.
  - But in React SSR your HTML response generally has to contain all the fetched data anyway (in addition the HTML you rendered using that data). You probably won’t get a significant end-to-end speed improvement until you throw on an HTTP cache/CDN.
- You probably don't need a SPA either.
