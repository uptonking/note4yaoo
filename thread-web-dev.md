---
title: thread-web-dev
tags: [frontend, thread, web]
created: '2020-12-05T07:43:47.005Z'
modified: '2021-01-08T17:13:43.392Z'
---

# thread-web-dev

# pieces

- ## 

- ## TIL about the Visual Viewport API
- https://twitter.com/rikschennink/status/1361598959828037633
  - When opening a soft keyboard `window.innerHeight` will stay the same but `visualViewport.height` won't!
  - Even better, you can listen for `resize` and `scroll` events on the `visualViewport` object.

- ## Unpopular opinion: ESM was a bad idea.
- https://twitter.com/devongovett/status/1356258095949885442
  - It has caused half a decade of churn in the JS ecosystem, broken almost every tool, caused maintenance nightmares for library authors, and for what? A different syntax? CJS was fine. 😐
- CJS is not perfect too. Resolving algo is a nightmare. It would never be compatible with web.
- As someone who has written a few Babel plugins that analyze dependencies etc, I will say that it is an advantage for toolability that ESM syntax is more constrained than what CJS allows. 
  - I believe Sasha is correct about sync vs async and the web being the main driver.
  - Wasn’t the reasoning behind this something along the lines of “node modules are FS-based and sync and web cannot work like this”?
- The main benefit of ESM is not in features it adds over CJS, it is the features it removes. 
  - The inability to specify dynamic synchronous dependencies comes to mind.
  - To my "we haven't capitalized on it yet" point though: CJS exports mix realms, whereas ES Module instances preserve the potential for future cross-realm dependencies (JS<->WASM, between threads, etc)
  - ES Modules feel like they will be more than just JavaScript, whereas CJS was obviously a JavaScript-first approach. e.g. Import assertions

- ## HTML(performance) tip: You can use the `loading=lazy` attribute to defer the loading of the image until the user scrolls to them
- https://twitter.com/denicmarko/status/1355439705853194241
- Here's how it works. 
  - When the user comes to your page, the browser will load all images you used. 
  - But, if you use this attribute, the images will be loaded only until (and if) the user scrolls to them. 
  - It will boost the performance of your page significantly.
- How can we do this for a whole section, not just image.
  - The `content-visibility` CSS property controls whether or not an element renders its contents at all

- ##  you no longer have to write <a target=“_blank” rel=“noopener”> to make external links secure!
- https://twitter.com/swyx/status/1354743782701375488
  - The HTML standard was changed in 2019 so that `rel=“noopener”` is always implied
- also worth noting that we cant drop rel=noopener right this second, bc this change only JUST landed (Chrome 88) and will take time to roll out. but will be soon!

- ## The MS-Edge/Blink folks are working on adding a <popup> HTML element, for tooltips/menus
- https://twitter.com/JoshWComeau/status/1354529361031024640
  - Handles all the hard stuff (layering, positioning, focus management, accessibility)
  - Built-in “light dismiss”
  - Can be fully styled
- This is super exciting! We've all spent too many hours fussing with popovers
- That would be really nice. No more Popper.js or libraries for custom dropdowns, date pickers, tooltips and menus.
- How is this different from `<dialog>` ?
  - I see it can be directly tied to a parent element.
- Nice but that means the popup will be native and different across browsers
- That smells of new IE6 in the making.

- ## If you ever looked inside a non-minified bundle, you might’ve seen a lot of automatically generated comments that look like this `/*#​__PURE__*/ `

- https://twitter.com/iamakulov/status/1353650608750825472
- In 2016, folks noticed that when you transpile a JS class with Babel, the class isn’t removed during tree-shaking. 
  - Even if it’s not used anywhere.
  - React was heavily relying on classes back then, so this was a pretty huge deal for React apps.
- Back then, classes were just a syntactic sugar around functions. 
  - So, to transpile a class, Babel was converting it into a function – and wrapping that function into an IIFE (immediately invoked function expression)
  - a problem with an IIFE is that UglifyJS (which did tree shaking in webpack back then) doesn’t know whether it’s safe to remove it.
  - An IIFE may simply create a class and do nothing else, like above. But it also may send a request to the server. UglifyJS doesn’t know
  - To solve this `/*#​__PURE__*/` was born.
  - Babel started to add /*#​__PURE__*/ comments in front of IIFEs it generates (as it knows they don’t have any side effects).
  - And UglifyJS started to recognize these comments – and dropping pure function calls if their result isn’t used.
