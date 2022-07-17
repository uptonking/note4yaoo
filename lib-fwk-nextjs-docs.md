---
title: lib-fwk-nextjs-docs
tags: [docs, nextjs]
created: 2020-12-17T09:11:37.605Z
modified: 2020-12-17T09:11:52.546Z
---

# lib-fwk-nextjs-docs

- The React Framework with all the features you need for production

# Overview

- Next.js is built around the concept of pages. 
- A page is a React Component exported from a `.js, .jsx, .ts, or .tsx` file in the `pages` directory.
- Each page is associated with a route based on its file name.
  - For example `pages/about.js` is mapped to `/about`. 
  - You can even add dynamic route parameters with the filename.

# Pages

- Static Generation (Recommended)
  - The HTML is generated at build time and will be reused on each request. 
  - To make a page use Static Generation, either export the page component, or export `getStaticProps` (and `getStaticPaths` if necessary). 
  - It's great for pages that can be pre-rendered ahead of a user's request. 
  - You can also use it with Client-side Rendering to bring in additional data.

- Server-side Rendering
  - The HTML is generated on each request. 
  - To make a page use Server-side Rendering, export `getServerSideProps`. 
  - Because Server-side Rendering results in slower performance than Static Generation, use this only if absolutely necessary.

- Next.js supports pages with dynamic routes. 
  - For example, if you create a file called `pages/posts/[id].js`, then it will be accessible at `posts/1, posts/2`, etc.

- By default, Next.js pre-renders every page. 
  - This means that Next.js generates HTML for each page in advance, instead of having it all done by client-side JavaScript.
  - Pre-rendering can result in better performance and SEO.
- Each generated HTML is associated with minimal JavaScript code necessary for that page.
  - When a page is loaded by the browser, its JavaScript code runs and makes the page fully interactive. 
  - (This process is called hydration.)
- Next.js has two forms of pre-rendering: Static Generation and Server-side Rendering. 
  - The difference is in when it generates the HTML for a page.
  - Static Generation (Recommended)
    - The HTML is generated at build time and will be reused on each request.
  - Server-side Rendering
    - The HTML is generated on each request.
- Next.js lets you choose which pre-rendering form you'd like to use for each page. 
  - You can create a "hybrid" Next.js app by using Static Generation for most pages and using Server-side Rendering for others.
- We recommend using Static Generation over Server-side Rendering for performance reasons. 
  - Statically generated pages can be cached by CDN with no extra configuration to boost performance. 
  - However, in some cases, Server-side Rendering might be the only option.
- You can also use Client-side Rendering along with Static Generation or Server-side Rendering. 
  - That means some parts of a page can be rendered entirely by client side JavaScript. 

- If a page uses Static Generation, the page HTML is generated at build time. 
  - That means in production, the page HTML is generated when you run `next build` . 
  - This HTML will then be reused on each request. It can be cached by a CDN.
  - In Next.js, you can statically generate pages with or without data

- By default, Next.js pre-renders pages using Static Generation without fetching data. 
  - Note that this page does not need to fetch any external data to be pre-rendered. 
  - In cases like this, Next.js generates a single HTML file per page during build time.

- Some pages require fetching external data for pre-rendering. 
- In each case, you can use a special function Next.js provides:
  - Your page content depends on external data
    - Use `getStaticProps`.
  - Your page paths depend on external data
    - Use `getStaticPaths` (usually in addition to `getStaticProps`).

- Scenario 1: Your page content depends on external data
  - To fetch this data on pre-render, Next.js allows you to `export` an `async` function called `getStaticProps` from the same file. 
  - This function gets called at build time and lets you pass fetched data to the page's `props` on pre-render.
- Scenario 2: Your page paths depend on external data
  - Next.js allows you to create pages with dynamic routes
  - However, which `id`(parameter in a route path) you want to pre-render at build time might depend on external data.
  - Next.js lets you `export` an `async` function called `getStaticPaths` from a dynamic page
  - This function gets called at build time and lets you specify which paths you want to pre-render

- We recommend using Static Generation (with and without data) whenever possible 
  - because your page can be built once and served by CDN, 
  - which makes it much faster than having a server render the page on every request.
