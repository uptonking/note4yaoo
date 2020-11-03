---
title: note-dev-state-redux-blog
tags: [blog, redux, state]
created: '2020-11-03T13:12:54.267Z'
modified: '2020-11-03T13:13:40.177Z'
---

# note-dev-state-redux-blog

## [Redux without React — State Management in Vanilla JavaScript](https://www.sitepoint.com/redux-without-react-state-management-vanilla-javascript/)

- https://github.com/morkro/tetrys

- What makes Redux great is that it forces you to think ahead and get an early picture of your application design. 
  - You start to define what should actually be stored, which data can and should change, and which components can access the store.
- I decided to adopt a file structure commonly found in Redux and React projects. 
  - store, actions, reducers
  - components
  - constants, utils
  - It’s a logical structure and is applicable to many different setups. 
  - There are many variations on this theme, and most projects do things a little differently, but the overall structure is the same.
- To access the store, it needs to be created once and passed down to all instances of an application. 
  - Most frameworks work with some sort of dependency injection container, so we as a user of the framework don’t have to come up with our own solution. 

- Originally I put the store in its own module (`scripts/store/index.js`), which could then be imported by other parts of my application. 
  - I ended up regretting this and dealing with circular dependencies real quick. 
  - The issue was that the store didn’t get properly initialized when a component tried to access it.
  - The application entry point was initializing all the components, which then made internal use of the store directly or via helper functions (called `connect` here). 
  - But since the store wasn’t explicitly created, but only as a side effect in its own module, components ended up using the store before it has been created.
  - There was no way to control when a component or a helper function called the store for the first time. It was chaotic.

``` JS
// scripts/store/index.js (☓ bad)
import { createStore } from 'redux'
import reducers from '../reducers'

const store = createStore(reducers)

export default store
export { getItemList } from './connect'

// scripts/store/connect.js (☓ bad)
import store from './'

export function getItemList() {
  return store.getState().items.all
}
```

- This is the exact moment when my components ended up being mutually recursive. 
  - The helper functions require the store to function, 
  - and are at the same time exported from within store initialization file to make them accessible to other parts of my application.

- I solved this problem by moving the initialization to my application entry point (`scripts/index.js`) , and passing it down to all required components instead.
  - this is very similar to how React actually makes the store accessible
- The application entry point creates the store first of all, then passes it down to all the components. 
- Then, a component can connect with the store and dispatch actions, subscribe to changes or get specific data.

``` JS
// scripts/store/configureStore.js (✓ good)
import { createStore } from 'redux'
import reducers from '../reducers'

export default function configureStore() {
  return createStore(reducers)
}

// scripts/store/connect.js (✓ good)
export function getItemList(store) {
  return store.getState().items.all
}

// scripts/index.js
import configureStore from './store'
import { PageControls, TetrisGame } from './components'

const store = configureStore()
const pageControls = new PageControls(store)
const tetrisGame = new TetrisGame(store)
```

- Presentational components do nothing else besides pure DOM handling; they aren’t aware of the store. 
- Container components on the other hand can dispatch actions or subscribe for changes.
- For me there are exceptions though. 
  - Sometimes a component is really minimal and only does one thing. 
  - I didn’t want to split them up into one of the aforementioned patterns, so I decided to mix them. 
  - If the component grows and gets more logic, I will separate it.

- One of the bigger questions I had, when starting the project, was how to actually update the DOM. 
  - React uses a fast in-memory representation of the DOM called Virtual DOM to keep DOM updates to a minimum.
  - I could well switch to Virtual DOM, if my application should grow bigger and more DOM heavy, 
  - but for now I do classic DOM manipulation and that works fine with Redux.
- The basic flow is as follows:
  - A new instance of a container component is initialized and passed the store for internal use
  - The component subscribes to changes in the store
  - And uses a different presentational component to render updates in the DOM

