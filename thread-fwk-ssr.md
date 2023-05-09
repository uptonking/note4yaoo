---
title: thread-fwk-ssr
tags: [framework, ssr, thread]
created: 2021-04-24T08:28:46.667Z
modified: 2021-04-24T08:29:02.272Z
---

# thread-fwk-ssr

# guide

# repeat

<!-- #region /folded renderToStaticMarkup -->

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

<!-- #endregion /folded renderToStaticMarkup -->

# discuss
- ## 

- ## [reactjs - How single-page application works in SSR (React) - Stack Overflow](https://stackoverflow.com/questions/57243697/how-single-page-application-works-in-ssr-react)
- When implementing Server Side Rendering (SSR), the server knows how to generate a full page with markup so the user gets a fully rendered page and from that moment, when the js resources get downloaded, the application will be live (event listeners will be enabled, the react lifecycle will be active and so on).
01. Get a request for a specific path
02. Initiate a new store instance for the request
03. In case of using react router (or other router solution), fill the state with the requested route
04. Render the app, but instead of rendering and mounting the App, render the App to string (with renderToString)
05. Dehydrate the state - take the latest state snapshot and append it to the result (after escaping it and wrapping it with script tag for example)
06. Return the markup as a response. The markup can look similar to the following: 

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

- ## [reactjs - How is server-side rendering compatible with single-page applications? - Stack Overflow](https://stackoverflow.com/questions/66893389/how-is-server-side-rendering-compatible-with-single-page-applications)
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