- You should ask yourself: "Can I pre-render this page ahead of a user's request?" 
  - If the answer is yes, then you should choose Static Generation.
  - Static Generation is not a good idea if you cannot pre-render a page ahead of a user's request. 

- Maybe your page shows frequently updated data, and the page content changes on every request.
  - Use Static Generation with Client-side Rendering
    - You can skip pre-rendering some parts of a page and then use client-side JavaScript to populate them.
  - Use Server-Side Rendering
    - Next.js pre-renders a page on each request. 
    - It will be slower because the page cannot be cached by a CDN, 
    - but the pre-rendered page will always be up-to-date.

- Server-side Rendering
  - Also referred to as "SSR" or "Dynamic Rendering".
  - If a page uses Server-side Rendering, the page HTML is generated on each request.

- To use Server-side Rendering for a page, you need to `export` an `async` function called `getServerSideProps`. 
  - This function will be called by the server on every request.
  - `getServerSideProps` is similar to `getStaticProps`, 
  - but the difference is that `getServerSideProps` is run on every request instead of on build time.

# Data Fetching

## `getStaticProps` (Static Generation): Fetch data at build time.

- You should use `getStaticProps` if:
  - The **data required to render the page is available at build time** ahead of a user’s request.
  - The data can be publicly cached (**not user-specific**).
  - The data comes from a headless CMS.
  - The page must be pre-rendered (for SEO) and be very fast 
    - `getStaticProps` generates HTML and JSON files, both of which can be cached by a CDN for performance.

- If you `export` an `async` function called `getStaticProps` from a page, Next.js will pre-render this page at build time using the props returned by `getStaticProps`.
- Redirecting at build-time is currently not allowed 
  - and if the redirects are known at build-time, they should be added in `next.config.js`.
- You can import modules in top-level scope for use in `getStaticProps`. 
  - Imports used in `getStaticProps` will not be bundled for the client-side.
  - This means you can write server-side code directly in `getStaticProps`. 
    - This includes reading from the filesystem or a database.
- You should not use `fetch()` to call an API route in your application. 
  - Instead, directly import the API route and call its function yourself. 
  - You may need to slightly refactor your code for this approach.
  - Fetching from an external API is fine!

``` JS
export async function getStaticProps() {
  // Call an external API endpoint to get posts.
  // You can use any data fetching library
  const res = await fetch('https://.../posts')
  const posts = await res.json()

  // By returning { props: posts }, the Blog component
  // will receive `posts` as a prop at build time
  return {
    props: {
      posts,
    },
  }
}
```

- Incremental Static Regeneration
  - With `getStaticProps` you don't have to stop relying on dynamic content, as static content can also be dynamic. 
  - Incremental Static Regeneration allows you to update existing pages by re-rendering them in the background as traffic comes in.
- Inspired by stale-while-revalidate, background regeneration ensures traffic is served uninterruptedly, always from static storage, 
  - and the newly built page is pushed only after it's done generating.
- Unlike traditional SSR, Incremental Static Regeneration ensures you retain the benefits of static:
  - No spikes in latency. 
    - Pages are served consistently fast
  - Pages never go offline. 
    - If the background page re-generation fails, the old page remains unaltered
  - Low database and backend load. 
    - Pages are re-computed at most once concurrently
- Files can be read directly from the filesystem in `getStaticProps`.
  - In order to do so you have to get the full path to a file.
  - Since Next.js compiles your code into a separate directory, you can't use `__dirname` as the path 
  - Instead you can use `process.cwd()`, which gives you the directory where Next.js is being executed.

- `getStaticProps` Only runs at build time
  - Because `getStaticProps` runs at build time, it does not receive data that’s only available during request time, such as query parameters or HTTP headers as it generates static HTML.
- Write server-side code directly
  - `getStaticProps` runs only on the server-side. 
  - It will never be run on the client-side. 
  - It won’t even be included in the JS bundle for the browser. 
  - That means you can write code such as direct database queries without them being sent to browsers. 
  - You should not fetch an API route from `getStaticProps`
  - instead, you can write the server-side code directly in `getStaticProps`.
