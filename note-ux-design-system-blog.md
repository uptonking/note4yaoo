---
title: note-ux-design-system-blog
tags: [blog, design-system]
created: '2020-12-29T16:18:21.626Z'
modified: '2020-12-29T16:18:39.028Z'
---

# note-ux-design-system-blog

## blog

### [Design Systems Should be JavaScript Framework Agnostic_201809](https://medium.com/hackernoon/design-systems-should-be-javascript-framework-agnostic-2a0c47129ec8)

- An emerging trend in design systems is the idea of separating your core HTML & CSS from the current JavaScript framework. 
  - There’s clearly a difference between presentational JavaScript, and the JavaScript used in modern frontend frameworks like React, Angular and Vue
- It would seem at first glance that our HTML & CSS are destined to be eternally coupled with their JavaScript at the component level.
- So why would you want to separate core HTML & CSS in your design system? The way I see it, there are three potential driving factors:
  - Product Variety
  - JavaScript Framework Churn
  - Predicting the Future
- Salesforce Lightning Design System
  - Is any JavaScript included as part of the framework?
    - No. The Salesforce Lightning Design System is a pure CSS framework that you can use with any front-end development framework you’d like, 
    - including Salesforce-specific technologies such as Visualforce and Lightning, as well as third-party frameworks like React or Angular.
    - The Salesforce team is able to take the core HTML & CSS Lightning components and create a separate React-based project from them
  - we do not have any JavaScript in our Open Source Design System 
    - and that is because once you introduce that, it is really difficult to stay agnostic; 
    - you basically introduce opinion into the stack.
- Microsoft Fabric Design System
  - Micah Godbolt wrote the fantastic Frontend Architecture for Design Systems, which included some very neat ideas for abstracting parts of your design system into JSON, what he referred to as “schema-driven design”. 
  - Since publication of the book, Micah has been working for Microsoft, on the Fabric design system.
  - The Fabric design system is built to support core web, React, Angular and iOS. 
  - The Fabric core contains very low-level CSS and design elements that are easily shared cross-project
  - What I’m really excited about is the “theme generator” in Fabric’s core
- Github Primer Design System
  - Primer is very well fleshed out, containing core principles (color, layout, typography, etc.), utility classes, and a very well documented component library.
  - a HTML/CSS framework as the foundation for your design system.
- The Nutshell
  - Its clear that there’s value in separating your HTML & CSS from your JavaScript at the design system level.
    - We ended up here because when MVC-style JS frameworks were introduced, they were treated as another dependency, when they are patently a fundamental shift in the role JavaScript plays. 
    - jQuery was the last popular “presentational” JavaScript library, which could be added as a dependency and used whenever functionality was required
  - MVC-style JavaScript frameworks are so different from layering in presentational JavaScript that we needed to change how we think about writing code for the web. 
  - In the above examples, we’ve seen how the emerging trend is to also change how we think about our design systems at the core level. 
    - React and Angular are treated as more similar to iOS in Fabric because they are just that: vastly different from the low-level pieces provided in Fabric’s core.
- I can envision a core HTML/CSS design system which 
  - not only contains all the low-level elements (colors, typography, etc.), and components built in vanilla HTML/CSS, 
  - but additionally examples of the components in the different templating languages or JS frameworks used in products the system supports. 

### [creating themeable design systems_2018_Brad Frost](https://bradfrost.com/blog/post/creating-themeable-design-systems/)

- TL; DR: Design systems + CSS Zen Garden = Awesome.
- Each component in a design system contains its own structure, style, and behavior.
- In my own design system work, I’ve found there’s often a finite number of ways to structure a component (with HTML) and make it interactive (with JavaScript), but the styling possibilities are seemingly endless.
- we can create systems that allow for a lot of aesthetic flexibility while still retaining a shared underlying structural foundation.
- So how do we actually go about creating design systems that can serve wildly different brands, audiences, and contexts?
- From Salesforce’s Lightning Design System, which popularized the term “design tokens” in design systems
- Design tokens move variables to a higher level, making it easier to manage brand attributes without diving deep into a codebase
- First tier variables define the brand’s core attributes, serving as the raw materials for the UI’s visual design
- The second tier takes the first-tier variables and starts applying them to high-level applications within the UI.
- The third tier is component-specific variables, which are found in each component’s partial. 
- We can now map the high-level application variables to specific components.
- Atomic design is a methodology for creating thoughtful UI design systems: all of the vastness and complexity of our UI universe can be broken down into a finite set of atomic elements. 
- Components are included inside of more complex components, which are in turn included inside even more complex components. 
- This Russian-nesting-dolls approach to UI design systems helps teams thoughtfully create the whole experience and the parts of the whole at the same time.
- Using the variable system described above, we can define the button atom‘s visual styles for 5 unique brands.
- A molecule is a component made up of a handful of atoms. A card molecule is a common component that can house all sorts of different content.
- An organism is a complex component that’s made up of atoms, molecules, or other organisms.

### [Atomic Design: Blowing Up What You Thought You Knew About Web Design](https://www.elegantthemes.com/blog/design/atomic-design)

- interfaces are made up of components that can be categorized into building blocks
- Atoms, Molecules, Organisms, Templates, Pages

## top design system

### [10 Best Design Systems and How to Learn (and Steal) From Them](https://designerup.co/blog/10-best-design-systems-and-how-to-learn-and-steal-from-them/)

01.  Google Material Design System
02.  Apple Human Interface Guidelines
03.  Microsoft Fluent Design System
04.  Atlassian Design System
05.  Uber Design System
06.  Shopify Design System
07.  IBM Carbon Design System
08.  Mailchimp Design System
09.  Salesforce Lightning Design System
10.  Helpscout Design System
