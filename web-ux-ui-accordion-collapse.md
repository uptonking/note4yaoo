---
title: web-ux-ui-accordion-collapse
tags: [accordion, components, ui]
created: '1970-01-01T00:00:00.000Z'
modified: '2021-04-23T15:42:22.362Z'
---

# web-ux-ui-accordion-collapse

# guide

# html-details-summary

## discuss

- ### What HTML element do you feel is still not used enough these days? How about `<details>`
- https://twitter.com/stackblitz/status/1312021847123390464
  - for doing this common "show more" feature in a nice semantic way, and with no JavaScript needed
- Nice, but can't customize with css
  - Which part? TMK it was fully customizable.
- Do you have any idea why browsers don't use a pointer cursor on details by default?
  - You can do it with css
- To get transitions I prefer to use radio buttons, or checkboxes and the sibling selector in CSS. 
  - Easy enough to generate unique ID server side and no JS needed on the client.

- ### Pretty curious about this actually: <details> and <summary>
- https://twitter.com/briankardell/status/1299819401995259905
- I love them, and the fact that they’re not searchable when closed is hopefully getting addressed with beforematch, and I _do_ hope all browsers implement this. 
  - Minor annoyances: styling of the triangle and no simple way to add animation.
- so you put the same content in twice and then use js to toggle a class?
  - Then the sibling shows when it's closed. Think of like a display/edit mode section. Common sort of component.
  - Not the same content, the details holds the open content and the .closed element holds the closed content. No JS, it's toggled by clicking the summary (which toggles the [open] attr)
- Only thing I had an issue with was they can hide content when printing a page due to browser implementation.
- Sorely missing: a way to force open/close state in CSS for use in media queries.
  - Nice to have: a way to style contents without an extra element.
  - Isn’t this the composition advantages, right? This would be anti-pattern because what’s inside the details may vary. You can put everything inside it, also a reusable element, and the details should not know about it. You can also style the details directly (which is the wrapper)
- Would like to be able to animate them
- Big fan here. I use it as a trigger for many things without using JS.
- Is details/summary suited for a drop-down navigation?
  - No. Because a disclosure widget does not strike me as appropriate  for a menu. 
  - It’s tedious and you often want to link the summary, too, which is weird because the summary is technically a button. 
  - Too hacky for me, too unexpected to many users
- I like them. Styling and animation need improvement. 
  - The biggest thing I'd add is standardization around expanding when the URL fragment identifier points to the `<details>` element or one of its children. Without this, links are pretty broken.
- recently I was frustrated that browser find-in-page wasn't finding something because it was inside a collapsed details. 
  - Hopefully the work with the `content-visibility` property (& getting hash URLs & Find to work with it) will help fix that, too.
- I tend to use them a lot in markdown documents. It's a convenient way to hide information and make a document shorter.
- They make me sad because they're not as good as they could be.
  - Main issue: it wasn't designed with CSS in mind. 
  - No way to override show/hide with media queries, weird incompatibilities between browsers, no state pseudoclass = no easy fallback, no control over the toggle icon.
  - Now, most of those issues are being addressed in the specs, but it's been slow & painful & there are still too many inconsistencies.
  - I mean, this isn't legacy like `<fieldset>`. CSS was standard when `<details>` was introduced. But the “separation of concerns” mindset took over.
    - E.g., the toggle icon is now defined as a CSS marker, with a keyword content value. But only Firefox implements it that way.
    - The content re-ordering & hiding is defined using shadow DOM. Not sure if we have consistency yet for how it interacts with pseudos.
  - But I can't see us ever getting a CSS-only way to force content open (other than by using the sibling selector hack), nor a CSS selector to distinguish `details[open]` in browsers that can and can't close it (but luckily that's becoming less & less of an issue over time).
- `<details>` is meant to model a disclosure control. 
  - A pure CSS way to open or close would be like a pure CSS way to check or uncheck a checkbox. 
  - I can see how it would be convenient, but it would violate separation of concerns. 
  - CSS should react to control state, not set it.
- I'm trying to love them, but every time I try doing something besides a simple "open & close text" I fail.
  - I wanna animate you hard, in all directions, expose parts of you and use you in all the dirty browsers
  - I'd also love to define the opening trigger element. Not in all cases is "click anywhere" the best idea.
- Dislike them. Widgets just seem out of place in HTML. 
  - The fact that blink and gecko implement them in totally different ways is a dead give-away they weren't introduced carefully enough.
- is it screenreader friendly?
  - Yes, screenreaders are able to correctly identify it and state something like: "[...] collapsed element, tap for more [...]" usually
- Use it in the past and had terrible support in Safari + Firefox regarding css customization. 
  - Ended up creating the same behavior from scratch in JS.

- ### Twitter A11y people if I am using a <details> element for the open and close behaviour in a menu, what should it's role be?
- https://twitter.com/AdaRoseCannon/status/1310515208482426880
- accessibility mappings for HTML is in its own spec

- ### If you use details::before or details::after on a <details>/<summary> widget
- https://twitter.com/AmeliasBrain/status/1046877972685238272
- I'm talking about the pseudos on the details element itself (details::before, details::after), not pseudos on the summary element.
  - summary::before & summary::after are laid out as children of summary in all browsers & aren't affected by open/close state.