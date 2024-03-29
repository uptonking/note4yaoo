---
title: ux-design-system-dev
tags: [design-system, dev]
created: 2020-12-31T14:52:30.364Z
modified: 2021-01-01T20:08:38.154Z
---

# ux-design-system-dev

# guide

- [2022设计年鉴](https://www.yuque.com/paidaxin/dkopg8/knob94hbnn0dmx8f)
# discuss

 

- ## 

- ## 

- ## 

- ## 🌰 [Linear on X: "How we redesigned the Linear UI (part Ⅱ)  _202403](https://twitter.com/linear/status/1773435685275328542)
- 
- 
- 

- ## In our design system, we have 2 different space scales:
- https://twitter.com/markdalgleish/status/1280029511807983617
  - Between UI elements (e.g. within a `<Stack>` )
  - Between wrapping lines of text (implicit in the relationship between font size and line height)
  - Change one, you have to manually adjust the other.
- We shouldn’t use `line-height` at all, 
  - we should have line spacing (the distance between to `x-height` lines and block spacing (the distance between two sibling block elements), 
  - with block spacing derived from the larger line spacing of the two blocks (but still overwritable)
  - That’s not ideal from a typography perspective, but neither is what we have now 
  - and at least this way it would always be clear where spacing is coming from and how to adjust it to an exact value without having to do math
  - `x-height` is not used in all writing systems, so this is a tricky one. All solutions might need to be locale aware
- I've found the best way to handle it is to set both based on the same baseline value. So like, 4dp or 8dp.
  - The scales can have different values, but it works if they're all based off the same baseline value.
  - Or polyfill line-height-step (and send me the link if you do!)
  - When you say "change one", what would you be changing? You mean changing the actual space scale?

    - Yeah, but more likely is that you're changing your typography.

  - The only solution I've seen for type setting issues is line-height-step
- Can you hoist them into custom properties and calcs? 
  - my hunch(直觉，预感) is that you should have a single space scale that's derived from your typographical scale. 
  - The space between lines and the space between UI elements both come from a single design decision.
  - Building systems for system's sake, huh?

    - In my experience, only one out of ten designers are actually designing UI all based on typographic baselines, 
    - and eventually they move on from their print layout practises and accept that it's impossible to enforce baselines on the web.

  - What I'm aiming for is a component system that follows the baseline grid for you automatically, and we're having a lot of success with it.
- Material UI uses a `gutterBottom` prop to add same space below an typography element element.  
  - Don't know if that would be better than adding Stack between multiple texts

- ## When I look back at old design system components I made that have surrounding white space.
- https://twitter.com/markdalgleish/status/1222710937167118336
- Putting responsibilities in the right place is IMO the hardest thing to get right in software. 
  - When you do get it right, the solution seems so simple and lots of code tends to just melt away. 
  - But it takes years of practice and diligence to get there.

- ## avoid adding default spacing (margin/padding) in your design system components
- https://twitter.com/sseraphini/status/1286756399268192256
- Padding yes, margin no.
  - Padding is essential for some components that need to keep a certain aspect. 
  - A themed button for instance. 
  - They need to be self contained, so adding margin would demand extra work from outside to get it placed.
- I think it's ok to use padding, but margin breaks component encapsulation bringing worst side effects.

- ## What's your preferred style of controlling margins for components?
- https://twitter.com/siddharthkp/status/1042780297744539649
  1. Bake them in the components
  2. Let the app take care of it with utilities
  3. Wrapper components that give margins to children
- Polaris seems to pick the 3rd with Page and TextContainer components
  - By default, our components don't have margins and they don't know how large they are. 
  - The layouts will size them and place them on the screen correctly.
  - do you write wrapper components like page or content?
  - Yep. We have set layout components that only purpose is to position their children, like a gallery, split, stack, page, toolbar, grid, page, et
- We let the applications take care of margins, but provide spacing tokens for users to hopefully create some consistency. 
  - We used to have set margins on form elements, but ran into many issues where users had to override them, so we took them out.
  - can you give me some examples?
  - We found ourselves often telling people how to override with `margin: 0` in their specific style sheet so we removed it.
  - that's exactly what i'm afraid of
  - It’s a tough problem to solve, because you definitely want consistent spacing but you also need flexibility.
- For spacing within the component, we provide the spacing as part of the component. 
  - For spacing outside of components, we let app teams decide the spacing using a `<Spacer />` component that can set margin/padding in any direction.
- We make every component a block level element with no external margin, 
  - and the user of the component provides how they should it should be laid out with wrapper components for layout that use our spacing values.
- Tend to avoid baking it in because it breaks composability. 
  - Prefer a wrapper component, something like `<VerticalSpacing size=“m” />`

- Basically using styled-system so every component can have a margin based on a scale defined in the theme.
  - I had this, too but figured out it’s rather messy when all you want is spacing between components. 

    - Simple example: add spacing between chips but not after the last one. 
    - Not possible with margin in a clean way but it’s very simple using stack abstraction.

- ## Exposing the internal DOM structure of the components in your design system is very dangerous
- https://twitter.com/devongovett/status/1197945884455030784
  - and you're probably doing it unintentionally.

    * className/style
    * DOM prop forwarding
    * Ref forwarding

  - Changes to internal DOM structure or styling can break usage of these props.
- Instead of forwarding all DOM props directly, you should expose an interface specific to each component. 
  - Intentionally consider what properties should be allowed for a given component (e.g. events, data attrs, etc.) 
  - and forward those to the most appropriate internal DOM element.
- Consider what style changes should be allowed. 
  - In a design system, you probably don't want to allow the full power of CSS to override things. 
  - This will be abused and easily broken.
  - Instead, expose specific styling options that should be allowed (e.g. layout props like margin).
- Instead of exposing direct refs to DOM elements (which is also discouraged in the React docs), expose an interface specific to each component. 
  - For example, a text field component could expose a `focus()` method. 
  - `useImperativeHandle` is perfect for this.
- Most design system components should be considered atomic. 
  - **Treat the internals as implementation details that could change at any time, and expose an interface that doesn't depend on them**. 
  - If you don't, it will be very hard to make design changes later without breaking things.
- Design systems are about consistency: 
  - it should be possible to make design changes in a single place. 
  - Allowing too much flexibility makes this much harder. 
  - Product teams should be contributing to the design system rather than making one-off customizations that can't be upgraded.
- This is something that has been bugging me for a long while as I have been advocating for this forever 
  - but now I am in a position where we ship a library that exposes a few public class names for customization.
  - I haven't thought of a better solution except "render props" to offer customizability.

- ## Do you use layout components in your React app? What do their APIs look like?
- https://twitter.com/mxstbr/status/1235354464975904768
  - (for example, Seek's design system has `<Stack />, <Columns />` etc)
- For a tiny app of mine I use three spacing components vertical, horizontal, around
- I’ve always found layout components restrictive. 
  - Container, Row, Col was all I ever needed until Flex and Box came along. 
  - Having Flex with a kind of push and pull would be good though.
- I really liked `<Stack /> and <Inline />` , until I ran into having to change the flex-direction at runtime. 
  - Now I prefer a general `<Flex />` component, even though it's a bit less readable.
- I'm currently working on an app in which we use `<Flex />` in a similar way to MUI's `<Grid />` component where it can be a container and/or an item, 
  - where the item-related props determine the column span. 
  - Also `<Stack />, <Tiles />, <Spacer />` etc.

- ## The difference between a component library and a design system is whether or not your components have 'className' and 'style' props.
- https://twitter.com/markdalgleish/status/1308330959973027846
- me using the `sx` prop
- I thought the difference was calling it a design system when you're trying to impress people.
- It's about the amount of flexibility and opinions and in some ways the design goals can be opposite.
  - You want a component library be flexible enough so people can build their design systems on top of that.
  - At the same time you want your design system to be rigid enough.
