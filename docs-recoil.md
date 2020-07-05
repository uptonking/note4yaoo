---
tags: [react, state]
title: docs-recoil
created: '1970-01-01T00:00:00.000Z'
modified: '2020-07-04T18:09:34.650Z'
---

# docs-recoil

- Recoil is an experimental set of utilities for state management with React.

## resources

- https://recoiljs.org/docs/introduction/getting-started
- https://github.com/facebookexperimental/Recoil

## Getting Started

``` typescript
import React from 'react';
import {
  RecoilRoot,
  atom,
  selector,
  useRecoilState,
  useRecoilValue,
} from 'recoil';

function App() {
  return (
    <RecoilRoot>
      <CharacterCounter />
    </RecoilRoot>
  );
}

function CharacterCounter() {
  return (
    <div>
      <TextInput />
      <CharacterCount />
    </div>
  );
}

const textState = atom({
  key: 'textState', // unique ID (with respect to other atoms/selectors)
  default: '', // default value (aka initial value)
});

function TextInput() {
  const [text, setText] = useRecoilState(textState);

  const onChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={onChange} />
      <br />
      Echo: {text}
    </div>
  );
}

const charCountState = selector({
  key: 'charCountState', // unique ID (with respect to other atoms/selectors)
  get: ({ get }) => {
    const text = get(textState);

    return text.length;
  },
});

function CharacterCount() {
  const count = useRecoilValue(charCountState);

  return <> Character Count: { count } </>;
}
```

## Motivation

- For reasons of compatibility and simplicity, it's best to use React's built-in state management capabilities rather than external global state. 
- But React has certain limitations:
  - Component state can only be shared by lifting it up to the common ancestor, but this might include a huge tree that then needs to re-render.
  - Context can only store a single value, not an indefinite set of values each with its own consumers.
  - Both of these make it difficult to code-split the top of the tree (where the state has to live) from the leaves of the tree (where the state is used).
