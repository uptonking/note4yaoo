---
title: lib-utils-gesture-dnd-kit-docs
tags: [dnd-kit, docs]
created: 2023-04-23T13:30:25.630Z
modified: 2023-04-23T13:30:39.223Z
---

# lib-utils-gesture-dnd-kit-docs

# guide

# blogs

## [How to create complex interactions with dnd-kit](https://github.com/clauderic/dnd-kit/discussions/809)

> A how-to that I hope is going to help some folks.

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
  - The creation of the Edge component was only done in response to not being able to tell which side of the droppable a draggable was dropped on, and, then, not sure if `onDragOver` allows you to see an edge-like position/information thingie.
- From day one, I was a big sponsor of re-writing the library's core to basically let both drag/drop events bubble as deep as they need to, until one handler decides to handle them, kinda like...how we wrote our page builder? 
  - As it stands, it takes some maneuvering to achieve anything complex and there's no down-side (that I can think of, from the outside, but that's easy to say, it's always easy to "just fix it") to doing things that way.
- Perhaps I'm wrong, but you can't swap DndContext's sensors or any of the collision detection algorithms on the fly, based on the item being dragged and so on. 
  - This is a limitation that I dislike. 
  - I wish there was some way. Some items in a page might prefer a certain collision technique than others.

### [On the topic of dndkit's tight-knit, non-bubbling architecture](https://github.com/clauderic/dnd-kit/discussions/280)

- I've been personally involved with looking for a DnD library that could help us build our "page/site builder"
- Unfortunately, everywhere I checked (although testing is still undergoing), a very painful constant appeared:
  - The libraries follow a lockdown approach where a droppable and a draggable are uniquely connected and they don't really talk to the outside world. 
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

- It's possible for the listeners to be attached to a different node than the one that setNodeRef is attached to.
  - A common example of this is when implementing a drag handle and attaching the listeners to the drag handle
  - When the activator node differs from the draggable node, we recommend setting the activator node ref(`setActivatorNodeRef`) on the activator node
  - This helps @dnd-kit more accurately handle automatic focus management and can also be accessed by sensors for enhanced activation constraints.
  - When the activator event is a Keyboard event, focus will automatically be restored back to the first focusable node of the activator node.
  - If no activator node is set via setActivatorNodeRef, focus will automatically be restored on the first focusable node of the draggable node registered via setNodeRef.

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

- There are two recommended patterns for this, either using wrapper nodes or ref forwarding.

- 💡 we recommend that the components you intend to make draggable be presentational components that are decoupled from @dnd-kit.
  - Using this pattern, create a presentational version of your component that you intend on rendering within the drag overlay, 
  - and another version that is draggable and renders the presentational component.

- make sure that the components rendered within the `DragOverlay` do not use the `useDraggable` hook.
  - Prefer conditionally rendering the children of `<DragOverlay>` rather than conditionally rendering `<DragOverlay>`, otherwise drop animations will not work.

- A common pitfall when using the `DragOverlay` component is rendering the same component that calls `useSortable` inside the DragOverlay. 
  - This will lead to unexpected results, since there will be an `id` collision between the two components both calling `useDraggable` with the same id, since `useSortable` is an abstraction on top of useDraggable.

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

## [Collision detection algorithms](https://docs.dndkit.com/api-documentation/context-provider/collision-detection-algorithms)

- One of the simpler forms of collision detection is between two rectangles that are axis aligned — meaning rectangles that are not rotated. 
  - This form of collision detection is generally referred to as **Axis-Aligned Bounding Box (AABB)**.
  - This means that even if the draggable or droppable nodes look round or triangular, their bounding boxes will still be rectangular

- Rectangle intersection
  - By default, DndContext uses the rectangle intersection collision detection algorithm. 
  - The algorithm works by ensuring there is no gap between any of the 4 sides of the rectangles. Any gap means a collision does not exist.

- Closest center
  - While the rectangle intersection algorithm is well suited for most drag and drop use cases, it can be unforgiving, since it requires both the draggable and droppable bounding rectangles to come into direct contact and intersect.
  - the closest center algorithm finds the droppable container who's center is closest to  the center of the bounding rectangle of the active draggable item

- Closest corners
  - Like to the closest center algorithm, the closest corner algorithm doesn't require the draggable and droppable rectangles to intersect.
  - it measures the distance between all four corners of the active draggable item and the four corners of each droppable container to find the closest one. 

- 💡 In most cases, the closest center algorithm works well, and is generally the recommended default for sortable lists because it provides a more forgiving experience than the rectangle intersection algorithm.
- when building interfaces where droppable containers are stacked on top of one another, for example, when building a Kanban, the closest center algorithm can sometimes return the underlaying droppable of the entire Kanban column rather than the droppable areas within that column.
  - In those situations, the closest corners algorithm is preferred and will yield results that are more aligned with what the human eye would predict

- Pointer within
  - the pointer within collision detection algorithm only registers collision when the pointer is contained within the bounding rectangle of other droppable containers.
  - This collision detection algorithm is well suited for high precision drag and drop interfaces.
  - this collision detection algorithm only works with pointer-based sensors. 

- Custom collision detection algorithms
  - You can either write a new collision detection algorithm from scratch, or compose two or more existing collision detection algorithms.
  - For advanced use cases or to detect collision between non-rectangular or non-axis aligned shapes, you'll want to build your own collision detection algorithms.

## Preset - useSortable

- `useSortable` hook combines both the `useDraggable` and `useDroppable` hooks to connect elements as both draggable sources and drop targets
  - In most cases, the draggable and droppable hooks will be attached to the same node, and therefore be identical in size. 

- Sortable preset requires its own context provider that contains the **sorted** array of the unique identifiers associated to each sortable item
  - It's important that the `items` prop passed to `SortableContext` be sorted in the same order in which the items are rendered, otherwise you may see unexpected results.
  - `SortableContext` does not expose any callback props. To know when a sortable (draggable) item is being picked or moved over another sortable (droppable) item, use the callback props of `DndContext`

- we added a droppable zone around each sortable context. 
  - This isn't required, but will likely be the behaviour most people want. 
  - If you move all sortable items from one column into the other, you will need a droppable zone for the empty column so that you may drag sortable items back into that empty column
# more
