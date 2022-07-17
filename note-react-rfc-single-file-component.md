---
title: note-react-rfc-single-file-component
tags: [react, rfc]
created: 2020-10-29T13:48:07.751Z
modified: 2021-02-17T04:09:23.752Z
---

# note-react-rfc-single-file-component

# guide

# discuss

- ## [React Single File Components Are Here](https://twitter.com/dan_abramov/status/1238810260082745344)
  - Dan Abramov: Not this particular format but it’s something that’s been on our mind a lot recently. 
    - The split we are interested in unifying though is more about server/client. 
    - (We use Suspense and error boundaries for visual states.) 
    - Watch out for Flight and Blocks work in React repo.
  - Blocks are generalization of “colocating the query without waterfalls” pattern from Relay, but without being tied to GraphQL. 
    - Instead of a query you have a function that runs on the server.
  - Hydration boundaries are `<Suspense>` components so nothing new there. Same place we already handle loading states.
  - Why is there no directives in reactjs? 引入新用法或DSL
    - We don’t like having a special way of doing things when you already have to learn JS constructs to do the same in other parts of your codebase.

- ref
  - [old proposal](https://github.com/react-sfc/react-sfc-proposal)

# blog

## [React Single File Components Are Here](https://www.swyx.io/react-sfcs-here/)

- The launch of RedwoodJS today marks a first: it is the first time React components are being expressed in a single file format with explicit conventions.
- For styling, we might use anything from Tailwind to Styled-JSX to Styled-Components/Emotion to Linaria/Astroturf to CSS Modules/PostCSS/SASS/etc and it is a confusing exhausting random eclectic mix of stuff that makes many experts happy and many beginners lost. 

- Here's what Redwood Cells look like

``` typescript
// Data Example 2
export const QUERY = gql`
  query {
    posts {
      id
      title
      body
      createdAt
    }
  }
`;

export const Loading = () => <div>Loading...</div>;

export const Empty = () => <div>No posts yet!</div>;

export const Failure = ({ error }) => <div>Error loading posts: {error.message}</div>;

export const Success = ({ posts }) => {
  return posts.map(post => (
    <article>
      <h2>{post.title}</h2>
      <div>{post.body}</div>
    </article>
  ));
};
```

- This is a format that is more native to React's paradigms than the Single File Component formats of Vue, Svelte, and my own React SFC proposal a year ago, and I like it a lot.
- Why Formats over Functions are better
  - The idea is that you don't actually need to evaluate the entire component's code and mock the data in order to access one little thing. I
  - This makes your components more consumable and statically analyzable by different toolchains, for example, by Storybook.

- Component Story Format(CSF)
- Team Storybook was actually first to this idea and a major inspiration for me, with it's Component Story Format. Here's how stories should be written

``` typescript
import React from 'react';
import { Button } from '@storybook/react/demo';

export default { title: 'Button' };

export const withText = () => <Button>Hello Button</Button>;

export const withEmoji = () => (
  <Button>
    <span role="img" aria-label="so cool">
      😀 😎 👍 💯
    </span>
  </Button>
);
```

- you can consume these files in a lot more different ways by different toolchains (including by design tools!) and none of them have to use Storybook's code, 
- because all they need to know is the spec of the format and how to parse JavaScript. 
  - (yes, JSX compiles to React.createElement, but that is easily mockable).

- Merging CSF and SFCs

``` typescript
// CSF + SFC Example
export default { 
  title: 'PostList',
  excludeStories: ['QUERY']
};

export const QUERY = gql`
  query {
    posts {
      id
      title
      body
      createdAt
    }
  }
`;

export const Loading = () => <div>Loading...</div>;

export const Empty = () => <div>No posts yet!</div>;

export const Failure = ({ error }) => <div>Error loading posts: {error.message}</div>;

export const Success = ({ posts }) => {
  return posts.map(post => (
    <article>
      <h2>{post.title}</h2>
      <div>{post.body}</div>
    </article>
  ));
};

```

- I think Styling is the last major frontier we need to integrate. Utility CSS approaches aside, here's how we can include static scoped styles for our components

``` typescript
// Styled SFC - Static Example
export const STYLE = `
  /* only applies to this component */
  h2 {
    color: red
  }
`
export const Success = ({ posts }) => {
  return posts.map(post => (
    <article>
      <h2>{post.title}</h2>
      <div>{post.body}</div>
    </article>
  ));
};

// Styled SFC - Dynamic Example
export const STYLE = props => `
  h2 {
    color: ${props.color} // dynamic!
  }
`
```

- What if styles or other future Single File Component segments need to interact with component state? We could lift hooks up to the module level

``` typescript
// Hooks SFC Example
const [toggle, setToggle] = useState(false)

export const STYLE = `
  h2 {
    color: ${toggle ? "red" : "blue"}
  }
`
export const Success = ({ posts }) => {
  return posts.map(post => (
    <article>
      <h2 onClick={() => setToggle(!toggle)}>{post.title}</h2>
      {toggle && <div>{post.body}</div>}
    </article>
  ));
};
```

- Dan Abramov replied with something I missed - the server/client split. 
  - There is ongoing work with React Flight (to do with streaming SSR) and Blocks (to do with blocking rendering without being tied to Relay/GraphQL) that I'm basically completely ignorant about.

- While Redwood uses exports to declare loading and error states, Suspense uses `<Suspense>` and error boundaries. 
  - It's possible to compile from the former to the latter but not the other way, 
  - which is a key point of the "formats over functions" idea - things are more consumable that way.

- It also brings to mind the work that Next.js has done with getStaticProps, getStaticPaths and getServerSideProps - as the first hybrid framework, 
  - it is nice to use static exports to let the framework pick from data requirements, as well as to not tie yourself so tightly to GraphQL. 
  - getStaticPaths in particular is very elegant - moving page creation inside components themselves.

- Conclusion - Ending with Why
  - It's reasonable to question why we want everything-in-one file rather than everything-in-a-folder. 
  - But in a sense, SFCs simply centralize what we already do with loaders.
  - Ultimately, Colocating concerns rather than artificially separating them helps us delete and move them around easier, and that optimizes for change.

## [Why I'm not a fan of Single File Components](https://dev.to/ryansolid/why-i-m-not-a-fan-of-single-file-components-3bfl)

- Single File Components(SFCs) are a style of application organization used by JavaScript UI libraries where each file represents a single component in all aspects. 
  - Typically they resemble an HTML document where you have HTML tags, Style Tag, and Script Tag all in a file. 
  - This is the common pattern for UI Frameworks like Vue and Svelte.
- I want to talk about the limitation of SFCs as a component format.
- Component Boundaries
  - So SFCs actually handle this pretty well. No problem so far. But let's dig deeper.
- Component Cost
  - I did some pretty deep performance testing of the Cost of Components in UI libraries. 
  - The TL; DR is for the most part, VDOM libraries like React scale well with more components whereas other libraries especially reactive libraries do not. 
  - They often need to synchronize reactive expressions with child component internals which comes at a small cost.
  - Where am I going with this? It isn't simple enough to congratulate the type of libraries that use SFCs for not forcing esoteric components on us.
- Component Refactoring
  - What is the most expensive part of refactoring? I'd personally nominate redefining boundaries.
  - React's Component model is actually pretty convenient for this. Starting with being able to have more than one component in a single file. 
  - When something gets a bit unwieldy we just break it off.
  - I mean how do you write less code in JavaScript? You write a function.
  - This is a simple example but this sort of one change touch multiple points is the same reason Hooks/Composition API/Svelte $ can produce more compact and easier maintainable code than class lifecycles. 
- The limitation of SFCs
  - The crux of the problem with restricting files to a single component is we only get a single level of state/lifecycle to work with. 
    - It can't grow or easily change. 
    - It leads to extra code when the boundaries are mismatched and cognitive overhead when breaking apart multiple files unnecessarily.
  - SFCs libraries could look at ways to do nested syntax. Most libraries. even non-SFC ones, don't support this though. 
    - React for instance doesn't allow nesting of Hooks or putting them under conditionals. 
  - And most SFCs don't really allow arbitrary nested JavaScript in their templates.
  - And that's why I dislike SFCs the same way I prefer Hooks over Class Components.
- SolidJS is a different UI Framework that while it looks similar to React uses granular reactivity instead of VDOM to handle DOM updates.
  - It's more similar to taking Vue's composition API and building a full render library from it
  - React introducing tuple returns with hooks solved a longstanding API issue I was having so I adopted it. 
  - But Solid being based completely on those primitives independent of the Component system has unlimited composability, which I was trying to highlight at the end of the document.
