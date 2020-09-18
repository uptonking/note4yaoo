---
title: lib-react-table-dev
tags: [lib, list, react-table]
created: '2020-07-13T02:29:20.525Z'
modified: '2020-07-14T10:27:12.335Z'
---

# lib-react-table-dev

## react-table表格实现的ui结构层次

- ### useBlockLayout
  - 必须设置cell的width，使用行内样式设置
- div-table
  - div-thead
    - row/tr
    - row/tr
      - columnheader/th
    - row/tr
  - div-tbody/rowgroup
    - row/tr
    - row/tr
      - cell/td
    - row/tr

``` CSS
.table {
  display: inline-block;
  border-spacing: 0;
  border: 1px solid black;
}

/* 设置表头行或数据行 */
.row {
  display: flex;
  width: 710px;
}

.cell,
.columnheader {
  display: inline-block;
  box-sizing: border-box;
  width: 150px;
  margin: 0;
  padding: 0.5rem;
  border-bottom: 1px solid black;
  border-right: 1px solid black;
  /* font-weight: bold; */
}

.rowgroup {}

.cell {}
```

- ### useAbsoluteLayout
- div-table
  - div-thead
    - row-header-group
    - row-header-group
      - columnheader
    - row/header-group
  - rowgroup/rows
    - row-body
    - row-body
      - cell
    - row-body

``` CSS
.table {
  box-sizing: border-box;
  max-width: 700px;
  overflow-x: auto;
  border: 1px solid #000;
}

.row-header-group {
  position: relative;
  width: 710px;
  height: 32px;
  border-bottom: 1px solid #000;
}

.cell,
.columnheader {
  position: absolute;
  top: 0px;
  left: 150px;
  width: 150px;
  height: 100%;
  padding-left: 5px;
  border-right: 1px solid #000;
  line-height: 30px;
}

.rowgroup {
  position: relative;
  width: 710px;
  overflow-y: auto;
}

.row-body {
  position: relative;
  width: 710px;
  height: 32px;
  border-bottom: 1px solid #000;
}

.cell {}
```

- ### useFlexLayout
- div-table
  - div-thead
    - row-tr
    - row-tr
      - columnheader
    - row-tr
  - div-tbody
    - row-tr
    - row-tr
      - cell
    - row-tr

``` CSS
.table {
  min-width: 735px;
  border-spacing: 0;
  border: 1px solid black;
}

/* todo flex without container 表头行和数据行的样式 */
.row-tr {
  flex: 1 0 auto;
  display: flex;
  min-width: 215px;
  border-bottom: 1px solid black;
}

.cell,
.columnheader {
  position: relative;
  flex: 150 0 auto;
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  box-sizing: border-box;
  width: 150px;
  min-width: 30px;
  padding: 0.5rem;
  margin: 0;
  border-right: 1px solid black;
}

.tbody {
  display: block;
  height: 250px;
  overflow-x: hidden;
  overflow-y: scroll;
}

.cell {}
```

## guide

