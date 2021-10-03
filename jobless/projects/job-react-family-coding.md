---
title: job-react-family-coding
tags: [coding, job, react, 手撕代码]
created: '2021-09-22T17:13:19.314Z'
modified: '2021-09-22T17:13:55.420Z'
---

# job-react-family-coding

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
