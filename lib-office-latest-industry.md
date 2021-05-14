---
title: lib-office-latest-industry
tags: [documentation, latest, office]
created: '2021-05-13T02:38:54.706Z'
modified: '2021-05-14T18:47:24.054Z'
---

# lib-office-latest-industry

# guide

- ## [Google Docs will now use canvas based rendering: this may impact some Chrome extensions](https://workspaceupdates.googleblog.com/2021/05/Google-Docs-Canvas-Based-Rendering-Update.html)
- We’re updating the way Google Docs renders documents. 
  - we’ll be migrating the underlying technical implementation of Docs from the current `HTML-based` rendering approach to a `canvas-based` approach 
  - to improve performance and improve consistency in how content appears across different platforms. 

# discuss

- ## Google docs is apparently moving to a canvas based editor. 
- https://twitter.com/devongovett/status/1392597989768585218
  - This is horrible for accessibility and a great example of what *not* to do. 
  - I’m surprised no one flagged this
  - [google docs canvas preview](https://docs.google.com/document/d/1N1XaAI4ZlCUHNWJBXJUBFjxSTlsD5XctCz6LB3Calcg/preview)
- They could have worked with the Chrome team to help improve standards where they are lacking and make the web better for all of us, 
  - but instead decided to reimplement the browser themselves. Very disappointing.
  - Well, to be fair, the old one was also very broken. But at least it had the potential for improvement. Switching to canvas kinda prevents that.
- Would you say that implementing web apps with the canvas API no-go? Are there other downfalls to be aware of? (aside of a11y problems)
  - Text selection, copy/paste, find in page, spell checking, dictionary, system wide text replacement/auto correct, etc would all need to be rewritten and would not integrate as expected with the system.
- I’ve thought about this approach on Paper in the past (especially for intensive things like tables), but accessibility is one of the bigger issues. 
  - We use content-editable for mutations so it gives us a lot of functionality out of the box (undo/redo, keyboard shortcuts, etc)
  - This approach limits us when trying to do any kind of optimization like virtualization, especially when you add the real time collaboration aspect to it. Its a love/hate relationship 🙂
  - Oh yeah, contenteditable is horrible as well. I’ve written a rich text editor in the past and it was painful. I can see how they reached this approach, but it seems like they didn’t really consider all users.
