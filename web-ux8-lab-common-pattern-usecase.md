---
title: web-ux8-lab-common-pattern-usecase
tags: [components, lab, usecase, ux]
created: 2021-09-13T13:32:14.868Z
modified: 2021-09-13T13:34:01.331Z
---

# web-ux8-lab-common-pattern-usecase
# guide


# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Cmd+k interfaces are so wonderful to come across. 
- https://twitter.com/timcchang/status/1437393810049359872
  - From Spotlight to @linear & @vercel, they've always sparked my curiosity in implementation.
  - I spent a few days building a little library that enable anyone to have this experience for their site
  - https://github.com/timc1/kbar

    - https://kbar.vercel.app/

- Functionally, kbar is built on the concept of "actions", wherein each action can trigger some type of explicit event. 
  - Static actions can be registered up front; e.g. basic page nav. 
  - Dynamic actions that are dependent on specific components/pages can be registered at runtime.
- How do we handle navigating to nested "folders"? 
  - Actions can have children, which are just references to other actions. 
  - While in a nested folder, hitting backspace on an empty search will take you back to the previous action.
- The smooth height animations are a combination of using `ResizeObserver` alongside the Web Animations API. Set the observer on the inner element, animate the outer on change.
- but what about chromium on Windows? Ctrl + K is natively bound to the the address bar?
  - It would be whatever the meta key is, so for your instance it would be the Windows key.
- Is there an equivalent for mobile?
  - You can attach a listener to a button and toggle the interface directly; in the demo just tap the logo
