---
title: job-coding-react-hooks
tags: [coding, job, react]
created: '2021-10-05T08:58:25.956Z'
modified: '2021-10-05T08:59:17.141Z'
---

# job-coding-react-hooks

# guide

# react-use

```JS
export function usePrevious(val) {
  const ref = useRef();

  useEffect(() => {
    ref.current = val;
  });

  return ref.current;
}
```
