---
title: lib-ui-spectrum-docs-aria
tags: [adobe-spectrum, docs]
created: 2021-04-12T17:59:04.250Z
modified: 2021-04-12T18:07:23.824Z
---

# lib-ui-spectrum-docs-aria

> platform-specific; theme-agnostic; 

# [overview](https://react-spectrum.adobe.com/react-aria/getting-started.html)
- It provides accessibility and behavior for many common UI components so you can focus on your unique design and styling.
- It implements adaptive interactions to ensure the best experience possible for all users, including support for mouse, touch, keyboard, and screen readers.
- It provides behavior and accessibility through React Hooks. 
  - Since it **does not provide any rendering**, you are responsible for defining the DOM structure for your component and passing the DOM props returned by each React Aria hook to the appropriate elements. 
  - This is powerful because it allows you to be in complete control over the DOM structure that you render.
  - you may need to add extra elements for styling or layout control. 
  - You also get complete control over how you style your components: you could use CSS classes, inline styles, CSS-in-JS, etc.

- Many components are stateless — they display information to a user. 
  - Examples of stateless components include buttons, progress bars, and links. 
  - These components don't update as the user interacts with them.
- A stateful component has some state, and allows a user to interact with the component in order to update that state. 
  - Examples of stateful components include text fields, checkboxes, and selects.
- react-aria separates the state management logic into a separate hook that lives in react-stately.
  - The state hook holds the state for the component, and provides an interface to read and update that state. 
  - This allows this logic to be reused across different platforms, e.g. in react-native. 
# [Why React Aria](https://react-spectrum.adobe.com/react-aria/why.html)
- The fully styleable primitives that the web offers (e.g. `<div>`) are quite powerful, but they lack semantic meaning. 
  - This means that accessibility is often missing
  - Even if you use ARIA to provide semantics, you still need to implement all of the behavior for each component from scratch using JavaScript, 
  - and this can be tricky to do across many devices and interaction models.
- react-aria separates the behavior and accessibility implementation for many common UI components out into React Hooks, which enables them to be reused easily between design systems. 
  - You remain in complete control over the rendering and styling aspects of your components, but get most of the behavior, accessibility, and internationalization support for free.
- react-aria is intentionally very low level: 
  - it provides no rendering at all, just behavior and accessibility. 
  - We impose no specific DOM structure or styling methodology. 
  - The hooks are small and composable, which allows you to combine them together and achieve your design with only the features you need in your component.
# [Accessibility](https://react-spectrum.adobe.com/react-aria/accessibility.html)
- Accessibility is the ability for applications to be used by everyone, including those with disabilities. 
  - This encompasses all types of disabilities, including vision, auditory, motor, and cognitive disabilities.
  - React Aria addresses aspects of vision and motor disabilities through screen reader and keyboard navigation support.
- React Aria implements accessibility support according to the W3C WAI-ARIA specification
  - assistive technology like screen readers can understand what our DOM nodes represent. 
- However, ARIA is a contract: it only specifies semantics, 
  - and it's up to the developer to implement the behavior and interactions for each control with JavaScript.
  - There is an additional document published by the W3C called the WAI-ARIA Authoring Practices, which provides patterns and examples of implementing this behavior on top of ARIA.
  - It specifies keyboard interactions that are expected by users of these controls, along with the required roles and states to make them accessible to assistive technology.
- React Aria provides hooks for many ARIA patterns, which provide the semantics and behavior together.
  - All you need to do is provide the styling.

- Labeling
- React Aria includes most component semantics by default, 
- but there is one important thing you must provide in your application: a textual label for each control. 
- This gives a screen reader user context about the control they are interacting with.
- In case a visible label is not desired for some reason, or you're using a control that doesn't have a built-in label, you must use the aria-label or aria-labelledby props to identify it to assistive technology. 

- Keyboard
  - React Aria implements keyboard support for all components
  - All keyboard behavior is implemented according to the WAI-ARIA Authoring Practices guidelines

- Mobile
  - all functionality must be accessible to a screen reader, including things that would typically be handled by keyboard interactions.
  - React Aria allows you to handle this by placing a hidden button inside the dialog or popover that screen reader users can navigate to in order to close it.
# [Interactions](https://react-spectrum.adobe.com/react-aria/interactions.html)
- the web supports mouse, touch, keyboard, gamepads, screen readers, and more.
- Unfortunately, the web platform doesn't have any high level abstractions across these interaction models.
  - We just have low level events like mouse, touch, keyboard, and focus events, and it's up to developers to put them together properly. 
