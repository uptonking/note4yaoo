---
title: thread-ux-design-system-tokens
tags: [design-system, design-tokens, thread, ux]
created: '2021-05-14T10:08:23.522Z'
modified: '2021-05-14T10:08:51.423Z'
---

# thread-ux-design-system-tokens

# guide

# pieces
- ## 

- ## 

- ## When I started building the Headless #DesignSystem I decided to move to a single @figma file per component.
- https://twitter.com/EstherCheran/status/1497669972826681344
  - I'm really happy I made this decision, but I'm curious what your experience/opinion is on this topic! How do you organise your library?
  - It feels very organised.
  - It allows me to version each component semantically having one page per version
  - I can create purposeful pages like: component, documentation, hand-off & token architecture, UX research & references
  - I can give component level access to collaborators or developers
  - It is symmetric to the structure of my StencilJS Web Components library
  - Less likely to run into large file performance issues
  - Tasks in Jira are linked to a specific component Figma file; reviews, approval and publishing becomes easier.





- ## Consistent Border-Radius
- https://twitter.com/d__raptis/status/1437410390149931008
  - Round images usually look weird when they're included in a card with a small border-radius. 
  - Use the simple rule of thumb: 𝙊𝙪𝙩𝙚𝙧 𝙍𝙖𝙙𝙞𝙪𝙨 = 2 * 𝙄𝙣𝙣𝙚𝙧 𝙍𝙖𝙙𝙞𝙪𝙨
- I got really curious whether avatars MUST be circular or not since traditional frames are rectangular.
  - It seems that UI trends make them circular & it's a way to bring the focus on the face


- ## why don't more people talk about asian typographic design!!! the latin alphabet could never
- https://twitter.com/milkjuus/status/1410034123662532608
- Middle Eastern can be quite beautiful too!

- ## @radix_ui Colors launching very soon.
- https://twitter.com/colmtuite/status/1392833951803211779
  - 6 grays, 20 hues, 11 steps.
  - a11y baked in.
  - Designed around specific use cases.
  - Dark mode support.
  - Works with CSS-in-JS and vanilla CSS.
  - https://design-system-radix-ui.vercel.app/colors
- So you design your site in light mode using these color tokens and you get dark mode for free (or vice versa) because the library already worked out the contrast that produces an =, a11y-safe feel? Freakin brilliant.
- You just stick to the use cases. Then dark mode just works.
  - 000 app background.
  - 100 light background.
  - 200 background.
  - 300 background hover.
  - 400 background pressed.
  - 500 lines.
  - 600 border.
  - 700 border hover.
  - 800 solid background.
  - 900 text.