- Fast forward to 2021:
  - Terser replaced UglifyJS in webpack (and is still responsible for most of tree shaking)
  - A lot of other tools adopted /*#​__PURE__*/ comments (eg babel-preset-react – for React.createElement – or babel-plugin-styled-components – for styled.whatever)
  - /*#​__PURE__*/ annotations were documented on the Terser website, along with a couple others

- ## The "hidden" cost of webfonts: you need to test everything twice. 
- https://twitter.com/rauchg/status/1352730054950703104
  - Blocking webfonts are a no-go, so you need to consider every page in 2 dimensions (font-display: optional).
  - Similar problem as light/dark mode. Not bad per se, but you need to be aware of the complexity space.
- Yup, dark mode isn’t just swapping color and background color. 
  - It’s an entire new color scheme, basically double the work in terms of color styles on the website.
- CSS is NP-Hard Problem. 
  - That's why it's so hard to automatize it. 
  - But there are ways to get optimal enough solutions. If I understand it correctly

- ## How to get the best image performance (Updated 2021)
- https://twitter.com/leeerob/status/1352264153411497993
1. Use `width` and `height` to prevent layout shift
2. Lazy-load images as they enter the viewport
3. Use modern image formats (WebP, AVIF)
4. Serve correctly sized images using `srcset` .
5. Provide blur-up placeholders

- ## using Intersection Observer on a handful of elements on a page
- https://twitter.com/ChrisFerdinandi/status/1352040366548135937
  - is it better to create a new observer for each one, or use the observer.observe() method to attach multiple elements to one observer?
- Group by callback.
  - If your callback will include a bunch of if else matches to parse through  the results each time to filter which elements intersectionality to act on, you better have different observers.
- Also note that the callback is called immediately on the observer being instantiated, with initial status on all matching elements