- Statically Generates both HTML and JSON
  - Next.js also generates a JSON file holding the result of running `getStaticProps`.
  - This JSON file will be used in client-side routing through `next/link` or `next/router`
  - When you navigate to a page that’s pre-rendered using `getStaticProps`, Next.js fetches this JSON file (pre-computed at build time) and uses it as the props for the page component. 
  - This means that client-side page transitions will not call `getStaticProps` as only the exported JSON is used.
- `getStaticProps` can only be exported from a page. 
  - You can’t export it from non-page files.
  - One of the reasons for this restriction is that React needs to have all the required data before the page is rendered.
  - Also, you must use `export async function getStaticProps() {}` — it will not work if you add `getStaticProps` as a property of the page component.
- In development (`next dev`), getStaticProps will be called on every request.
- Preview Mode
  - In some cases, you might want to temporarily bypass Static Generation and render the page at request time instead of build time. 
  - For example, you might be using a headless CMS and want to preview drafts before they're published.
  - This use case is supported by Next.js by the feature called Preview Mode. 

## `getStaticPaths` (Static Generation): Specify dynamic routes to pre-render based on data.

- You should use `getStaticPaths` if you’re statically pre-rendering pages that use dynamic routes.

- If you export an `async` function called `getStaticPaths` from a page that uses dynamic routes, Next.js will statically pre-render all the paths specified by `getStaticPaths`.
- The `paths` key determines which paths will be pre-rendered.
- If you have a page that uses dynamic routes named `pages/posts/[id].js`, you should use

``` JS
export async function getStaticPaths() {
  return {
    paths: [
      { params: { id: '1' } },
      { params: { id: '2' } }
    ],
    fallback: false
  };
}
```

- Then Next.js will statically generate `posts/1` and `posts/2` at build time using the page component in `pages/posts/[id].js`.
- Note that the value for each `params` must match the parameters used in the page name
- The object returned by `getStaticPaths` must contain a boolean `fallback` key.
- If `fallback` is `false`, then any paths not returned by `getStaticPaths` will result in a 404 page.

- If `fallback` is `true`, then
  - The paths returned from `getStaticPaths` will be rendered to HTML at build time by `getStaticProps`.
  - The paths that have not been generated at build time will not result in a 404 page. Instead, Next.js will serve a “fallback” version of the page on the first request to such a path
  - In the background, Next.js will statically generate the requested path HTML and JSON. This includes running `getStaticProps`.
  - When that’s done, the browser receives the JSON for the generated path. 
    - This will be used to automatically render the page with the required props. 
    - From the user’s perspective, the page will be swapped from the fallback page to the full page.
  - At the same time, Next.js adds this path to the list of pre-rendered pages. 
  - Subsequent requests to the same path will serve the generated page, just like other pages pre-rendered at build time.

- In the “fallback” version of a page:
  - The page’s props will be empty.
  - Using the router, you can detect if the fallback is being rendered, router.isFallback will be `true`.

- When is `fallback: true` useful?
  - if your app has a very large number of static pages that depend on data 
  - You want to pre-render all product pages, but then your builds would take forever.
  - Instead, you may statically generate a small subset of pages and use `fallback: true` for the rest. 
  - When someone requests a page that’s not generated yet, the user will see the page with a loading indicator. 
  - Shortly after,  `getStaticProps` finishes and the page will be rendered with the requested data. 
  - From now on, everyone who requests the same page will get the statically pre-rendered page.
  - This ensures that users always have a fast experience while preserving fast builds and the benefits of Static Generation.
  - `fallback: true` will not update generated pages, for that take a look at Incremental Static Regeneration.

- If `fallback: 'blocking'`, new paths not returned by `getStaticPaths` will wait for the HTML to be generated, 
  - identical to SSR (hence why blocking), and then be cached for future requests so it only happens once per path.
  - The paths returned from `getStaticPaths` will be rendered to HTML at build time by `getStaticProps`.
  - The paths that have not been generated at build time will not result in a 404 page. 
  - Instead, Next.js will SSR on the first request and return the generated HTML.
  - When that’s done, the browser receives the HTML for the generated path. 
  - From the user’s perspective, it will transition from "the browser is requesting the page" to "the full page is loaded". 
  - There is no flash of loading/fallback state.
  - At the same time, Next.js adds this path to the list of pre-rendered pages. 
  - Subsequent requests to the same path will serve the generated page, just like other pages pre-rendered at build time.
  - `fallback: 'blocking'` will not update generated pages by default. 
  - To update generated pages, use Incremental Static Regeneration in conjunction with `fallback: 'blocking'`.

