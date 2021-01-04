---
title: docs-react-p7-concurrent-mode
tags: [concurrent, docs, react]
created: '2020-06-23T07:35:14.835Z'
modified: '2020-07-05T18:55:35.555Z'
---

# docs-react-p7-concurrent-mode

# Introducing Concurrent Mode

- Concurrent Mode is a set of new features that help React apps stay responsive and gracefully adjust to the user’s device capabilities and network speed.
- This illustrates how UI libraries, including React, typically work today. 
  - Once they start rendering an update, including creating new DOM nodes and running the code inside components, they can’t interrupt this work. 
  - We’ll call this approach “blocking rendering”.
- In Concurrent Mode, rendering is not blocking. 
  - It is interruptible.
  - This improves the user experience. 
  - It also unlocks new features that weren’t possible before. 
- Consider a filterable product list. 
  - Have you ever typed into a list filter and felt that it stutters on every key press? 
  - Some of the work to update the product list might be unavoidable, such as creating new DOM nodes or the browser performing layout
- A common way to work around the stutter is to “debounce” the input. 
  - When debouncing, we only update the list after the user stops typing. 
  - However, it can be frustrating that the UI doesn’t update while we’re typing. 
- As an alternative, we could “throttle” the input, and update the list with a certain maximum frequency. 
  - But then on lower-powered devices we’d still end up with stutter. 
- Both debouncing and throttling create a suboptimal user experience.
- The reason for the stutter is simple: once rendering begins, it can’t be interrupted. 
  - So the browser can’t update the text input right after the key press.
- No matter how good a UI library (such as React) might look on a benchmark, if it uses blocking rendering, a certain amount of work in your components will always cause stutter. 
  - And, often, there is no easy fix.
- **Concurrent Mode fixes this fundamental limitation by making rendering interruptible**.
  - This means when the user presses another key, React doesn’t need to block the browser from updating the text input. 
  - Instead, it can let the browser paint an update to the input, and then continue rendering the updated list in memory. 
  - When the rendering is finished, React updates the DOM, and changes are reflected on the screen.
- Conceptually, you can think of this as React preparing every update “on a branch”. 
  - Just like you can abandon work in branches or switch between them, 
  - React in Concurrent Mode can interrupt an ongoing update to do something more important, 
  - and then come back to what it was doing earlier.
- Concurrent Mode techniques reduce the need for debouncing and throttling in UI. 
  - Because rendering is interruptible, React doesn’t need to artificially delay work to avoid stutter.
  - It can start rendering right away, but interrupt this work when needed to keep the app responsive.
- In Concurrent Mode, React starts preparing the new screen in memory first , or, as our metaphor goes, “on a different branch”. 
  - So React can wait before updating the DOM so that more content can load. 
- In Concurrent Mode, we can tell React to keep showing the old screen, fully interactive, with an inline loading indicator. 
  - And when the new screen is ready, React can take us to it.
- In Concurrent Mode, React can work on several state updates concurrently, just like branches let different team members work independently
  - For CPU-bound updates (such as creating DOM nodes and running component code), concurrency means that a more urgent update can “interrupt” rendering that has already started.
  - For IO-bound updates (such as fetching code or data from the network), concurrency means that React can start rendering in memory even before all the data arrives, and skip showing jarring empty loading states.
- React uses a heuristic to decide how “urgent” an update is, and lets you adjust it with a few lines of code so that you can achieve the desired user experience for every interaction.
- For example, research shows that displaying too many intermediate loading states when transitioning between screens makes a transition feel slower. 
- Similarly, we know from research that interactions like hover and text input need to be handled within a very short period of time, while clicks and page transitions can wait a little longer without feeling laggy. 
- The different “priorities” that Concurrent Mode uses internally roughly correspond to the interaction categories in the human perception research.

# Suspense for Data Fetching

- React 16.6 added a ` <Suspense>` component that lets you “wait” for some code to load and declaratively specify a loading state indicator (like a spinner) while we’re waiting
- Suspense for Data Fetching is a new feature that lets you also use `<Suspense>` to declaratively “wait” for anything else, including data. 
- This page focuses on the data fetching use case, but it can also wait for images, scripts, or other asynchronous work.
- Suspense lets your components “wait” for something before they can render
- Suspense is not a data fetching library. 
  - It’s a mechanism for data fetching libraries to communicate to React that the data a component is reading is not ready yet.
  - React can then wait for it to be ready and update the UI. 
- It is not a data fetching implementation. 
  - It does not assume that you use GraphQL, REST, or any other particular data format, library, transport, or protocol.
- It is not a ready-to-use client. 
  - You can’t “replace” fetch or Relay with Suspense. 
  - But you can use a library that’s integrated with Suspense (for example, new Relay APIs).
