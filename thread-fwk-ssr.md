---
title: thread-fwk-ssr
tags: [framework, ssr, thread]
created: '2021-04-24T08:28:46.667Z'
modified: '2021-04-24T08:29:02.272Z'
---

# thread-fwk-ssr

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

# pieces

- ## 

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
