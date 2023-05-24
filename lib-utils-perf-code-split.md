---
title: lib-utils-perf-code-split
tags: [code-split, perf, utils]
created: 2023-05-24T17:45:06.809Z
modified: 2023-05-24T17:46:24.865Z
---

# lib-utils-perf-code-split

# guide

# dev

# [loadable-components](https://loadable-components.com/docs/getting-started/)

- Loadable lets you render a dynamic import as a regular component.

```JSX
import loadable from '@loadable/component';

const OtherComponent = loadable(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <OtherComponent />
    </div>
  )
}
```

- The best way to introduce code-splitting into your app is through the dynamic `import()` syntax.
- React supports code splitting out of the box with `React.lazy`. However it has some limitations, this is why `@loadable/component` exists.
  - `Suspense` is not available server-side and `React.lazy` can only work with `Suspense`. 
  - That's why today,  `React.lazy` is not an option if you need Server Side Rendering.
# more
