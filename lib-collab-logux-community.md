---
title: lib-collab-logux-community
tags: [collaboration, community, logux]
created: 2023-05-14T04:30:48.793Z
modified: 2023-05-14T04:31:17.785Z
---

# lib-collab-logux-community

# guide

- resources
  - https://twitter.com/logux_io
  - [CRDT: Conflict-free Data Types for Collaborative Editing and Offline-First - NEJSCONF - YouTube_201810](https://www.youtube.com/watch?v=JqsAw_3JDII)
  - [ReactiveConf 2017: Andrey Sitnik - Using Logux in Production - YouTube](https://www.youtube.com/watch?v=DvHNOplQ-tY)
    - [ppt: Using Logux in Production](https://slides.com/ai/logux2)
# discuss-authors
- ## 

- ## 

- ## [Vector clock and Lamport timestamps](https://github.com/logux/core/issues/14)
- First, what clock is better for distributed system is still an open question. 
- To solve all these requirements Logux uses own clock `[timestamp, uniqueNodeID, actionNumberInCurrentMillisecond]` .
- But clock doesn’t really hard-coded in Logux components. 
  - If your tasks need Lamport clock, you still can do it by customizing

- ## We released Nano Stores 0.5, _202110
- https://twitter.com/sitnikcode/status/1452629669933731849
- a new version of tiny (200-900 bytes) state manager for React/Vue/Svelte, designed to:
  - — Move logic from components to stores and separate application logic and UI
  - — Support tree-shaking
- The main change is store’s event.
  - With onMount you can, for example, lazy load data from the server only when the store was used on the page.

- Logux Client 0.14 was released with migration to Nano Stores 0.5

- ## I renamed my new state manager from Logux State to Nano Stores:_202106
- https://twitter.com/sitnikcode/status/1402611749195497473
  - — Nano-libraries family (Nano ID, Nano Events) better fit to 152 bytes project
  - — Anyway, state manager doesn’t require @logux_io
  - — Now names explain the main idea of multiple stores

- Logux State was renamed to Nano Stores in 0.3 version

- Renamed Logux State to Nano Stores. Now state manager name describes its features: very small (like NanoID) and based on many atomic stores (for tree-shaking).

- Svelte store contract is a very nice way to integrate your state manager with the framework. 
  - Logux State implements this contract and doesn’t need any compatibility layer (like we have for React and Vue). Just put $ before store name.

- ## Logux State, my new state manager was finally released._202105
- https://twitter.com/sitnikcode/status/1392102480037699589
  - Only 157 bytes (!), zero dependencies
  - Multiple atomic and derived stores
  - Stores tree shaking
  - Good TypeScript support
  - Was created to move logic from components to stores

- Storeon will be maintained, but I do not plan to add new features.

- ### The main feature is our own Logux State state manager for client-side.
- https://twitter.com/logux_io/status/1395064339200151552
  - It allows us to hide CRDT implementation into high-level stores.
- Logux State is a tiny (159 bytes!) state manager inspired by @EffectorJS and Recoil, but was created to move logic from components into stores.
  - https://github.com/logux/state 后来变成了nanostores
  - It can be used without Logux and supports Svelte, React, Vue.
- **Logux Client 0.11 uses Logux State to create SyncMap stores, which hide CRDT Map logic inside the store**.
  - We will support Logux Redux and Logux Vuex for a while, but now the main use case of using Logux is to use CRDT stores build on top of Logux State.

- Logux is a framework to build real-time web apps with:
  - — Collaboration and CRDT conflict resolutions
  - — Real-time updates by WebSocket
  - — Optimistic UI and Offline data editing
- It hides all complexity by replacing the idea of request/response to background action log sync.

- ## Logux State got offline cache support. API is very simple since log-based architecture is great for offline._202012
- https://twitter.com/logux_io/status/1333715528674930688
  - With a special flag, Logux will not clean the log from model’s actions on unsubscribing (and the log can be stored in IndexedDB).

- ## A nice Proxy use case from Logux State.
- https://twitter.com/logux_io/status/1331191103131951105
  - Don’t forget checking isLoading while you are loading anything from the server.
  - To protect a developer from making mistakes, in development we wrap a model into Proxy. It throws an error on accessing any properties before isLoading.
- good idea. Doesn’t work well with destructuring assignment, the order is limited

- ## Logux State now has its own tiny router (716 bytes!). 
- https://twitter.com/logux_io/status/1319259745178497026
  - We added it to test state manager and because we think that router should be part of models, not React.
  - we will support non-React environment in our state manager.
- We believe that business logic should be separated from UI library (like React), so subscribe() for vanilla JS was written before the React support.
- I’m using the same pattern for a long time and I agree with you the best architecture for that. Also I use a builder to construct urls from page name and optional params object. Wondering how you solve it.

- ## Need feedback for new @logux_io API. Can it replace GraphQL in your project?_202010
- https://twitter.com/sitnikcode/status/1314898780270080001
  - It is the last layer before the Logux promotion. We decided to replace Redux with models with built-in CRDT implementation.

- Logux Data API is a replacement for Redux, MobX, and other state managers.
  - You will be able to create a compatibility layer between MobX objects and Logux Data, but it is reasonable only for legacy project.
  - Does Logux Data API provide everything that you may need?

- 💡 What features will be unavailable for such models in api with logux if you don’t recommend to use mobx for new projects? I would like to have all this great sync functionality but with pluggable models library.
1. Bigger bundle size because of compatibility layer
2. Logux Data API is very similar to MobX API, so there is not big reason for compatibility layer
3. Component’s code in MobX will be bigger because of data loading. MobX is just state manager. Logux Data = state manager + sync

- We already have Logux Redux with separation between the sync tool and state manager. We found that it requires much more code than GraphQL, where the state manager and loading tool were combined.
  - It is clear that it will require more code to bind mobx or redux with logux sync. It is OK for many types of applications. But if it will be unsupported way to use logux it is hard to justify to switch from mobx or other library.

- You still have action based API to be used for Redux.
  - The problem with Logux MobX, that you anyway need a state manager in Logux to work with CRDT models. So all MobX code become unnecessary.

- ## [Logux Data API](https://github.com/logux/logux/issues/11)
- [Logux Data API Proposal](https://gist.github.com/ai/dfea0fcbfe8fba1b1e11180a1e5d16e3)
- I plan to start with Map implementation (key-value object with last-write-wins per each key). 
  - Then we plan to implement Vector (like an Array in CRDT, where multiple users can add/remove keys at the same moment without overriding each other) and Set. 
  - In the end we will implement Text.

- ## ✨ My new project, @logux_io_20200319
- https://twitter.com/sitnikcode/status/1240346978153902083
- Main question: where do we need Logux?
  1. For collaborative apps where multiple users work on the same document.
  2. For real-time apps with live data changes streaming. Especially if you are using Redux since we are good at integrating Redux API with WebSocket.

- How Logux works?
  - Logux has a client (with Redux/Vuex API and low-level API for other frameworks) and proxy server to resend Redux actions to other clients via WebSocket and convert actions to HTTP requests to your back-end (with syntax sugar for Rails).

- What is Logux benefits?
  - 1. Logux keeps the same order of the actions on all machines. It is critical for collaborative apps to have the same result for all clients.
  - 2. Good DX for Redux. Replace dispatch → dispatch.sync to sync action with server, other clients and browser tabs
  - 3. Logux was created for Optimistic UI (which is critical for collaborative apps as well). You do not need to add loader for data changes. User can go to the next task and Logux will sync action in the background when it will have Internet.
- Any other benefits?
  1. Logux would ask a client to reload the page if you deployed a new app.
  2. Instant sync actions between browser tabs.
  3. Reduce using server resources. Only one browser tab will keep WebSocket connection.

- What if the server will have an error?
  - This is why Logux is good at Optimistic UI (and because it has conflicts resolution). If the server has an error, Logux will revert action, and Logux has global UI to show the error to the user.

- But do we need a loader for data loading?
  - Of course. But instead of querying the data, Logux is subscribing to the data. We have a subscription hook for React.
  - On the server, Logux will check user access, load initial data from the database, and will resend all further actions.

- Can I make Google Docs on Logux?
  - Logux doesn’t have yet out-of-the-box component for collaborative text editing. But it is in out plans. Logux low level API was designed to have ability to make CRDT on top of it.

- If you have atomic Redux actions (change the single key instead of replace all values) you will have “last writes wins”.
  - If you will receive old action, Logux will revert newer action, apply that old action and re-apply newer actions.
- But you can change a conflict resolution approach in Logux by writing more tricky reducer.
  - Logux will provide you distributed time and reducers time travel to make development easier.
# discuss
- ## 

- ## How we at @evilmartians reduced regressions in @amplifr front-end and performed a huge refactoring without stopping feature delivery
- https://twitter.com/sitnikcode/status/1237811692777680896
- We started regression reduction by splitting the project into 4 layouts:
  1. Visual components. Only them use CSS and animations.
  2. Controllers to convert the global state to props for visual components and bind event listeners.
  3. Global state enhancements
  4. Libraries
- If logic can be described as a pure function, we moved it to the library. For example: timezone helpers, hashtag parser, data converters. It is easy to write unit tests for libraries. We used @fbjest.
- All AJAX requests were moved from components into small functions inside the api/ folder.
  - Instead of tests, we wrote a DSL to made helper code self-documenting and kept it simple.
  - But then we moved on @logux_io, where we do not need an extra layer to communicate with a server
  - More details on how @logux_io simplified client-server communications for us
- We tried to move all the business logic that is not relevant to UI out of React. It is much simpler to test non-React code.
  - For instance, data sync state we track in event listener and replace favicon and browser theme on error without going to React.

- Storeon framework has a good example of how the router can be simplified by moving away from JSX.
  - Code listens for a click on `<a>` and popstate events, parses the URLs, and changes the global state.
- Controllers are React components which convert the global state to props for visual components and bind event listeners.

- Another big challenge was to perform the refactoring without affecting the delivery of new features.
  - To achieve that, we split the project into “generations.”
- Each generation has its own folder in a project. 
  - Unit tests and UI kit for visual components count as a separate generation with its own place. 
  - In new dirs, you can only write code by new rules—Broken window theory in practice.
- Because of the Broken window theory, it’s hard to keep using all new practices in real projects.
  - So first we adopted new practices in sandboxed folders. Nobody wants to be a first developer to bring bad code into a cleanroom.

- ## I'll likely use yjs for the collaborative editing. I'm using http://Logux.io for the offline heavy lifting. Any overlap?
- https://twitter.com/getclibu/status/1383207937745690626
  - I didn't know about Logux. My first impression is that they focus on syncing React / Vue state. This is also in the scope of Yjs.
- Unfortunately the docs are somewhat React/Vue heavy however they aren't required and I don't use either, just plain JS. I use logux for eventual consistency between browser and server databases. The author is also working on a CRDT lib that uses Logux.
- CRDTs typically retain a full history of changes which can be prohibitively expense in terms of memory and storage.
  - By default Yjs compacts the history which fixes the issue you are describing. However, you can still keep the full history, or only part of it.

- ## what solutions/libraries exist for real-time server-owned state synchronization?
- https://twitter.com/heyImMapleLeaf/status/1582180994752589824
  - ❌not firebase or liveblocks. state is controlled and updated directly by client
  - ❌not socket io or pusher. it's just generic messaging, no handling of state
- My @logux_io was created to sync state via web sockets. 
  - It is self-hosted and very flexible system. You can limit a state control by the server only.
  - It has types for all API. I am specially proud that you can define a one interface for Map and then re-use it between client and server as an API contract.

- ## Jira is too slow. We moved to GitHub Projects.
- https://twitter.com/sitnikcode/status/1382318017263104003
  - The main component of Jira slowness is the lack of Optimistic UI. Loader on every action. 
  - You can’t start writing description before the server creates the task in DB.
