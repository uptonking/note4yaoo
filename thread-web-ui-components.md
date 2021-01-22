---
title: thread-web-ui-components
tags: [components, thread, ui, web]
created: '2021-01-19T04:45:46.454Z'
modified: '2021-01-19T04:46:23.100Z'
---

# thread-web-ui-components

# guide

# pieces

- ## 

- ## Thinking on ways to solve a SIDENAV
- https://twitter.com/argyleink/status/1352343431914299393
  - No position absolute anywhere, and the JS is only ux enhancements
- [Building a sidenav component](https://web.dev/building-a-sidenav-component/)
  - how I prototyped a Sidenav component for the web that is responsive, stateful, supports keyboard navigation, works with and without Javascript, and works across browsers. 
  - Try the [demo](https://gui-challenges.web.app/sidenav/dist/).

- ## How to implement a tooltip positioning engine
- https://twitter.com/lihautan/status/1352431000559607809
  - positioning in 12 directions
  - move as you scroll
  - flip as it hits the edge
  - constrained within a boundary
  - hide when the target leaves the screen
- https://www.youtube.com/watch?v=tBn0lVUzUbA

- ## Intent to Prototype: HTMLPopupElement - <popup>
- https://twitter.com/intenttoship/status/1352410513876119554
- https://groups.google.com/a/chromium.org/g/blink-dev/c/9y-Thg9UCxY/m/_4gShWjQAAAJ?pli=1
- [Enabling Popups](https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/Popup/explainer.md)

- ## I've been experimenting a lot with "pure CSS theming" and composition with CSS variables
- https://twitter.com/MaximeHeckel/status/1352289351024181250
- One of the cool things I did [here](https://twitter.com/MaximeHeckel/status/1343589258859319298) was to base this system solely on CSS variables: bye-bye ThemeProvider!

- ## High compatability and longevity pattern libraries shouldn’t include JavaScript, just document the states JavaScript can affect. 
- https://twitter.com/heydonworks/status/1351478317183074304
  - Document the toggle button pressed and unpressed, and what HTML/CSS these states need.
- I’ve been a big fan of this for large orgs.
  - It's (kinda) what I did with my last client (my bad jQuery with a big - "write your own JS" caveat) and with my current client where we’re trying to show/document those things rather than code examples up.
  - This is what happened with one design pattern from a previous clients design system that had (essentially) an HTML, CSS and minimal Javascript based component library
  - when you have the coded components of your design system written in HTML, CSS, and (vanilla) JavaScript it lets your pattern filter into products that use: asp, php, ruby on rails, angular, vue
- I (gut reaction!) strongly disagree with this, especially as more and more CSS features arrive with accompanying JS APIs.
  - I have no idea if React will be more or less prevalent in 10 years, but I definitely think many declarative UI patterns from it will.
  - The costs of describing complex patterns and states with them decoupled from JS seem too high to me?
  - It feels like an ends justify the means approach—implementation doesn’t matter, just the result. 
  - I’m biased as I work primarily with a DS built in React.
  - I’ve wanted to extract everything generic from it for a long time, to find what is expressed such that it can also be expressed as just HTML/CSS and what cannot. But it’s a staggering undertaking.
  - Personally, I think front end would benefit immensely from standardizing how we do UI in JS more, and that’s where most of the chaos/confusion comes from, rather than promoting even greater agnosticism.
- Cannot agree more. Too often is a pattern lib of high quality but intertwined to a JS lib that could change within months.
- I've been pondering this myself as I build our design system. 
  - My inclination was the same but then I had to build a JS templated modal gallery and it made sense to me to include the JS. 
  - As the audience is PHP CMS developers I couldn't expect them to do the JS. Not ideal but...
- Hard agree, each time the patterns are implemented as components in a framework that can be shared for reuse, but you the look & feel shouldn't be tightly coupled to the scripts

- ## I like to make my design systems two tiered. 
- https://twitter.com/stubbornella/status/1351600378849103874
  - Tier 1: html and CSS only. 
  - Tier 2: HTML, CSS, and JS flavor. 
  - Teams can choose 1 and get flexibility with more breaking changes. 
  - Or 2, and get more guardrails and fewer breaking changes. Both are valid.
- Cool! Presumably, for (2), you take the extant HTML+CSS stuff and compile it with a separate JS repo or something?
- @neal4d did a talk about "Trap Doors" in architecture/designs a while back, IIRC, too, so maybe I either channeled him or adapted it. 
  - His slides/videos might be on the Interwebs somewhere, too.

- ## With so many website designs being updated to feature large border radiuses, I'm finding them much more well rounded.
- https://twitter.com/markdalgleish/status/1351642575908732928
- We really have come full border-radius: 50% back to the trends of "web 2.0"

- ## Lots of designers try to avoid modals, but I don't think they should be so quick to dismiss them.
- https://twitter.com/markdalgleish/status/1351300138233282561
- Implementation wise, you often want the URL to represent the UI State. 
  - If the user refreshes the page, or accidentally closes the browser, or duplicates the tab, or shares the URL to another computer, when that URL finishes loading, the state of the UI should be identical.
  - You end up needing to either:
  1. totally break the contract of URL with UI State
  2. invent your own bespoke convention for representing Modal state consistently on the URL for each URL path.
  - Every app will end up implementing #2 a little differently
  - just the open/close state. 
  - if the modal is a form, it'd be a bit much to shove the form into the URL -- that sort of data instead goes in local storage if at all.
  - Nested modals make this even more complex/stupid.
- Idea: an app where every new page is a modal stacked on top of one another so users have ~ u l t i m a t e   c o n t e x t ~
- It's just really hard to dialog with them.
- So true. When discussing usage of modals with the rest of team it’s important to keep an open dialog
- They have good reason to! 
  - Modals are not inherently bad but in many cases they end disrupting the user flow and limiting the user experience.
  - They have been used for bad more than for good, that's for sure. 
  - Exit modals when the user heads for the back button, are some of the worst UX yet stats show they work.
- You’re gonna have to try harder if you are to keep my focus.
  - I guess it's tough to stay on top of things and maintain focus.
