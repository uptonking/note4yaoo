---
title: lib-utils-gesture-beautiful-dnd-blog
tags: [blog, react-beautiful-dnd]
created: 2023-09-03T15:31:15.636Z
modified: 2023-09-03T15:31:29.988Z
---

# lib-utils-gesture-beautiful-dnd-blog

# guide

# blogs

## 🌰 [Building Custom Animations in the Workflow Builder - Slack Engineering_202312](https://slack.engineering/building-custom-animations-in-the-workflow-builder/)

- The react-beautiful-dnd library works by using responders. These are “top-level application events that you can use to perform your own state updates, style updates, as well as to make screen reader announcements.” The library required us to maintain the state of drag-and-drop information and to have a centralized place for state-specific actions.
- Our custom context provider wrapper was a great solution for this. We stored information about the step being dragged, the destination information, and the location of where the step was being dragged over. Actions — such as what happens when you drop or add a step — were also maintained here. This information was updated dynamically by the provided react-beautiful-dnd responders and maintained in an isolated Workflow Builder drag-and-drop component wrapper.
- react-beautiful-dnd did not support adding placeholders.  We needed to be creative to achieve the dragging effect we wanted. Drawing some inspiration, we created a custom segment to dynamically render a placeholder based on where the user was dragging a step.
- We replaced the `onBeforeDragStart` responder with `onBeforeCapture`. The difference between these responders is that `onBeforeCapture` supports modifying the DOM before any calculation occurs. Hiding and resetting the hint box before the dragging action allowed us to create a better user experience and solve our problem.

## [react-beautiful-dnd: Behind the magic_Alex Reardon_202003](https://www.youtube.com/watch?v=Kz50msV-zq0)

- 
- 
- 
- 

## [Dragging React performance forward_201801](https://medium.com/@alexandereardon/dragging-react-performance-forward-688b30d40a33)

## [Grabbing the flame_201811](https://medium.com/@alexandereardon/grabbing-the-flame-290c794fe852)

## [Rethinking drag and drop_201708](https://medium.com/@alexandereardon/rethinking-drag-and-drop-d9f5770b4e6b)

- 
- 
- 
- 

## [Natural keyboard movement between lists_201709](https://medium.com/@alexandereardon/friction-gravity-and-collisions-3adac3a94e19)

- 
- 
- 
- 

## [Beautiful drag and drop: a year in review_201808](https://medium.com/@alexandereardon/beautiful-drag-and-drop-a-year-in-review-1febc3fac7ce)

## [Beautiful interactions: Crafting elegant and robust drag and drop animations_201903](https://medium.com/@alexandereardon/beautiful-interactions-8f67502ccf73)

## [Overhauling our collision engine_201912](https://dev.to/alexandereardon/overhauling-our-collision-engine-962)

- 
- 
- 

# more-blogs
- [What does react-beautiful-dnd cost to maintain?](https://dev.to/alexandereardon/what-does-react-beautiful-dnd-cost-to-maintain-52e8)
  - Maintenance has been made easier by proactively pursuing self-service and continuing to engage with the project
