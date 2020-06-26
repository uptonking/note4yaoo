---
tags: [docs, react]
title: read-docs-react-p5-codebase-deisgn-test
created: '2020-06-25T17:53:19.549Z'
modified: '2020-06-26T13:50:18.764Z'
---

# read-docs-react-p5-codebase-deisgn-test

## How to Contribute
- https://reactjs.org/docs/how-to-contribute.html

## Codebase Overview
- React has almost no external dependencies. 
  - However, there are a few relatively rare exceptions, such as fbjs.
- We don’t necessarily recommend any of these conventions in React apps.
  - Many of them exist for historical reasons and might change with time.
- After cloning the React repository, you will see a few top-level folders in it
	- `packages` contains metadata (such as package.json) and the source code (src subdirectory) for all packages in the React repository. 
	  - If your change is related to the code, the src subdirectory of each package is where you'll spend most of your time.
	- `fixtures` contains a few small React test applications for contributors.
	- `build` is the build output of React. 
    - It is not in the repository but it will appear in your React clone after you build it for the first time.
- We don't have a top-level directory for unit tests. 
  - Instead, we put them into a directory called `__tests__` relative to the files that they test.
- We recently started introducing Flow checks to the codebase. 
  - Files marked with the `@flow` annotation in the license header comment are being typechecked.
- React uses dynamic injection in some modules. 
	- The main reason it exists is because React originally only supported DOM as a target. 
	- React Native started as a React fork. We had to add dynamic injection to let React Native override some behaviors.
	- In the future, we intend to get rid of the dynamic injection mechanism and wire up all the pieces statically during the build.
- React is a monorepo containing multiple separate packages
	- React core is located in `packages/react` in the source tree. 
		- includes all the top-level React APIs
		- React.createElement()
		- React.Component
		- React.Children
		- React core only includes the APIs necessary to define components. 
    - It does not include the reconciliation algorithm or any platform-specific code.
		- It is used both by React DOM and React Native components.
	- Renderers manage how a React tree turns into the underlying platform calls.
		- React DOM Renderer renders React components to the DOM. 
		- React Native Renderer renders React components to native views. It is used internally by React Native.
		- React Test Renderer renders React components to JSON trees.
	- Reconcilers
    - Even vastly different renderers like React DOM and React Native need to share a lot of logic. 
    - In particular, the reconciliation algorithm should be as similar as possible so that declarative rendering, custom components, state, lifecycle methods, and refs work consistently across platforms.
    - To solve this, different renderers share some code. We call this part of React a “reconciler”.
		- Reconcilers are not packaged separately because they currently have no public API. 
		- Instead, they are exclusively used by renderers such as React DOM and React Native.
  - Stack Reconciler is the implementation powering React 15 and earlier. 
    - We have since stopped using it, but it is documented in detail in the next section
	- Fiber Reconciler is a new effort aiming to resolve the problems inherent in the stack reconciler and fix a few long-standing issues. 
    - It has been the default reconciler since React 16.
    - Ability to split interruptible work in chunks.
    - Ability to prioritize, rebase and reuse work in progress.
    - Ability to yield back and forth between parents and children to support layout in React.
    - Ability to return multiple elements from render().
    - Better support for error boundaries.
    - While it has shipped with React 16, the async features are not enabled by default yet.
    - Its source code is located in `packages/react-reconciler`
    - https://github.com/acdlite/react-fiber-architecture
    - https://blog.ag-grid.com/inside-fiber-an-in-depth-overview-of-the-new-reconciliation-algorithm-in-react/
	- `packages/legacy-events`
		- React implements a synthetic event system which is agnostic of the renderers and works both with React DOM and React Native.

## Implementation Notes for  Stack Reconciler
- https://reactjs.org/docs/implementation-notes.html
- It is very technical and assumes a strong understanding of React public API as well as how it’s divided into core, renderers, and the reconciler. 
- located at `src/renderers/shared/stack/reconciler`  
- The reconciler itself doesn’t have a public API. Renderers like React DOM and React Native use it to efficiently update the user interface according to the React components written by the user.
- **Mounting as a Recursive Process**
	- React elements are plain objects representing the component type (e.g. App) and the props.
	- User-defined components (e.g. App) can be classes or functions but they all “render to” elements.
	- Mounting is a recursive process that creates a DOM or Native tree given the top-level React element (e.g. <App />).
- **Mounting Host Elements**
	- In addition to user-defined (“composite”) components, React elements may also represent platform-specific (“host”) components. 
	- If element's type property is a string, we are dealing with a host element:
	- When the reconciler encounters a host element, it lets the renderer take care of mounting it. For example, React DOM would create a DOM node.
