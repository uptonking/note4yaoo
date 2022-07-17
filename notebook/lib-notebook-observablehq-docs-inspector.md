---
title: lib-notebook-observablehq-docs-inspector
tags: [docs, inspector, notebook, observablehq]
created: 2021-05-22T18:46:37.275Z
modified: 2021-05-22T18:47:06.718Z
---

# lib-notebook-observablehq-docs-inspector

# guide
- inspector是runtime的observer实现方式的一个示例
# docs
- https://github.com/observablehq/inspector
  - implements the default strategy for rendering DOM and JavaScript values into a live web page — although you’re free to write your own.
  - takes live values from the notebook and puts them into your HTML
  - The inspector doesn’t include any inline styles, but there is a default stylesheet
    - https://github.com/observablehq/inspector/blob/master/src/style.css

- An inspector implements the Observable runtime’s Observer interface by rendering the current value of its associated variable to a given DOM element. 
  - Inspectors display DOM elements “as-is”, and create interactive “devtools”-style inspectors for other arbitrary values such as numbers and objects.
- When used with the Observable runtime as observers, inspectors can insert elements into the DOM and render interactive displays for arbitrary values.
