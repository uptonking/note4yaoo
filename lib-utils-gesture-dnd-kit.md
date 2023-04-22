---
title: lib-utils-gesture-dnd-kit
tags: [dnd, drag, gesture, lib, list, utils]
created: 2022-02-06T13:40:34.638Z
modified: 2022-06-04T00:44:30.749Z
---

# lib-utils-gesture-dnd-kit

# guide

- not-yet
  - resize

- features
  - good docs and examples
    - tree
    - kanban
  - 官方提供了virtualized示例
    - 基于同作者的 react-tiny-virtual-list
  - Built for React
    - exposes hooks such as useDraggable and useDroppable, 
    - and won't require you to re-architect your app or create additional wrapper DOM nodes.
  - Feature packed
    - customizable collision detection algorithms, multiple activators, draggable overlay, drag handles, auto-scrolling, constraints, and so much more.
  - Fully customizable & extensible
    - Customize every detail – animations, transitions, behaviours, styles. 
    - Build your own sensors, collision detection algorithms, customize key bindings and so much more.
  - Zero dependencies and modular
    - the core of the library weighs around 10kb minified and has no external dependencies. 
    - It's built around built-in React state management
  - Built-in support for multiple input methods
    - Pointer, mouse, touch and keyboard sensors.
  - Performance
    - It was built with performance in mind in order to support silky smooth animations.
  - Presets
    - Check out @dnd-kit/sortable

