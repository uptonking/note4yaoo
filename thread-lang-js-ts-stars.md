---
title: thread-lang-js-ts-stars
tags: [js, lang, thread, typescript]
created: '2021-06-22T11:54:15.957Z'
modified: '2021-06-22T11:54:44.506Z'
---

# thread-lang-js-ts-stars

# pieces

- ## 


- ## 


- ## 


- ## 


- ## Question: Do you use an object, or an array of objects?
- https://twitter.com/housecor/status/1420032929829380107
  - Situation: You need to work with key/value pairs. 
- Object advantages:
  - Less code
  - Fast, direct access by key
- Array of object advantages:
  - Easily add another property if requirements change
  - Can document each property with a comment above the property in the type declaration
  - More obvious what the code means at a glance
- The point is, it all depends on requirements. 
  - Do I need to serialize it? Are the keys strings? `{ [K]: V }`;
  - Do I need to clear it? Key it by something other than a string? `Map<K,V>`;
  - Do I just need to loop over the key value pairs, and that's it? `[K,V][]`;
  - Am I trying to be slick with memory/loops? Maybe `[K, V, K, V]`;
-  what's most important:
   1. Does it work?
   2. Can my team maintain it?
   3. Can we test it?
- This 1,2,3 is very good before creating ANY abstraction
- 87% of the time - arrays. Will enable other indexing/iteration abilities. Examples: index by ID, group by role, filtering, mapping etc.
It's always easy to do _.keyBy(users, 'username') to get the object you mentioned, and keep the flexibility.
- Object has some upsides (ensures key is unique, faster getting value by key) and you can easily turn it into array with Object.entries if needed.
- In this case, it's clearly a set of objects. If needed for data access then reduce the array into a map and use either the objects themselves as the key and the desired result as the value.
- Another benefit of object is you can enforce uniqueness of your object keys.




- ## Just a reminder that using `reduce` doesn't always mean iterating less. 
- https://twitter.com/i_like_robots/status/1418874992146755584
  - 追求极致性能时可适度放弃immutable，使用mutable方法
  - The first example using has O(n²) complexity due to the additional iterations required by the spread operator and is ~50x slower than `filter/map` and ~100x slower than using array `push` .

```JS
// slow
items.reduce((acc, item) => item.prop ? [...acc, item.prop] : acc, []);

// equivalent to slow
items.reduce((acc, item) => {
  if (item.name) {
    return [].concat(
      typeof acc[Symbol.iterator] === 'function' ? acc.map(i => i) : [], item.name
    )

    return acc;
  }
}, []);

// fast
items.filter((item) => item.prop).map((item) => item.prop);

// faster
items.reduce((acc, item) => {
  item.prop && acc.push(item.prop);
  return acc;
}, []);
```

- if you're thinking "that's cool in theory but I'm sure engines have optimisations for this" then nope, you're wrong. And 100x slower is generous, some browsers are 1000x slower! If you're doing this lots of times in your apps then you could make them noticeably faster.
- And of course **`reduce` with object spread creating a newly cloned object for each iteration is no better - it's also super slow**.

- Ditch the `reduce` in the final example for a `for-of` loop to make it more readable. If you're using reduce simple for looping, just use a loop. Way less for the reader to think about, and it reads sequentially.

- Nice! It's also doesn't counted as a harmful mutation because it's internal scoped one with no effect on externals. @getify talked nicely about this in his book "Functional-light JavaScript"
  - tbh I don’t bother sticking to theory and mutate when it is ok

- ## If you were to quickly explain the fetch API to someone and you don't have an URL handy, data: URLs for the rescue!
- https://twitter.com/GNUmanth/status/1415560838472105984
  - const resp = await fetch('data:, {"name":"yoda"}')
  - const data = await resp.json()
- This is actually a great idea for tutorials. Usually I create some sort of mock. But this is definitely interesting
- This would work same way for all HTTP verbs ?
  - No, as it's not HTTP we can't use the verbs.
  - I would use http://httpbin.org (flask) in such cases
- http://httpstat.us/ is another useful site to test HTTP errors.
- What’s the function of the \uFEFF (zero-width no-break space?) here?
  - ou may skip it the ZWSP! According to RFC 2397: If `<mediatype>` is omitted, it defaults to "text/plain; charset=US-ASCII"