- It does not couple data fetching to the view layer. 
  - It helps orchestrate displaying the loading states in your UI, 
  - but it doesn’t tie your network logic to React components.
- It lets data fetching libraries deeply integrate with React. 
  - If a data fetching library implements Suspense support, using it from React components feels very natural.
- It lets you orchestrate intentionally designed loading states. 
  - It doesn’t say how the data is fetched, 
  - but it lets you closely control the visual loading sequence of your app.
- It helps you avoid race conditions. 
  - Even with await, asynchronous code is often error-prone. 
  - Suspense feels more like reading data synchronously — as if it were already loaded.
- In the long term, we intend Suspense to become the primary way to read asynchronous data from components — no matter where that data is coming from.
- This page is more conceptual and is intended to help you see why Suspense works in a certain way, and which problems it solves.
- Although it’s technically doable, Suspense is not currently intended as a way to start fetching data when a component renders. 
- Rather, it lets components express that they’re “waiting” for data that is already being fetched.
- Unless you have a solution that helps prevent waterfalls, we suggest to prefer APIs that favor or enforce fetching before render.
- **Fetch-on-render** (for example,  `fetch` in `useEffect` )
  - Start rendering components. Each of these components may trigger data fetching in their effects and lifecycle methods. 
  - This approach often leads to **waterfalls**.
- **Fetch-then-render** (for example,  `Relay` without `Suspense` ) 
  - Start fetching all the data for the next screen as early as possible. 
  - When the data is ready, render the new screen. 
  - We can’t do anything until the data arrives.
- **Render-as-you-fetch** (for example,  `Relay` with `Suspense` ) 
  - Start fetching all the required data for the next screen as early as possible, and start rendering the new screen immediately — before we get a network response. 
  - As data streams in, React retries rendering components that still need data until they’re all ready.
- This is a bit simplified, and in practice solutions tend to use a mix of different approaches. Still, we will look at them in isolation to better contrast their tradeoffs.
- **Approach 1: Fetch-on-Render (not using Suspense)**
  - A common way to fetch data in React apps today is to use an effect in `useEffect` hook or `componentDidMount`
  - We call this approach “fetch-on-render” because it doesn’t start fetching until after the component has rendered on the screen. This leads to a problem known as a “waterfall”.

``` typescript
function ProfilePage() {
  const [user, setUser] = useState(null);
  useEffect(() => {
    fetchUser().then(u => setUser(u));
  }, []);
  if (user === null) {
    return <p>Loading profile...</p>;
  }
  return (
    <>
      <h1>{user.name}</h1>
      <ProfileTimeline />
    </>
  );
}
function ProfileTimeline() {
  const [posts, setPosts] = useState(null);
  useEffect(() => {
    fetchPosts().then(p => setPosts(p));
  }, []);
  if (posts === null) {
    return <h2>Loading posts...</h2>;
  }
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

  - If you run this code and watch the console logs, you’ll notice the sequence is:

``` 

