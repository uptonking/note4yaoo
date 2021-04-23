---
title: web-ui-comp-layout-container
tags: [components, layout, ui, web]
created: '2021-04-14T18:35:52.173Z'
modified: '2021-04-23T15:53:50.281Z'
---

# web-ui-comp-layout-container

> 布局/网格类组件

# guide

# discuss

- ## 

- ## 

# container(常用于布局)

- usecase-examples
  - halfmoon文档: container-fluid
  - bootstrap5文档: container-xxl
  - pico文档: container各断点都有max-width，最小屏除外

- ## Media Query Breaks Modularity, Use Container Query
- https://react-container-query.github.io/react-container-query/
- https://github.com/react-container-query/react-container-query
- if you have created responsive web site, you likely have used media queries to change styles according to the width of viewport.
- Everytime we change page's padding, we have to change media query for list item component. 
  - This behavior breaks the modularity of list item component.
- It is also problematic when we want to apply different styles to the same component at the same viewport width.
- Container query is a work in process CSS feature. 
  - With it you can apply media query to an element instead of viewport. 
- Note: before the container query idea, there is element query. They are the essentially the same concept except container query are not allowed to change styles of container itself to avoid infinite loop.

# box(常用于样式)

- ## material-ui: Grid vs Box vs Container
- https://spectrum.chat/material-ui/help/grid-vs-box-and-now-vs-container~73cef09f-1eb9-4d0f-a3a3-d46c44232524
- The `Container` component is intended to be used as the main layout component. 
  - It sets minimum padding on the right and the left side, so your content doesn't touch the edges. 
  - At the same time, it horizontal centers your content when the screen is too wide. 
  - For instance, a small container width improves readability.
- The `Grid` component handles the layout positioning within a `Container` . 
  - It's a slim abstraction on top of the CSS flexbox model. 
  - It has two interesting features: the items spacing and the responsive columns handling. 
- The `Box` component is a style toolbox
  - it's an abstraction for people who like the tailwinds approach. 
  - Instead of writing custom CSS, you can use the Box style props
- You might be confused by `<Container />` vs `<Grid container />` . 
  - But make no mistakes, you can't use the two interchangeably. 
  - A Grid container, abstracts a flex container. 
  - A Container abstracts a page top level element.
- What's the difference between `Grid` and `Box` ? 
  - You should be able to replace the Grid usage with the Box. 
  - However, the Box is a direct mapping to CSS properties, while the Grid tries to be smarter, with a more abstracted API. 
  - The Grid should be the default go to solution. 
  - Only consider the Box or custom CSS if it's not the case.
- I personally, never used Box component. 
  - It's an awesome component, but I prefer to style my components using useStyles with makeStyles. 
  - Box component is a component that accepts props as utilities for styling.
  -  Box is a component that accepts specific styling props and converts them into classNames to style your element.

- ## What's in your Box?
- https://spectrum.chat/styled-system/general/whats-in-your-box~6f41c990-f49f-4063-ba64-fcea702014f9
  - Whenever I'm looking at a project that uses styled-system I like to look at what style props they put in their base Box component. 
  - Most seem to at least have the usual space and color, but I'm curious what other folks have opted to put in their own Box components. 
  - Has it grown over time? Would you do it differently if you had a fresh start?
  - I can see us adding more props for controlling max/min heights/widths, along with more flex item props like order and alignSelf, but I'm concerned with how a large API like that might affect usability.
- see Github Primer's Box uses docs
- How many times do you actually use Box in your design systems?
  - I started out trying to extend everything based on Box, but I then really started loving being very explicit with which styled-system functions to expose in a component's API, so I preferred to not use Box at all.
  - In theory, my understanding of the Box concept is that it kinda creates a styled-system breed of div that you can build everything else upon, is that how everyone out there in s-s land is using it?
- For me, I'm mostly using Box in other components and exposing whatever props I want rather than extending the entire API.
  - So far we're just extending Box for building the rest of our design system components like Flex, Text, etc., but not so much for situations like NotificationBar.
- I've started with an omnipotent(全部) box and occasionally check which props I use throughout the design system, remove little used/unused ones and refactor accordingly.
  - This box makes a pretty good base box.
  - const Box = styled.div(space, color, width, minWidth, maxWidth)
- started out with the default one but in the end put everything in it, I use these pretty much everywhere in my layout
- i think override when you do more than just 1 thing, most of the time its only 1-2 props, if you want to change 5 or so it gets really tedious to do it as props
  - get your point, but it's still an arbitrary decision. It's obvious too much props is suboptimal, same with no props at all, but the line between the two is pretty blurry, if it even exists  
