---
title: lib-utils-gesture-use-gesture-community
tags: [community, use-gesture]
created: 2023-07-03T08:55:28.024Z
modified: 2023-07-03T08:55:45.218Z
---

# lib-utils-gesture-use-gesture-community

# guide

# issues
- ## [Handling for drop targets?](https://github.com/pmndrs/use-gesture/issues/88)
  - I've been digging around the issues and examples looking for solutions for discrete draggable components and drop targets, but haven't been able to find much

- I’m sorry but unfortunately this lib doesn’t support drag and drop events.

- I found a solution to simulate drop events that solved my problem perfectly. `Document.elementFromPoint(x, y)` 100% mobile browser compatible

- ## [Drag movement does not include pre-threshold movement](https://github.com/pmndrs/use-gesture/issues/314)
- The "gesture" starts as soon as the user starts interacting, and the threshold controls when we determine it to be an intentional gesture and call handlers. 
  - the gesture had already started before the threshold was reached.

- the main reason why I though to not include threshold is because when moving the dragged element, you generally want to respond 1:1 with your pointer. 
  - 👉🏻 If you include the pre-threshold in the movement, you will experience a jump equivalent to the threshold — unless you animate the jump, but you might have to catchup with the pointer, so this will result in using an animation library during the whole gesture if you see what I mean.

- ## [Keyboard accessibility improvements](https://github.com/pmndrs/use-gesture/issues/598
- It would be good to contemplate(考虑) the keyboard accessibility for drag move gestures, as the current implementation is not working the same as other libraries that implement this feature. 
- The current implementation starts the drag gesture as soon as any of the keyboard keys are pressed and it brings the following issues:
  - Dragging from the keyboard is complicated and doesn't feel good because the actions are direction locked where the gesture was initiated.
  - This makes implementing accessibility for complex gestures or even dnd oriented libraries based on use-gesture really complicated, as many drag gestures in those cases would rely on moving elements on more than a single axis.

- It could be good togo with the dnd-kit approach, where the gesture has to be activated with Enter or Spacebar before moving when you are using the keyboard (This is also used in other libraries like svelte-dnd-action and react-beautiful-dnd, so it seems like the common / intuitive behavior). 

- I believe that adding an option to debounce the `keyup` handler and leave it to the user to config the debounce time seems like a good fix for the issue in the meantime.

- [4 Major Patterns for Accessible Drag and Drop | by Jesse Hausler | Salesforce Designer | Medium](https://medium.com/salesforce-ux/4-major-patterns-for-accessible-drag-and-drop-1d43f64ebf09)
# discuss
- ## 

- ## 

- ## [update local value from outside ?](https://github.com/pmndrs/use-gesture/discussions/54)
- [Pragmatically set value of X](https://github.com/pmndrs/use-gesture/discussions/55)

- ## [Exclude children from the gesture](https://github.com/pmndrs/use-gesture/issues/433)
  - Is there a way to exclude specific children of an element from triggering the gesture / getting events as they should ? 
  - For example, is there a way to correctly **select text within a draggable elements** ?
  - [Exclude children from the gesture](https://github.com/pmndrs/use-gesture/discussions/428)

- For the general vanilla JS purpose, I would rely on an element property (ex. use-gesture-ignore="true"), or something along those lines. This is less ideal for React as custom properties are not idiomatic, and don't work in a straightforward way if you want to wrap a fragment / list.
- For react, this use case seems to be most compatible with the Context API ; ie a provider at the useGesture level (useGesture and the child component would both subscribe to this context to communicate)
- I find the react-dnd lib extremely well designed in this aspect, it allows to very easily and modularly communicate between drag / drop components without any prop sharing whatsoever.

- we could add an option like accepting an array of nodes that would be tested against when the gesture starts and that would prevent the gesture.
  - that's pretty much what I ended up doing - not magnificent but it works. One way you could implement this is creating a wrapper component for excluded children, which adds an attribute to the underlying node (ex `use-gesture-excluded="true"`) ; and the lib could check for this attribute to prevent the gesture if the attribute is present on one of the parents of the target
  - the most react-way of doing it would be using `Context` but it means wrapping the entire gesture-enabled component with a provider (like in React-dnd) - that being said it would enable a lot of additional potential functionality, such as children subscribing to the gesture and being able to cancel it mid gesture, etc.
