---
title: thread-fwk-lit-html-element
tags: [lit-element, lit-html, thread]
created: '2021-01-07T19:36:55.221Z'
modified: '2021-01-07T19:37:16.414Z'
---

# thread-fwk-lit-html-element

## lit-html vs handlebars

- lit-html approach is very similar to what handlebars template do. Perhaps with nicer syntax and dev experience
  - Much more than that. 
  - Using platform caching mechanism for speed.
  - No transpilation needed and the list goes on

- Some template languages have built-ins for ifs and loops. like `{{#if }}` in Handlebars. 
  - lit-html is more like JSX in that templates themselves have no control-flow, and control-flow is done by composing templates with JS.
  - `when()` is JavaScript, and a directive. 
    - It's not part of the core functionality, and not part of any template syntax. 
    - It's just a JavaScript expression that interacts with the Parts API.

- Polymer 3 and lit-html have very different template syntaxes. 
  - lit-html is pure JavaScript, not handlebars-like. 
  - lit-html is easier to debug than JSX because it's plain, standard, JavaScript and doesn't get transformed by a build step. 
  - You debug the actual source.

# pieces

 