We start fetching user details
We wait…
We finish fetching user details
We start fetching posts
We wait…
We finish fetching posts
```

  - If fetching user details takes three seconds, we’ll only start fetching the posts after three seconds! 
  - That’s a **waterfall**: an unintentional sequence that should have been parallelized.
  - Waterfalls are common in code when using fetch-on-render. 
- **Approach 2: Fetch-Then-Render (not using Suspense)**
  - Libraries can prevent waterfalls by offering a more centralized way to do data fetching. 
  - For example, Relay solves this problem by moving the information about the data a component needs to statically analyzable fragments, which later get composed into a single query.

``` typescript
// Kick off fetching as early as possible
const promise = fetchProfileData();
function ProfilePage() {
  const [user, setUser] = useState(null);
  const [posts, setPosts] = useState(null);
  useEffect(() => {
    promise.then(data => {
      setUser(data.user);
      setPosts(data.posts);
    });
  }, []);
  if (user === null) {
    return <p>Loading profile...</p>;
  }
  return (
    <>
      <h1>{user.name}</h1>
      <ProfileTimeline posts={posts} />
    </>
  );
}
// The child doesn't trigger fetching anymore
function ProfileTimeline({ posts }) {
  if (posts === null) {
    return <h2>Loading posts...</h2>;
  }
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

  - The event sequence now becomes like this:

``` 

We start fetching user details
We start fetching posts
We wait…
We finish fetching user details
We finish fetching posts
```

  - We’ve solved the previous network “waterfall”, but accidentally introduced a different one. 
  - We wait for all data to come back with `Promise.all()` inside `fetchProfileData` , so now we can’t render profile details until the posts have been fetched too. 
  - We have to wait for both.
  - It’s hard to write reliable components when arbitrary parts of the data tree may be missing or stale. 
  - So fetching all data for the new screen and then rendering is often a more practical option.
- **Approach 3: Render-as-Fetch (using Suspense)**
  - In the previous approach, we fetched data before we called setState
    - start fetching > finish fetching > start rendering
  - With Suspense, we still start fetching first, but we flip the last two steps around
    - start fetching > start rendering > finish fetching
  - With Suspense, we don’t wait for the response to come back before we start rendering. 
  - In fact, we start rendering pretty much immediately after kicking off the network request

``` typescript
// This is not a Promise. It's a special object from our Suspense integration.
const resource = fetchProfileData();

function ProfilePage() {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails() {
  // Try to read user info, although it might not have loaded yet
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline() {
  // Try to read posts, although they might not have loaded yet
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

  - Here’s what happens when we render ` <ProfilePage>` on the screen

    - We’ve already kicked off the requests in `fetchProfileData()` . It gave us a special “resource” instead of a Promise. In a realistic example, it would be provided by our data library’s Suspense integration, like Relay.
    - React tries to render `<ProfilePage>` . It returns `<ProfileDetails>` and `<ProfileTimeline>` as children.
    - React tries to render `<ProfileDetails>` . It calls `resource.user.read()` . None of the data is fetched yet, so this component “suspends”. React skips over it, and tries rendering other components in the tree.
    - React tries to render `<ProfileTimeline>` . It calls `resource.posts.read()` . Again, there’s no data yet, so this component also “suspends”. React skips over it too, and tries rendering other components in the tree.
    - There’s nothing left to try rendering. Because `<ProfileDetails>` suspended, React shows the closest ` <Suspense>` fallback above it in the tree: `<h1>Loading profile...</h1>` . We’re done for now

  - This `resource` object represents the data that isn’t there yet, but might eventually get loaded. 

    - When we call `read()` , we either get the data, or the component “suspends”.

  - As more data streams in, React will retry rendering, and each time it might be able to progress “deeper”. 

    - When `resource.user` is fetched, the `<ProfileDetails>` component will render successfully and we’ll no longer need the `<h1>Loading profile...</h1>` fallback. 
    - Eventually, we’ll get all the data, and there will be no fallbacks on the screen.

- Because we render-as-fetch (as opposed to after fetching), if `user` appears in the response earlier than posts, we’ll be able to “unlock” the outer `<Suspense>` boundary before the response even finishes. 
- We might have missed this earlier, but even the fetch-then-render solution contained a waterfall: between fetching and rendering. 
- Suspense doesn’t inherently suffer from this waterfall, and libraries like Relay take advantage of this.
- This doesn’t only remove boilerplate code( `if` loading checks), but it also simplifies making quick design changes. 
  - For example, if we wanted profile details and posts to always “pop in” together, we could delete the `<Suspense>` boundary between them. 
  - Or we could make them independent from each other by giving each its own `<Suspense>` boundary. 
  - Suspense lets us change the granularity of our loading states and orchestrate their sequencing without invasive changes to our code.
- If you’re working on a data fetching library, there’s a crucial aspect of Render-as-Fetch you don’t want to miss. We kick off fetching before rendering.

``` JS
// Start fetching early!
const resource = fetchProfileData();

function ProfileDetails() {
  // Try to read user info
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}
```

- Note that the `read()` call in this example doesn’t start fetching. 
- It only tries to read the data that is already being fetched. 
- This difference is crucial to creating fast applications with Suspense. 
- We don’t want to delay loading data until a component starts rendering. 
- As a data fetching library author, you can enforce this by making it impossible to get a resource object without also starting a fetch. 
- You might object that fetching “at the top level” like in this example is impractical. 
- The answer to this is we want to start fetching in the event handlers instead.

``` JS
// First fetch: as soon as possible
const initialResource = fetchProfileData(0);

function App() {
  const [resource, setResource] = useState(initialResource);
  return (
    <>
      <button onClick={() => {
        const nextUserId = getNextId(resource.userId);
        // Next fetch: when the user clicks
        setResource(fetchProfileData(nextUserId));
      }}>
        Next
      </button> <
    ProfilePage resource = { resource }
    /> < / >
  );
}
```

- With this approach, we can fetch code and data in parallel. 
  - When we navigate between pages, we don’t need to wait for a page’s code to load to start loading its data. 
  - We can start fetching both code and data at the same time (during the link click), delivering a much better user experience.
- This poses a question of how do we know what to fetch before rendering the next screen. 
  - There are several ways to solve this (for example, by integrating data fetching closer with your routing solution).
- Suspense itself as a mechanism is flexible and doesn’t have many constraints. Product code needs to be more constrained to ensure no waterfalls, but there are different ways to provide these guarantees. Some questions that we’re currently exploring include:
  - Fetching early can be cumbersome to express. How do we make it easier to avoid waterfalls?
  - When we fetch data for a page, can the API encourage including data for instant transitions from it?
  - What is the lifetime of a response? Should caching be global or local? Who manages the cache?
  - Can Proxies help express lazy-loaded APIs without inserting read() calls everywhere?
  - What would the equivalent of composing GraphQL queries look like for arbitrary Suspense data?
- Race conditions are bugs that happen due to incorrect assumptions about the order in which our code may run. 
  - Fetching data in the `useEffect` Hook or in class lifecycle methods like `componentDidUpdate` often leads to them. 
  - Suspense can help here, too
- **Race Conditions with useEffect**

``` typescript
function getNextId(id) {
  // ...
}

function App() {
  const [id, setId] = useState(0);
  return (
    <>
      <button onClick={() => setId(getNextId(id))}>
        Next
      </button>
      <ProfilePage id={id} />
    </>
  );
}
function ProfilePage({ id }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetchUser(id).then(u => setUser(u));
  }, [id]);

  if (user === null) {
    return <p>Loading profile...</p>;
  }
  return (
    <>
      <h1>{user.name}</h1>
      <ProfileTimeline id={id} />
    </>
  );
}

