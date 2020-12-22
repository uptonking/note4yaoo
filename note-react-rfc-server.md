---
title: note-react-rfc-server
tags: [react, rfc]
created: '2020-12-22T14:08:04.179Z'
modified: '2020-12-22T14:08:27.952Z'
---

# note-react-rfc-server

## react server components

### [faq](https://github.com/reactjs/rfcs/blob/2b3ab544f46f74b9035d7768c143dc2efbacedb6/text/0000-server-components.md#faq)

- Does this replace SSR?
  - No, they’re complementary. 
  - SSR is primarily a technique to quickly display a non-interactive version of client components. 
  - You still need to pay the cost of downloading, parsing, and executing those Client Components after the initial HTML is loaded.
  - You can combine Server Components and SSR, where Server Components render first, with Client Components rendering into HTML for fast non-interactive display while they are hydrated. 
  - When combined in this way you still get fast startup, but you also dramatically reduce the amount of JS that needs to be downloaded on the client.

- Does this replace GraphQL?
  - GraphQL is one approach for building API endpoints that can help apps reduce under/over-fetching and reduce round trips (among other features)
  - Server Components are focused on building user interfaces.
  - developers may find it helpful to use GraphQL client to load data for their Server Components too. 

- Is this just working around the lack of a compiler in JavaScript?
  - No, a static compiler can help with some things 
  - but we found that many real world apps have a lot of dynamic branches such as user-specific options, A/B tests, feature flags, etc. that make static optimizations hit a limit. 

- Are you reinventing PHP/JSP/whatever for the front end?
  - The history of application development is a series of pendulum swings between “thin” and "thick" clients
  - But the reality is that some parts of any app are more "static" - non-interactive, don’t need immediate data-consistency
  - while others are "dynamic" and need interactivity and immediate responsiveness. 
  - Neither pure server rendering or pure client rendering are ideal for all situations. 
  - Server Components — when combined with existing Client Components — allow developers to write each part of their app using the approach that makes the most sense, 
  - while sharing a single language and framework and even sharing code across server and client.

- Is this in production at Facebook?
  - We are running an experiment with a small number of users on a single page, 
  - with encouraging results (already ~30% product code size reduction). 
  - We expect more savings in an app designed with Server Components for the start.

- Is this specific to Next.js?
  - No. We are partnering with Next.js to build out an initial integration. 
  - However, Server Components are designed from the beginning to be used with any framework or integrated into custom application setups. 
  - Given the scope of Server Components — including router, bundler, and server/client coordination aspects
  - we felt that a high-quality initial integration would allow us to demonstrate the setup to other developers.

- Why don’t you just use HTML instead of a custom protocol?
  - We do want to use streaming HTML for the initial render, 
  - but the custom protocol lets us transfer data (component props), and reconcile trees so that the client state as well as DOM focus/scroll/state doesn’t get blown away.

- Isn’t static generation better?
  - Static generation is great for some use cases, and you can run Server Components at build time for that.

- Do I have to read my database directly from components?
  - No, although it might be convenient when you’re starting up. 
  - The goal is to be able to scale up or down, and let you move freely between direct database access, microservices, or other approaches without rewriting your app. 
  - You can also build JavaScript abstractions that let you manage batching queries and provide authorization layers.

- What is the response format?
  - It’s like JSON, but with “slots” that can be filled in later. 
  - This lets us stream content in stages, breadth-first. 
  - Suspense boundaries mark intentionally designed visual state so we can start showing the result before all of it has fully streamed in. 
  - This protocol is a richer form that can also be converted to an HTML stream in order to speed up the initial, non-interactive render.

- How does this relate to Suspense?
  - The Server Components data fetching APIs are integrated with Suspense. 
  - We use Suspense to provide loading states and unblock parts of the stream so that the client can show something before the whole response is done.

- How does this relate to Concurrent Mode?
  - Concurrent Mode is a set of optimizations across React and also integrates with Server Components. 
  - For example, Concurrent Mode lets us start rendering Client Components as their data streams in, without waiting for the whole response to be finished.

- How do you do routing?
  - We don’t know yet. It’s an active area of research. 
  - There is a missing feature similar to Context for Server Context that we need to build into React first.