- ### [Design Data Tables with Real Tables: Part 1](https://learnreact.design/2020/02/08/design-data-tables-with-real-tables-part-1)
  - [Data Grid (Table) Framer package](https://packages.framer.com/package/lintonye/data-grid-table)
  - https://github.com/lintonye/tables

- ### [What big things do you think will happen in the JavaScript ecosystem in the next 5 years?](https://twitter.com/kentcdodds/status/1237417106594861056)
  - I would say that in 5 years, we'll see:
    - a few more nice syntax improvements
    - improvements around package management
    - bundling
    - delivery
    - Frameworks will continue to compete and thrive
    - ++ Patterns
  - I think there's a good chance that some of the more CPU-intensive parts of our current build tools (like Terser/Uglify) will be replaced by WASM equivalents (maybe written in Rust?).  SWC is already trying to do this for Babel.

- ### [table vs div](https://twitter.com/tannerlinsley/status/1254534413741780992)
- `<table>` Table
  - Auto col width
  - Native aria/structure
  - Native col/row span
  - No infinite scroll
  - No sticky/pinned cols
- `<div>` Table
  - Manual col width
  - Resizable cols
  - Simulated col/row span
  - Infinite Scroll
  - Sticky cols
- ref
  - [aria grid pattern](https://www.w3.org/TR/wai-aria-practices/#grid)
  - today has left me with a pretty solid plan that anything that is missing from `<table>` grids can *almost* be replicated fully in a `<div>` grid, plus all the other great possibilities you gain by not locking yourself into the `<table>` spec.
    - What interesting is that *most* things that native tables have over div tables can be ported to div tables including a11y, col/rowSpan, etc.
    - Auto col-width though is problematic. There's just not a good solution that I've seen to do that.
  - I chose table over div.  
    - The no sticky columns thing can be solved, and flawlessly-smooth infinite scroll is low on my list.
    - The biggest issue for me is the incessant tinkering with column widths when using a div, especially when headers, footers, and grouping is involved.
    - How did you solve sticky cols?
    - Two tables side by side.  One fixed and one scrolling.
  - The most important one IMO to cross-port to divs properly is the auto width or at the very least, flex-fill for when tables are wide and columns can fill the extra space
    - not an easy one. We did that in the past in a custom table implementation (2-pass render) but I was never proud of it. 
    - I like the flex-fill approach though. I think having something pragmatic enough will be ok. It's not that auto-width is required for any table out there.
  - You can get auto column width with div tables :). We do this at my work. We do a two-pass render to measure and it's fast enough most of the time. Working on an implementation with CSS Grid that I'll write about soon.
  - Sticker headers lets the user quickly be able to refer to what a cell represents in large tables. Resizing also helps expand/collapse columns that are more/less important or have dynamic contents. Default column widths can optimize for less text overflow.
    - [not ssr friendly yet](https://ministrycentered.github.io/ui-kit/datatable)

## pieces

- `useGetLatest(instanceRef.current)` how it's helping avoiding memory leaks 
  - `const getInstance = useGetLatest(instanceRef.current);`
  - Instead of using `instanceRef.current` all over the place, you just use `getInstance()` which just looks better imo less clutter(n, 杂乱，混乱)
    - as for memory leaks, it’s not the getLatest implementation that does this. It’s just the fact that it’s used at all as opposed to creating closures around `instanceRef.current`
  - Converted almost all usages of `instanceRef.current` to use `useGetLatest(instanceRef.current)` to help with avoiding memory leaks and to be more terse.
    - It avoids closing over stale instance properties and holding on to them in memory. 
    - Only when they are needed, they are accessed on demand though the getter.
    - Could you please expand on why calling a function avoids closing over state instance properties?
    - I'm definitely not an expert, but I know that previously when we would simply close over the instance we were "snapshotting" the entire instances in a closure, and as long as that closure stuck around, that memory for the instance snapshot would be there.
    - Some of that doesn't matter if you are actually reusing or mutating a single instance, but if you are handling computed or immutable data that is changing, then you can potentially be hanging on to a lot of unused data for no reason.
    - By just storing a reference to a getter function, you aren't closing over the data, just the getter. 
    - Thus, the memory of the result of that getter doesn't come into play until you use it, which in the case of all of the callbacks and API used in something like React Table is alot
  - ref
    - https://twitter.com/tannerlinsley/status/1257068142242656256
    - https://spectrum.chat/react-table/general/v7-can-some-one-explain-usegetlatest-instanceref-current~54763a00-66ae-4211-bb35-52ca25686546

- FWIW your React Table library is actually impossible to fully type properly. 
  - Its architecture and typescript are not friends because the API of the hook changes based on runtime arguments. 
  - Converting it to strict TS would need changes

- Column “Pivoting” !== Row Grouping
  - Pivoting is the operation of taking unique row values from a column and materializing new columns from them, eg. A column for each salesperson’s total sales, derived from a sales history.
  - So, next time you see a library that is advertising itself as a "Pivot Table", you'll know how to actually tell if it's a true pivot table, or if it's just row-grouping and aggregating.

- If you had a data grid with sticky headers and pinned columns, which of the following would you prefer?
  1. Sticky Header alignment lag when scrolling horizontally
  2. Pinned Column alignment lag when scrolling vertically
  - To achieve the same results I would need to break out of the render phase for a massive amount of the logic surrounding virtualization which would suck for DX
  - I've been able to achieve perfect vertical alignment with zero lag when scrolling and chose to do artificial syncing to the headers. In a prod build, the scroll is near perfect, but depends on the CPU speed.
  - for me, definitely 1. Our users do waaaay more vertical scrolling than horizontal scrolling.
  - I agree, if we have paging, we can make vertical scrolling unnecessary (or at least less significant than vertical).

- If you had a data grid with sticky headers and pinned columns, [which of the following would you prefer?](https://twitter.com/tannerlinsley/status/1262438548344619008)
  1. Headers and Pinned column alignment lag by a frame or two when scrolling, but scrolls at 60fps
  2. Zero alignment lag, but scrolls at 24fps
  - I forgot to mention that the no-lag 24fps version would be a transform-translate simulated scroll, whereas the lagged-60fps version would be a native scroll (still virtualized)
  - I think it of as - Not having 60fps is a bad ux because slow/blocking scroll is pain to users

- Any idea on how to make it work with dynamic height and width on the div? 
  - Check out the dynamic example. 
  - The secret sauce is the `measureRef` that you place on your element that you want to measure. The rest is auto.

- Well, the amazing thing about what I'm building is that you can not only theme the styles of the grid, but also the markup. So if you want to "retrofit" the table for IE 11, that would be easy to do with some polyfills or by just using a theme that uses absolute positioning.
  - Using css grid with grid-area: 1/1

- [Would you pay a per-month micro-subscription for a massively-full-featured, bullet-proof, drop-in React Table component?](https://twitter.com/tannerlinsley/status/1255916019404517377)
  - no

- If you ever find yourself worrying about triggering an "unnecessary" rerender in your React App, then you're doing something wrong.
  - Rerenders === Your UI is in sync with your state
  - Code for rerenders to happen. A lot of them. At any time. All the time.
  - Make them fast, useMemo
  - Rule of thumb, don't memoize expensive components, memoize the expensive work/computation/cpu that they are doing.
  - [Why I almost always `useMemo` and `useCallback` ](https://dev.to/andyrichardsonn/why-i-almost-always-usememo-and-usecallback-4776)

- Why is wrapping every component in React.memo() a bad thing ?
  - `export default React.memo(MyConponent)`
  - So many things. Over checking for changes, children prop somewhat invalidates memo, your app will likely get out of sync from state from not rerendering. Don’t do that. You would be better off not using it at all.

- Do you try to useMemo everything from the get go? A balance? I find it time consuming to track down what needs to be useMemo'd after the fact. Often resorting to manually logging which dependency key has changed -- maybe the are developer tools for this I haven't found.
  1. Don't memoize unless required because of other useEffect/useMemo/useCallback dependency arrays
  2. Wait for slow renders to show up. They might not at all!
  3. Profile the slow render
  4. useMemo computations making it slow
  - I always try to avoid memoizing component ouput, too

- do you have mental model for when memoization should happen "inside" or "outside" of a component?
  - I always found it a bit strange that react-table documented props that need to memoized rather than just doing their own data diffing.
  - Requiring memoized objects is not strange at all for custom hooks. In fact, if you use hooks, you are already required to pass arrays of memoized deps to useEffect, useMemo, and useCallback, the only difference is where you pass them: `useEffect(..., [dep])` , `useTable({ dep })`
  - I think there is still a place for diffing data inside of a custom hook (and thus not requiring your users to memoize) for certain optimization cases, but I guess that react-table avoids that need.
  - For example (I'm guessing here) if you append a new column to your table, the other columns' values won't be recomputed because they would still each have stable accessors across the render.
  - Yes, true. I've actually modeled some of React Table's internals to do that, but it doesn't take very long for the internals to get very complicated and bloated. 
  - In my experience it's better to exhaust(用完) all of your resources making an atomic version that's as fast as possible first

- I think I just figured out “semi-controlled components” maybe I’ll call them “suggestible components”
  - what would be a use case?
  - Setting scroll position when you need to without controlling it always.
  - Sidebars that can be toggled on their own, but if the window is big it can’t.
  - Anything that almost always can manage it’s own state but one random little interaction needs to change it.
  - https://twitter.com/ryanflorence/status/1252023520701280256

- Rendering 100k rows = bad
  - Rendering only 10 rows at a time because that's how big the virtual window is and breaking search functionality = bad
  - To be fair, I don't know the best solution for this. Searching a webpage shouldn't be broken by virtualization.
  - Sometimes searching a web requires tools catered for the data. Eg. a table with full-text search that can span both pagination and virtualization.

- Learned about `useLatestValue` utility hook which provides a static callback function so child components where you pass the callback won't be updated. Thanks for idea 

@tannerlinsley

  - I believe setting refs in render is not safe in concurrent mode
  - It needs to be synchronously set, otherwise it won’t be up to date for later use in the render function
  - This won’t work with newer features like useTransition because it assumes that every render immediately gets committed to the screen. But we want to be able to do renders in memory without committing them until later.
  - Think of rendering as a calculation. If you’re mutating something during a calculation, it’s not safe to interrupt it or delay applying its results.
  - ref
    - https://twitter.com/NoahZinsmeister/status/1251288355117109250
    - https://twitter.com/dan_abramov/status/1253663995749453825

- [What is your favourite API to make http requests in js?](https://twitter.com/FrancescoCiull4/status/1248711341243850765)
  - xmlhttprequest
  - fetch
  - axios
  - $.ajax
  - other
  - If I'm working with framework axios, with vanilla I'll use fetch
  - I’d actually go for xml, yes i also use fetch, but in vanilla its no package needed, simpler, better error and wrap it in a promise and you have a better fetch 
  - Axios is useful if you do SSR.
    - Because nodejs doesn't include the fetch API.
    - So if your code runs on both the back end and the front, it's an easy way to not do a test.
    - Fetch is a clean browser API that everyone should use.
  - Axios: Perfect handling of TCP & HTTP error, Hybrid (NodeJs and Browsers)

- [What are the biggest pain points for you and your team building a React App?](https://twitter.com/ryanflorence/status/1249841029374595072)
  - Bundling / code-splitting ...
  - Server Rendering
  - Fetching/caching/reading data
  - Boot / Runtime performance
  - UI components (dropdowns, grids, etc.)
  - Developer ergonomics
  - other stuff ...

- [TLDR: Fetch is way easier to use than XHR, but XHR can be better in some situations, specifically with more explicit error handling](https://twitter.com/dan_abramov/status/1246251834324516868)
  - Tbh I think when we rewrite React docs to use Hooks, this is what the section on "ad hoc data fetching" should look like. (At least until we have something better.) XHR seems way more convenient to wrap in a custom Hook than fetch, and built-in cancellation is neat.
  - Promises are not cancellable. Also known as the “no backsies” rule.
  - There were also facilities for canceling cancellable promises (like XHR, timers, media playback). Plus, the hierarchy of nested proxies could negotiate whether the component could be allowed to unmount, through guarded promises (e.g. a pending save).

- [promises make hooks look bad](https://twitter.com/tannerlinsley/status/1246274175448145920)

- How do you persist the user's authenticated state between refreshes? 
  - How does the auth service know that the user making the request is authenticated without requiring them to authenticate?
  - I don't, but my oauth provider does (which I'm happy to outsource, since oauth security is something I never want to be responsible for).
  - I'm not sure how they do it, but they can re authenticate invisibly (probably using a hidden iframe or something) and quickly on page reload.
  - The auth provider sets an httpOnly cookie on their own domain. On app start, you redirect the user to your auth provider (popup, redirect or hidden iFrame), you get the access token back and dont care if user had to enter a password or had a valid cookie.
  - The other great thing about this is that you can set your token expiration to something ridiculously short-term and not have a lot of adverse effects. Token expires, client is notified (or gets rejected), silently auths again via oauth provider, gets a new short-lived token.
  - So basically, @tannerlinsley, are you saying that there will be a request on every page load/reload just for the auth?
  - If you want to completely avoid storing the key, then yes.
  - either HTTP-only JWT w/CRSF protection, or re-auth every pageload
  - To be clear, I mean asking the user for their username/password on every reload is a non-starter.
  - that doesn't need to happen. All I'm referring to is outsourcing the auth/invisibleAuth/reAuth flow to the oauth provider so you don't have to worry about storing anything or much security details at all.
  - Yeah, that makes sense
    - I'm thinking that the "solution" is either to have your own auth server for cookies or use something like auth0.
    - In any case, HTTP Cookies seems like the *only* solution for the web for secure communication of tokens.
    - https://twitter.com/kentcdodds/status/1245780612218142720

- [How does "JAMStack" solve the problem of securely storing authentication tokens?](https://twitter.com/drunknhik/status/1245743256798998529)
  - localStorage is accessible by third party scripts, so HTTP only cookies are recommended to side-step this.
  - You could use a tool like @Firebase auth, @auth0, or create a serverless function endpoint, the 'A' in JAM, to authenticate against your own DB and return the cookie to the client-side. These are just a few options.  I prefer the @Firebase auth approach.
  - From what I understand, the recommended practice is to pass a JWT with any API request where the service behind it can decrypt and extract the user's data.
    - but where do you store the JWT is the question
    - Since the JWT signature is encrypted, storing it on the locale storage does present a threat. Even if a hacker gets a hold of it, s/he will need to decrypt and re-encrypt it back with secrets S/he do not have. Also these tokens should have very short TTL.
    - If I get a hold of a JWT, I can just send it back with any HTTP request. Who cares if you have the secret or not.
    - I think that secured cookies are the best option here (given you protect against XSRF), but I also read that in-memory might be a good option as well
  - In memory is what I usually do, because the apps I create require login each time, and use SSO. So if the refresh, it just logs them in again...no problem. Not everybody can do that though.
  - An interesting pattern I've seen lately is to split the token: save the public part in localstorage or a normal cookie (to read the Scopes and whatnot) and the encrypted part in an HTTP only cookie.
    - This of course requires the API requiring that token  to put it back together
  - Technically you're never supposed to store keys, even in LS. 
    - The way I do it, the token is always retrieved (hopefully invisibly) from auth service and stored in-memory on every page load.
    - Refresh token can be stored in local storage or as cookie since it will be useless whenever access token gets revoked.
    - I would say that's highly discouraged. Any oauth provider will tell you that, too. While it may be possible, you are still assuming some level of risk within the timeframe before it is revoked. Someone gets that key, and they can become that person, even if it's short-lived.
    - I just saw you said "refresh" token. It's a bit different, yes, but I would still take extreme caution storing any keys in the client that could potentially lead to impersonation.
    - Second thought, using local storage for refresh token is not a good idea, but using secure cookie for it along with the short-lived access token sounds okay to me. Or is there any other way to achieve keeping session going with the page refresh?
    - You store a session ID in an httpOnly cookie, and that session id is matched on the server to a session entry with userID in it. That's standard session authentication, and it's the best way to to handle persistent login
    - [stop using jwt](https://t.co/ynPDoXdv9k?amp=1)

- Remix It's still early and our cache is closely coupled to locations, but we intend to support things like SWR, react-query, Relay, Apollo. etc. 
  - They all have their own cache that we'll need to interact with, but we think location based caching is an important user expectation.
  - If only to reinforce your assumptions, a vast majority of React Query use cases I see in the wild are 1:1 with route params. List/Item/List/Item hierarchies all the way.
  - Apps will need to make their own choices here, but, 
    - By default a browser will add a new history entry if you click on a link from one.html to one.html.
    - When you click back it will restore scroll position, and you may want to see what the data looked like before your last action
  - So at the core, the cache allows different data at different locations for the same route and same route parameters because that's how browser caching works w/o client side routing (it even ignores your http cache headers when you click back!)
  - We'll support both though.
  - https://twitter.com/tannerlinsley/status/1253187840147517442

- WRT(With respect to) React Table, I'm not sure what's been worse: all of the requests I got from devs asking for more control over the UI for 2+ years, or all of the hate I'm now getting from devs wondering why the heck react table is just a hook now

- Sometimes destructuring your JS objects can ultimately hurt your productivity, especially when destructuring generic variable names or multiple instances of the same type of object.
  - For a change of pace, embrace that dot notation and don't be afraid to `use?.optional?.chaining` !

- Dan keeps telling me that they won't be throwing promises in the future, but nobody's given me any idea what they'll change it to. My only thought is that we'll throw *something* just maybe not promises Man shrugging

- Avoid using `React.memo` on components that use `props.children` ! 
  - Those children will almost certainly change every render, so React.memo will never prevent the component from re-rendering, making it unnecessary overhead 

- [I need to build a presentation for a talk. What should I use?](https://twitter.com/tannerlinsley/status/1217607012416020480)
  - apple keynote
  - mdx deck
  - slides.com

- [React Table 7 - Hooks based library](https://thewidlarzgroup.com/react-table-7/)
  - https://github.com/TheWidlarzGroup/RT7-example
  - https://rt7-example.netlify.app/
  - hooks-table-demo-with-pagination
