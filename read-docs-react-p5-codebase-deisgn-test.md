---
tags: [docs, react]
title: read-docs-react-p5-codebase-deisgn-test
created: '2020-06-25T17:53:19.549Z'
modified: '2020-06-25T18:01:16.082Z'
---

# read-docs-react-p5-codebase-deisgn-test

## How to Contribute

- https://reactjs.org/docs/how-to-contribute.html   
- Before submitting a pull request, please make sure the following is done:
	- Fork the repository and create your branch from master.
	- Run yarn in the repository root.
	- If you've fixed a bug or added code that should be tested, add tests!
	- Ensure the test suite passes (yarn test). 
	- yarn flow runs the Flow typechecks.
	- yarn build creates a build folder with all the packages.
	- yarn build react/index,react-dom/index --type=UMD creates UMD builds of just React and ReactDOM.

## Codebase Overview

- React has almost no external dependencies. However, there are a few relatively rare exceptions, such as fbjs.
- After cloning the React repository, you will see a few top-level folders in it
	- `packages` contains metadata (such as package.json) and the source code (src subdirectory) for all packages in the React repository. 
	  If your change is related to the code, the src subdirectory of each package is where you'll spend most of your time.
	- `fixtures` contains a few small React test applications for contributors.
	- `build` is the build output of React. It is not in the repository but it will appear in your React clone after you build it for the first time.
- We don't have a top-level directory for unit tests. Instead, we put them into a directory called __tests__ relative to the files that they test.
- We recently started introducing Flow checks to the codebase. Files marked with the @flow annotation in the license header comment are being typechecked.
- React uses dynamic injection in some modules. 
	- The main reason it exists is because React originally only supported DOM as a target. 
	- React Native started as a React fork. We had to add dynamic injection to let React Native override some behaviors.
	- In the future, we intend to get rid of the dynamic injection mechanism and wire up all the pieces statically during the build.
- React is a monorepo. Its repository contains multiple separate packages
	-  React core is located in `packages/react` in the source tree. 
		-  includes all the top-level React APIs
		- React.createElement()
		- React.Component
		- React.Children
		- React core only includes the APIs necessary to define components. It does not include the reconciliation algorithm or any platform-specific code.
		- It is used both by React DOM and React Native components.
	- Renderers manage how a React tree turns into the underlying platform calls.
		- React DOM Renderer renders React components to the DOM. 
		- React Native Renderer renders React components to native views. It is used internally by React Native.
		- React Test Renderer renders React components to JSON trees.
	-  different renderers share some code between them. We call this part of React a “reconciler”.
		- Reconcilers are not packaged separately because they currently have no public API. 
		- Instead, they are exclusively used by renderers such as React DOM and React Native.
		- The “stack” reconciler is the implementation powering React 15 and earlier. We have since stopped using it
		- The “fiber” reconciler is a new effort aiming to resolve the problems inherent in the stack reconciler and fix a few long-standing issues. It has been the default reconciler since React 16.
			- Ability to split interruptible work in chunks.
			- Ability to prioritize, rebase and reuse work in progress.
			- Ability to yield back and forth between parents and children to support layout in React.
			- Ability to return multiple elements from render().
			- Better support for error boundaries.
			- While it has shipped with React 16, the async features are not enabled by default yet.
			- Its source code is located in `packages/react-reconciler`
	- `packages/events`
		- React 实现了一个合成的事件系统，它是渲染器不可知的，在React DOM 和React Native 中工作

## Implementation Notes for  Stack Reconciler

-  located at `src/renderers/shared/stack/reconciler`
- Mounting as a Recursive Process
	- React elements are plain objects representing the component type (e.g. App) and the props.
	- User-defined components (e.g. App) can be classes or functions but they all “render to” elements.
	- Mounting is a recursive process that creates a DOM or Native tree given the top-level React element (e.g. <App />).
- Mounting Host Elements
	- In addition to user-defined (“composite”) components, React elements may also represent platform-specific (“host”) components. 
	- If element's type property is a string, we are dealing with a host element:
	- When the reconciler encounters a host element, it lets the renderer take care of mounting it. For example, React DOM would create a DOM node.
- Introducing Internal Instances
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
- Unmounting
	- unmounting DOM components also removes the event listeners and clears some caches
- Updating
	- The goal of the reconciler is to reuse existing instances where possible to preserve the DOM and the state
	- When a composite component receives a new element, we run the componentWillUpdate() 
	- Host component implementations, such as DOMComponent, update differently. When they receive an element, they need to update the underlying platform-specific view. 
		- In case of React DOM, this means updating the DOM attributes
- Stack reconciler has inherent limitations such as being synchronous and unable to interrupt the work or split it in chunks. 
- https://reactjs.org/docs/implementation-notes.html
	- more details

## Design Principles

- This document assumes a strong understanding of React. It describes the design principles of React itself, not React components or applications.
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