- **Introducing Internal Instances**
	- The key feature of React is that you can re-render everything, and it won't recreate the DOM or reset the state:
	- Instead of separate mountHost and mountComposite functions, we will create two classes: DOMComponent and CompositeComponent.
	- The composite internal instances need to store:
		- The current element.
		- The public instance if element type is a class.
		- The single rendered internal instance. It can be either a DOMComponent or a CompositeComponent.
	- The host internal instances need to store:
		- The current element.
		- The DOM node.
		- All the child internal instances. Each of them can be either a DOMComponent or a CompositeComponent.
- **Unmounting**
	- unmounting DOM components also removes the event listeners and clears some caches
- **Updating**
	- The goal of the reconciler is to reuse existing instances where possible to preserve the DOM and the state
	- When a composite component receives a new element, we run the componentWillUpdate() 
	- Host component implementations, such as DOMComponent, update differently. When they receive an element, they need to update the underlying platform-specific view. 
		- In case of React DOM, this means updating the DOM attributes
- **Updating Composite Components**
- **Updating Host Components**
- **Top-Level Updates**
- **What We Left Out**
- **Jumping into the Code**
- Stack reconciler has inherent limitations such as being synchronous and unable to interrupt the work or split it in chunks. 
- The new Fiber reconciler comes with a completely different architecture.

## Design Principles
- We wrote this document so that you have a better idea of how we decide what React does and what React doesn’t do, and what our development philosophy is like
  - This document assumes a strong understanding of React.
  - It describes the design principles of React itself, not React components or applications.
- The key feature of React is composition of components. 
	- Components written by different people should work well together. 
- Common Abstraction
	- If we notice that many components implement a certain feature in incompatible or inefficient ways, we might prefer to bake it into React. 
	-  raising the abstraction level benefits the whole ecosystem. State, lifecycle methods, cross-browser event normalization are good examples of this.
- Escape Hatches
	- If we can't figure out a perfect API for something that we found necessary in many apps, 
	   we will provide a temporary subpar working API as long as it is possible to get rid of it later and it leaves the door open for future improvements.
- Stability
	- We value API stability. At Facebook, we have more than 50 thousand components using React. 
	- When we add a deprecation warning, we keep it for the rest of the current major version, and change the behavior in the next major version.
- We place high value in interoperability with existing systems and gradual adoption.
	- This is why React provides escape hatches to work with mutable models, and tries to work well together with other UI libraries. 
- Scheduling
	- It is a key goal for React that the amount of the user code that executes before yielding back into React is minimal. 
	- This ensures that React retains the capability to schedule and split work in chunks according to what it knows about the UI.
- Developer Experience
- Debugging
- Configuration
	-  global configuration doesn't work well with composition. Since composition is central to React, we don't provide global configuration in code.
	- We do, however, provide some global configuration on the build level.
- Beyond the DOM
	- Being renderer-agnostic is an important design constraint of React.
	- React Native
- Implementation
	- We try to provide elegant APIs where possible. 
	- When we evaluate new code, we are looking for an implementation that is correct, performant and affords a good developer experience. Elegance is secondary.
- Optimized for Tooling
	- make the points of interaction with the library highly visible.
	- We value distinct verbose names, and especially for the features that should be used sparingly.
	- optimized for search
- Dogfooding
	- Dogfooding it means that our vision stays sharp and we have a focused direction going forward.

## Testing Overview
- There are a few ways to test React components. Broadly, they divide into two categories:
  - Rendering component trees in a simplified test environment and asserting on their output.
  - Running a complete app in a realistic browser environment (also known as “end-to-end” tests).
- This documentation section focuses on testing strategies for the first case. 
  - While full end-to-end tests can be very useful to prevent regressions to important workflows, such tests are not concerned with React components in particular, and are out of the scope of this section.
- When choosing testing tools, it is worth considering a few tradeoffs:
  - Iteration speed vs Realistic environment
  - How much to mock
- Jest is a JavaScript test runner that lets you access the DOM via jsdom. 
- React Testing Library is a set of helpers that let you test React components without relying on their implementation details.

## Testing Recipes
- Setup/Teardown
  - For each test, we usually want to render our React tree to a DOM element that’s attached to document. 
  - This is important so that it can receive DOM events. 
  - When the test ends, we want to “clean up” and unmount the tree from the document.