function ProfileTimeline({ id }) {
  const [posts, setPosts] = useState(null);

  useEffect(() => {
    fetchPosts(id).then(p => setPosts(p));
  }, [id]);

  if (posts === null) {
    return <h2>Loading posts...</h2>;
  }
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

- If we try this code, it might seem like it works at first. 
  - However, if we randomize the delay time in our “fake API” implementation and press the “Next” button fast enough, we’ll see from the console logs that something is going very wrong. 
  - Requests from the previous profiles may sometimes “come back” after we’ve already switched the profile to another ID — and in that case they can overwrite the new state with a stale response for a different ID.
- This problem is possible to fix (you could use the effect cleanup function to either ignore or cancel stale requests), but it’s unintuitive and difficult to debug.
- Race Condition Problem 
  - React components have their own “lifecycle”. They may receive props or update state at any point in time. 
  - However, each asynchronous request also has its own “lifecycle”. It starts when we kick it off, and finishes when we get a response. 
  - The difficulty we’re experiencing is “synchronizing” several processes in time that affect each other. This is hard to think about.
- **Solving Race Conditions with Suspense**

``` typescript
const initialResource = fetchProfileData(0);

function App() {
  const [resource, setResource] = useState(initialResource);
  return (
    <>
      <button onClick={() => {
        const nextUserId = getNextId(resource.userId);
        setResource(fetchProfileData(nextUserId));
      }}>
        Next
      </button>
      <ProfilePage resource={resource} />
    </>
  );
}
function ProfilePage({ resource }) {
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails resource={resource} />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline resource={resource} />
      </Suspense>
    </Suspense>
  );
}

function ProfileDetails({ resource }) {
  const user = resource.user.read();
  return <h1>{user.name}</h1>;
}

function ProfileTimeline({ resource }) {
  const posts = resource.posts.read();
  return (
    <ul>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

- In the previous Suspense example, we only had one `resource` , so we held it in a top-level variable. 
- Now that we have multiple resources, we moved it to the `<App>` ’s component state
- When we click “Next”, the `<App>` component kicks off a request for the next profile, and passes that object down to the `<ProfilePage>` component
- Again, notice that we’re not waiting for the response to set the state. 
- It’s the other way around: 
  - we set the state (and start rendering) immediately after kicking off a request. 
  - As soon as we have more data, React “fills in” the content inside `<Suspense>` components.
- The Suspense version doesn’t suffer from race conditions. 
  - The answer is that in the Suspense version, we don’t have to think about time as much in our code. 
  - Our original code with race conditions needed to set the state at the right moment later, or otherwise it would be wrong. 
  - But with Suspense, we set the state immediately — so it’s harder to mess it up.
- With Suspense, handling fetching errors works the same way as handling rendering errors
  - you can render an error boundary anywhere to “catch” errors in components below.
  - It would catch both rendering errors and errors from Suspense data fetching.
- Suspense answers some questions, but it also poses new questions of its own:
  - If some component “suspends”, does the app freeze? How to avoid this?
  - What if we want to show a spinner in a different place than “above” the component in a tree?
  - If we intentionally want to show an inconsistent UI for a small period of time, can we do that?
  - Instead of showing a spinner, can we add a visual effect like “greying out” the current screen?
  - Why does our last Suspense example log a warning when clicking the “Next” button?

# Concurrent UI Patterns

- Usually, when we update the state, we expect to see changes on the screen immediately. 
  - This makes sense because we want to keep our app responsive to user input. 
- However, there are cases where we might prefer to defer an update from appearing on the screen.
  - For example, if we switch from one page to another, and none of the code or data for the next screen has loaded yet, 
  - it might be frustrating to immediately see a blank page with a loading indicator. 
  - We might prefer to stay longer on the previous screen. 
- **Transitions**
- It would be nice if we could “skip” the undesirable loading state indicator and wait for some content to load before transitioning to the new screen.
- React offers a new built-in `useTransition()` Hook to help with this.
- First, we’ll make sure that we’re actually using Concurrent Mode. 
- We need to use `ReactDOM.createRoot()` rather than `ReactDOM.render()` for this feature to work
- Next, we’ll add an import for the `useTransition` Hook from React
- Finally, we’ll use it inside the `App` component
- We will need to use this Hook’s return values to set up our state transition. 
- we passed a configuration object to `useTransition` . 
  - Its `timeoutMs` property specifies how long we’re willing to wait for the transition to finish. 
  - By passing `{timeoutMs: 3000` }, we say “If the next profile takes more than 3 seconds to load, show the big spinner — but before that timeout it’s okay to keep showing the previous screen”.
- There are two values returned from `useTransition` :
  - `startTransition` is a function. 
    - We’ll use it to tell React which state update we want to defer.
  - `isPending` is a boolean. 
    - It’s React telling us whether that transition is ongoing at the moment.
- Wrapping setState in a Transition
  - We’ll wrap that state update into `startTransition` . 
  - That’s how we tell React we don’t mind React delaying that state update if it leads to an undesirable loading state
- Adding a Pending Indicator
  - React gives `isPending` boolean to us so we can tell whether we’re currently waiting for this transition to finish.
- Reviewing the Changes
  - As a result, clicking “Next” doesn’t perform an immediate state transition to an “undesirable” loading state, but instead stays on the previous screen and communicates progress there.
- Where Does the Update Happen?
  - Clearly, both “versions” of `<ProfilePage>` exist at the same time. 
  - We know the old one exists because we see it on the screen and even display a progress indicator on it. 
  - And we know the new version also exists somewhere, because it’s the one that we’re waiting for!
  - But how can two versions of the same component exist at the same time?
  - Wrapping a state update in startTransition begins rendering it “in a different universe”, much like in science fiction movies. 
  - We don’t “see” that universe directly — but we can get a signal from it that tells us something is happening (isPending). 
  - When the update is ready, our “universes” merge back together, and we see the result on the screen!
  - An operating system switches between different applications very fast. 
  - Similarly, React can switch between the version of the tree you see on the screen and the version that it’s “preparing” to show next.
- Transitions Are Everywhere
  - As we learned from the Suspense walkthrough, any component can “suspend” any time, if some data it needs is not ready yet. 
  - We can strategically place `<Suspense>` boundaries in different parts of the tree to handle this, but it won’t always be enough.
  - To avoid showing an undesirable loading state, we can wrap the state update in a transition
- Baking Transitions Into the Design System
  - We can now see that the need for useTransition is very common. This can lead to a lot of repetitive code across components. 
  - This is why we generally **recommend to bake `useTransition` into the design system components of your app**
  - When a `button` gets clicked, it starts a transition and calls `props.onClick()` inside of it — which triggers `handleRefreshClick` in the `<ProfilePage>` component. 
    - We start fetching the fresh data, but it doesn’t trigger a fallback because we’re inside a transition, 
    - and the 10 second timeout specified in the useTransition call hasn’t passed yet. 
    - While a transition is pending, the button displays an inline loading indicator fallback UI.
  - We can see now how Concurrent Mode helps us achieve a good user experience without sacrificing isolation and modularity of components. 
  - React coordinates the transition.
- **The Three Steps**
- By now we have discussed all of the different visual states that an update may go through. 
- In this section, we will give them names and talk about the progression between them.
- At the very end, we have the **Complete** state. 
  - That’s where we want to eventually get to. 
  - It represents the moment when the next screen is fully rendered and isn’t loading more data.
- But before our screen can be Complete, we might need to load some data or code. 
  - When we’re on the next screen, but some parts of it are still loading, we call that a **Skeleton** state.
- Finally, there are two primary ways that lead us to the Skeleton state. 

- Default: Receded(逐渐减弱、逐渐远去) → Skeleton → Complete
  - `Receded` : For a second, you will see the `<h1>Loading the app...</h1>` fallback.
  - `Skeleton` : You will see the `<ProfilePage>` component with `<h2>Loading posts...</h2>` inside.
  - `Complete` : You will see the `<ProfilePage>` component with no fallbacks inside. Everything was fetched.
- The difference is that the `Receded` state feels like “taking a step back” to the user, while the `Skeleton` state feels like “taking a step forward” in our progress to show more content.
- When a component suspends, React needs to show the **closest** fallback.
- This scenario (Receded → Skeleton → Complete) is the default one. However, the Receded state is not very pleasant because it “hides” existing information.

- Preferred: Pending → Skeleton → Complete
  - When we `useTransition` , React will let us “stay” on the previous screen — and show a progress indicator there. 
  - We call that a **Pending** state. 
  - It feels much better than the **Receded** state because none of our existing content disappears, and the page stays interactive.

- Wrap Lazy Features in Suspense
  - If we don’t want to stay in the Pending state for too long, our first instinct might be to set `timeoutMs` in `useTransition` to something smaller
  - This lets us escape the prolonged Pending state, but we still don’t have anything useful to show!
  - Instead of making the transition shorter, we can “disconnect” the slow component from the transition by wrapping it into `<Suspense>`
  - React always prefers to go to the Skeleton state as soon as possible. Even if we use transitions with long timeouts everywhere, React will not stay in the Pending state for longer than necessary to avoid the Receded state.
  - f some feature isn’t a vital part of the next screen, wrap it in `<Suspense>` and let it load lazily. This ensures we can show the rest of the content as soon as possible. 
  - Conversely, if a screen is not worth showing without some component, such as `<ProfileDetails>` in our example, do not wrap it in `<Suspense` >. Then the transitions will “wait” for it to be ready.

- Suspense Reveal “Train”
  - When we’re already on the next screen, sometimes the data needed to “unlock” different `<Suspense>` boundaries arrives in quick succession. 
  - For example, two different responses might arrive after 1000ms and 1050ms, respectively. 
  - If you’ve already waited for a second, waiting another 50ms is not going to be perceptible. 
  - This is why React reveals `<Suspense>` boundaries on a schedule, like a “train” that arrives periodically. 
  - This trades a small delay for reducing the layout thrashing and the number of visual changes presented to the user.

- Delaying a Pending Indicator
  - Our Button component will immediately show the Pending state indicator on click. This signals to the user that some work is happening. 
  - However, if the transition is relatively short (less than 500ms), it might be too distracting and make the transition itself feel slower.
  - One posible solution to this is to delay the spinner itself from displaying:
  - With this change, even though we’re in the Pending state, we don’t display any indication to the user until 500ms has passed. This may not seem like much of an improvement when the API responses are slow.
  - Even though the rest of the code hasn’t changed, suppressing a “too fast” loading state improves the perceived performance by not calling attention to the delay.

- Recap
  - By default, our loading sequence is `Receded → Skeleton → Complete` .
  - The Receded state doesn’t feel very nice because it hides existing content.
  - With `useTransition` , we can opt into showing a Pending state first instead. This will keep us on the previous screen while the next screen is being prepared.
  - If we don’t want some component to delay the transition, we can wrap it in its own `<Suspense>` boundary.
  - Instead of doing `useTransition` in every other component, we can build it into our design system.

- **Other Patterns**
- Splitting High and Low Priority State
  - When you design React components, it is usually best to find the “minimal representation” of state.
  - This lets us avoid mistakes where we update one state but forget the other state.
  - However, in Concurrent Mode there are cases where you might want to “duplicate” some data in different state variables. 
  - If some state update causes a component to suspend, that state update should be wrapped in a transition.
  - We’ve fixed the first problem (suspending outside of a transition). But now because of the transition, our state doesn’t update immediately, and it can’t “drive” a controlled input!
  - The answer to this problem is to **split the state in two parts**
    - a “high priority” part that updates immediately
    - a “low priority” part that may wait for a transition.
  - So the correct fix is to put setQuery (which doesn’t suspend) outside the transition, but setResource (which will suspend) inside of it.

- Deferring a Value
  - By default, React always renders a consistent UI (=f(data)).
  - This makes sense in the vast majority of situations. Inconsistent UI is confusing and misleading
  - However, sometimes it might be helpful to intentionally introduce an inconsistency. 
  - We could do it manually by “splitting” the state like above, but React also offers a built-in Hook for this
  - If we’re willing to sacrifice consistency, we could pass potentially stale data to the components that delay our transition. That’s what `useDeferredValue()` lets us do

``` typescript
function ProfilePage({ resource }) {
  const deferredResource = useDeferredValue(resource, {
    timeoutMs: 1000
  });
  return (
    <Suspense fallback={<h1>Loading profile...</h1>}>
      <ProfileDetails resource={resource} />
      <Suspense fallback={<h1>Loading posts...</h1>}>
        <ProfileTimeline
          resource={deferredResource}
          isStale={deferredResource !== resource}
        />
      </Suspense>
    </Suspense>
  );
}

function ProfileTimeline({ isStale, resource }) {
  const posts = resource.posts.read();
  return (
    <ul style={{ opacity: isStale ? 0.7 : 1 }}>
      {posts.map(post => (
        <li key={post.id}>{post.text}</li>
      ))}
    </ul>
  );
}
```

  - The tradeoff we’re making here is that `<ProfileTimeline>` will be inconsistent with other components and potentially show an older item. 
    - Click “Next” a few times, and you’ll notice it. 
  - But thanks to that, we were able to cut down the transition time from 1000ms to 300ms.
  - Whether or not it’s an appropriate tradeoff depends on the situation. 
  - But it’s a handy tool, especially when the content doesn’t change noticeably between items, 
  - and the user might not even realize they were looking at a stale version for a second.
  - It’s worth noting that useDeferredValue is not only useful for data fetching. 
    - It also helps when an expensive component tree causes an interaction (e.g. typing in an input) to be sluggish
    - Just like we can “defer” a value that takes too long to fetch (and show its old value despite other components updating), we can do this with trees that take too long to render.
  - How is this different from debouncing? 
    - Our example has a fixed artificial delay (3ms for every one of 80 items), so there is always a delay, no matter how fast our computer is. 
    - However, the `useDeferredValue` value only “lags behind” if the rendering takes a while. 
    - There is no minimal lag imposed by React. 
    - With a more realistic workload, you can expect the lag to adjust to the user’s device.
    - That’s the advantage of this mechanism over debouncing or throttling, which always impose a minimal delay and can’t avoid blocking the thread while rendering.
  - Even though there is an improvement in responsiveness, this example isn’t as compelling yet because Concurrent Mode is missing some crucial optimizations for this use case. 
  - Still, it is interesting to see that features like useDeferredValue (or useTransition) are useful regardless of whether we’re waiting for network or for computational work to finish.

- SuspenseList

``` JS
function ProfilePage({ resource }) {
  return (
    <>
      <ProfileDetails resource={resource} /> <
    Suspense fallback = { <h2>Loading posts...</h2> } >
    <ProfileTimeline resource={resource} /> <
    /Suspense> <
    Suspense fallback = { <h2>Loading fun facts...</h2> } >
    <ProfileTrivia resource={resource} /> <
    /Suspense> < / >
  );
}
```

  - The API call duration in this example is randomized. If you keep refreshing it, you will notice that sometimes the posts arrive first, and sometimes the “fun facts” arrive first.
  - This presents a problem. If the response for fun facts arrives first, we’ll see the fun facts below the `<h2>Loading posts...</h2>` fallback for posts. We might start reading them, but then the posts response will come back, and shift all the facts down. This is jarring.
  - One way we could fix it is by putting them both in a single boundary
  - The problem with this is that now we always wait for both of them to be fetched. 
  - However, if it’s the posts that came back first, there’s no reason to delay showing them.
  - Other approaches to this, such as composing `Promise` s in a special way, are increasingly difficult to pull off when the loading states are located in different components down the tree.
  - `<SuspenseList>` coordinates the “reveal order” of the closest `<Suspense>` nodes below it
  - The `revealOrder="forwards"` option means that the closest `<Suspense>` nodes inside this list will only “reveal” their content in the order they appear in the tree — even if the data for them arrives in a different order.
  - You can control how many loading states are visible at once with the `tail` prop. If we specify `tail="collapsed"` , we’ll see at most one fallback at a time.
  - Keep in mind that `<SuspenseList>` is composable, like anything in React. 
    - For example, you can create a grid by putting several `<SuspenseList>` rows inside a `<SuspenseList>` table.

# Adopting Concurrent Mode

- Normally, when we add features to React, you can start using them immediately. 
  - Fragments, Context, and even Hooks are examples of such features. 
  - You can use them in new code without making any changes to the existing code.
- Concurrent Mode introduces semantic changes to how React works. 
  - Otherwise, the new features enabled by it wouldn’t be possible. 
  - This is why they’re grouped into a new “mode” rather than released one by one in isolation.
- You can’t opt into Concurrent Mode on a per-subtree basis. 
- Instead, to opt in, you have to do it in the place where today you call `ReactDOM.render()`

``` JS
import ReactDOM from 'react-dom';

// If you previously had:
// ReactDOM.render(<App />, document.getElementById('root'));
// You can opt into Concurrent Mode by writing:

ReactDOM.createRoot(
  document.getElementById('root')
).render(<App />);
```

- This will enable Concurrent Mode for the whole `<App />` tree
- Concurrent Mode APIs such as `createRoot` only exist in the experimental builds of React.
- In Concurrent Mode, the lifecycle methods previously marked as “unsafe” actually are unsafe, and lead to bugs even more than in today’s React. 
- We don’t recommend trying Concurrent Mode until your app is Strict Mode-compatible.
- If you have a large existing app, or if your app depends on a lot of third-party packages, please don’t expect that you can use the Concurrent Mode immediately.
- In our experience, code that uses idiomatic React patterns and doesn’t rely on external state management solutions is the easiest to get running in the Concurrent Mode.
- Legacy Mode: `ReactDOM.render(<App />, rootNode)` . 
  - This is what React apps use today. 
  - There are no plans to remove the legacy mode in the observable future 
  - but it won’t be able to support these new features.
- Blocking Mode: `ReactDOM.createBlockingRoot(rootNode).render(<App />)` . 
  - It is currently experimental. 
  - It is intended as a first migration step for apps that want to get a subset of Concurrent Mode features.
- Concurrent Mode: `ReactDOM.createRoot(rootNode).render(<App />)` . 
  - It is currently experimental.
  - In the future, after it stabilizes, we intend to make it the default React mode.
  - This mode enables all the new features.
- However, gradually moving the ecosystem away from the Legacy Mode will also solve problems that affect major libraries in the React ecosystem, 
  - such as confusing Suspense behavior when reading layout and lack of consistent batching guarantees. 
  - There’s a number of bugs that can’t be fixed in Legacy Mode without changing semantics, but don’t exist in Blocking and Concurrent Modes.
- You can think of the Blocking Mode as a “gracefully degraded” version of the Concurrent Mode.
- Legacy mode has automatic batching in React-managed events but it’s limited to one browser task. 
  - Non-React events must opt-in using `unstable_batchedUpdates` . 
  - In Blocking Mode and Concurrent Mode, all `setState` s are batched by default.

# Concurrent Mode API Reference

- Enabling Concurrent Mode
  - createRoot
  - createBlockingRoot
- Suspense API
  - Suspense
  - SuspenseList
  - useTransition
  - useDeferredValue

## `ReactDOM.createRoot(rootNode).render(<App />);`

- Replaces `ReactDOM.render(<App />, rootNode)` and enables Concurrent Mode.

## `ReactDOM.createBlockingRoot(rootNode).render(<App />)`

- Replaces `ReactDOM.render(<App />, rootNode)` and enables Blocking Mode.
- Blocking Mode only contains a small subset of Concurrent Mode features and is intended as an intermediary migration step for apps that are unable to migrate directly.

## Suspense

``` JS
<Suspense fallback={<h1>Loading...</h1>}>
  <ProfilePhoto />
  <ProfileDetails />
</Suspense>
```

- Suspense lets your components “wait” for something before they can render, showing a fallback while waiting.
- It is important to note that until all children inside `<Suspense>` has loaded, we will continue to show the fallback.
- Suspense takes two props:
  - `fallback` takes a loading indicator. 
    - The fallback is shown until all of the children of the Suspense component have finished rendering.
  - `unstable_avoidThisFallback` takes a boolean. 
    - It tells React whether to “skip” revealing this boundary during the initial load. 
    - This API will likely be removed in a future release.

## SuspenseList

``` JS
<SuspenseList revealOrder="forwards">
  <Suspense fallback={'Loading...'}>
    <ProfilePicture id={1} />
  </Suspense>
  <Suspense fallback={'Loading...'}>
    <ProfilePicture id={2} />
  </Suspense>
  <Suspense fallback={'Loading...'}>
    <ProfilePicture id={3} />
  </Suspense>
  ...
</SuspenseList>
```

- SuspenseList helps coordinate many components that can suspend by orchestrating the order in which these components are revealed to the user.
- When multiple components need to fetch data, this data may arrive in an unpredictable order. 
- However, if you wrap these items in a SuspenseList, React will not show an item in the list until previous items have been displayed (this behavior is adjustable).
- `SuspenseList` only operates on the closest `Suspense` and `SuspenseList` components below it. 
  - It does not search for boundaries deeper than one level. 
  - However, it is possible to nest multiple `SuspenseList` components in each other to build grids.

## `useTransition(SUSPENSE_CONFIG);`

- `useTransition` allows components to avoid undesirable loading states by waiting for content to load before transitioning to the next screen. 
- It also allows components to defer slower, data fetching updates until subsequent renders so that more crucial updates can be rendered immediately.
- If some state update causes a component to suspend, that state update should be wrapped in a transition.
- We recommend that you share Suspense Config between different modules.

## `useDeferredValue(value, { timeoutMs: 2000 });`

- Returns a deferred version of the value that may “lag behind” it for at most `timeoutMs` .
- This is commonly used to keep the interface responsive when you have something that renders immediately based on user input and something that needs to wait for a data fetch.

``` JS
function App() {
  const [text, setText] = useState("hello");
  const deferredText = useDeferredValue(text, { timeoutMs: 2000 });

  return (
    <div className="App">
      {/* Keep passing the current text to the input */}
      <input value={text} onChange={handleChange} />
      ...
      {/* But the list is allowed to "lag behind" when necessary */}
      <MySlowList text={deferredText} />
    </div>
  );
}
```

- This allows us to start showing the new text for the `input` immediately, which allows the webpage to feel responsive. 
  - Meanwhile,  `MySlowList` “lags behind” for up to 2 seconds according to the `timeoutMs` before updating, allowing it to render with the current text in the background.
- `timeoutMs` tells React how long the deferred value is allowed to lag behind.
- React will always try to use a shorter lag when network and device allows it.
