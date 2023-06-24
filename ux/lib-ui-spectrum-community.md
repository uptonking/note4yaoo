---
title: lib-ui-spectrum-community
tags: [adobe-spectrum, community, ui]
created: 2021-04-12T16:29:13.012Z
modified: 2021-04-12T18:07:01.092Z
---

# lib-ui-spectrum-community

# guide

- [Add CRUD example for Table and add useListData and useTreeData hooks](https://github.com/adobe/react-spectrum/pull/439)
# disccuss-stars
- ## 

- ## 

- ## [Framework agnostic aria tools · react-spectrum](https://github.com/adobe/react-spectrum/issues/1329)
- 202201: It's not on the core team roadmap because it's not something we need ourselves


- ## [Support for React Native/Native](https://github.com/adobe/react-spectrum/issues/696)
- The architecture is designed to support using the lowest layer, `react-stately`, cross platform. 
  - `react-aria` specifically is **web only** since it relies heavily on browser APIs. Electron should work since it's essentially just Chrome. 
  - We don't have anything around React Native yet, but we'd be interested in working with the community on building out the higher layers on top of react-stately.

- https://github.com/gluestack/react-native-aria
  - A library of React Hooks for React-Native (Android/iOS/web) to provide accessible UI primitives for a design system
  - 依赖很多react-aria的子包
  - https://github.com/GeekyAnts/react-native-aria /archived
# disccuss
- ## 

- ## 

- ## 

- ## I'm often asked why React Aria is hooks-based rather than component-based. 
- https://twitter.com/devongovett/status/1438188332001808384
  - [Consider upgrading to a component-based API](https://github.com/adobe/react-spectrum/issues/2331)
  - We've also heard some feedback that it could be easier to use in some simple cases. 
  - I wrote a reply on GitHub about how we think about this tradeoff, and how we plan to improve.
  - We're focused on the low level behavior, and I was hoping the community would build lots of higher level wrappers. I think there's room for API experimentation and integrations with different styling methodologies.
- FWIW we are offering both in React Router v6.
  - For example, we have a `<Routes>` component and a `useRoutes()` hook. 
  - The idea here is that the use cases for a hook vs component are subtly different. 
  - The hook lets you express your routes as plain JS objects and get the element back as a variable. 
  - But the component lets you declare your routes as JSX if you prefer.
- Back in 2018, I proposed a hook-based API similar to react-aria for Reakit 
  - but we concluded that was much lower level than we wanted. 
  - As a user, it was also super inconvenient to adhere to the rules of hooks and work with React Context and Portals.
  - We ended up adopting a hybrid component-based approach where we export both the hooks and the components with render props
  - [reakit RFC: Hooks](https://github.com/reakit/reakit/issues/288)
- I’m actually surprised I haven’t come across a UI library that uses React Aria and React Stately internally

- ## Table is out!
- https://twitter.com/devongovett/status/1437855303899365377
  - Keyboard navigation
  - Sorting
  - Multi-selection
  - Async loading
  - Infinite scrolling
  - Virtualization
- We have many more features planned.
  - Inline edit mode
  - Mac style highlight selection (i.e. no checkboxes)
  - Resizing and reordering columns
  - Drag and drop
  - Multiple sections
  - Tree grid support (i.e. outline view)

- ## React Aria's data table component is coming along nicely!
- https://twitter.com/devongovett/status/1407747623268671490
  - Keyboard navigation to rows, cells, and focusable elements within cells
  - Multi selection
  - ARIA selection announcements
  - Sorting
  - Tiered headings
  - Async data loading + infinite scrolling
  - Typeahead
  - And more!
- We sometimes have tables inside a table and expanding rows. Is that something you plan to implement?
  - Yeah, we will eventually support expanding rows. We would follow the ARIA treegrid pattern for that
- Does it have the "basic" features tables proposed as in react-virtualized or react-windows?
  - Yes! Our own tables in Spectrum are all virtualized. It should work with any virtualization library. We'll add some examples to the docs. Eventually we might make our own virtualizer public as well.

- ## Initial implementation of collections API and Tree
- https://github.com/adobe/react-spectrum/pull/31
- A Collection is an interface which has getKeys and getItem methods to retrieve items from the collection. 
- CollectionManager
- useCollectionState
- CollectionView
- CollectionBuilder
  - It handles converting both the static and dynamic forms using the `<Section>` and `<Item>` components into a form consumable by `CollectionView` . 
  - it generates normalized Node objects which are essentially tree nodes with a key, value, children, etc. 
  - Item states like `isSelected` and `isExpanded` are also set here so that nodes update when state change.
  - The keys on nodes are global to the entire collection, not within each parent like normal react. 
  - This allows us to track changes even if the items change parents (e.g. an item is moved to a different folder by a user).
  - In the dynamic form, CollectionBuilder also handles caching so that only changed nodes are re-rendered. 
  - This is only possible in the dynamic form because we can cache based on the item objects, whereas in the static form we don't have the original values - only the rendered JSX.
- useTreeState
  - uses a CollectionBuilder to build a TreeCollection from its child items, 
  - and also manages expanded and selected states for items as a Set of keys. 

- ## is useListData useful? 
- https://twitter.com/kamal/status/1299086783284559872
  - i only see the usage in docs. 
  - seems only the main thing i would get from it is selectedKeys, but useListState maintains that for me too.
- `useListData` is more meant for application developers rather than component developers. 
  - You'd use it to manage and update data and then pass it to the `items` prop of a collection component. 
  - `useListState` manages it internal to the component itself.

- ## React events propagate the *React tree* and not just the DOM tree. 
- https://twitter.com/devongovett/status/1317205109265215488
  - We take advantage of this at @modulz to suppress click out/focus out/focus in events when interacting with portalled content
- I think that's the only use case where event bubbling on React Portal is helpful. Most of the time, it's really annoying. There's this long-standing issue asking for, at least, an option to disable this behavior
  - Ugh yeah. I haven’t seen a single use case where bubbling through portals made sense. We’re constantly having to detect when this happens using DOM contains and ignoring these events.
- A classic one: Modal with focus lock + select with portaled content? Especially when modal and select and from different libraries and don’t know about each other. An ability to know that something is happening “inside you” is good to have.
  - That’s a valid use case. But this would break if you used actual DOM events (which could also be another library). A better solution would be the Select library providing a way to set the portal container so you could stack portals in the DOM.
  - Yeah we do this by tracking a stack of open overlays and only closing the top-most one when interacting outside.
  - @MaterialUI seem to do the same
- We're working on supporting more than just react though, so we'll probably have to find another way of solving this. E.g. preact does not bubble events through portals.
  - We usually use a portal for the tooltip itself as well in react spectrum.

- ## We put a lot of effort into making our tooltips fully accessible, and as native-like as possible, 
- https://twitter.com/devongovett/status/1311787561094848512
  - including matching the delay behavior when hovering over multiple elements with tooltips.
  - The DialogContainer component in React Spectrum gives you more control over where dialogs are rendered. Use it when your dialogs don't have an explicit trigger, or when the trigger unmounts while the dialog is open (e.g. a menu).
- I'm building a generic component library for our company and use react-aria as the foundation for most of the components. I just noticed that the tooltip examples on the react-spectrum docs does not work on android chrome on my mobile.
  - Is this by purpose? Because as we know we don't have a mouseover event on mobile. But shouldn't they appear on a long press for example?
  - Yes, this is intentional. In general, tooltips don't really exist on touch, and long press may already have a behavior depending on the component. We may add an opt-in mode though.
  - As mentioned in that issue, Tooltips are not supported on mobile devices by default but it is something we might be interested in adding in the future.

- ## Invented a new React pattern I'm calling the "fake child" pattern.
- https://twitter.com/markdalgleish/status/1370951759284162565
  - When making composite components (e.g. `<Select> and <Option>` ) it lets you pass private props (i.e. not on the type signature) from parent to child *without* using context.
  - Note that this also prevents `<Child>` from being rendered outside of `<Parent>` , which is pretty neat given there's no use of context here.
  - https://codesandbox.io/s/dry-surf-jfmzx?file=/src/App.tsx
- This breaks composition though.
  - `const SpecialChild = () => <Child />` .
  - The child component is a dead blob, it can't be bound to state or made dynamic.
  - This is something where imo context should always be used.
  - If it's not clear, the trade-off here is that `<Child>` must be a *direct* child of `<Parent>` , i.e. it can't be rendered by another component.
- Why do you want to avoid using Context here? It seems like a good use case for it.

- I think react-aria has been doing sth similar, but your example is much understandable
- We do this exact thing in React Spectrum for all our collection components. They all share the same `<Item>` “component”, which is just mapped to the appropriate internal element based on the parent
  - Another cool thing about this is it enables virtualized scrolling without changing the API. 
  - Rather than passing all children through, we can simply not render some of them until they are scrolled into view.
  - We actually built a whole system for this type of component using generators
  - This does break composition though - ie no wrappers of `<Item>` are allowed. I wish React had a mechanism to query the rendered tree without actually rendering to the DOM.

- Having some feature for this has been on the plans for a while but don’t really have a great plan that isn’t very limiting. Eg server streaming gets tricky if the parent can change the output. This pattern also doesn’t always work well with Server Components...
- Depending on if both or either are client components rendered from a server component. Either the server component parent can observe children that are representations of the client children, not the real child. Or client parent can observe a placeholder for a suspended child.
- Breaking composition has some deep implications.
  - Yeah though in the cases we apply this pattern you wouldn’t ever render the parent in one place and children in another, and I think that’s a reasonable restriction. The children are not real components, they’re just providing data for the parent like any other prop, but via JSX.
  - What about HOC? It’s less of a problem now with lots of libraries going with hooks, but they’re still wildly used. For example Relay pre-Hooks.
    - Generally we recommend placing anything you would have wrapped around `<Item>` inside the item instead which works pretty well. The content is generally what people want to customize anyway.
- Perhaps. That `<Select><Option /></Select>` pattern is commonly great for Server Components though because it allows for highly reusable Client Components so you have to download zero code specific to that usage. I'm sure we'll figure something out though.
- Another option for this is to have a wrapper around both Select and Options that are "Shared" which does the loop over the children and then pass to some client specific implementation detail. The problem doesn't really kick in since the child can't suspend so maybe it's nbd.
  - I think with this API you could put the content inside the Option in a server component instead of the Option itself. Eg `<Select><Option><ServerContent /></Option></Select>`. Makes some sense because the Option itself doesn’t render anything anyway.
  - Could there be a simple useIndex hook that maintained the proper index in the tree and was only readable similar to a ref? In practice, it seems you never need that index on initial render, just things like keyboard interaction.
    - We use this for more than just passing an index through though, eg rendering only some of the items for virtualized scrolling, and mapping to completely different UIs depending on the parent component. It’s more of a JSX replacement for passing a list of objects to a prop.

- ## React is amazing because it makes building components so easy. 
- https://twitter.com/devongovett/status/1120783819978629120
  - But it's a double edged sword: everyone is building their own components from scratch now instead of using a library. 
  - That’s bad for accessibility, bad for internationalization, and a giant waste of developer time!
- Supporting accessibility is not just adding role and aria props. 
  - It’s proper focus and tab management, keyboard navigation support, internationalized labels for screen readers, and much more. 
  - It takes years to build a component library with all of this in mind.
- This is why the web is still perceived as an inferior(较差的) app platform. 
  - Since it is so hard to build high quality components with all the features that native has out of the box, almost no one does it. 
  - The web gives us `<div>` , while native has huge libraries of customizable components
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
  - I was going through the codebase and implementation of these decisions in react spectrum and saw everything is in `px` . 
- we used rem in the previous design system to enable scalable UIs. 
  - We used ems in some places for typography and icons that needed to scale contextually. 
  - We switched to pixels and sizing classes because designers wanted more control over how things scaled

- ## Fascinating post about how @discord avoided to “burden [their] engineers” with `:focus` and `outline` by creating a `FocusRing` component in React.
- https://twitter.com/sarah_federman/status/1339894190092607497
- Curious about the performance of needing to use so much calculation and getComputedStyle.
  - We(react-spectrum) have a `FocusRing` component too but it just applies a class to the wrapped element.
  - We thought about taking the absolute positioned approach described here but deemed it too hard/expensive and pushed back on design where necessary instead
- Interesting! And yours has `:focus-visible` -like behavior, it seems?
  - Yep! We have a polyfill `useFocusVisible` .
- Seems like a lot of calculation that you would otherwise get free/done by browsers

- ## CSS tip: Layer solid box-shadows to create a rounded focus ring which appears offset from the element `box-shadow: 0 0 0 2px #fff, 0 0 0 4px #005fcc` .
- https://twitter.com/stowball/status/1356041743842467847
  - And of course, don't forget Windows High Contrast mode with: `outline: 2px solid transparent` .
  - And if you use a CSS custom property, you can change the inset colour as appropriate
- Looks like React Spectrum does something similar for this offset focus ring, but more complicated. They create a pseudo element and push it away from the main element
  - Would mean they don’t need to know the bg colour of the parent in order to do that.
  - Yeah, exactly. Most scenarios will be on the same background anyway, so it kinda feels like overkill; having to recreate all the border-radius etc

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
