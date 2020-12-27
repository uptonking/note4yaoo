---
title: web-dev-fwk-vanillajs-comp
tags: [components, vanillajs, web]
created: '2020-11-06T13:55:26.840Z'
modified: '2020-12-27T20:28:20.539Z'
---

# web-dev-fwk-vanillajs-comp

## react-like

## more-vanillajs-components

### [Vanilla Components Draft](https://github.com/websdk/vanilla)

- The primary design goals are to refine the boundaries/seams of components, and maximise the ergonomics of authoring components. 
- This is to separate out the concerns of and enable further customisations and innovations to take place orthogonal to the implementation of components. 
- The components are framework-agnostic, but not the lowest common denominator at the cost of being a long-term solution.

``` JS
/* Define - component.js */
export default function component(node, data) {.. }
```

``` CSS
/* Style - component.css */
:host {}
```

``` JS
// Communicate
node.addEventListener('event', d => {.. })
node.dispatchEvent(event)
```

``` JS
// The simplest way to invoke a component
import { component } from 'component'
component.call(node, data)
```

- There are a few example repo's that covers all the above points:
  - https://github.com/pemrouz/sweet-alert
  - pemrouz/markdown-editor
  - pemrouz/d3-chosen
  - https://github.com/vanillacomponents/ux-input

## ref

- [Vanilla JavaScript Components](https://medium.com/bunnyllc/vanilla-js-components-8d20c58b69f4)
- [To people who work in JS, how often do you use vanilla vs a framework or library?](https://www.reddit.com/r/javascript/comments/7y4r4u/to_people_who_work_in_js_how_often_do_you_use/)
  - You should do what makes sense. 
    - For instance, building your own state management or rendering engine is probably not something you want to do, so you use React, Vue, or Angular.
    - You probably don't have any reason to build your own short-id system when you can just pull a library down that does it for you and save 20-30 min.
- [As a experienced vanilla boy, I don't see the benefit of using react or angular. Change my mind.](https://www.reddit.com/r/Frontend/comments/c2z9hv/as_a_experienced_vanilla_boy_i_dont_see_the/)
  - If you’re working alone, vanilla is an option.
    - If you’re on a medium/large dev team.. good luck building even a moderately complex web app without a framework and maintaining and iterating on it over time
  - Basically the more complex the app is, the more time you can save when using these frameworks. 
    - Good luck with writing your own state management, routing, dom manipulaton helpers, lifecycle etc. 
    - If your client doesn't mind paying 10 times more for his app just for your pleasure to write vanilla js
  - **One thing people often miss in these debates is the question is testing**. 
    - People love to say that you should use such and such because it's better/easier to do something. 
    - Actually one of the key reasons for the development of angular was to offer testing capabilities via dependency injection.
    - can you build and maintain an enterprise application like that over years and dozens of developers?
- [Whats so wrong with direct DOM manipulation?](https://www.reddit.com/r/javascript/comments/6btma7/whats_so_wrong_with_direct_dom_manipulation/)
  - if you're keeping the application state in both the DOM and your js at such a scale, your introducing complexity that makes performance, testing and refactoring much more difficult. 
    - if you are keeping your state only in the js, then you need to keep the view in sync with that anyway.
    - react, vue and other frameworks attempt to reduce that complexity by handling the data/view relationship (plus other things like http stuff) for you and offering you an API and a general set of 'best' practices.
  - Absolutely, with enough discipline and careful programming you can build complex applications that handle DOM state management, without using a framework.
    - But for a lot of people just don't have that level of discipline (or really, the experience/willpower) to execute that sort of strategy properly.
    - especially if you've got a team, a framework is generally going to be much easier for them to work with
  - The same thing that's wrong with global variables and spaghetti code with no modularisation or isolation 
    - it's not a problem in small, simple cases, but as your system complexity grows it rapidly becomes untenable 
    - because every part of the system can affect every other part, 
    - and you can't abstract away any part of it into a simple interface that lets you reason about it abstractly without getting mired in the details.
- [Let's talk about a good possible vanilla js modular scalable architecture](https://www.reddit.com/r/javascript/comments/9agxp9/lets_talk_about_a_good_possible_vanilla_js/)
  - with the benefits of componentization, modularization, state management and testing
    - you will end with another one, but your own framework, with many bugs and problems that already have been solved by more mature ones
  - I think the only solution would be time. 
    - In time, technologies will start being built around JavaScript - if it’s not already happening.
