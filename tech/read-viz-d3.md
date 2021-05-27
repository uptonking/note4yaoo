---
title: read-viz-d3
tags: [d3, read, viz]
created: '2021-05-27T19:54:19.960Z'
modified: '2021-05-27T19:54:31.731Z'
---

# read-viz-d3

# d3 for the impatient_201906

## c1

- I believe that many of the difficulties experienced by new users are due to incorrect assumptions.
  - the new user is unpleasantly surprised at the verbosity required to set something as elementary as the color of an element
- The mistake here is that D3 is not a graphics library: 
  - instead, it is a JavaScript library to manipulate the DOM tree! 
  - Its basic building blocks are not circles and rectangles, but nodes and DOM elements; 
  - the typical activity does not involve the painting of a graphical shape on a canvas, but the styling of an element through attributes
  - The “current location” is not so much given through an xy- coordinate on a canvas, but through a selection of nodes in a DOM tree.
- D3 is a web technology, and relies on a collection of other web technologies; 
  - the DOM API and event model, Cascading Style Sheet (CSS) selectors and properties, the JavaScript object model, and of course Scalable Vector Graphics (SVG).
  - D3 does make them easier to use, and it provides a considerable amount of unification and abstraction on top of them.
  - The only area where it is definitely not enough to “wing it” is SVG.
- **why d3**
  - D3 provides a convenient way to deliver graphics over the web
  - D3 makes it easy and convenient to create animated and interactive graphics
  - easy-to-learn, and easy-to- use framework for general-purpose DOM handling

- ### Conventions of the D3 API
- D3 is primarily an access layer to the DOM tree. 
  - As a rule, D3 makes no attempt to encapsulate underlying technologies, and instead provides convenient, but otherwise generic, handles on them. 
  - For example, D3 does not introduce “circle” or “rectangle” abstractions of its own, but instead gives the programmer direct access to the SVG facilities for creating graphical shapes. 
  - The advantage of this approach is that D3 is tremendously adaptable and not tied to one particular technology or version. 
  - The disadvantage is that programmers need to have knowledge of the underlying technologies, in addition to D3, since D3 itself does not provide a complete abstraction layer.
- Because JavaScript does not enforce formal function signatures, all function arguments are technically optional. 
  - Many D3 functions use the following idiom:
  - when called with appropriate arguments, these functions act as setters; 
  - when called without arguments, these functions act as getters
  - To entirely remove a property, call the appropriate setter while supplying `null` as argument.
- When called as setters, functions typically return a reference to the current object, thus enabling method chaining. 
  - (This idiom is so intuitive and consistent that it will rarely be mentioned explicitly again.)
- Instead of a value, many D3 setters can take an `accessor` function as argument, which is expected to return a value that will be used to set the property in question. 
  - The parameters expected by accessor functions are not the same across all of D3, but a set of related D3 functions will always call accessor functions in a uniform way. 
- Some important D3 facilities are implemented as function objects. 
  - They perform their primary task when called as a function, but they are also objects, with member functions and internal state (examples are scale objects; and generators and components). 
  - It is a common pattern to instantiate such an object, configure it using its member functions, and finally invoke it to complete its purpose. 
  - Frequently, the final invocation does not use explicit function-call syntax, but instead employs one of JavaScript’s methods for “synthetic” function calls: the function object is passed to another function (such as `call()`), which supplies the required arguments and finally evaluates the function object itself.

- ### Conventions for the API Reference Tables
- D3 functions are either called on the global `d3` object, or as member functions of some D3 object; 
  - some functions are available both ways. 
  - If a function is called through an object, this object is referred to as the `receiver` of the method call. 
  - Inside the member function, the `receiver` is the object pointed to by the `this` variable.
- Function signatures attempt to indicate the type of each argument, but many functions accept such a wide variety of different argument types that no unambiguous notation is practical. 
  - Where they are used, brackets indicate an array. 

- Naming conventions
- First-letter acronyms for individual objects: c for “circle, ” p for point, and so on. 
  - Append an “s” for collections: cs will be an array of circles
- Frequently occurring quantities have their own notation: 
  - pixels are denoted with px, scale objects with sc. 
  - Generators and components are function objects that “make” something and thus are called mkr.
- The letter d is used generically to indicate “the current thing” in anonymous functions. 
  - When working with D3 selections, d is usually an individual data point bound to a DOM element; 
  - when working with arrays, d is an array element (as in ds.map( d => +d )).
- Data sets are called data or ds.
- Selections representing either an `<svg>` or a `<g>` element are common and, when assigned to a variable, are denoted as svg or g.

## c2
- 
- 
- 
- 