- When you use `getStaticProps` on a page with dynamic route parameters, you must use `getStaticPaths`.
- You cannot use `getStaticPaths` with `getServerSideProps`.
- `getStaticPaths` only runs at build time on server-side.
- `getStaticPaths` can only be exported from a page.
  - You can’t export it from non-page files.
- In development (`next dev`), getStaticPaths will be called on every request.

## `getServerSideProps` (Server-side Rendering): Fetch data on each request.

- You should use `getServerSideProps` only if you need to pre-render a page whose data must be fetched at request time.
  - Time to first byte (TTFB) will be slower than `getStaticProps`

  - because the server must compute the result on every request, 
  - and the result cannot be cached by a CDN without extra configuration.

If you don’t need to pre-render the data, then you should consider fetching data on the client side

- If you export an `async` function called `getServerSideProps` from a page, Next.js will pre-render this page on each request using the data returned by `getServerSideProps`.
- You can import modules in top-level scope for use in `getServerSideProps`.
  - Imports used in `getServerSideProps` will not be bundled for the client-side.
  - This means you can write server-side code directly in getServerSideProps.
  - You should not use fetch() to call an API route in your application. 
  - Instead, directly import the API route and call its function yourself. 
  - Fetching from an external API is fine!

``` JS
// This gets called on every request
export async function getServerSideProps() {
  // Fetch data from external API
  const res = await fetch(`https://.../data`)
  const data = await res.json()

  // Pass data to the page via props
  return { props: { data } }
}
```

- `getServerSideProps` only runs on server-side and never runs on the browser.
  - When you request this page directly,  `getServerSideProps` runs at the request time, 
  - and this page will be pre-rendered with the returned props.
  - When you request this page on client-side page transitions through `next/link` or `next/router`, Next.js sends an API request to the server, which runs `getServerSideProps`. 
  - It’ll return JSON that contains the result of running getServerSideProps, and the JSON will be used to render the page. 
  - All this work will be handled automatically by Next.js, so you don’t need to do anything extra as long as you have `getServerSideProps` defined.
- `getServerSideProps` can only be exported from a page. 
  - You can’t export it from non-page files.

## Fetching data on the client side

- If your **page contains frequently updating data**, and you don’t need to pre-render the data, you can fetch the data on the client side.
  - An example of this is user-specific data. 
- Here’s how it works:
  - First, immediately show the page without data. 
  - Parts of the page can be pre-rendered using Static Generation. 
  - You can show loading states for missing data.
  - Then, fetch the data on the client side and display it when ready.
- This approach works well for user dashboard pages, for example. 
  - Because a dashboard is a private, user-specific page, 
  - SEO is not relevant and the page doesn’t need to be pre-rendered. 
  - The data is frequently updated, which requires request-time data fetching.
- We highly recommend SWR, if you’re fetching data on the client side. 
  - It handles caching, revalidation, focus tracking, refetching on interval, and more.

``` JS
import useSWR from 'swr';

