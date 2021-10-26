---
title: page-frontend-why-I-still-dont-use-graphql
tags: [api, graphql]
created: '2020-08-06T08:48:07.770Z'
modified: '2021-01-19T10:57:46.316Z'
---

# page-frontend-why-I-still-dont-use-graphql

# [Why do Webdevs keep trying to kill REST?](https://www.swyx.io/client-server-battle/)
- Watching recent trends in client-server paradigms, from Apollo GraphQL to React Server Components to Rails Hotwire, I've had a revelation that helped me make sense of it all: They're all abstractions over REST!
- There are two schools of thought:
- Smart Client: State updates are rendered clientside first, then sent back to the server.
  - Use a state management solution like Redux or Svelte Stores and handwrite every piece of the client-server coordination logic.
  - You can use libraries that combine state and data fetching: Apollo Client, React Query, RxDB, GunDB, and Absurd-SQL all do dual jobs of fetching data and storing related state.
  - You can use frameworks that abstract it away for you: Blitz.js and Next.js
  - Or you can take it off the shelf: Google's Firebase and AWS' Amplify/AppSync are fully vendor provided and vertically integrated with backend resources like auth, database, and storage (arguably MongoDB Realm and Meteor's minimongo before it)
- Smart Server: State updates are sent to the server first, which then sends rerenders to the client (whether in HTML chunks, serialized React components, or XML).
  - Phoenix Liveview
  - Rails Hotwire
  - React Server Components
  - ASP. NET Web Forms
- Of course the "Smart Server" paradigm isn't wholly new. It has a historical predecessor — let's call it the "Traditional Server" paradigm. 
  - The Wordpress, Django, Laravel type frameworks would fill out HTML templates and the browser's only job is to render them and send the next requests.
- We gradually left that behind for more persistent interactive experiences with client-side JS (nee(原姓的) AJAX). 
  - For a long time we were happy with just pinging REST endpoints from the client, ensuring a clean separation of concerns between frontend and backend.

> So why are we tearing up the old client-server paradigm? And which side will win?

## It's about User Experience

- Ironically, the two sides have very different goals in UX and would probably argue that the other is less performant

- Smart clients enable offline-first apps and optimistic updates so your app can keep working without internet and feels instant 
  - because you are doing CRUD against a local cache of remote data (I wrote about this in Optimistic, Offline-First Apps).
  - This improves perceived performance for apps.
  - However their downside is tend to come with large JS bundles upfront: Firebase adds as much as 1mb to your bundle
  - 还可以节省服务器资源
  - 还可以方便设计跨平台的后端接口
- Smart servers directly cut JS weight by doing work serverside rather than clientside, yet seamlessly patching in updates as though they were done clientside. 
  - This improves first-load performance for sites.
  - However their downside is that every single user of yours is doing their rendering on your server, not their browser. This is bound to be more resource intensive. The problem is mitigated if you can easily autoscale (eg with serverless rendering on Cloudflare Workers or AWS Lambda). There are also real security concerns that should get ironed out over time.
- The "winner" here, if there is such, will depend on usecase 
  - if you are writing a web app where any delay in response will be felt by users, then you want the smart client approach
  - but if you are writing an ecommerce site, then your need for speed will favor smart servers.

## It's about Developer Experience

- Platform SDKs. 
  - For the Frontend-Platform-as-a-Service vendors like Firebase and AWS Amplify, their clients are transparently just platform SDKs 
  - since they have total knowledge of your backend, they can offer you a better DX on the frontend with idiomatic language SDKs.
- Reducing Boilerplate for Invocations. 
  - Instead of a 2 stage process of writing a backend handler/resolver and then the corresponding frontend API call/optimistic update, you can write the backend once and codegen a custom client, or offer what feels like direct database manipulation on the frontend (with authorization and syncing rules).
- Offline. 
  - Both Firebase Firestore and Amplify AppSync also support offline persistence. 
  - Since they know your database schema, it's easy to offer a local replica and conflict resolution. 
  - There are vendor agnostic alternatives like RxDB or Redux Offline that take more glue work.
  - Being Offline-first requires you to have a local replica of your data, which means that doing CRUD against your local replica can be much simpler.
- Reducing Boilerplate for Optimistic Updates.
  - When you do normal optimistic updates, you have to do 4 things:
  1. send update to server,
  2. optimistically update local state,
  3. complete the optimistic update on server success,
  4. undo the optimistic update on server fail
  - With a local database replica, you do 1 thing: write your update to the local DB and wait for it to sync up. 
  - The local DB should expose the status of the update (which you can reflect in UI) as well as let you centrally handle failures.
- People
  - This is an organizational, rather than a technological, argument.
  - fontend to backend is hugely disruptive to workflow. 
  - Give the developer full stack access to whatever they need to ship features, whether it is serverless functions, database access or something else. 
  - Smart Clients/Servers can solve people problems as much as UX problems.
  - This is why I am a big champion of shifting the industry divide from "frontend vs backend" to "product vs platform". 
  - GraphQL is also secretly a "people technology" because it decouples frontend data requirements from a finite set of backend endpoints.

- Both smart clients and smart servers greatly improve the DX on all these fronts.

## It's about Protocols

- Better protocols lead to improved UX (eliminating user-facing errors and offering faster updates) and DX (shifting errors left) 
  - and they're so relevant to the "why are you avoiding REST" debate that I split them out to their own category. 
- Technically of course, whatever protocol you use may be a layer atop of REST - if you have a separate layer (like CRDTs) that handles syncing/conflict resolution, then that is the protocol you are really using.
- A lot of these comments will feature GraphQL, because it is the non-REST protocol I have the most familiarity with; but please feel free to tell me where other protocols may fit in or differ.
- Type Safety
  - GraphQL validates every request at runtime. 
  - trpc does it at compile time
- Bandwidth
  - Sending less data (or data in a format that improves UX) over the wire
  - React Server Components sends serialized component data over the wire; more compact because it can assume React, and smoothly coordinated with on-screen loading states
  - Hotwire sends literal HTML Over The wire
  - GraphQL helps solve the overfetching problem. In practice, I think the importance of this is overhyped(过分宣传的，大肆宣扬的) unless you are Facebook or Airbnb. However the usefulness of persisted queries for solving upload bandwidth problems is underrated.
- Real-time: offering "live" and "collaborative" experiences on the web
  - This is doable with periodic polling and long-polling, but more native protocols like UDP, WebRTC and WebSockets are probably a better solution
  - Replicache (used for Next.js Live) and Croquet look interesting here
  - UDP itself seems like a foundation that is ripe for much more protocol innovation; even HTTP/3 will be built atop it
- There remain some areas for growth that I don't think are adequately answered yet:
- Performance
  -  One nightmare of every backend developer is unwittingly letting a given user kick off an expensive query that could choke up system resources. It's a touchy(棘手的，敏感性的；易生气的) subject, but new protocols can at least open up a more interesting dance between performance and flexibility.
- Security
  - allowing frontend developers direct database access requires much more guard rails around security. 
  - Vendors with integrated auth solutions can help somewhat, but the evangelists for a new protocol need to be as loud about their security requirements as they are the developer experience upsides.

## Not Everyone is Anti-REST

- REST is perfectly fine for the vast majority of webdevs. 
- There are even people pushing boundaries within the REST paradigm.
- Remix
  - the React metaframework from the creators of React Router, embraces native browser standards so you get progressive enhancement "for free", 
  - for example requiring that you POST from a HTML form (they have clarified that anything but GET is fine, and they are pro-HTTP, and neutral REST)
- Supabase
  - a "smart client" solution that works equally well on the server, which invests heavily in the open source PostgREST project.

## discussion

- JSONAPI is a JSON REST spec, and the Relay spec is essentially a GraphQL superset spec
  - Similar to JSONAPI, OpenAPI (formerly Swagger) is another superset rest spec that offers a unique perspective on REST API usage.

- Not Everyone is Anti-REST
  - Splitting hairs, but we're pro-HTTP, indifferent to REST. 
  - A form can send a graphql mutation via POST or a PUT to a REST endpoint, we just care that's it's not GET.

- I'd love to get more attention on @OrbitJS and @jsonapi
  - They don't seem like much at first but it is the best realization of the smart client pattern you mention that I've seen. Totally REST friendly but sadly not marketed as well as GQL

# Why I Still Don't Use GraphQL
- Some thoughts I've gathered over the years on what I think about GraphQL. 
  - All of this is subject to change of course, and some of it may be "hot-take"-ish, 
  - but at the end of the day, I've made decisions regarding GraphQL with my customers, users, and fellow developers in mind and with the mantra that if it ultimately doesn't make a big difference for any of those people and justify the work that it requires, it's not the best investment of time. 
  - It's more important to please your users, ship products in a timely manner, and use tools that keep processes simple and familiar.

- A majority of the world still runs on REST and probably will for a while.
- The challenges of larger companies that originally benefitted from GQL are not everyones challenges and they likely never will be.
- I don't want to require my API users to have knowledge of GQL.
- Strongly typed APIs are good, but I don't particularly enjoy the tools in the ecosystem right now to use them via GQL
- GraphQL seems to have been born out of the requirement of "deep" querying of assets via graph-like relationships
- Deep querying without field masking presents a problem with bandwidth and overfetching, thus GraphQL forced field masking on you. You cannot `select *` so to speak.
- Deep querying with field masking can end up producing a massive amount of partially-saturated entities/objects from a server.
- You can implement field masking and relational graph-style querying via REST *if you need it*. I rarely have.
- Because of this "fragmentation", GQL uses query fragments as part of it's "benefits"
- Fragments to some extent assume that any clients or consumers of the API have a reliable way of keeping all of these fragments up to date, but doesn't (to my knowledge) offer anything official to do this.
- Tools like Apollo approach this with semi-automated normalized caching (based on the schema) and stitch together fragments and keep entities/fragments up to date as different queries are consumed on the client. This seems extremely complex for most use cases.
- Relay is another tool that people swear by, but seems to have a high level of buy-in/commitment. Not only do you have to use GQL, but you have to do things in the Relay way.
- At the end of the day, I would wager that a vast majority of apps won't benefit enough from GQL to justify the costs (opinionated and relatively proprietary syntax, specialized tools/libraries for interacting with it) that it currently requires.
- If you have a massively public API that needs to be generally queryable for general purpose things, then you may want GQL and it will likely be worth it. 
  - I think of companies like Facebook and Github here, or essentially any company that needs to have some type of ecosystem built upon it.
- The benefit that is the most alluring of GQL is the type safety, but that is not the only way to have a type safe API. 
  - You can do this with other tools like `buf` , JSON-schema, and typescript. 
  - I think I would go after these first.
# ref
