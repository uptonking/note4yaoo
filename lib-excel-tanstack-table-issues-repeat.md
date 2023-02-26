---
title: lib-excel-tanstack-table-issues-repeat
tags: [issues, repeat, tanstack-table]
created: 2021-12-15T07:00:06.143Z
modified: 2022-08-21T10:19:58.756Z
---

# lib-excel-tanstack-table-issues-repeat

# guide

# server side
- [A server side external sorting and filtering example · TanStack/table](https://github.com/TanStack/table/discussions/2033)
# hooks

## [Pass custom hooks conditionally in useTable](https://github.com/tannerlinsley/react-table/discussions/2452)

- React does not allow you to render hooks conditionally.
- There aren't many elegant solutions (that I know of) for this, I usually do one of the following:
  1. Forget about it and just use a single hook;
  2. Refactor/create new hook that does all that is needed. Maybe you can have a hook that allows you to change its instance behavior based on the `props.multi`? This could work, since it would still be the same hook rendered at all the times and you would be playing with its instance.
  3. Or you can keep both hooks rendered at all times and somehow use the `props.multi` to switch between their instances instead of rendering a different hook; 
- So, yeah, make sure the same hooks are rendered on every component render until it unmounts. You are able to play as much as you want with the hook instances, but you you can't conditionally render or not render them.

- The most important thing I've learned about hooks is to always offer an `enabled` property that essentially disables everything.

- I know this is an old thread, but I often use a key to force react to see it as a new component when I have something that needs to change the number of hooks. Not the most performant maybe, but a nice escape hatch.

```JS
const [multi, setMulti] = useState(false)
return <MyReactTable {...{ key: multi, data, columns, multi }}  />

const MyReactTable = ({ data, columns, multi }) => {
  const instance = useTable({ data, columns }, multi ? useRowSelect : useSingleRowSelect)
}
```
