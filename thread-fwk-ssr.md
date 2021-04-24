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

- ## 

- ## 
