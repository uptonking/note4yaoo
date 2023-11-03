---
title: web-fwk-layer-community
tags: [community, layer, web]
created: 2021-08-15T16:49:15.428Z
modified: 2021-08-15T16:49:35.180Z
---

# web-fwk-layer-community

# guide

- [uber base design: Layers/LayersManager/Tether](https://baseweb.design/components/layer/)
# discuss
- ## 

- ## 

- ## 

- ## Fun React tip: Did you know that React Portals can share state and events across browser windows? 
- https://twitter.com/ralex1993/status/1720123606183621049
  - Thanks to React's virtual DOM and synthetic events system, the app behaves as if it were in the same window, even though the state is shared between windows.
  - https://stackblitz.com/edit/demo-react-portal-ksmarb

- Just the nature of portals. They keep a reference to the DOM element they are attached to, even if it's in another window. When it comes time to commit the React tree to the DOM, it knows where to put the updates. Same with adding the necessary event handlers - it's just DOM.
- Same with iframes thats how the events work inside the iframe but are controlled outside
  - https://github.com/ryanseddon/react-frame-component/blob/master/src/Frame.jsx#L133

- Only if the app launches that window. But service workers can do that and a lot more!

- Yep. We're using it to allow users to split out a part of our UI into a separate window they can place on a 2nd screen.

- ## Anyone has links for inspiration about how component libraries approach z-index? 
- https://twitter.com/blvdmitry/status/1426915191552413707
  - Especially cases when a component might be above and below another component at the same time. 
  - For instance, sticky header that goes over opened dropdowns on the page but also has a dropdown in it
- I like to have a zIndices object with keys for certain things. Makes it easier to shift stuff around, and see all the custom indexes in one place.
  - Absolutely. I also have one but store it on the css variables side instead to keep it working with any css framework.
