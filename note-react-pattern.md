---
title: note-react-pattern
tags: [pattern, react]
created: '2021-05-11T14:35:46.252Z'
modified: '2021-05-11T14:36:13.256Z'
---

# note-react-pattern

# react pattern

# [The State Reducer Pattern with React Hooks](https://kentcdodds.com/blog/the-state-reducer-pattern-with-react-hooks)

- Downshift is currently implemented as a render prop component, 
  - because at the time, render props was the best way to make a "Headless UI Component" (typically implemented via a "render prop" API) 
  - which made it possible for you to share logic without being opinionated about the UI. 
- Today however, we have React Hooks and hooks are way better at doing this than render props. 

- As a reminder, the benefit of the state reducer pattern is in the fact that it allows "inversion of control" which is basically a mechanism for the author of the API to allow the user of the API to control how things work internally.
- Ok, so the concept goes like this:
  - End user does an action
  - Dev calls dispatch
  - Hook determines the necessary changes
  - Hook calls dev's code for further changes (this is the inversion of control part)
  - Hook makes the state changes

- Now, let's say we wanted to adjust the `<Toggle />` component so the user couldn't click the `<Switch />` more than 4 times in a row unless they click a "Reset" button

- an easy solution to this problem would be to add an if statement in the `handleClick` function and not call `toggle` if `tooManyClicks` is true, 

``` JS
function useToggle() {
  const [on, setOnState] = React.useState(false)
  const toggle = () => setOnState(o => !o)
  const setOn = () => setOnState(true)
  const setOff = () => setOnState(false)
  return { on, toggle, setOn, setOff }
}

// traditional solution: change useState
function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;
  const { on, toggle, setOn, setOff } = useToggle();

  function handleClick() {
    toggle()
    setClicksSinceReset(count => count + 1)
  }

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch on={on} onClick={handleClick} />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}
```

- use api to invert control

``` JS
function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;
  const { on, toggle, setOn, setOff } = useToggle({
    reducer(currentState, action) {
      const changes = toggleReducer(currenState, action);
      if (tooManyClicks && action.type === actionTypes.toggle) {
        // other changes are fine, but on needs to be unchanged
        return { ...changes, on: currentState.on }
      } else {
        // the changes are fine
        return changes
      }
    },
  });

  function handleClick() {
    toggle();
    setClicksSinceReset(count => count + 1);
  }

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch on={on} onClick={handleClick} />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}
```

- We could add logic to every one of these helper functions, but I'm just going to skip ahead and tell you that this would be really annoying
- https://codesandbox.io/s/9j0pkq30lo?from-embed

``` JS
import * as React from 'react'
import ReactDOM from 'react-dom'
import Switch from './switch'

const actionTypes = {
  toggle: 'TOGGLE',
  on: 'ON',
  off: 'OFF',
}

function toggleReducer(state, action) {
  switch (action.type) {
    case actionTypes.toggle: {
      return { on: !state.on };
    }
    case actionTypes.on: {
      return { on: true };
    }
    case actionTypes.off: {
      return { on: false };
    }
    default: {
      throw new Error(`Unhandled type: ${action.type}`)
    }
  }
}

function useToggle({ reducer = toggleReducer } = {}) {
  const [{ on }, dispatch] = React.useReducer(reducer, { on: false });
  const toggle = () => dispatch({ type: actionTypes.toggle });
  const setOn = () => dispatch({ type: actionTypes.on });
  const setOff = () => dispatch({ type: actionTypes.off });
  return { on, toggle, setOn, setOff };
}
// export {useToggle, actionTypes, toggleReducer}

function Toggle() {
  const [clicksSinceReset, setClicksSinceReset] = React.useState(0);
  const tooManyClicks = clicksSinceReset >= 4;

  const { on, toggle, setOn, setOff } = useToggle({
    reducer(currentState, action) {
      const changes = toggleReducer(currentState, action)
      if (tooManyClicks && action.type === actionTypes.toggle) {
        // other changes are fine, but on needs to be unchanged
        return { ...changes, on: currentState.on };
      } else {
        // the changes are fine
        return changes;
      }
    },
  });

  return (
    <div>
      <button onClick={setOff}>Switch Off</button>
      <button onClick={setOn}>Switch On</button>
      <Switch
        onClick={() => {
          toggle()
          setClicksSinceReset(count => count + 1)
        }}
        on={on}
      />
      {tooManyClicks ? (
        <button onClick={() => setClicksSinceReset(0)}>Reset</button>
      ) : null}
    </div>
  )
}

function App() {
  return <Toggle />
}
ReactDOM.render(<App />, document.getElementById('root'))
```

- Remember, what we've done here is enable users to hook into every state update of our reducer to make changes to it. 
  - This makes our hook WAY more flexible, 
  - but it also means that the way we update state is now part of the API 
  - and if we make changes to how that happens, then it could be a breaking change for users. 
  - It's totally worth the trade-off for complex hooks/components, but it's just good to keep that in mind.

- discussion

- https://twitter.com/kentcdodds/status/1256265379648700416
  - Great talk by @kentcdodds on why having too many props in a component can hurt performance and add unnecessary complexity, followed by a practical approach on how to avoid apropcalypse by using the state-reducer pattern with hooks!

## uncontrollable components

- https://github.com/jquense/uncontrollable
  - Wrap a controlled react component, to allow specific prop/handler pairs to be omitted by Component consumers. 
  - Uncontrollable allows you to write React components, with minimal state, and then wrap them in a component that will manage state for prop/handlers if they are excluded.