- examples
  - [virtualized with react-tiny-virtual-list](https://master--5fc05e08a4a65d0021ae0bf2.chromatic.com/?path=/story/presets-sortable-virtualized--basic-setup)
  - [Drag and Drop Form Builder](https://github.com/clauderic/dnd-kit/discussions/639)
    - https://codesandbox.io/s/dnd-kit-form-builder-fii0zh

- alternatives
  - use-gesture(vanillajs)
  - react-dnd
# issues

## not-yet

- [Is there any way to force a droppable to accept draggables that come from outside its parent DndContext? ](https://github.com/clauderic/dnd-kit/discussions/181)
  - [Difficult to manage drags across sections of the app](https://github.com/clauderic/dnd-kit/issues/58)
  - This should be a lot easier to manage with the introduction of the `useDndMonitor` hook along with the fact that data defined in `useDraggable` and `useDroppable` is now exposed on the `active` and `over` properties.

## done

- perf regression: all Sortables in 5.0 rerender constantly on even smallest mouse movement
  - https://github.com/clauderic/dnd-kit/issues/623
  - The same problem is happening to me, 'useSortable' is causing retenders due to 'useContext'. 
  - The easiest way to fix this is to use `useContextSelector` .

- [How to drag by copying?](https://github.com/clauderic/dnd-kit/issues/456)
  - when you drop that item you keep that same unique id and generate a new one for the sidebar to replace the item that was just moved from the sidebar to your other droppable region
# discuss
- ## 

- ## 

- ## 

- ## [Is there a built-in sorting strategy for virtualized grids in `@dnd-kit/sortable` ?](https://github.com/clauderic/dnd-kit/discussions/411)
- virtualized grids aren't currently supported by any of the sorting strategies. 
  - It's been a while since I looked at this, but I believe the `rectSortingStrategy` strategy needs all elements to be mounted to work properly.
  - Having said that, you could fairly easily look at the source code of react-sortable-hoc's grid sorting logic and port it over as a custom sorting strategy for @dnd-kit
  - This isn't a feature I need so I won't be prioritizing it myself for the time being.

- Actually, I have a virtualized grid implementation which works pretty well with @dnd-kit/sortable
  - I'm using `rectSortingStrategy`, and there doesn't seem to be any issues even without all the items being rendered. 
  - The only thing I had to do was to ensure that the item currently being dragged was rendered even when it's outside of the visible range. 
# docs

## overview

- Augment your existing components using the `useDraggable` and `useDroppable` hooks, 
  - or combine both to create components that can both be dragged and dropped over.
  - 是否应该再封装一个useDnd，同时支持
- Handle events and customize the behaviour of your draggable elements and droppable areas using the `<DndContext>` provider.  
  - Configure sensors to handle different input methods.
- Use the `<DragOverlay>` component to render a draggable overlay that is removed from the normal document flow and is positioned relative to the viewport.

## [How to create complex interactions with dnd-kit. A how-to that I hope is going to help some folks.](https://github.com/clauderic/dnd-kit/discussions/809)

- This is an extremely long, exhaustive read about how we created a completely full-fledged drag & drop page builder with what I believe is a very elegant solution, using dnd-kit.

- In our system, an `editable` is a `section | row | column | component`. 
  - Editables can be dragged around. 
  - A section after another section, a component inside a column, a row after another row and so on. 
  - We have a total of ~100-something interactions like this, even combining rows. 
  - The idea is as follows - when you define your DndContext, you have the onDragEnd prop to decide what you want to happen when a drag event has finished.
- we're using Redux (RTK). 
- The very first to fire is that "we're no longer dragging", when the user has let go of the click, whatever the outcome, we are done dragging. 
  - We keep track of this `isTracking` global variable so that we can prevent some actions from happening, enable some classes and so on, you get the point. 
  - Then, we check that there is both an `active` and an `over`, if there aren't, it either means that:
    - The user has dragged an editable on another editable which doesn't want to interact with it (more on this later)
    - The drag event is somehow bugged. Who knows? Something got in the way, weird z-index plays and so on.

- 👉🏻 Things I wish dnd-kit had and limitations you should be aware of (possibly, not entirely sure if we just simply don't know enough about dnd-kit):
- Some way to detect edges of a droppable. 
  - The creation of the Edge component was only done in response to not being able to tell which side of the droppable a draggable was dropped on, and, then, not sure if onDragOver allows you to see an edge-like position/information thingie.
- From day one, I was a big sponsor of re-writing the library's core to basically let both drag/drop events bubble as deep as they need to, until one handler decides to handle them, kinda like...how we wrote our page builder? 
  - As it stands, it takes some maneuvering to achieve anything complex and there's no down-side (that I can think of, from the outside, but that's easy to say, it's always easy to "just fix it") to doing things that way.
- Perhaps I'm wrong, but you can't swap DndContext's sensors or any of the collision detection algorithms on the fly, based on the item being dragged and so on. 
  - This is a limitation that I dislike. 
  - I wish there was some way. Some items in a page might prefer a certain collision technique than others.

## architecture

- Unlike many drag and drop libraries, dnd kit is intentionally not built on top of the HTML5 Drag and drop API. 
- The HTML5 Drag and drop API has some severe limitations. 
  - It does not support touch devices, which means that the libraries that are built on top of it need to expose an entirely different implementation to support touch devices. This typically increases the complexity of the codebase and the overall bundle size of the library. 
  - Further, it requires workarounds to implement common use cases such as customizing the drag preview, locking dragging to a specific axis or to the bounds of a container, or animating the dragged item as it is picked up. 
- The main **tradeoff** with not using the HTML5 Drag and drop API is that you won't be able to drag from the desktop or between windows(移动端不需要). 
  - If the drag and drop use-case you have in mind involves this kind of functionality, you'll definitely want to use a library that's built on top of the HTML 5 Drag and drop API. 
  - We highly recommend you check out react-dnd for a React library that's has a native HTML 5 Drag and drop backend.

- Minimizing DOM mutations
  - dnd kit lets you build drag and drop interfaces without having to mutate the DOM every time an item needs to shift position. 
- 💡 This is possible because dnd kit lazily calculates and stores the initial positions and client rects of your droppable containers when a drag operation is initiated. 
  - These positions are passed down to your components that use useDraggable and useDroppable so that you can compute the new positions of your items while a drag operation is underway, and move them to their new positions using performant CSS properties that do not trigger a repaint such as `translate3d` and `scale`.
  - This isn't to say that you can't shift the position of the items in the DOM while dragging, this is something that is supported and sometimes inevitable.

- Synthetic events
  - Sensors use SyntheticEvent listeners for the activator events of all sensors, which leads to improved performance over manually adding event listeners to each individual draggable node.

## DndContext

- make sure that the part of your React tree that uses them is nested within a parent `<DndContext>` component

## useDroppable

- You can set up as many droppable containers as you want, just make sure they all have a unique `id` so that they can be differentiated. 

- If you're building a component that uses both the `useDroppable` and `useDraggable` hooks, they can both share the same identifier since droppable elements are stored in a different key-value store than draggable elements.

```typescript
interface UseDroppableArguments {
  id: string;
  disabled?: boolean;
  data?: Record<string, any>;
}

{
  rect: React.MutableRefObject<LayoutRect | null>;
  isOver: boolean;
  node: React.RefObject<HTMLElement>;
  over: {id: UniqueIdentifier} | null;
  setNodeRef(element: HTMLElement | null): void;
}

```

## useDraggable

- `useDraggable` hook requires that you attach listeners to the DOM node that you would like to become the activator to start dragging.

- creating a drag handle with the useDraggable hook is as simple as manually attaching the listeners to a different DOM element than the one that is set as the draggable source DOM node
  - When attaching the `listeners` to a different element than the node that is draggable, make sure you also attach the attributes to the same node that has the listeners attached so that it is still accessible. 
  - You can even have multiple drag handles if that makes sense in the context of your application

- React attaches a single event listener for every type of event we listen to on the `document`. 

- we recommend that the components you intend to make draggable be presentational components that are decoupled from @dnd-kit
  - create a presentational version of your component that you intend on rendering within the drag overlay, and another version that is draggable and renders the presentational component.

```typescript
interface UseDraggableArguments {
  id: string;
  attributes?: {
    role?: string;
    roleDescription?: string;
    tabIndex?: number;
  },
  data?: Record<string, any>;
  disabled?: boolean;
}

{
  active: {
    id: UniqueIdentifier;
    node: React.MutableRefObject<HTMLElement>;
    rect: ViewRect;
  } | null;
  attributes: {
    role: string;
    tabIndex: number;
    'aria-roledescription': string;
    'aria-describedby': string;
  },
  isDragging: boolean;
  listeners: Record<SyntheticListenerName, Function> | undefined;
  node: React.MutableRefObject<HTMLElement | null>;
  over: {id: UniqueIdentifier} | null;
  setNodeRef(HTMLElement | null): void;
  transform: {x: number, y: number, scaleX: number, scaleY: number} | null;
}

```

## DragOverlay

- usecase
  - show a preview of drop position
  - move from one container to another while dragging
  - If your useDraggable items are within a virtualized list
  - If your draggable item is within a scrollable container
  - If you want smooth drop animations 

- `<DragOverlay>` component provides a way to render a draggable overlay that is removed from the normal document flow and is positioned relative to the viewport.

- `<DragOverlay>` component should remain mounted at all times so that it can perform the drop animation. 
  - If you conditionally render the `<DragOverlay>` component, drop animations will not work.
  - Instead, you should conditionally render the children passed to the `<DragOverlay>`.
  - As a rule of thumb, try to render the `<DragOverlay>` outside of your draggable components, and follow the presentational component pattern to maintain a good separation of concerns.

- make sure that the components rendered within the drag overlay do not use the useDraggable hook.
  - Prefer conditionally rendering the children of `<DragOverlay>` rather than conditionally rendering `<DragOverlay>`, otherwise drop animations will not work.

```typescript
function App() {
  const [isDragging, setIsDragging] = useState(false);

  return (
    <DndContext onDragStart={handleDragStart} onDragEnd={handleDragEnd}>
      <Draggable id="my-draggable-element">
        <Item />
      </Draggable>
      
      <DragOverlay>
        {isDragging ? (
          <Item />
        ): null}
      </DragOverlay>
    </DndContext>
  );

  function handleDragStart() {
    setIsDragging(true);
  }

  function handleDragEnd() {
    setIsDragging(false);
  }
}

function Draggable(props) {
  const Element = props.element || 'div';
  const { attributes, listeners, setNodeRef } = useDraggable({
    id: props.id,
  });

  return (
    <Element ref={setNodeRef} {...listeners} {...attributes}>
      {props.children}
    </Element>
  );
}

const Item = forwardRef(({ children, ...props }, ref) => {
  return (
    <li {...props} ref={ref}>{children}</li>
  )
});
```

## Sensors

- Sensors are an abstraction to detect different input methods in order to initiate drag operations, respond to movement and end or cancel the operation. 
- Sensors may define one or multiple activator events.
- Sensors are initialized once one of the activator events is detected.

## Modifiers

- Modifiers let you dynamically modify the movement coordinates that are detected by sensors. 

## Preset - useSortable

- `useSortable` hook combines both the `useDraggable` and `useDroppable` hooks to connect elements as both draggable sources and drop targets
  - In most cases, the draggable and droppable hooks will be attached to the same node, and therefore be identical in size. 

- Sortable preset requires its own context provider that contains the **sorted** array of the unique identifiers associated to each sortable item
  - It's important that the items prop passed to SortableContext be sorted in the same order in which the items are rendered, otherwise you may see unexpected results.

- we added a droppable zone around each sortable context. 
  - This isn't required, but will likely be the behaviour most people want. 
  - If you move all sortable items from one column into the other, you will need a droppable zone for the empty column so that you may drag sortable items back into that empty column
# changelog

## [v6.0.0_202205](https://github.com/clauderic/dnd-kit/releases/tag/%40dnd-kit%2Fcore%406.0.0)

- Accessibility-related props have been regrouped under the `accessibility` prop of `<DndContext>`.
- The DOM nodes for the screen reader instructions and announcements are no longer portaled into the document.body element by default.
- The drop animation now ensures that the the draggable node that we are animating to is in the viewport before performing the drop animation and scrolls it into view if needed.

- @dnd-kit/sortable@7.0.0
  - The UniqueIdentifier type has been updated to now accept either string or number identifiers. 
    - As a result, the id property of useDraggable, useDroppable and useSortable and the items prop of `<SortableContext>` now all accept either string or number identifiers.
  - Better handling of overlapping droppable
  - Introducing the concept of activator node refs for useDraggable and useSortable. 
    - This allows @dnd-kit to handle common use-cases such as restoring focus on the activator node after dragging via the keyboard or only allowing the activator node to instantiate the keyboard sensor.
  - Focus management is now automatically handled by @dnd-kit.
# examples
- https://github.com/shaddix/dnd-kit-sortable-tree
  - https://shaddix.github.io/dnd-kit-sortable-tree/
  - a Tree component extracted from dnd-kit examples and abstracted a bit. 

- https://github.com/ThaddeusJiang/react-sortable-list
  - Easy Drag & Drop sort items

- https://github.com/wuifdesign/antd-react-extensions
  - https://wuifdesign.github.io/antd-react-extensions/
  - Extentions for Ant Design React

- https://github.com/jado66/reactive-site-creator
  - A website creator for React.
  - 依赖react-quill、react-reveal、bootstrap5

- react-tiny-virtual-list /MIT/1.8kStar/201910/ts
  - https://github.com/clauderic/react-tiny-virtual-list
  - https://clauderic.github.io/react-tiny-virtual-list/
  - A tiny but mighty 3kb list virtualization library, with zero dependencies
  - Supports variable heights/widths, sticky items, scrolling to index, and more
  - forks
    - https://github.com/matyas-igor/react-small-virtual-list

## repos-more

- https://github.com/wyhinton/react_konva-dnd_kit
  - https://codesandbox.io/s/react-konva-dnd-kit-e6rck
  - Example of using dnd-kit to drag an element out a react konva canvas
  - 依赖konva、react-konva

- https://github.com/onmotion/react-tabtab-next
  - A mobile support, draggable, editable and api based Tab for ReactJS
