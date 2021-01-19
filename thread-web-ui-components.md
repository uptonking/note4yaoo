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