- Another important point is to implement a use case driven store. 
  - In my opinion it’s important to only store what is essential for the application. 
  - At the very beginning I stored almost everything: current active view, game settings, scores, hover effects, the user’s breathing pattern, and so on.

- I have worked on Redux projects with and without React and my main take-away is, that huge differences in application design aren’t necessary. 
  - Most methodologies used in React can actually be adapted to any other view handling setup. 
  - I took me a while to realize this, as I started off thinking I have to do things differently, but eventually I figured this is not necessary.
- What is different however, is the way you initialize your modules, your store, and how much awareness a component can have of the overall application state. 
  - The concepts stay the same, but the implementation and amount of code is suited to exactly your needs.

## [Life after Redux: React’s new APIs can provide pause as to whether or not it is a necessity in your next app](https://itnext.io/life-after-redux-21f33b7f189e)

- There are many benefits to using Redux.
  - It allows developers to easily share state data between different components throughout an application via the use of helper libs such as react-redux.
  - You get control flow, a middleware pattern and the resulting ecosystem of middleware extensions available.
  - By using a single master store, you can be sure your state remains consistent which has been an issue prior to Redux and Flux with certain MVC patterns.
  - Subsequently centralisation allows for developers to potentially explore and debug application state over time a technique supported by Redux Devtools also known as time travel debugging.
  - The state reducer pattern is an effective and simple way to manage and configure atomic state changes and importantly Redux provides a common language and conventions for managing state within JavaScript applications.
- So that all is great however Redux is still not without some problems:
  - Redux tends towards becoming a global dependency that will have its tentacles throughout your codebase.
  - It can lead developers to be tempted to store far more state globally than is actually required.
  - Redux is considered as a state management container but is often used as an event bus which is a practice that depending on context could be considered an anti-pattern.
  - Redux does not deal well with asynchronicity out of the box and requires middleware to even support async events.
  - Redux does not deal with side effects out of the box either.
  - Integration with other implicit state management containers such as Routers have always been problematic.
  - You don’t actually need Redux to manage your application data because of the new React APIs.