- [Should IntersectionObserver represent the observation of a single target Element?](https://github.com/w3c/IntersectionObserver/issues/81)

- ## The JavaScript story for protobufs is SO painful.
- https://twitter.com/BenLesh/status/1351618444286976000
- I gave up on protobufs long time ago for the same reasons. 
  - For me the most productive way to do that is to wrap/augment my transportable objects with a discriminator using `.toJSON` impl and revive them upon reception with `JSON.parse` . 
  - This does not cover binary data use case though
- Going from "I have a .proto file" to "I have a client that can communicate with a server" or "I have a Node.js server" is, frankly, an awful experience. 
  - Nothing is straightforward, there's a lot of half-baked libraries that try to help, but aren't well supported.
  - When you do finally generate JavaScript via the blessed libraries, what you end up with looks like something dreamed up by Java developers in 1999, rather than anything resembling what you could do with plain HTTP or WebSockets given modern JS and Node.
  - There's so much more. Network tab debuggability, etc. etc.
  - That one is definitely true, but isn't that a general problem with protobuffs, not limited to JavaScript implementation per se?
- Not just painfully. 
  - If you want to use it from browser there is no good option. 
  - Large amount of code is generated if you went the grpc-web route. 
  - I find ts-proto and grpc-gateway a middle ground. 
  - But with this client deals with json not protos, but no extra client side code.
- I'd thought that TypedArrays and DataViews made it simpler. 
  - Support for binary data on the web is quite solid by now.

- ## Just learned about how @excalidraw implements encryption by encrypting the data 
- https://twitter.com/christoomey/status/1351234746139947013
  - and then putting the key in the hash of the URL (which browsers don't send with the request). 
  - Self-contained security via browser features, so neat!
- Interesting, I didn’t think about adding it to the payload. 
  - That would solve the problem I was trying to avoid: increasing the length of the url. Thanks! Would you be interested in implementing it?

- ## It might be a "Hot take". But. You need a really good reason to be mocking API requests in @storybookjs
- https://twitter.com/jh3yy/status/1351288120881385479
  - It's a tool for building UI components in ISOLATION 
  - If your UI components are coupled to API requests, something can likely be designed better 
- There's usually a way to design and architect your UI in a way that gets around this
  - The ideal scenario is that you're able to drop in as out components without things falling apart 
  - Only place I can see where this can be tricky is things like widgets
- Mocks can be useful for page-level components and side-loaded data. 
  - In these cases, a components inherent complexity can be more awkward to abstract away.
  - Even if it's more verbose to create "container" components for pages it challenges the design process
  - That's one thing I really appreciate about Storybook. 
  - Especially when you develop Storybook first
- Thinking more on it. 
  - I guess this comes more from a "Because you can, doesn't mean you necessarily should" mindset.
  - Where I've used this in the bigger projects. 
  - The joy has been where things are kept "simple". 
  - Purely presentational. Because coupling isn't fun to maintain.
  - For sure, that's how we build UIs internally. 
  - Presentational all the way to the page and then hydrate data down
- I don't like seeing nested arrays or objects in storybook at all if I can help it!
  - Often that means there's something else to extract, which can then be imported into the parent test.
  - (Obviously this isn't a hard rule, sometimes they're needed)

- ## I was going to work on removing the outlines around buttons when you click on them but I'm having trouble focusing.
- https://twitter.com/markdalgleish/status/1350999134631768069
- No outlines? You know I care deeply about a11y. Seems like you guys are just pressing my buttons.
- Bug Report: Can't focus while PMs are hovering
  - `.markDalgleish:not(:focus) { }`

- ## Two of my most- and first-used checks when doing a performance audit are surprisingly old school:
- https://twitter.com/csswizardry/status/1349400099647090694
  - Validate HTML 
  - Disable JS.

- ## Pages opened with `target="_blank"` allow the new page to access the original's `window.opener` . 
- https://twitter.com/denicmarko/status/1349247474083508224
  - This can have security and performance implications. 
  - Include `rel="noopener"` or `rel="noreferrer"` to prevent this.
  - `noopener` sets `window.opener` to `null` on the new page, so it's good for the security and performance. 
  - `noreferrer` does the same but also omit the `Referer` header, which can have SEO implications, because all traffic to the targeted website will be registered as direct clicks.
- One of the obvious issues is that the original page can be redirected.

- ## Google's Web Vitals site doesn't pass Google's Core Web Vitals assessment 🤔 irony?
- https://twitter.com/toddmotto/status/1349128843928477704
- I get a different view. 
  - Tried in incognito mode in order to not run extensions.
- That looks like Desktop, try mobile over [here](https://developers.google.com/speed/pagespeed/insights/?url=https%3A%2F%2Fweb.dev%2Fvitals%2F&tab=mobile)

- ## Avoid layout shifts on long pages by adding a scrollbar
- https://twitter.com/JoshWComeau/status/1349374805418635264
  - `overflow-y: scroll;`

  - Improves CLS score
- this is indeed annoying.
  - what's your solution for modals opening and hiding that scrollbar, producing a content shift on opening?

- ## url state
- https://twitter.com/kentcdodds/status/1349173470567964673
  - If you find yourself synchronizing some local component state with the URL (for example, query parameters), you'd be better off treating the URL as the source of truth 

    - and ditching your local state in favor of getting the value from the URL (or your router) and updating the URL.

- Agreed almost always. 
  - There are a few cases where you want to sync state though, like an autocomplete that goes up to the url search params, you’ll want to throttle that user interaction (maybe not with CM though!)
  - Although you can also navigate inside of a throttle ... so maybe you’re right always.
- I’ve said same thing before 
  - but I’ve since changed my mind because of performance issues it causes in many cases. 
  - Instead I suggest making an abstraction that mirrors the state using what ever throttling or debouncing mechanism you need, and ideally testing that error-prone code.
  - Imagine a search component. 

    - Updating the url on each keypress is not awesome anyway because it fills the history with crap (ignoring replace here). 
    - Updating it if you click a button to run the new search is fine though.

- Unfortunately updating the URL is throttled by browsers, 
  - so this doesn't work for state that is updated a lot, 
  - e.g. a search query that updates as you type 

- ## A downside of modern SSG's (e.g. Next.js getStaticProps or Gatsby) is that builds are dirty.
- https://twitter.com/jaredpalmer/status/1349060733837963265
  - Same input != same output. 
  - Even with @turborepo cache, we need better incremental bundler caching + hosting providers (like @vercel ISSG/revalidate) to handle last mile for SSG workflow
- It's so, so hard. 
  - Most tools are just not designed for caching at all. 
  - We've had to do so much work in Parcel 2 to properly track all possible changes that could invalidate the cache. 
  - And in some cases we still have to bail
- In what scenario would the same input would give different outputs?
  - When you fetch blog posts from an external CMS at build time and then use that to generate a page for each post
- SSG could be pure if all you used was the filesystem data as a source. Same for Next.js. 
  - However, that's not guaranteed at all. 
  - Anything can be placed onto gatsby's graphql graph and any code can run in getStaticProps

- ## The three features of React that we are going to rely on most in Remix are (probably):
- https://twitter.com/mjackson/status/1348816271933014021
  - renderToString
  - error boundaries
  - react-refresh
  - I would have said `Suspense` a few months ago, but we are targeting stable React so Suspense is out for now.
- We actually have our own mini suspense inside Remix itself, built on top of current stable React and React Router
  -  It includes:

     - async data fetching (that works during server rendering too!)
     - dynamic code loading (both styles and components)
     - a “pending transition” hook

  - I’m particularly excited about the error handling work we are doing. You’ve never seen anything like it before, I promise
  - Remix error boundaries work both for render errors *and* errors that occur during data fetching. Handling errors has never been easier.
- `Suspense` does make some things nicer, like image pre-loading, 
  - but I'm increasingly doubtful it's worth the added complexity and CM breakage.

- ## Do any of you create raw web components? e.g. custom elements without Stencil, lit, or any other tooling?
- https://twitter.com/claviska/status/1348797980854378496
- Any convenience utilities you’ve created/are using for data binding and similar things?
  - I’m weird I guess but I like to use jQuery it already supports scope `$(this, ’.element’)`

  - The util functions I often end up using is a function to `queryselector(all)` in the shadowDOM; 

    - and a function to fire a custom event - that automatically sets `composed:true` etc as default

- Yes! I love to build #webcomponents from scratch and I used to do that quite often to learn the in’s and out’s of the API. 
  - I won’t recommend it for production apps though since libs like #stenciljs have a great set of build tools, linters and optimizers in place.
- Oh yes. Occasionally bring in lit-html when I need data binding in a performant manner. 
  - Outside of that though, the DOM has everything I need!
  - Things like a static getter for ‘tagName’ and also one called ‘register’ that contains the call to `customElements.define()` .
  - The tagName allows use in templates of other components, and the register helps with testability.
- Not anymore. Created myself a base class when I did, plus a few small utilities for creating DOM from template strings.
  - This is where I’d ended up too (more or less). 

    - I still use my own lil toolkit for side project stuff, but for work I use Lit now.
    - Every so often I do still write something for work that doesn’t use anything external, but those are unusual cases.

- Absolutely! For me one of the best features for raw web components is extending native HTML elements

- ## list: Data fetching in #reactjs
- https://twitter.com/cse_as/status/1349025492389613570
  - There are a lot of strong opinions about this in the community about what's the best method. 
  - Here's an overview of all the different methods available with pros and cons
- axios
  - In a small application with no routes, if you want to quickly put together something, 

    - you can use a regular fetch/axios inside a `useEffect()` hook and store the response in a `useState()` variable.

  - Pro: Quick setup
  - Con: No caching, your data disappears on new routes
- react-query
  - With this, you can stick your async API calling function inside a hook, 

    - give the API call a name and global caching will be automatically handled for you.

  - Pro: Beginner-friendly, each component can handle data on it's own
  - Con: Relatively new library
- redux-saga
  - This middleware helps you push your API call response to the redux store for storing into global state. 

    - You control everything from fetching the data to how it is stored & retrieved.

  - Pro: You'll find this used in many large applications
  - Con: Lot of boilerplate
- redux-thunk
  - Another redux middleware that can be used to perform async tasks.
  - Pro: Slightly easier to understand than redux-saga, great for new applications, built into ReduxToolkit
  - Con: Existing applications might've already setup redux-saga so you'll need to learn that too
-  Apollo Client
  - This is the go-to library if you've already decided that you want a GraphQL backend.
  - Pro: Has built-in caching, can be used for global state management, very popular
  - Con: You'll need to convert all your APIs to GraphQL
- Personal opinion:
  - Use react-query for handling all data coming from an API. 
  - Use ReduxToolkit for anything left needed in global state.
  - This setup is easy to learn & understand, scales well, minimises the code you need to write & you don't need to learn sagas, thunks or GraphQL.

- ## We can use the `unknown` type in TypeScript when we don't know the type of a variable. 
- https://twitter.com/benmvp/status/1348784718808899586
  - I've found it most useful for functions that are passing thru data to another function
- `unknown` is likely preferable to `any` cuz we can't reassign it, manipulate it or pass it to a function
  - it says to me: "this type is unknown"
  - `any` (which allows anything) says "I was unable/unwilling to determine the type"
  - Type narrowing does make `unknown` usable tho
  - Generics are another good alternative to `any` but that's a whole other topic  

- ## list: what's your favorite transactional email API and why?
- https://twitter.com/swyx/status/1349028510786994176
  - for nice-looking, simple, reliable, API-sent email for customer fulfilment. I've really only used nodemailer before!
- AWS SES - I wrote a blog post about using it
- @SendGrid *was* great, but recently their support has been absolutely non-existent since acquisition by @twilio
- I'm using @Mail_Gun . 
  - Affordable and reliable. 
  - You can send mails via SMTP and their API. 
  - For legal reasons it's also important for me that you can select EU (European Union) as a region.
  - I'm from Germany and it's about GDPR. Also, depending on your product and industry, customers expect you to use services with servers in Europe.
- Sendgrid API, at least from Python, is really simple. I prefer it to using SMTP directly.
- i think the IH favorite is @postmarkapp. they also recently added broadcasts. 
  - i use sendgrid and it's also fine for transactional emails, but i do not recommend their marketing email product.
- +1 for postmark. 
  - I've found it has significantly faster and better delivery than mailgun. 
  - This is super important if you're doing passwordless auth

- ## dilemma: 1.0 is pretty much beta but everyone jumps on the new hotness anyway. 
- https://twitter.com/devongovett/status/1349015005371506696
  - But no one will try 2.0 beta even if it’s more stable than 1.x because it says “beta”. 
  - Version numbers are hard
- A major version bump tells me things that were working before can stop working. 
  - If a release is only making things more stable why would you bump the version by a major version number?
- I didn't know at about Parcel 2 initially because the tooling in VSCode/CodeSandbox on hover only showed 1.x. 
  - A blind npm install gets you the same. 
  - When it isn't on the latest tag the numbers of people using will always be significantly smaller.
  - Would it be weird for the default installed tag to be a beta?

    - That's what vite does I think, although they never reach v1... They went from v1 alpha to v2 beta.

- If there are any breaking changes that will impact many users and/or are hard to migrate prioritize them in 2.0. 
  - Otherwise, they can be deferred to Parcel 3 ~1 year after Parcel 2.0 stable.
  - We are trying to do this for Babel 8, to avoid the Babel 7 situation.
  - If you manage to only defer small breaking changes to 3.0, there is nothing wrong with not waiting years before a new major since for most users it will be easy to upgrade anyway.

- ## Let's Bring Spacer GIFs Back!
- https://www.joshwcomeau.com/react/modern-spacer-gif/
- Instead of using margin, I create a new element explicitly to add some space between the icon and text!
- In the late 90s, if you were to pop open the source of a typical website, you'd likely encounter this curious fella
  - `<img alt="" src="spacer.gif" width="1" height="1" />`

- CSS didn't exist yet, and web layouts were built using HTML tables. 
  - GIFs were used because GIFs were the only image format that supported transparency (this is pre-PNG). 
  - Our spacer friend consisted of a single transparent pixel, a completely empty image.
- CSS was added to the browser to offer an alternative to styling. 
  - The language wasn't originally designed with layout in mind, 
  - but developers quickly realized that — through the use of some clever float hacks — it could entirely replace table layouts!
- By separating our concerns
  - HTML for structure, CSS for layout and presentation, JS for behaviour
  - we had a convention that would help us keep complexity down, ultimately making it easier to maintain things.
- In the original Jambalaya table-layout days, the spacer GIF was a tasty complementary ingredient. 
  - It didn't taste so good when we switched to making deconstructed sandwiches. 
  - But now that many of us are working with component-driven architectures, our code might benefit from a pinch of spacer GIF.
- Originally, my `<Spacer>` component rendered a `div` instead of a `span` , but I found it was a little limiting. 
  - According to the HTML spec `div` s aren't supposed to be put within certain elements, like `p` and `button` .

- ## Quiz time! for histroy back
- https://twitter.com/ryanflorence/status/1346562678869790720
  - No JavaScript on the page, normal document requests:

    - You land at http://example.com
    - You click a link to /page.html
    - Again, you click a link to /page.html
    - You click the browser back button

- Turns out when you go to the same URL, the browser still makes a document request to the server, still gets the a fresh page, 
  - but it *does not* push a new entry into the stack, it *replaces* the current one!
  - It's the same as clicking "refresh", and that makes sense.
  - 结果是回到example.com
- 实践测试
  - 在空标签页打开 a.html，然后按返回键，会回到空标签页
  - 在空标签页打开 a.html，再点刷新按钮，然后按返回键，也会回到空标签页

- ## To help me decide exactly what my media query tweak points should be.
- https://twitter.com/Malarkey/status/1345873190380253187
- If I had to print something for debug purpose, I'd prefer to show a different content, with the information of the media applied, on a `body::before` pseudo element absolutely positioned.
- I went with a `content:"XS";`  `content: "S"/"M" ` and so on. 
  - I've got this `debug.sass` file damn full of ways to figure out common gotchas behind html classes like debug_viewport debug_grids and so on. 
  - It's annoying to maintain but it has saved me tons of time @ the job at least twice
- [Custom properties for breakpoint debugging_201802](https://thatemil.com/blog/2018/02/23/custom-properties-breakpoint-debugging/)

- ## State machines are great, so why aren’t we rewriting all of our async/await code to them?
- https://twitter.com/dan_abramov/status/1344502932704788480
- the simple answer: async/await is easier. 
  - It leaves out edge cases. When you include the edge cases, async/await is more complex... So developers just hope for the best.
- state machines are great at representing systems that have cycles & many possible transitions between each state, 
  - async await is better for relatively linear paths with limited branching
  - its a little bit like how regular expressions work well for the state machines that represent string matching, since those also tend to have lots of sequential states with no branches
  - Indeed. And regexes are generally convertible to pointer bumping string scanning code, with loops replacing eager Kleene star. 
  - See how hand-written lexers implement regex matching in code where lex would use a state machine. Instruction pointer replaces state code.
  - Regexes and automata are isomorphic, a regex is literally a state machine
- This made me think of XHR’s `onreadystatechange` event and how devs were really really happy to use `$.get` instead of considering all of the possible ready states. 
- Babel rewrites your async/await code into small state machines
  - As well as any of your code is executed on hardware state machines
  - So here you go, exactly as you asked
- I'd much rather go the other way and remove state machines and caching layers from async/await
  - [callback based, simplified async/await](https://es.discourse.group/t/callback-based-simplified-async-await/343)

- ## What advice were you given for your career that turned out to be a complete waste of time and effort?
- https://twitter.com/buildsghost/status/1343650869904986112
- I was told to go take a bunch of night classes on computer science by two MIT grads if I ever wanted to be "serious" about programming.
  - I took some free student-taught classes, 
  - and we spent months learning languages I have not used since.
- This isn't about tech, but when I was in school to be a licensed massage therapist.
  - I had a teacher tell us that we should work our first year *for free* in order to build a client base.
  - Thankfully, I didn't, but I am sure some folks listened.
- You *need* to be good in math
- Go to conferences.
- I was told that how people feel in a moment is more important than the outcome of the work. 
  - Now, I couldn't be happier to work somewhere frank, timely, respectful feedback is foundational to the culture. 
  - Spoiler alert: great work outcomes _make people feel good_
- Was also told "PHP is dead, JSP is the future" in around 2006. They were very wrong.

- ## I want to *scale* a div and all of its contents to fully fit wall-to-wall inside its container div. 
- https://twitter.com/erikras/status/1343480294654046209
- Similar to what `background-size: contain;` can do for images. Possible in CSS only? JS ok, too.
- I think scaling is the wrong thing for my use case.

- ## A year ago I made a bet on full-stack JS and switched my focus from @laravelphp to Node.js. A year later, I found that Node mostly just slowed me down.
- https://twitter.com/tylerlwsmith/status/1341557868571422722
- Server-rendered React components look really exciting. 
  - I just wish the Node ecosystem was less fragmented and more productive so it would be easier to take full advantage of it.
  - Until then, I can continue to get a ton of productivity out of Laravel 
- React Router is the reason I love React. 
  - It also has the most innovative front-end libraries, and the front-end is the part that users interact with. 
  - React also works great with extremely complicated state management.

- ## [Reflecting on a year with Node.js and why I should have stuck with Laravel_202012](https://dev.to/tylerlwsmith/reflecting-on-a-year-with-node-js-and-why-i-should-have-stuck-with-laravel-e5a)
- Earlier this year, I was two months into building a full-stack JavaScript app. 
  - I used an Express server, set up Next.js for server-side rendering, added Chokidar for instant server reloading, used Next.js's Webpack config to compile my server's TypeScript code, hooked up cookie authentication with Argon2 encryption, found the perfect Node ORM, and had the app running in separate containers for Node, PostgreSQL and Redis.
- After two months of hard work, all I had built was a mediocre server-rendered CRUD app hacked together with two-dozen NPM libraries. 
  - If I had used Laravel and jQuery, I could have built this all in a weekend.
- After a year of building Node.js apps, I discovered I was spending more time piecing together tools than writing application code. 
  - 这是因为基于php的传统web开发框架laravel已经非常成熟，工具丰富

    - 基于nodejs作为服务端的web开发框架，还处于快速发展阶段，可选工具不够多，并且功能不够丰富

  - Laravel gives me 80% of my tooling out-of-the-box for 20% of the work. 
  - If moving fast is important to you, you should consider batteries-included frameworks like Laravel and Rails first.
- What I've learned is if you want to develop applications quickly, it isn't about staying in one language: 
  - it's about reaching for the tools that let you move quickly, whatever those are.
  - I use React for most of my front-end web applications, and Laravel gives me the tools I need to spin up the backend quickly. 
- Rather than sharing code between the front-end and back-end, I've learned to 
  - move almost all of my business and validation logic to the back-end, 
  - and I consume it on the front-end via API. 
  - Just because you're using two different languages doesn't mean you need to write the same code twice.
- I prefer Laravel over Node.js because it lets me move fast.

- discussion

- I like Adonis. And Sails.js. And Nest.js. Loopback also looks cool.
  - I've never adopted any of them for a few reasons though:
  - 总结：支持node的大公司少了，工具不多
  - Lack of adoption. 
    - None of the batteries-included Node.js frameworks have major adoption, so I have to figure out how to integrate other tools myself.
    - It also means if I run into a problem, there are far fewer resources available than Laravel.
  - Uncertain future. 
    - Adonis is mostly carried by one person. Sails is maintained by a company out of Texas. 
    - For long term projects, using Adonis feels like a risk.
  - Lack of first-party integrations
    - Laravel kills it with the amount of first party integrations they have. 
    - It's a compelling reason to choose Laravel over Node

- ## if I was building a CMS using MongoDB would you tell me to stop immediately? If so, why?
- https://twitter.com/JakeDohm/status/1341892219511459842
- Every developer build a CMS at some point in their career. 
  - Might as well check it off of your bucket list.
- I’m going to get technical and ask what type of content your CMS would be housing. 
- That would determine DB for me. 
- Mongo doesn’t seem appropriate for most content I’ve worked with, as CMS tends to be highly relational.
- Maker me: Build whatever you want with whatever tools you want.
- Developer me: Don't use MongoDB, most of your stuff with be relational, 
  - and in the event you cannot use relational, use JSONB data type in PostgreSQL.

# ref

- [Custom Properties as State](https://css-tricks.com/custom-properties-as-state/)