- Why not use async/await?
  - The React IO libraries used in the demo and RFC follow the conventions we've discussed previously for writing Suspense-compatible data-fetching APIs. 
  - Suspense-compatible APIs return data synchronously when it is already available, throw if there is an error, or "suspend" to indicate to React that they are unable to return a value. 
  - The mechanism for Suspending is to throw a `Promise` value. 
  - React uses resolution of the promise to know when the API may be ready to provide a value (or that it has failed) and to schedule an attempt to render the component again.
  - One new consideration in the design of Suspense from this proposal is that 
    - we would like to use a consistent API for accessing data across Server Components, Client Components, and Shared Components. 

- Are Server Components refetched whenever their props change?
  - No, Server Components in the middle of the tree won’t refetch when a parent Client component re-renders.
  - From the Client’s perspective, there are no Server Components at all
  - When a Server component needs to update, such as a result of a mutation, React will refetch the whole Server Component tree output that renders from top to bottom (though finer-grained invalidation is an active area of research). 
  - Currently, the Server Component tree starts at the root of the app, but we plan to allow more granular refetching from explicitly chosen entry points.

- Are you always refetching the whole app? Isn’t that slow?
  - We are planning to introduce a more granular refetching mechanism so that you have the option to refetch only a part of the screen, 
  - but it is not available yet.

- What are the performance benefits of Server Components?
  - Server Components let you put most of your data fetching on the server so that the client doesn’t need to make many requests. 
    - This also avoids client network waterfalls, which is typical for fetching in useEffect
  - Server Components also let you add non-interactive features to your app without increasing the bundle size. 
    - Moving features from the client to the server decreases the initial code size and client JS parse time. 

- Doesn’t always re-fetching the UI make interactions slow?
  - You can (and should) use Client components at any level of the tree for fast interactions. 
  - Also, you don’t want to always refetch — the fetched trees can stay in the client cache and be reused for navigations like back button.

- How is this different from PHP/Rails/etc?
  - You can reuse some components between Client and Server for use cases with different tradeoffs. 
  - E.g. Markdown renderer that offers live preview on the client but is rendered for consumption on the server. 
  - This is possible because they’re written in the same paradigm and language.

- Why not Rx?
  - Rx is a great solution for managing streams of data. 
  - Rx is a good fit for implementing a transport layer to receive the stream of rendered UI chunks that React creates on the server and stream them to the client.

### [pr: React Server Components](https://github.com/reactjs/rfcs/pull/188)

### [RFC: React Server Components](https://github.com/reactjs/rfcs/blob/2b3ab544f46f74b9035d7768c143dc2efbacedb6/text/0000-server-components.md)

- Server Components allow developers to build apps that span the server and client, 
  - combining the rich interactivity of client-side apps with the improved performance of traditional server rendering
- Server Components run only on the server and have zero impact on bundle-size.
  - Their code is never downloaded to clients, helping to reduce bundle sizes and improve startup time.
- Server Components can access server-side data sources, such as databases, files systems, or (micro)services.
- Server Components seamlessly integrate with Client Components — ie traditional React components. 
  - Server Components can load data on the server and pass it as props to Client Components, 
  - allowing the client to handle rendering the interactive parts of a page.
- Server Components can dynamically choose which Client Components to render, 
  - allowing clients to download just the minimal amount of code necessary to render a page.
- Server Components preserve client state when reloaded. 
  - This means that client state, focus, and even ongoing animations aren’t disrupted or reset when a Server Component tree is refetched.
- Server Components are rendered progressively and incrementally stream rendered units of the UI to the client. 
  - Combined with Suspense, this allows developers to craft intentional loading states and quickly show important content 
  - while waiting for the remainder of a page to load.
- Developers can also share code between the server and client, 
  - allowing a single component to be used to render a static version of some content on the server on one route
  - and an editable version of that content on the client in a different route.

``` JS
// Note.server.js - Server Component

import db from 'db.server';
// (A1) We import from NoteEditor.client.js - a Client Component.
import NoteEditor from 'NoteEditor.client';

function Note(props) {
  const { id, isEditing } = props;
  // (B) Can directly access server data sources during render, e.g. databases
  const note = db.posts.get(id);

  return (
    <div>
      <h1>{note.title}</h1>
      <section>{note.body}</section>
      {/* (A2) Dynamically render the editor only if necessary */}
      {isEditing 
        ? <NoteEditor note={note} />
        : null
      }
    </div>
  );
}
```