- act()
  - When writing UI tests, tasks like rendering, user events, or data fetching can be considered as “units” of interaction with a user interface. 
  - React provides a helper called `act()` that makes sure all updates related to these “units” have been processed and applied to the DOM before you make any assertions
  - This helps make your tests run closer to what real users would experience when using your application.
  - To avoid some verbose `act()` boilerplate, you could use a library like React Testing Library, whose helpers are wrapped with `act()`
- Rendering
  - test whether a component renders correctly for given props. 
- Data Fetching
  - Instead of calling real APIs in all your tests, you can mock requests with dummy data. 
  - Mocking data fetching with “fake” data prevents flaky tests due to an unavailable backend, and makes them run faster. 
- Mocking Modules
  - Some modules(like 3rd party Component GoogleMap) might not work well inside a testing environment, or may not be as essential to the test itself. 
  - Mocking out these modules with dummy replacements can make it easier to write tests for your own code.
- Events
  - We recommend dispatching real DOM events on DOM elements, and then asserting on the result. 
  - `button.dispatchEvent(new MouseEvent("click", { bubbles: true }));`
  - Different DOM events and their properties are described in MDN. 
  - Note that you need to pass `{ bubbles: true }` in each event you create for it to reach the React listener because React automatically delegates events to the document
- Timers
  - Your code might use timer-based functions like setTimeout to schedule more work in the future. 
  - We can write tests for this component by leveraging Jest’s timer mocks, and testing the different states it can be in
  - You can use fake timers only in some tests. 
  - The main advantage they provide is that your test doesn’t actually have to wait five seconds to execute, and you also didn’t need to make the component code more convoluted just for testing
- Snapshot Testing
  - Frameworks like Jest also let you save “snapshots” of data with toMatchSnapshot / toMatchInlineSnapshot. 
  - With these, we can “save” the rendered component output and ensure that a change to it has to be explicitly committed as a change to the snapshot.
  - It’s typically better to make more specific assertions than to use snapshots. 
  - These kinds of tests include implementation details so they break easily, and teams can get desensitized to snapshot breakages
  - Selectively mocking some child components can help reduce the size of snapshots and keep them readable for the code review.
- Multiple Renderers
  - In rare cases, you may be running a test on a component that uses multiple renderers. 
  - For example, you may be running snapshot tests on a component with `react-test-renderer`, that internally uses `ReactDOM.render` inside a child component to render some content. 
  - In this scenario, you can wrap updates with `act()`s corresponding to their renderers

## Testing Environments
- This document goes through the factors that can affect your environment and recommendations for some scenarios.
- Jest is widely compatible with React projects, supporting features like mocked modules and timers, and jsdom support. 
  - If you use Create React App, Jest is already included out of the box with useful defaults.
- Tests often run in an environment without access to a real rendering surface like a browser. 
- For these environments, we recommend simulating a browser with jsdom, a lightweight browser implementation that runs inside Node.js.
  - In most cases, jsdom behaves like a regular browser would, but doesn’t have features like layout and navigation.
  - Just like in a real browser, jsdom lets us model user interactions; tests can dispatch events on DOM nodes, and then observe and assert on the side effects of these actions 
  - A large portion of UI tests can be written with the above setup: using Jest as a test runner, rendered to jsdom, with user interactions specified as sequences of browser events, powered by the act() helper (example). 
  - For example, a lot of React’s own tests are written with this combination.
- Mocking functions
  - mock out the parts of our code that don’t have equivalents inside our testing environment (e.g. checking navigator.onLine status inside Node.js). 
  - This is especially useful for data fetching. 
  - It is usually preferable to use “fake” data for tests to avoid the slowness and flakiness due to fetching from real API endpoints
- Mocking modules
  - Some components have dependencies for modules that may not work well in test environments, or aren’t essential to our tests
  - It can be useful to selectively mock these modules out with suitable replacements 
- Mocking timers
  - Components might be using time-based functions like setTimeout, setInterval, or Date.now.
  - In testing environments, it can be helpful to mock these functions out with replacements that let you manually “advance” time. 
  - This is great for making sure your tests run fast!
- End-to-end tests
  - End-to-end tests are useful for testing longer workflows, especially when they’re critical to your business (such as payments or signups). 
  - For these tests, you’d probably want to test how a real browser renders the whole app, fetches data from the real API endpoints, uses sessions and cookies, navigates between different links
  - You might also likely want to make assertions not just on the DOM state, but on the backing data as well (e.g. to verify whether the updates have been persisted to the database).
  - Frameworks like Cypress, puppeteer and webdriver are useful for running end-to-end tests.
    - you can navigate between multiple routes and assert on side effects not just in the browser, but potentially on the backend as well.



