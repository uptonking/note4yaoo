---
title: job-coding-react-family
tags: [coding, job, react, 手撕代码]
created: '2021-09-22T17:13:19.314Z'
modified: '2021-10-05T15:35:15.751Z'
---

# job-coding-react-family

# hooks

```JS
export function usePrevious(state) {
  const ref = useRef();

  useEffect(() => {
    ref.current = state;
  });

  return ref.current;
}
```

# redux-like

# react-router-like

# jsx-parser

# react-like