function Profile() {
  const { data, error } = useSWR('/api/user', fetch)

  if (error) return <div>failed to load</div>
  if (!data) return <div>loading...</div>
  return <div>hello {data.name}!</div>
}
```

# Configuration

- you can create a `next.config.js` in the root of your project directory
  - It is a regular Node.js module, not a JSON file. 
  - It gets used by the Next.js server and build phases, and it's not included in the browser build.
- `phase` is the current context in which the configuration is loaded
- The commented lines are the place where you can put the configs allowed by `next.config.js`
- None of the configs are required
- `next.config.js` will not be parsed by Webpack, Babel or TypeScript.
  - Avoid using new JavaScript features not available in your target Node.js version.

- Environment Variables
- Custom Webpack Config
- Runtime Configuration
  - Generally you'll want to use build-time environment variables to provide your configuration
  - runtime configuration adds rendering/initialization overhead and is incompatible with Automatic Static Optimization.
  - Place any server-only runtime config under `serverRuntimeConfig`.
  - Anything accessible to both client and server-side code should be under `publicRuntimeConfig`.

- To start, you only need to define a `.babelrc` file at the top of your app. 
  - If such a file is found, it will be considered as the source of truth, 
  - and therefore it needs to define what Next.js needs as well, which is the `next/babel` preset.
  - Next.js uses the current Node.js version for server-side compilations.
  - The modules option on "preset-env" should be kept to false, otherwise webpack code splitting is turned off.

# Styling 

- Next.js allows you to import CSS files from a JavaScript file. 
- These styles (`styles.css`) will apply to all pages and components in your application. 
  - Due to the global nature of stylesheets, and to avoid conflicts, you may only import them inside `pages/_app.js`.
- In development, expressing stylesheets this way allows your styles to be hot reloaded as you edit them
  - meaning you can keep application state
- In production, all CSS files will be automatically concatenated into a single minified `.css` file.
- Since Next.js 9.5.4, importing a CSS file from `node_modules` is permitted anywhere in your application.
- For global stylesheets, like bootstrap4, you should import the file inside `pages/_app.js`. 
- For importing CSS required by a third party component, you can do so in your component

- Next.js supports CSS Modules using the `[name].module.css` file naming convention.
  - CSS Modules locally scope CSS by automatically creating a unique class name. 
  - This allows you to use the same CSS class name in different files without worrying about collisions.
- This behavior makes CSS Modules the ideal way to include component-level CSS.
- CSS Module files can be imported anywhere in your application.
- CSS Modules are an optional feature and are only enabled for files with the `.module.css` extension.
- Regular `<link>` stylesheets and global CSS files are still supported.
- In production, all CSS Module files will be automatically concatenated into many minified and code-split `.css` files. 
  - These .css files represent hot execution paths in your application, ensuring the minimal amount of CSS is loaded for your application to paint.

- Next.js allows you to import Sass using both the `.scss` and `.sass` extensions. 
  - You can use component-level Sass via CSS Modules and the `.module.scss` or `.module.sass` extension
- Sass support has the same benefits and restrictions as the built-in standard CSS support

- It's possible to use any existing CSS-in-JS solution. 
  - The simplest one is inline styles
- We bundle `styled-jsx` to provide support for isolated scoped CSS. 
  - The aim is to support "shadow CSS" similar to Web Components, which unfortunately do not support server-rendering and are JS-only.

# Image Component

- Since version 10.0.0, Next.js has a built-in Image Component and Automatic Image Optimization.
- The Next.js Image Component `next/image`, is an extension of the HTML `<img>` element, evolved for the modern web.
- The Automatic Image Optimization allows for resizing, optimizing, and serving images in modern formats like WebP when the browser supports it. 
  - This avoids shipping large images to devices with a smaller viewport. 
  - It also allows Next.js to automatically adopt future image formats and serve them to browsers that support those formats.
- Automatic Image Optimization works with any image source. 
  - Even if the image is hosted by an external data source, like a CMS, it can still be optimized.
- Instead of optimizing images at build time, Next.js optimizes images on-demand, as users request them. 
  - Unlike static site generators and static-only solutions, your build times aren't increased, whether shipping 10 images or 10 million images.
- Images are lazy loaded by default. 
  - That means your page speed isn't penalized for images outside the viewport. 
  - Images load as they are scrolled into viewport.
- mages are always rendered in such a way as to avoid prevent Cumulative Layout Shift, a Core Web Vital that Google is going to use in search ranking.

- the caching algorithm for the default loader.
  - Images are optimized dynamically upon request and stored in the `<distDir>/cache/images` directory. 
  - The optimized image file will be served for subsequent requests until the expiration is reached. 
  - When a request is made that matches a cached but expired file, the cached file is deleted before generating a new optimized image and caching the new file.

# Static File Serving

- Next.js can serve static files, like images, under a folder called `public` in the root directory. 
  - Files inside `public` can then be referenced by your code starting from the base URL (`/`).
  - This folder is also useful for `robots.txt, favicon.ico`, Google Site Verification, and any other static files (including `.html`)!
  - The name `public` cannot be changed and is the only directory used to serve static assets.
- Only assets that are in the public directory at build time will be served by Next.js. 
  - Files added at runtime won't be available. 
  - We recommend using a third party service like AWS S3 for persistent file storage.

# Fast Refresh

- Fast Refresh is enabled by default in all Next.js applications on 9.4 or newer. 
- With Next.js Fast Refresh enabled, most edits should be visible within a second, without losing component state.
- How It Works
  - If you edit a file that only exports React component(s), Fast Refresh will update the code only for that file, and re-render your component.
  - If you edit a file with exports that aren't React components, Fast Refresh will re-run both that file, and the other files importing it.
  - Finally, if you edit a file that's imported by files outside of the React tree, Fast Refresh will fall back to doing a full reload
- You might have a file which renders a React component but also exports a value that is imported by a non-React component. 
  - For example, maybe your component also exports a constant, and a non-React utility file imports it. 
  - In that case, consider migrating the constant to a separate file and importing it into both files. 
  - This will re-enable Fast Refresh to work. 
  - Other cases can usually be solved in a similar way.

- Here's a few reasons why you might see local state being reset on every edit to a file:
  - Local state is not preserved for class components (only function components and Hooks preserve state).
  - The file you're editing might have other exports in addition to a React component.
  - Sometimes, a file would export the result of calling higher-order component like HOC(WrappedComponent). If the returned component is a class, state will be reset.
  - Anonymous arrow functions like `export default () => <div />;` cause Fast Refresh to not preserve local component state. 
    - For large codebases you can use our n`ame-default-component` codemod.

- Tips
  - Fast Refresh preserves React local state in function components (and Hooks) by default.
  - Sometimes you might want to force the state to be reset, and a component to be remounted. 
    - For example, this can be handy if you're tweaking an animation that only happens on mount. 
    - To do this, you can add `// @refresh reset` anywhere in the file you're editing. 
    - This directive is local to the file, and instructs Fast Refresh to remount components defined in that file on every edit.
  - You can put `console.log` or `debugger;` into the components you edit during development.

