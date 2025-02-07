---
title: pattern-dev-functional
tags: [functional, pattern]
created: 2020-08-28T07:37:32.196Z
modified: 2020-12-20T16:01:15.556Z
---

# pattern-dev-functional

# guide

- 函数式编程
  - 对象字面量的属性为函数时，使用this需要注意

- 闭包
  - 私有变量可以放置外部拿到，但class对象的私有属性外部也可以拿到
# reactivity
- [Patterns for Reactivity with Modern Vanilla JavaScript_202308](https://frontendmasters.com/blog/vanilla-javascript-reactivity/)
  - https://twitter.com/1Marc/status/1693672383360508261

- [A Reactive Framework in 40 Lines](https://www.ctnicholas.dev/articles/reactive-framework-in-40-lines)
# [A Simple, Functional Module Pattern for TypeScript](https://spin.atomicobject.com/2017/10/26/typescript-functional-module-pattern/)
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

```typescript
interface SearchParams {
  readonly query: string;
  readonly facets: FacetConstraints.Type;
  readonly page: number;
  readonly limit?: number;
}

export type Type = SearchParams;
```

- Export your API for dealing with this abstraction

```typescript
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

```typescript
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

```typescript
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

# discuss-functional
- ## 

- ## 

- ## 

- ## [If Inheritance is so bad, why does everyone use it? | Hacker News _202404](https://news.ycombinator.com/item?id=39999019)
- The key is "prefer composition to inheritance" and dates back to Gang of Four.

- Nobody calls it this, but cascading styles in CSS is just like inheritance and I think should be avoided for all the same reasons. I feel it's a big part of why CSS at scale becomes unmaintainable. There isn't even a built-in way to compose two classes together if you want to avoid cascading/inheritance.

- 
- 
- 

- ## [What is a simple explanation of Decorators in JavaScript and how useful is it in functional programming - Stack Overflow](https://stackoverflow.com/questions/50168239/what-is-a-simple-explanation-of-decorators-in-javascript-and-how-useful-is-it-in)
- Decorators are specific to classes. As long as you don't mix OOP and FP, they aren't useful. 
- The other benefit of using functional programming is that, the testing becomes super easy because you have to test individual functions and while coding in react, it saves a lot of your time and energy. I use `recompose` all the time and don't even use the `class` keyword.

- ## [haskell - Functional equivalent of decorator pattern? - Stack Overflow](https://stackoverflow.com/questions/7064389/functional-equivalent-of-decorator-pattern)
- Currying functional parameters / composition is the closest equivalent. 
  - However, it's a mistake to even ask this question, because patterns exist to compensate for weaknesses in the host language.

- ## OOP really disillusioned generations of programmers into thinking the way to do polymorphism is to construct overly complex class hierarchies instead of just using sum types (tagged/discriminated unions)
- https://twitter.com/zack_overflow/status/1709670429680353718
- What are sum types?
  - The non-insane way to represent data that takes up multiple forms: Sum types fall under a category types known as "Algebraic data types" which just mean types that can be composed. ez way to think of sum types is they can be composed by "adding" multiple types together
- Isn’t the polymorphic example actually Shape.area() vs area(shape)?
  - I take polymorphism to mean types that can take up multiple shapes.
  - The example I gave is a case where there is a finite amount of shapes, it's just better to construct a sum type
  - The other non-OOP approach which I think you are thinking of is typeclasses/interfaces/traits (depending on which language you use), which let you accept any type that implements an interface

- If only the first ANSI standardized OOP system was mainstream, where classes do not own their methods. Instead most langs went with something like the structs with function pointers approach, and this world is the result.

- The one thing I can't get around is dynamic dispatch. Still end up with classes between layers and procedural within each layer
  - Not to mention the performance implications of it
- we don't need dynamic dispatch through sum types, we have dynamic dispatch at home

- Sum types are better for many cases but one goal of Java style OOP was PitL: allow many teams working separately to contribute to a whole. Can sum types that require all variants (whether they are represented as sub-types) to appear in the same compilation help with PitL?
  - Scala style sealed classes (and as adopted by Kotlin) have really nicely integrated discriminated unions and by-construction style programming into an ecosystem that still allows for OOP-style modelling where it's appropriate.

- The biggest benefit of classes is not polymorphism, it is data abstraction. Which sum types do not give you.

- It's all good until you realize you need to extend the sum. Or someone else's sum.