- The (`state, action) => state` Reducer is at the heart of Redux as it controls the transformation stage of a data transaction. 
- When building a Redux driven React app you might want to think about the building blocks looking a little like this
  - A Component dispatches data in the form of an Action to the Pub/Sub or Event Bus implementation within Redux.
  - The Pub/Sub sends the data through a series of Middleware that manipulate the Action proceed with a mutation or defer it. I like to call this Transaction Pre-processing
  - Eventually the Action is sent through to a Transaction Engine which runs a pure Reducer function to merge the current State with the given Action immutably to produce a new state tree.
  - The new state tree is stored in a Data Store which exists as an in memory object but can also be cached elsewhere such as localStorage or a database.
  - The State Dependency Injector receives changes from the data store and provides the new state to components that require it
  - A recipient Component finally receives the new state and re-renders displaying the updated data.
- You can think about this flow and the technology mix that provides each piece in the following way where react-redux is the state dependency injector and redux itself provides several pieces. 

- The useReducer hook also manages to provide an immutable data store. 
- Then we can take advantage of the new useContext API to act as a state dependency injector. 

- Now above you can see that what is missing is a Pub/Sub (or Event System) and a Transaction Pre-processor.
- Some might argue that `useReducer` provides an Event System already in that it exposes a `dispatch` function that can be shared to children. 
  - The thing is that because of the details of React’s Fibre re-write and eventually-consistent state resolution, there is no easy way to apply a sequential transaction-preprocessing layer to useReducer. 
  - Basically this means it is far less problematic to use dispatch as a client of an Event System and the influx into the React side of the transaction as opposed to the Event System itself. 
  - You also get an extra advantage in separating your event dispatcher from your state which becomes important when you are temporally tying app contexts together that should not mix their data.
- There are also some concerns about `createContext`’s performance in terms of being able to render very fast state updates to a large shared state redux tree. 
- One of the things you gain by separating your event bus out from your state management is 
  - the ability to treat each part of state differently in terms of it’s performance requirements. 
  - So for most situations, using React’s createContext will be fine 
  - but when you require faster update performance, one technique available to you is to simply listen directly to dispatched events from the event bus and manage this internally with a local cache if required.

- With projects such as reinspect allowing developers to hook up Devtools to useReducer and useState, there is now no hard dependency on Redux for Redux devtools anymore

- So what should you actually use as your event system? 
- You might consider something like RxJS because you get a transaction pre-processing engine for free.
- Alternatively, we could use the isomorphic port of Node’s EventEmitter module to dispatch events. 
- This will work but it doesn’t support listening to wild-carded or name-spaced events which can be useful when we want to separate out sections of our app to only respond to relevant events. 
- I have found success with EventEmitter2 that allows for wildcard events. 
- It may not be for everyone but my technique was to wrap this in a simple Event Bus API that contains good TypeScript support providing only the small subset of the features I actually needed in an Event Bus. 
- I have created my own library for this technique called ts-bus .
- https://github.com/ryardley/ts-bus
  - TypeScript event bus to help manage your application architecture
- Either of these arrangements provides more flexibility than using Redux alone.

- There are many benefits to separating out the Event System from state management.
- You don’t always need state to change based on an event
  - Whilst it is common for state to be changed in response to an event, you don’t always need to connect state change with an event. 
  - Sometimes all that is needed is to start an asynchronous background process and have it report when it is done. 
  - Bringing external state in where it is not required leads to added complexity and overhead.
- You have limited your dependency exposure to a small simple component
  - An eventing system will become a major dependency hazard for any large app as every component that has to communicate with another will need to have access to an instance of your event dispatcher. 
  - By using a separate Event System we have avoided automatically connected state management to all your app components.
- You can manage asynchronicity however you like
  - Events are no longer tied to state change so async becomes easier. 
  - Want to use an async function to manage asynchronous events? 
  - Easy. You control how asynchronicity is managed and what state dependencies you have available. 
  - Admittedly, implementing a cancellable saga workflow is more difficult but that is never an easy problem to solve to begin with and is rarely actually required.
- It’s simple to track state in a separate store such as a Router
  - Occasionally state needs to be managed but cannot be tracked in your state container. 
  - This most often occurs with navigation where state is held within the browser URL via some kind of Router. 
  - Having a separate Event System means that you can easily provide a point of abstraction for your Router. 
  - An added benefit to this technique is that you don’t need to share your router code all over your application.
- You have the flexibility of an event driven architecture
  - By using a simple Event Emitter you can handle your events however you like. 
  - Whether that be by running handlers in service workers or by setting up Observable streams or offloading computation to a server. 
  - Send events to the server, receive events from the server, synchronise a second micro-Vue frontend application, Manage side effects with RxJS; 
  - So long as you can share your event bus, your application architecture can support it. 
  - This is the power of an event based architecture you have the ability to connect up your app however you like.

- Lastly, because we are talking about basic Event Bus architectures and Redux contains an Event Bus, 
  - these systems can certainly be set up by using Redux itself. 
  - The caveat here is that with Redux you drag along data with your bus that may actually cause more harm than good as developers inadvertently(不经意地) share state between systems that should remain separate.

- Redux is a valuable and versatile library but it is more than just a state management container. 
  - When you choose to use Redux, you are choosing your Event Bus, your Data Store, your canonical DI mechanism and so on 
  - and depending on a single package for all of these separate application functions may not be what you need in every situation.
- Whilst it certainly makes no sense to re-write a large app to remove Redux, 
  - due to Redux’s tendency towards becoming a global dependency, 
  - new or smaller apps should think carefully about whether or not their needs can be served by selecting an appropriate event bus and using in-built React state management 
  - as this will lead to a cleaner and more flexible architecture.