- React Aria includes a collection of Hooks that provide higher level abstractions over the low level events exposed by the web platform, 
  - and helps normalize the behavior across browsers and devices. 
  - This includes support for high level events like “press”, “hover”, and “focus”. 

- Pointer events
  - The web was originally designed for mouse events
  - browsers needed to emulate mouse events on touch devices to ensure some compatibility with them.
- Mobile browsers also support many types of gestures by default, e.g. double tap to zoom, scrolling, and long press to select text. 
  - Because of this, touch devices often delay firing events like `onClick` in order to first determine if the user intends to zoom or scroll the page. 
  - In the context of a highly interactive web application, this leads to a sub-optimal user experience.
- The new pointer events spec helps simplify handling events across mouse, touch, and stylus/pen interaction models. 
  - React Aria uses pointer events where available with fallbacks on older devices to mouse and touch events. 
  - React Aria supports additional interaction models like keyboard and focus events
- CSS pseudo classes like `:hover` and `:active` are also problematic in many cases, especially on hybrid devices that support both mouse and touch. 
  - They also emulate mouse behavior on touch devices, e.g. showing hover effects when you touch elements. 
  - It's best to use JavaScript events that apply CSS styles rather than these pseudo classes for the best cross-device experience.

- Keyboard and focus behavior
  - At a high level, keyboard navigation is broken up into tab stops
  - A tab stop may be an atomic component like a text field or button, or a composite component like a listbox, radio group
  - Composite components behave as a single tab stop. 
  - Elements within a composite component are typically navigated with the arrow keys, while the Tab key continues to navigate to the next/previous tab stop. 
  - React Aria implements hooks for many of these composite components and handles all of the keyboard navigation behavior for elements inside them
- Overlay elements like dialogs, popovers, and menus have additional focus behavior to ensure that focus stays within them while they are open, 
  - and focus is restored back to the element that opened them when they are closed. 
  - In React Aria this is implemented by the `FocusScope` component.
- Another important feature for keyboard users is a focus ring. 
  - It should only be visible when navigating with a keyboard
  - This can be implemented using the `useFocusRing` hook or the `FocusRing` component. 
  - The `useFocusVisible` hook can also be used to determine whether the user is currently navigating with a keyboard or not.

- Assistive technology
  - An assistive technology, such as a screen reader, relies on semantic information exposed to the browser through ARIA or native HTML element semantics. 
  - React Aria is careful to handle events fired by assistive technology, and normalizes this behavior as needed so it is consistent with other interactions.
# [Internationalization](https://react-spectrum.adobe.com/react-aria/internationalization.html)
- React Aria supports many aspects of localization for many components out of the box, 
  - including translations for builtin strings, localized date and number formatting, right-to-left interactions, and more.
- because React Aria provides no rendering, most of the builtin strings are for non-visible content to provide accessible labels. 
  - All application provided content must be localized and passed in to components. 
  - This can be done with libraries such as react-intl. 
  - Internally, React Aria uses the same `intl-messageformat` library used by `react-intl`.
- React Aria also formats numbers and dates according to the current locale, and uses internationalized algorithms for collation, sorting, and text search. 
- These are implemented with the builtin browser `Intl` APIs under the hood, so there's no large libraries or locale data for users to download.

- Bi-directionality/RLT
  - Since React Aria provides no rendering, it is up to you to implement RTL support in your design.
  - you can account for it in your CSS using logical properties or other means.
  - For example, flexbox and CSS grid both automatically flip their layouts depending on the direction.
- The root most element of your application should define the `lang` and `dir` attributes so that the browser knows which language and direction the user interface should be rendered in. 
# [Server Side Rendering/SSR](https://react-spectrum.adobe.com/react-aria/ssr.html)
- In React, SSR works by rendering the component to HTML on the server, and then hydrating the DOM tree with events and state on the client. 
  - This enables applications to both render complete HTML in advance for performance and SEO, but also support rich interactions on the client.
- When using SSR, only a single copy of React Aria can be on the page at a time.
  - Internally, many components rely on auto-generated ids to link related elements via ARIA attributes. 
  - These ids typically use a randomly generated seed plus an incrementing counter to ensure uniqueness even when multiple instances of React Aria are on the page. 
  - With SSR, we need to ensure that these ids are consistent between the server and client. 
  - This means the counter resets on every request, and we use a consistent seed.
  - Due to this, multiple copies of React Aria cannot be supported because the auto-generated ids would conflict.
- When using server side rendering, the application should be wrapped in an `I18nProvider` with an explicit `locale` prop, 
  - rather than relying on automatic locale selection. 
  - This ensures that the locale of the content rendered on the server matches the locale expected by the browser.
