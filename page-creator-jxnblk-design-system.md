---
title: page-creator-jxnblk-design-system
tags: [creator, design-system]
created: '2020-08-17T07:31:32.942Z'
modified: '2020-08-17T07:33:23.548Z'
---

# page-creator-jxnblk-design-system

## guide

- The Cascade is Not Inheritance
  - Inheritance is when a child element inherits styles from one of its parent elements. 
  - The Cascade is the set of rules that a browser uses to determine which particular styles should apply to a given element, when there are conflicting rules.

## [Themeability_201907](https://jxnblk.com/blog/themeability/)

- I've been interested in the idea of constraint-based design for a while. 
- By constraining the solution space for a particular problem, new and novel ideas can emerge
- In the context of UI design, when you don't need to decide whether a heading's font size should be 22 or 24 pixels, you have more time to decide what that heading should say in the first place or whether there should be a heading at all.
- Like other tools aimed at promoting creative focus, design constraints can help create a distraction-free environment for creative thought. 
- Design constraints can be viewed as a sort of hierarchy of needs
  - when you stop spending energy on lower-level problems, you can start exploring higher level abstractions in design.
- I've tried to distill some of this thinking into several different open source libraries over the years, notably Basscss, Rebass, and Styled System
  - Styled System is becoming a more-and-more widely-used solution for applying visual design constraints within component libraries and design systems.
- By defining a typographic scale, negative space scale, color palettes, and other visual attributes in a theme object, these values can be systematically applied to components where needed, 
  - while still allowing the flexibility to override values contextually within an application.
- While Styled System is great for building design systems and component libraries, it's not an ideal solution in and of itself for creating white-labels or themeable user interfaces. 
  - Styled System is completely framework-agnostic and requires the user to create their own components that integrate with other CSS-in-JS libraries. 
  - It requires you to make intentional, upfront decisions about the overall component API, which is great for corporate design systems, but shouldn't be necessary for applying a design constraints in general-purpose UI development. 
- Styled System doesn't provide much guidance for creating applications that are truly themeable.
- The render props pattern has become popular in recent years to allow this sort of logic to be packaged into reusable components that aren't concerned with the styling of the UI. 
  - The problem with this idea is that every component has its own unique API, and all theming APIs vary from implementation to implementation. 
- Without a standard API for theming components, we'll never have UI components that can truly operate as interchangeable parts.
- If even a handful of UI component libraries conformed to a common specification for themeable components, these components could be installed in many different applications without the need to add custom styles. 
- This is the idea behind the Theme Specification, which is intended to be an unopinionated foundation for other libraries to be built upon
- The theme specification itself is a design constraint.
- Theme UI is a framework for building themeable and interoperable UI components based on visual design constraints.
  - Like Styled System, it uses a theme object for applying design constraints in an application, but unlike Styled System it doesn't require custom UI components to apply these styles. 
  - Both Theme UI and Styled System use the same underlying theme specification, which means if you've created components with Styled System, they should work in applications that are built with Theme UI.

## [Defining Component APIs in React_201807](https://jxnblk.com/blog/defining-component-apis-in-react/)

- Aim for a small API surface area
- Make things easy to find
- Avoid renderThing methods
- Split components at data boundaries
- Avoid Apropcalypse
- Use composition
- Avoid boolean props for enums
- Keep props APIs parallel
- Ask your teammates