- ## Never realized destructing could be used to trim unwanted properties
- https://twitter.com/angustweets/status/1415734961886408704
  - const { yawn, sigh, ...usefulProperties } = obj; 
- I do a lot of that with React where the caller could pass lots of things but I only need to deal with a few.
- Removing a property from an object immutably by destructuring it

- ## TypeScript: How do you format members of enums?
- https://twitter.com/justinfagnani/status/1413886888528605184
- Solution: don't use enums. Stick to the type-system portion of TypeScript.
- Are there any other TS features that are not simply type-strippable?
  - enums, namespaces, constructor parameter properties, JSX, and debatably import assignment. 
  - TypeScript stopped adding non-type features and joined TC39 though, so that's all there ever will be now.
  - Oh and decorators, kind of, but that's a whole other story
- we can write an object that gives nice names to "enum" values, derive the type of the allowed values, and do exhaustiveness.
  - The thing I like about this pattern is the code is what you'd write in JS. The TS is just added types.
  - What you don't get as easily is the reverse mapping from value to name, but I find that I rarely use that, and you can write the utility pretty easily.
- Good points. Objects-as-enums really are easier to understand (compared to the subtle quirks of TS enums).
  - Depending on what is needed, a Java-style enum pattern can be useful, too

- ##  `export default thing` is different to `export { thing as default }`

- https://jakearchibald.com/2021/export-default-thing-vs-thing-as-default/
- Imports are references, not values
- But 'export default' works differently. 导出的是快照值

- ## don't let friends write JS functions with multiple optional parameters, each of which can have multiple overloaded values and behaviors
- https://twitter.com/acemarke/status/1409971795894181904
  - this tweet brought to you by me looking at the `connect` implementation for the first time in a while and my mind boggling at how the `mapState/mapDispatch` overload detection behavior is implemented
- All JavaScript functions should only be allowed to take one argument
  - you already do this in @Reactjs as "props" 
- When I got started with JS, I treated jquery's design as the ideal and made functions with lots of different overloads and argument shortcuts.
  - First awkwardness was when I had to make some wrapper functions around these and it was pain making the wrappers support parsing the args the same way. 
  - It's a solvable problem, but it was effort for a design that had other downsides too. Sometimes you have to judge whether it's worth it to solve a problem versus just removing the problem.
- I’m increasingly close to adding a lint rule that forces all function definitions to have 0 or 1 param. Object definitions are cheap enough that I don’t see much a reason to have multiple function params
  - 0 or 1 required, 1 optional (often boolean), is my empirical limit

- ## What's the best way to dynamically import an npm package on the client-side? Like in documentation code playgrounds.
- https://twitter.com/diegohaz/status/1409278109573160960
- By appending a script at runtime. Use something like react helmet
- Perhaps dynamically replace the imports with links to a CDN like https://skypack.dev ?

- ## named exports exports a dynamic reference to the variable being exported, 
- https://twitter.com/yagopereiraaz/status/1406974989203611654
  - default exports only export the current value of the variable at the time of import.
- This is intentional in the spec.
  - `export default <expr>` snapshots the value of `<expr>` as if it were a new constant binding
  - `let x = 1;  export { x as default }` results in x becoming a live binding for the default export
- I very rarely use default exports as they don't play so well with refactoring tooling. This feels like another reason to double down on that choice!
  - I wrote a short (internal) article to prefer named exports. 
  - In particular, as an alternative to the common pattern of having a default exported object that contains all the functions you want to expose.
  - So far it seems uncontroversial.
- Please tell me you titled it "default exports considered harmful"
  - Unfortunately it's just a preference so doesn't deserve such a famous label.
- is this why you can't default export a declaration? example: export default const hello = 'world'; 
- Default exports de-sugar roughly to the below, which is why incrementing num has no effect. It's assignment by value, not reference.(Invalid syntax since you can't name an export "default", but you get the point).
  - `export const default = num'` 类似
- Same if you actually define a function at the module to update the variable thats being exported. Defaults exports are immutable, it seems
