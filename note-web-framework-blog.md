---
title: note-web-framework-blog
tags: [blog, framework, web]
created: '2020-11-08T10:01:14.339Z'
modified: '2020-11-08T10:02:00.337Z'
---

# note-web-framework-blog

## web-framework

### [lit-html vs hyperHTML vs lighterhtml_201902](https://webreflection.medium.com/lit-html-vs-hyperhtml-vs-lighterhtml-c084abfe1285)

- When `lit-html` released at the end of July 2017 as an experimental, not production ready, library, 
  - I’ve created few days after a huge gist comparing it with what was, at that time, the already production ready `hyperHTML`.
- `lighterhtml` was also recently born as hyperHTML drop-in simplified alternative, making the comparison actually fair
- To start with, hyperHTML has a viperHTML node server side alter ego, with API features parity, asynchronous streamed renders, and components.
  - viperHTML is isomorphic hyperHTML , but deprecated
  - This is also true for most modern alternatives of mine, such as ucontent, but if that's the only deal breaker, have a look at heresy-ssr, which is 1:1 based on lighterhtml, hence likely always 100% in features parity with it, 
- Removing all these features, plus simplifying the API, was the goal of lighterhtml, 
  - which in its 0.9 version is as fast as lit-html, but also always smaller, in size, than hyperHTML

- **lit-html VS lighterhtml**
- It is true that lit-html might be slightly richer in features, if you use its directives, 
  - but what I consider important here, is what we can do with just their core, summarized as such:
    - be as standard based as possible
    - create, and use, arbitrary DOM content
    - be able to quickly change content on the page (aka: DOM diffing)
  - These points are what lit-html core offers as a whole, while lighterhtml includes some extra feature we’ll see, and compare, later on.

- How much standard ?
  - Both lighterhtml and lit-html are based on “just standards”, meaning you can use JS without the need to transpile it, and you declare HTML, or SVG, through template literals.
- As developer, you don’t need to do anything different than writing HTML as you know, the library will figure out at runtime, 
  - accordingly with the kind of node it’s dealing with, what should result as input.value, as input.disabled, and as input.addEventListener("click", handler) .
- The only real non standard syntax available in lighterhtml, but already widely accepted by the community, is the self closing tag.

- What does `html` return ?
  - In the case of lit-html, the html function tag returns some instance of some internal class used by the library to understand its own content.
  - In lighterhtml though, you can use right away html or svg to create content

- What about performance ?
  - There are two sides to this metric: 
    - one is the bundled size, where smaller would mean faster time to be interpreted, 
    - and one is the raw rendering performance of the library itself.
  - Currently, lighterhtml wins in the keyed benchmark 
    - while lit-html wins in the non keyed one
    - if you’d like to know why lighterhtml is heavier, 
      - it’s mostly because it inherits the same compatibility granted by hyperHTML, 
      - and it patches internally, at runtime, a lot of little gotchas found in various browsers or JavaScript transpilers.
    - lit-html also fixes through little global runtime shims some browser, but it’s not as backward compatible as lighterhtml is.
- What does keyed VS non-keyed mean?
  - In few words, keyed results are the one you’d expect the most, while non keyed results mean that any created node could represent any sort of data.
  - If it makes any sense, you can think of non-keyed as the result of any server side rendered page, 
    - where nodes that relate to specific articles, items, database results, or user preferences, are just on the layout with some info exposed through some attribute.
  - With keyed results, html.for(entity) will always return the node associated to entity object, 
    - giving us the ability to eventually retrieve, or update, directly, 
    - any node associated to a single entity without even knowing if such node has been already rendered or not.
    - Instead, only what needs to get updated will actually get updated, as you can see in the console.

- In both hyper and lighterhtml case, updates are performed through the domdiff helper 
  - which uses just a node and any sort of algorithm to quickly compute the amount of changes needed between one DOM state, and another.
- Beside constant faster time in the initial creation, I wouldn’t say lighterhtml is any significantly faster than lit-html in these Code Pens.

- I think both lighterhtml and lit-html win on the Web, cause both provide a relatively straight forward and simple mechanism to create, and update, any sort of content.

- lit-html pros
- built-in directives to simplified common tasks and easily extends the lib
- smallest core when directives, repeat, style-map, and guard functionalities are not needed
- blazing fast compared to any bigger framework

- lighterhtml pros
  - React like hooks out of the box through its `lighterhtml.hook(useRef)`feature 
    - and any hooks oriented project such as augmentor, dom-augmentor, or TNG-Hooks, 
    - so that hooks can provide a way to extend renders as you need, just like directives would do
  - simple to start, simpler to use when it comes to keyed items, 
    - with no need of a repeater and style maps out of the box
  - widely backward compatible and transpilers resistant
  - blazing fast compared to any bigger framework
  - it always wins in terms of memory consumption

## ref

- [Vanilla JS Plugins](https://vanillajstoolkit.com/plugins/)
  - These are hand-selected plugins that I would actually use or have used on a project.
  - 大多数framework agnostic，质量高
- [Building State management system like react from scratch with VanillaJS.](https://dev.to/logeekal/building-state-management-system-like-react-from-scratch-with-vanillajs-3eon)
  - I want to build a state Management system similar to React but very bare-bones. 
  - But it should follow one-way data flow. 
