---
title: ux-design-system-blog
tags: [blog, design-system]
created: '2020-12-29T16:18:21.626Z'
modified: '2021-01-01T20:08:32.485Z'
---

# ux-design-system-blog

# blog

## [Why I build Design Systems with Stitches and Radix](https://ped.ro/blog/why-i-build-design-systems-with-stitches-and-radix)

- I've built design systems, But they never felt quite right—some were too laborious(耗时的，辛苦的) and too error-prone. Others were too slow and too opinionated.
- I've lost count of how many times I've been asked to build complex components from scratch—dialogs, tooltips, dropdown menus, popovers, sheets, tabs.
- But they were all flawed and lacked fundamental accessibility features.
- When working against a deadline, it's almost impossible to build them correctly.
- So for the last couple of years, we at Modulz worked hard to facilitate how teams can build, maintain and scale their design systems—all whilst adhering to the WAI-ARIA design pattern.

- Stitches is a styling solution focusing on component architecture and developer experience.
  - It introduces a first-class variant API, enabling design system authors to express their intent better. 
  - It's fully typed
- With Stitches, you're able to create resilient, maintainable and scalable design systems. 
  - You can focus on what matters the most. 
  - The system itself — your theme, scales and tokens. 
  - The look and feel of the components and their potential variations. 
  - The way each component can look at different breakpoints.(responsive)

- Radix Primitives is a low-level UI component library focusing on accessibility, customisation and developer experience. 
  - It's a comprehensive library of unstyled, and accessible components, with over twenty-five to choose from.
  - All its components adhere to the WAI-ARIA design patterns. 
  - They can be the base layer of your design system or adopted incrementally.
- With Radix, you're able to delegate the logic and accessibility concerns of complex components while having full control over their aesthetics and behaviour. 
  - Style its parts and states.
  - Use them controlled or uncontrolled. 
  - Add animations, either with CSS or an animation library.

- [discussion](https://twitter.com/peduarte/status/1388040430860701696)

- I'm fascinated. Wondering, why did you go with magic strings (e.g. `$turq`) as opposed to variables/constants?
  - Because it offers a simpler developer experience and feels more first-class
- Good to know! Are there compile time errors in case a referenced theme variable doesn't exist?
  - We are trying to type check the token when used in a string more strictly. But there are some limitation by typescript 
  - If you want strict typing it’s recommended you import the theme

## [spotify: Customization vs. Configuration in Evolving Design Systems](https://engineering.atspotify.com/2021/04/28/customization-vs-configuration-in-evolving-design-systems/)

- When a design system first starts out, the promise of visual consistency glows bright
  - the ideal product would have only one set of buttons, a unified typography scale, and elements that look the same no matter which designer made the design or which developer programmed them to be real and deployed.
- As the product grows, Your once-perfect button doesn’t quite cover the new specs needed for a new feature. 
  - Some restrictions in the way a component is coded means it would be quicker and easier to spin up something new, rather than pull from the component library.
- As a system grows more complex, this evolution can be handled by developing an abstract shared vocabulary around component properties or by ensuring that base properties remain accessible for modification by end consumers.
- In this post, we’ll dive into the factors at play as a design system evolves, and the pros and cons of this range of approaches.    

- Abstraction
- In this context, we define it as a simplified version of a more complex concept. 
- Abstraction can make some concepts easier by obscuring(使模糊) underlying characters of a system in favor of a more high-level representation. 
- We are looking at abstraction here as a measure of how different the code we write is from the HTML and CSS that is ultimately rendered. 
- For the scope of this piece, we will be discussing abstraction from the lens of frontend development using React, starting with written code through to what is rendered in the browser. 
- In this context, a low level of abstraction would define something that touches CSS or HTML elements directly, 
- whereas a high level of abstraction would define changing custom properties that have their own subjective meaning and value, that in turn modify some underlying CSS or elements within the component.

- Customization
  - Custom styles are added external to the component. 
  - These styles reference HTML elements and touch CSS properties directly. 
  - A low level of abstraction.
- Pros: Autonomy, speed, innovation
- Cons: Lack of coherency, loss of maintainability, potential duplication

- Configuration
  - The original component is made more flexible. 
  - Additional parameters are passed to the component for more varied behavior. 
  - A high level of abstraction.
- Pros: Consistency, contribution, maintainability 
- Cons: Can become a bottleneck, rigidness, vocabulary awareness

- With both ends of the abstraction spectrum carrying implications for the key functions of your design system, it should come as no surprise that you will end up with a mix of approaches. 

## [7 Rules for Creating Gorgeous UI (Updated for 2020)](https://learnui.design/blog/7-rules-for-creating-gorgeous-ui-part-1.html)

### Light comes from the sky

- Shadows are invaluable cues in telling the human brain what user interface elements we’re looking at.

### Black and white first

- Designing in grayscale before adding color simplifies the most complex element of visual design– and forces you to focus on spacing and laying out elements.
- UX designers are really into designing “mobile-first” these days. 
  - That means you think about how pages and interactions work on a phone before imagining them on your zillion-pixel $6000 pro monitor.
  - That sort of constraint is great. It clarifies thinking. You start with the harder problem (usable app on a teeny-weeny screen), then adopt the solution to the easier problem (usable app on a large screen).
- Well here’s another similar constraint: design black and white first. 
  - Start with the harder problem of making the app beautiful and usable in every way, but without the aid of color. Add color last, and even then, only with purpose.

### Double your whitespace

- To make UI that looks designed, add a lot of breathing room.
- In Rule 2, I said that B&WF forces designers to think about spacing and layout before considering color, and how that’s a good thing. Well, it’s time we talk about spacing and layout.

### Learn the methods of overlaying text on images (in Part 2)

### Make text pop — and un-pop (in Part 2)

### Use only good fonts (in Part 2)

### Steal like an artist (in Part 2)

## [Design Systems Should be JavaScript Framework Agnostic_201809](https://medium.com/hackernoon/design-systems-should-be-javascript-framework-agnostic-2a0c47129ec8)

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

## [creating themeable design systems_2018_Brad Frost](https://bradfrost.com/blog/post/creating-themeable-design-systems/)

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

## [Atomic Design: Blowing Up What You Thought You Knew About Web Design](https://www.elegantthemes.com/blog/design/atomic-design)

- interfaces are made up of components that can be categorized into building blocks
- Atoms, Molecules, Organisms, Templates, Pages

# top design systems

## [UI Design Trend of 2021](https://dev.to/harshhhdev/ui-design-trend-of-2021-4fb7)

- Glassmorphism is possibly the new UI Design Trend of 2021, which in my opinion has a lot of potential.
- The design trend for 2020 was Neumorphism which had some rather obvious issues.
  - there are of course accessibility issues for people who have eyeshight issues

## [10 Best Design Systems and How to Learn (and Steal) From Them](https://designerup.co/blog/10-best-design-systems-and-how-to-learn-and-steal-from-them/)

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

# ref

- [Web Design Trends in 2021](https://www.editorx.com/prowebsites/web-design-trends)
  - The screen will surpass our real-world expectations by creating stimulating, immersive experiences that make up for what we’ve lost in real life. 
    - Robust platforms will blur the boundaries between real and virtual 
    - by creating practical experiences—like attending a concert or lecture—that are spatial and rich with elaborate visual effects.
  - Web designers will focus on human identity as they create experiences that not only appeal to end users, but also feature them. 用户画像
  - This will result in interfaces that are singular to each user, reflecting their taste, style and identity. 
    - Users will be able tweak interfaces to match their varying needs, from enlarging typefaces to choosing a high-contrast palette for better legibility.
