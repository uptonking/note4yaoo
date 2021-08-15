---
title: web-fwk-layer-community
tags: [community, layer, web]
created: '2021-08-15T16:49:15.428Z'
modified: '2021-08-15T16:49:35.180Z'
---

# web-fwk-layer-community

# guide

- [uber base design: Layers/LayersManager/Tether](https://baseweb.design/components/layer/)
# discuss
- ## Anyone has links for inspiration about how component libraries approach z-index? 
- https://twitter.com/blvdmitry/status/1426915191552413707
  - Especially cases when a component might be above and below another component at the same time. 
  - For instance, sticky header that goes over opened dropdowns on the page but also has a dropdown in it
- I like to have a zIndices object with keys for certain things. Makes it easier to shift stuff around, and see all the custom indexes in one place.
  - Absolutely. I also have one but store it on the css variables side instead to keep it working with any css framework.
