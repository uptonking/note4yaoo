---
title: pattern-dev-functional
tags: [functional, pattern]
created: '2020-08-28T07:37:32.196Z'
modified: '2020-12-20T16:01:15.556Z'
---

# pattern-dev-functional

## A Simple, Functional Module Pattern for TypeScript

- [A Simple, Functional Module Pattern for TypeScript](https://spin.atomicobject.com/2017/10/26/typescript-functional-module-pattern/)

- We’ve been using TypeScript with our React apps quite a bit recently. 
- One common need that we have when programming in a functional style is a good pattern for creating small abstractions that can be used widely in an application.
- These are the kind of things where you might traditionally use a class, but we wanted a pattern that would be:
  - Based on simple data, not objects
  - Functional – able to work well with Redux
  - Easy to use, where the abstraction in use is clear
  - Well-supported by editor autocomplete
  - Able to lend itself to tree shaking with webpack.

- The problem with classes is that they’re not simple data and don’t lend themselves to serialization. 
- A class gives you a few things:
  - A type – a shape that TypeScript will check your code against
  - Operations on that type
  - A code pattern that groups operations with values of that type(数据与行为绑定)

- After trying a few approaches, we settled on a pattern inspired from ML-like languages, such as F#. 
- When we identify an abstraction we want to implement, we create an ES module for that abstraction that exports a type called Type and a set of functions and lenses for operating on that type.

- Define yor type

``` typescript
interface SearchParams {
  readonly query: string;
  readonly facets: FacetConstraints.Type;
  readonly page: number;
  readonly limit?: number;
}

export type Type = SearchParams;
```

- Export your API for dealing with this abstraction

``` typescript
export const EMPTY: SearchParams = {
  query: "",
  page: 1,
  facets: FacetConstraints.EMPTY
};

export const query = Lens.from<SearchParams>().prop("query");
export const facets = Lens.from<SearchParams>().prop("facets");
export const page = Lens.from<SearchParams>().prop("page");
/** Check if a thing is a valid SearchParams.SearchParams */
export function isValid(aThing: any): aThing is SearchParams {
  // ...
}
/** Convert to a query string which can be put in the search page URL */
export function toQueryString(searchParams: SearchParams) {
	// ...
}

/** Attempt to convert a query string into a SearchParams.SearchParams. This can fail. */
export function fromQueryString(queryString: string): SearchParams | null {
	// ...
}

```

- Example use and editor support

``` typescript
import * as SearchParams from 'domain/search-params';

function updateFacets(
  searchParams: SearchParams.Type,
  facets: FacetConstraints.Type
) {
  searchParams = SearchParams.facets.set(searchParams, facets);
  searchParams = SearchParams.page.set(searchParams, 1);
  return searchParams;
  }
// We can also create local aliases of the module in cases where we’re dealing primarily with one abstraction
const SP = SearchParams;
SP.fromQueryString(query);

```

- [Small, Simple, Functional Lenses for TypeScript](https://spin.atomicobject.com/2017/09/27/typescript-lens-library/)
  - https://github.com/atomicobject/lenses

- Building apps in Redux requires frequent updates to nested immutable data structures–something that’s not particularly natural in TypeScript or JavaScript.
- Static functional languages solved this problem long ago with lenses–functional get/set pairs that can be used to read/update values within data structures, composed together, and more. 
- One way to think of them is like a type- and memory-safe functional pointer offset. 
- Given a base structure and an offset in C, I can read from and write to a value within it…except lenses are much safer.
- We put together a tiny little lens library for TypeScript, focusing on the following qualities:
  - Small size
  - Static type safety
  - Composition over DSLs
  - Zero dependencies

- Lenses are getter/setter pairs that let you represent a location within some data structure for both reading and updating that location. 
  - "Update" in this case is in the functional sense – not by mutation, but by creating a new data structure with a new value in the location of interest. 
  - A little like a pointer offset in C, but memory-, type-, and mutation-safe.

``` typescript
// define a type
type Something = { foo: number; bar: string };

// define a helper module with lenses for interacting with this type
export namespace Something = {
  export const foo = Lens.from<Something>().prop("foo");
  export const bar = Lens.from<Something>().prop("bar");
}

// Given a value of type Something
let o: Something = { foo: 1, bar: "hello" };

// Get the foo of a Something
expect(Something.foo.get(o)).toBe(1);
// Or just treat the lens as a function to do the same thing:
expect(Something.bar(o)).toEqual("hello")

// And we can create updated by setting the lens:
let o2 = Something.foo.set(o, 10);
expect(o2).toEqual({ foo: 10, bar: "hello" });

let o3 = Something.foo.update(o, i => i+1);
expect(o3).toEqual({ foo: 2, bar: 'hello'})
```