- When possible, Fast Refresh attempts to preserve the state of your component between edits. 
- In particular `useState` and `useRef` preserve their previous values as long as you don't change their arguments or the order of the Hook calls.
- Hooks with dependencies such as `useEffect, useMemo, useCallback`, will always update during Fast Refresh. 
  - Their list of dependencies will be ignored while Fast Refresh is happening.
- Sometimes, this can lead to unexpected results. 
  - For example, even a useEffect with an empty array of dependencies would still re-run once during Fast Refresh.
  - However, writing code resilient to occasional re-running of `useEffect` is a good practice even without Fast Refresh. 
  - It will make it easier for you to introduce new dependencies to it later on 
  - and it's enforced by React Strict Mode, which we highly recommend enabling.

# TypeScript

- Next.js uses Babel to handle TypeScript, which has some caveats, and some compiler options are handled differently.
- The file `next-env.d.ts` ensures Next.js types are picked up by the TypeScript compiler. 
- TypeScript `strict` mode is turned off by default
- By default, Next.js will do type checking as part of `next build`.

# Supported Browsers and Features

- Next.js supports IE11 and all modern browsers (Edge, Firefox, Chrome, Safari, Opera, et al) with no required configuration.
- We transparently inject polyfills required for IE11 compatibility. 
- In addition, we also inject widely used polyfills, including:
  - `fetch()`
    - Replacing: whatwg-fetch and unfetch.
    - Next.js polyfills `fetch()` in the Node.js environment
  - `URL`
    - Replacing: the url package (Node.js API).
  - `Object.assign()`
    - Replacing: object-assign, object.assign, and core-js/object/assign.
- In addition, to reduce bundle size, Next.js will only load these polyfills for browsers that require them. 
- you can add polyfills yourself.
  - you should add a top-level import for the specific polyfill you need in your Custom `<App>` or the individual component.
- Next.js allows you to use the latest ES features out of the box.
  - Async/await (ES2017)
  - Object Rest/Spread Properties (ES2018)
  - Dynamic import() (ES2020)
  - Optional Chaining (ES2020)
  - Nullish Coalescing (ES2020)
  - Class Fields and Static Properties (part of stage 3 proposal)
  - and more!

# Routing

- Next.js has a file-system based router built on the concept of pages.
- When a file is added to the `pages` directory, it's automatically available as a route.
- Index routes
- Nested routes
- Dynamic route segments
- The Next.js router allows you to do client-side route transitions between pages, similarly to a single-page application.
  - use `import Link from 'next/link'`