- **Motivation**
- Zero-Bundle-Size Components
- Full Access to the Backend
- Automatic Code Splitting
- No Waterfalls
  - The problem isn’t really the round trips, 
    - it’s that they are from client to server. 
    - By moving this logic to the server, we reduce the request latency and improve performance. 
    - Even better, Server Components allow developers to continue fetching the minimal data they need directly from within their components
- Avoiding the Abstraction Tax
- Distinct Challenges, Unified Solution

- **Detailed Design**
- Simplified Loading Sequence
- Update (Refetch) Sequence
- Capabilities & Constraints of Server and Client Components
- Sharing Code Between Server and Client
- Naming Convention for Server/Client Components
- Open Areas of Research
  - Routing
  - Bundling
  - Pagination and partial refetches
  - Mutations and invalidations
  - Pre-rendering
  - Static Site Generation
  - Developer Tools

- **Drawbacks**
  - Introducing a new form of components means more to learn.
  - This approach requires a convention for distinguishing server, client, and “shared” components, which may be confusing or off-putting.

- **Alternatives**
  - Client-only rendering
  - Server-only rendering
  - “Server-side rendering” (SSR)
  - Static Site Generation
  - AOT compilation
- none of these techniques alone is sufficient to achieve the combination of familiar developer experience, user experience, and features achieved by this proposal.

- Adoption Strategy
  - using Server Components will require integration with an application’s routing system and bundler.

- [Introducing Zero-Bundle-Size React Server Components](https://reactjs.org/blog/2020/12/21/data-fetching-with-react-server-components.html)
- [server-components-demo](https://github.com/reactjs/server-components-demo)
  - The demo is a note-taking app called React Notes.
    - It uses a Webpack plugin (not defined in this repo) that allows us to only include client components in build artifacts
    - An Express server that:
      - Serves API endpoints used in the app
      - Renders Server Components into a special format that we can read on the client
    - A React app containing Server and Client components used to build React Notes
  - This early demo is built on top of our Webpack plugin, 
    - but this is not how we envision using Server Components when they are stable. 
    - They are intended to be used in a framework that supports server rendering — for example, in Next.js.
- [server-components-demo-no-db](https://github.com/pomber/server-components-demo/)
  - a fork of the original demo without the Postgres dependency
  - you can run the demo app without needing a database.
  - you won't be able to execute SQL queries (but fetch should still work).

## pieces

- Sharing app views between server and client is magical:
  - https://twitter.com/DavidKPiano/status/1341391171176816644
  - LiveView (Elixir - Phoenix)
  - Turbolinks (Ruby - Rails)
  - Livewire (PHP - Laravel)
  - Server Components (Node - React Soon)
  - In the future, we can (hopefully) do the same for app logic, regardless of language 
  - We do this in our platform (low code tool for building apps quickly). 
    - What’s even more interesting is that modeling the app logic in a language independent visual way allows for automatic calculation of dom diffs as well. 
    - And we have visual state machines
  - That would be awesome, kind of like if markdown was it’s own independent that can be used in any other “real” language and we all agree on the spec
  - It’d be cool if we had a standard for the intermediary representation for the components 
    - and then we could share components across frameworks/libs/languages.
    - Judging by some of the comments under the RFC that's definitely on their mind
    - I wonder how web components fit into all this (or can they fit even).

- The eventual future is server-side with a sprinkle of client-side for instant interactions
  - https://twitter.com/mxstbr/status/1198627346955350021
  - 关于服务端计算还是客户端计算的争论
  - I don’t buy it. User experience happens on the client side.
    - Native apps are fucking 900% superior to web apps and they dont server render shit
    - I mean if we're talking web pages, then by all means, have it cho way. But apps. Pushing it all to the server is defeat.
  - But my colleagues on the native side have been server rendering significant chunks for years for a variety of reasons. 
    - So it’s not completely unnecessary. Just less commonly needed.
  - The performance and UX is always better on apps that don’t server render. 
    - That said, for apps that need to render across dozens of devices like Netflix and YouTube 
    - there is value in server rendering, especially when the device is low powered

- As noted in RFC, frameworks such as Rails were one of many inspirations for React Server Components. 
  - We’re not swinging the pendulum(钟摆；摇摆) fully to the server: 
  - we’re acknowledging that neither server- or client-rendering are ideal for all cases. 
  - Choose *per component* not per app.
