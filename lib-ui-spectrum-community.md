---
title: lib-ui-spectrum-community
tags: [adobe-spectrum, community, ui]
created: '2021-04-12T16:29:13.012Z'
modified: '2021-04-12T18:07:01.092Z'
---

# lib-ui-spectrum-community

# guide

# pieces

- ## React is amazing because it makes building components so easy. 
- https://twitter.com/devongovett/status/1120783819978629120
  - But it's a double edged sword: everyone is building their own components from scratch now instead of using a library. 
  - That’s bad for accessibility, bad for internationalization, and a giant waste of developer time!
- Supporting accessibility is not just adding role and aria props. 
  - It’s proper focus and tab management, keyboard navigation support, internationalized labels for screen readers, and much more. 
  - It takes years to build a component library with all of this in mind.
- This is why the web is still perceived as an inferior(较差的) app platform. 
  - Since it is so hard to build high quality components with all the features that native has out of the box, almost no one does it. 
  - The web gives us `<div>`, while native has huge libraries of customizable components
  - Efforts like @ryanflorence 's reach-ui are heading in the right direction I think.
- This is what my team is currently working on at Adobe. 
  - We’ve spent years building our design system to support accessibility, internationalization, keyboard navigation, cross platform, and more, and have learned a lot along the way.
  - We’re working on abstracting away the Adobe-specific design into a reusable, accessibility-first library of React Hooks that you can use as a starting point for your design system. 

- https://twitter.com/sarah_federman/status/1121106681226616832
  - Zendesk Garden has a similar approach
  - There's a middle ground here between totally open endedness and constrained to one company's design.
- Garden aims to provide an extremely solid and a11y foundation for other teams to build with.  
  - Our containers save lots of external teams time and effort already, and we want to jumpstart that.
  - We've actually already starting to do this with our react-containers repo. A series of hooks that help with a11y and keyboard navigation and you provide the UI

- ## What were your decisions making points behind choosing px over rems?
- https://twitter.com/_kamlesh_/status/1362041207501688832
  - I was going through the codebase and implementation of these decisions in react spectrum and saw everything is in `px`. 
- we used rem in the previous design system to enable scalable UIs. 
  - We used ems in some places for typography and icons that needed to scale contextually. 
  - We switched to pixels and sizing classes because designers wanted more control over how things scaled...

- ## Fascinating post about how @discord avoided to “burden [their] engineers” with `:focus` and `outline` by creating a `FocusRing` component in React.
- https://twitter.com/sarah_federman/status/1339894190092607497
- Curious about the performance of needing to use so much calculation and getComputedStyle.
- We(react-spectrum) have a `FocusRing` component too but it just applies a class to the wrapped element.
  - We thought about taking the absolute positioned approach described here but deemed it too hard/expensive and pushed back on design where necessary instead
- Seems like a lot of calculation that you would otherwise get free/done by browsers

- ## Something Reakit gets *really* right is API consistency. 
- https://twitter.com/_alanbsmith/status/1344389070533713920
  - If you know how to use one component, you can figure out how to use completely unrelated components. 
  - Consumers being able to learn and guess how to use new  components with minimal doc reference is the gold standard.
- Reakit, chakra, react-spectrum, and styled-system are my biggest influences right now.

- ## When building a component library, avoid spreading props onto native elements—including className and style props (unless it's a primitive like Box).
- https://twitter.com/devongovett/status/1305722928013606914
- Agreed! React Spectrum goes even farther and doesn’t allow arbitrary DOM props/events, custom styles, or even DOM refs, which all leak implementation details and can cause breakages later. We’ve seen this happen very frequently in practice.
  - To be clear, refs are allowed, but we expose an interface for accessing elements. 
  - `UNSAFE_getDOMNode()` gets the outer node (unsafe because element type can change), and in e.g. a textfield, we would expose a `getInputElement()` method that always returns the input.
  - The problem with forwarding refs directly is that you don't know exactly where it will end up. Do you send it to the outer most element, or something inside? What if you wrap the element in another later? Do you move the ref? Will that break things? Better to be explicit IMO.
  - We do allow data attributes. As for aria, we only include attributes that make sense to override for each individual component rather than just passing all possible props through.
- Exposing the internal DOM structure of the components in your design system is very dangerous and you're probably doing it unintentionally.
  * className/style
  * DOM prop forwarding
  * Ref forwarding
  - Changes to internal DOM structure or styling can break usage of these props.
- We also started banning anything related to passing style props, className or setting direct attributes. 
  - However, forward refs are useful if you don't rely on the framework for event handling or for dom manipulation in some cases.