- In Next.js you can add brackets to a page (`[param]`) to create a dynamic route (a.k.a. url slugs, pretty urls, and others).

- Dynamic routes can be extended to catch all paths by adding three dots (`...`) inside the brackets.
- Catch all routes can be made optional by including the parameter in double brackets (`[[...slug]]`).
  - The main difference between catch all and optional catch all routes is that with optional, the route without the parameter is also matched

- Caveats
  - Predefined routes take precedence over dynamic routes, and dynamic routes over catch all routes. 
  - Pages that are statically optimized by Automatic Static Optimization will be hydrated without their route parameters provided, i.e `query` will be an empty object ({}).
    - After hydration, Next.js will trigger an update to your application to provide the route parameters in the `query` object.

- `next/link` should be able to cover most of your routing needs, 
  - but you can also do client-side navigations without it, take a look at `next/router`.

- Shallow routing allows you to change the URL without running data fetching methods again, that includes `getServerSideProps, getStaticProps, getInitialProps`.
- Shallow routing only works for same page URL changes
  - If that's a new page, it'll unload the current page, load the new one and wait for data fetching even though we asked to do shallow routing.

- Next.js has built-in support for internationalized (i18n) routing since v10.0.0. 

# API Routes

- API routes provide a straightforward solution to build your API with Next.js.
- Any file inside the folder `pages/api` is mapped to `/api/*` and will be treated as an API endpoint instead of a page. 
  - They are server-side only bundles and won't increase your client-side bundle size.
- For an API route to work, you need to export as default a function (a.k.a request handler)
- To handle different HTTP methods in an API route, you can use `req.method` in your request handler, 

- API Routes do not specify CORS headers, meaning they are same-origin only by default. 
  - You can customize such behavior by wrapping the request handler with the cors middleware.
- API Routes can't be used with `next export`

- API routes support dynamic routes, and follow the same file naming rules used for `pages`.
- Predefined API routes take precedence over dynamic API routes, and dynamic API routes over catch all API routes.

- API routes provide built in middlewares which parse the incoming request (`req`). 

- The response (`res`) includes a set of Express.js-like methods to increase the speed of creating new API endpoints

# Preview Mode

# Dynamic Import

- Next.js supports ES2020 dynamic `import()` for JavaScript. 
  - With it you can import JavaScript modules dynamically and work with them. 
  - They also work with SSR.
- You can think of dynamic imports as another way to split your code into manageable chunks.
- React components can also be imported using dynamic imports, 
  - but in this case we use it in conjunction with `next/dynamic` to make sure it works just like any other React Component. 

# Static HTML Export

# Absolute Imports and Module path aliases

# Automatic Static Optimization

- If `getServerSideProps` or `getInitialProps` is present in a page, Next.js will switch to render the page on-demand, per-request (meaning Server-Side Rendering).
- If the above is not the case, Next.js will statically optimize your page automatically by prerendering the page to static HTML.

# Measuring performance

- Next.js has a built-in relayer that allows you to analyze and measure the performance of pages using different metrics.

# AMP Support

- With Next.js you can turn any React page into an AMP page, with minimal config, and without leaving React.

# Customization

- Pages can also be added under `src/pages` as an alternative to the root `pages` directory.
  - `src/pages` will be ignored if `pages` is present in the root directory
  - Config files like `next.config.js` and `tsconfig.json` should be inside the root directory, moving them to `src` won't work
    - Same goes for the `public` directory

# Debugging

- It requires you to first launch your Next.js application in debug mode in one terminal 
  - and then connect an inspector (Chrome DevTools or VS Code) to it.

# Deploy

- A zone is a single deployment of a Next.js app. 
  - You can have multiple zones and merge them as a single app.
- With multi zones support, you can merge both these apps into a single one allowing your customers to browse it using a single URL, 
  - but you can develop and deploy both apps independently.

- Incrementally Adopting Next.js
  - Next.js has been designed for gradual adoption.
  - The first strategy is to configure your server or proxy such that, everything under a specific subpath points to a Next.js app.
    - Using `basePath`, you can configure your Next.js application's assets and links to automatically work with your new subpath
  - The second strategy is to create a new Next.js app that points to the root URL of your domain.
