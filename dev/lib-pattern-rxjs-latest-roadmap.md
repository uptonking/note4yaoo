---
title: lib-pattern-rxjs-latest-roadmap
tags: [pattern, roadmap, rxjs]
created: 2020-12-14T14:43:37.508Z
modified: 2020-12-14T14:44:16.570Z
---

# lib-pattern-rxjs-latest-roadmap

# guide

- ref
  - [[WIP] Roadmap V7](https://github.com/ReactiveX/rxjs/issues/5795)

# latest

## [RxJS 7 and Beyond: What to Expect and Prepare For_202012](https://labs.thisdot.co/blog/rxjs-7-and-beyond-what-to-expect-and-prepare-for)

- we interviewed Ben Lesh, the author of RxJS, on the most recent updates for RxJS 7 and its targeted release date.
- Better TypeScript typings
  - RxJS implementation is using all of the stricter settings for TypeScript, We're trying to be strict as possible and I recommend that too by the way.
- .toPromise operator will be deprecated in RxJS 7 and it will be removed by RxJS 8
  - In its place, you'll find firstValueFrom() and lastValueFrom().
- RxJS is smaller
  - it's now almost 50% smaller.
  - The original code was written 6 years ago and there have been about four rewrites 
- RxJS 7 and Beyond
  - It looks like, at this point, version 8 will not need to be a complete rewrite. 
  - RxJS 8 will just go through the pending deprecations and finally get rid of them, 
  - mainly because a lot of them were sitting there for about 2 years. 
- What about RxJS 9 or even future versions?
  - Ben explained that some libraries and APIs started using the `AbortSignal` interface
  - It can be used currently with fetch as a cancellation primitive
  - This API exists in the browser, and will be available in Node.js. 
  - RxJS would probably want to use the same cancellation mechanism. 
