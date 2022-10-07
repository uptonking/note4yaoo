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
  - Built for React
    - exposes hooks such as useDraggable and useDroppable, 
    - and  won't require you to re-architect your app or create additional wrapper DOM nodes.
  - Feature packed
    - customizable collision detection algorithms, multiple activators, draggable overlay, drag handles, auto-scrolling, constraints, and so much more.
  - Fully customizable & extensible
    - Customize every detail – animations, transitions, behaviours, styles. 
    - Build your own sensors, collision detection algorithms, customize key bindings and so much more.
  - Zero dependencies and modular
    - the core of the library weighs around 10kb minified and has no external dependencies. 
    - It's built around built-in React state management and context, which keeps the library lean.
  - Built-in support for multiple input methods
    - Pointer, mouse, touch and keyboard sensors.
  - Performance
    - It was built with performance in mind in order to support silky smooth animations.
  - Presets
    - Check out @dnd-kit/sortable, which is a thin layer built on top of @dnd-kit/core. 
    - More presets coming in the future.

- alternatives
  - react-dnd
# not-yet-dnd-kit
- [ ] onDragEnd delta.y property inaccurate when inside position fixed container
  - https://github.com/clauderic/dnd-kit/issues/298

- [x] perf regression: all Sortables in 5.0 rerender constantly on even smallest mouse movement
  - https://github.com/clauderic/dnd-kit/issues/623
  - The same problem is happening to me, 'useSortable' is causing retenders due to 'useContext'. 
  - The easiest way to fix this is to use `useContextSelector` .
# docs

## overview

- Augment your existing components using the `useDraggable` and `useDroppable` hooks, 
  - or combine both to create components that can both be dragged and dropped over.
  - 是否应该再封装一个useDnd，同时支持
- Handle events and customize the behaviour of your draggable elements and droppable areas using the `<DndContext>` provider.  
  - Configure sensors to handle different input methods.
- Use the `<DragOverlay>` component to render a draggable overlay that is removed from the normal document flow and is positioned relative to the viewport.

## architecture

- Unlike many drag and drop libraries, dnd kit is intentionally not built on top of the HTML5 Drag and drop API. 
- The HTML5 Drag and drop API has some severe limitations. 
  - It does not support touch devices, which means that the libraries that are built on top of it need to expose an entirely different implementation to support touch devices. This typically increases the complexity of the codebase and the overall bundle size of the library. 
  - Further, it requires workarounds to implement common use cases such as customizing the drag preview, locking dragging to a specific axis or to the bounds of a container, or animating the dragged item as it is picked up. 
- The main **tradeoff** with not using the HTML5 Drag and drop API is that you won't be able to drag from the desktop or between windows(此设计不符合移动端). 
  - If the drag and drop use-case you have in mind involves this kind of functionality, you'll definitely want to use a library that's built on top of the HTML 5 Drag and drop API. 
  - We highly recommend you check out react-dnd for a React library that's has a native HTML 5 Drag and drop backend.

- Minimizing DOM mutations
  - dnd kit lets you build drag and drop interfaces without having to mutate the DOM every time an item needs to shift position. 
  - This is possible because dnd kit lazily calculates and stores the initial positions and client rects of your droppable containers when a drag operation is initiated. 
  - These positions are passed down to your components that use useDraggable and useDroppable so that you can compute the new positions of your items while a drag operation is underway, and move them to their new positions using performant CSS properties that do not trigger a repaint such as `translate3d` and `scale`.
  - This isn't to say that you can't shift the position of the items in the DOM while dragging, this is something that is supported and sometimes inevitable.

- Synthetic events
  - Sensors use SyntheticEvent listeners for the activator events of all sensors, which leads to improved performance over manually adding event listeners to each individual draggable node.

## DndContext

- make sure that the part of your React tree that uses them is nested within  a parent `<DndContext>` component

## useDroppable

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

```JS
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

- useSortable hook is an abstraction that composes the useDroppable and useDraggable hooks
- we added a droppable zone around each sortable context. 
  - This isn't required, but will likely be the behaviour most people want. 
  - If you move all sortable items from one column into the other, you will need a droppable zone for the empty column so that you may drag sortable items back into that empty column
# examples

## repos-dnd-kit

- https://github.com/shaddix/dnd-kit-sortable-tree
  - https://shaddix.github.io/dnd-kit-sortable-tree/
  - a Tree component extracted from dndkit examples and abstracted a bit. 

- https://github.com/ThaddeusJiang/react-sortable-list
  - Easy Drag & Drop sort items

- https://github.com/wuifdesign/antd-react-extensions
  - https://wuifdesign.github.io/antd-react-extensions/
  - Extentions for Ant Design React

- https://github.com/jado66/reactive-site-creator
  - A website creator for React.
  - 依赖react-quill、react-reveal、bootstrap5

## repos-more

- https://github.com/wyhinton/react_konva-dnd_kit
  - https://codesandbox.io/s/react-konva-dnd-kit-e6rck
  - Example of using dnd-kit to drag an element out a react konva canvas
  - 依赖konva、react-konva

- https://github.com/onmotion/react-tabtab-next
  - A mobile support, draggable, editable and api based Tab for ReactJS
