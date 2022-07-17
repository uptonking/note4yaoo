---
title: web-fwk-layer
tags: [layout, viz, web]
created: 2020-07-17T11:55:40.790Z
modified: 2021-07-28T19:22:37.309Z
---

# web-fwk-layer

# guide

- app图层设计是整体思维，是否与局部component的设计相矛盾
  - 那就从全局角度设计Component，考虑使用context api

# faq

- ## [Can css3 translateZ() be used instead of z-index?](https://stackoverflow.com/questions/17977220/can-css3-translatez-be-used-instead-of-z-index)
  - The answer now is that you can. You need to use `transform-style: preserve-3d;` on the parent
- 使用z-index隐藏元素有什么缺点
  - 要考虑用户操作是否会导致layout, repaint
  - If an element or group of elements should only become visible after the user performed a conscious action, use `display: none; ` or `visibility: hidden;`
  - If something should remain hidden until the user performs a conscious action, use `display: none;` . 
  - Should something, on the other hand, become visible when navigated to via the keyboard, or be discoverable by screen reader users right away, use negative positioning.
  - moving elements away will not affect performance at all, except for perhaps making it a drop slower due to extra calculations.
  - ref
    - [Is better (by a performance point of view) to stack hidden elements with z-index or to move them away 'horizontally'?](https://stackoverflow.com/questions/27122882/is-better-by-a-performance-point-of-view-to-stack-hidden-elements-with-z-index)
- 使用z-index或z-idex的数值过大，对性能的影响大吗
  - 视情况而定
  - The number of layers matters, but the actual value of the z-index does not. 
    - When rendering the page, the browser just sorts all of the absolutely-positioned elements by their z-index (ascending) and draws them in that order.
    - Also, the performance hit from sorting only occurs when you change the z-index of the layers. 
    - If the z-indices aren't changing often, the performance hit probably won't be noticeable at all. 
    - Even if you are changing the z-indices a lot, sorting a list of 15 items is almost instantaneous.
  - z-index are relative, not absolute. 
    - An element with z-index 1,000,000 renders in front of elements with lower z-index and behind elements with higher z-index. If does not mean that the browser will create 1,000,000 layers.
    - I think it is the number of distinct z-indexes (stacking contexts to be more precise) that matters.
  - ref
    - [z-index, how does it affect performance?](https://stackoverflow.com/questions/5887220/z-index-how-does-it-affect-performance)
    - [Does the inclusion of z-index increase browser processing times?](https://stackoverflow.com/questions/13968097/does-the-inclusion-of-z-index-increase-browser-processing-times)
- Difference between auto, 0, and no z-index?
  - `auto` is the default `z-index` value that is initially used by the browser on all positioned elements.
    - auto can also set a positioned child to be the same as it’s parent’s stacking level.
  - Not specifying z-index is the same as `z-index: auto;` ; that is its initial value.
  - `z-index: 0` creates a stacking context while `z-index: auto` do not. 
  - auto: The box does not establish a new local stacking context. The stack level of the generated box in the current stacking context is the same as its parent’s box.
  - The big difference is that z-index:auto does not set a stacking context which means a positioned child can have a z-index take effect outside of the current context. 
  - If the parent had a z-index of zero (anything other than auto) then it becomes ‘atomic’ and a positioned child is forever trapped at the same level as the parent ( z-index:0 in this case). 
    - It does not matter what the child’s z-index may be because in respect of other positioned elements outside of this context it’s the parent’s z-index that will take effect if it is anything other than auto. 
    - The child element though will honour its own z-index in respect of other positioned elements under this same parent.
  - If the parent has z-index:auto then the positioned child’s z-index will determine if the element overlaps anything else outside this context.
  - z-index numbers (including zero and negative numbers) are basically the same and just allow to determine if one element is above or below another in the same stacking context.
  - ref
    - [Difference between auto, 0, and no z-index?](https://stackoverflow.com/questions/14109862/difference-between-auto-0-and-no-z-index)
    - [Why element with z-index 0 is shown above element with z-index 1](https://stackoverflow.com/questions/44291136/why-element-with-z-index-0-is-shown-above-element-with-z-index-1)

# pieces

- z-index的最大值就是：2147483647

# z-index

- The `z-index` CSS property sets the z-order of a positioned element and its descendants or flex items. 
- Overlapping elements with a larger `z-index` cover those with a smaller one.
- For a positioned box (that is, one with any position other than `static` ), the `z-index` property specifies:
  - Whether the box establishes a local stacking context.
  - The stack level of the box in the current stacking context.

- **values**

``` 

Initial value	auto
Applies to	positioned elements
Inherited	no
Computed value	as specified
Animation type	an integer
Creates stacking context	yes
```

- `auto`
  - initial value
  - The box does not establish a new local stacking context. 
  - The stack level of the generated box in the current stacking context is the same as its parent's box.
- `<integer>`
  - This `<integer>` is the stack level of the generated box in the current stacking context. 
  - The box also establishes a local stacking context in which its stack level is 0. 
  - This means that the z-indexes of descendants are not compared to the z-indexes of elements outside this element.

- ref
  - [mdn: z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index)

# Understanding CSS z-index

- [mdn: Understanding z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index)
  - [Stacking without the z-index property](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Stacking_without_z-index)
  - [Stacking with floated blocks](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Stacking_and_float)
  - [Using z-index](https://developer.mozilla.org/en/CSS/Understanding_z-index/Adding_z-index)
  - [The stacking context](https://developer.mozilla.org/en/CSS/Understanding_z-index/The_stacking_context)

- In the most basic cases, HTML pages can be considered two-dimensional, because text, images, and other elements are arranged on the page without overlapping. 
- In this case, there is a single rendering flow, and all elements are aware of the space taken by others. 
- The `z-index` attribute lets you adjust the order of the layering of objects when rendering content.
- In CSS 2.1, each box has a position in three dimensions. 
- This means that CSS style rules allow you to position boxes on layers in addition to the normal rendering layer (layer 0). 
- The Z position of each layer is expressed as an integer representing the stacking order for rendering. Greater numbers mean closer to the observer. 
- Z position can be controlled with the CSS `z-index` property.
- However, when `z-index` is applied to complex hierarchies of HTML elements, its behaviour can be hard to understand or predict. This is due to complex stacking rules.
- This tutorial will try to explain those rules, with some simplification and several examples.

## Stacking without the z-index property

> The stacking rules that apply when z-index is not used.

- When the `z-index` property is not specified on any element, elements are stacked in the following order ( from bottom to top )
  1. The background and borders of the root element
  2. Descendant non-positioned blocks, in order of appearance in the HTML
  3. Descendant positioned elements, in order of appearance in the HTML

- When the `order` property alters rendering from the "order of appearance in the HTML" within `flex` containers, it similarly affects the order for stacking context.
- static元素即使在html标签中的顺序在后面，也可能显示在positioned elements的下层、下面

## Stacking with floated blocks

- Floating blocks are placed between non-positioned blocks and positioned blocks:
  1. The background and borders of the root element
  2. Descendant non-positioned blocks, in order of appearance in the HTML
  3. **Floating blocks**
  4. Descendant non-positioned inline elements
  5. Descendant positioned elements, in order of appearance in the HTML

- The background and border of the non-positioned block (DIV #4) is completely unaffected by floating blocks, but the content is affected. This happens according to standard float behaviour.
- If an `opacity` value is applied to the non-positioned block (DIV #4), then something strange happens: the background and border of that block pops up above the floating blocks and the positioned blocks. 
- This is due to a peculiar part of the specification: applying a `opacity` value creates a new stacking context

## Using z-index

> How to use z-index to change default stacking.

- If you want to create a custom stacking order, you can use the `z-index` property on a **positioned** element. 
  - z-index只能用在非static定位元素上，若用在static定位元素上则无效果

``` 

bottom layer (farthest from the observer)
...
Layer -3
Layer -2
Layer -1
Layer 0 (default rendering layer)
Layer 1
Layer 2
Layer 3
...
top layer (closest to the observer)
```

- When no `z-index` property is specified, elements are rendered on the default rendering layer 0 (zero)
- If several elements share the same `z-index` value (i.e., they are placed on the same layer), stacking rules explained in the section Stacking without z-index apply.

## The stacking context 

- The stacking context is a three-dimensional conceptualization of HTML elements along an imaginary z-axis relative to the user, who is assumed to be facing the viewport or the webpage. 
- HTML elements occupy this space in priority order based on element attributes.
- The rendering order of certain elements is influenced by their `z-index` value. This occurs because these elements have special properties which cause them to form a stacking context.

- A stacking context is formed, anywhere in the document, by any element in the following scenarios:
  - Root element of the document ( `<html>` ).
  - Element with a position value `absolute` or `relative` and `z-index` value other than `auto` .
  - Element with a position value `fixed` or `sticky`
  - Element that is a child of a `flex` (flexbox) container, with `z-index` value other than `auto` .
  - Element that is a child of a `grid` (grid) container, with `z-index` value other than `auto` .
  - Element with a `opacity` value less than `1`
  - Element with the following properties with value other than `none`
    - tranform
    - filter
    - perspective
    - clip-path
    - mask/mask-image/mask-border
  - Element with a `isolation` value `isolate` .
  - Element with a `-webkit-overflow-scrolling` value `touch` .
  - Element with a `will-change` value specifying any property that would create a stacking context on non-initial value.
  - Element with a `contain` value of layout, or paint, or a composite value that includes either of them (i.e. `contain: strict/content` ).
  - Element with a `mix-blend-mode` value other than `normal` .

- Within a stacking context, child elements are stacked according to the same rules previously explained. 
- Importantly, the `z-index` values of its child stacking contexts only have meaning in this parent. 
- Stacking contexts are treated atomically as a single unit in the parent stacking context.

- Stacking contexts can be contained in other stacking contexts, and together create a hierarchy of stacking contexts.
- Each stacking context is completely independent of its siblings: only descendant elements are considered when stacking is processed.
- Each stacking context is self-contained: after the element's contents are stacked, the whole element is considered in the stacking order of the parent stacking context.
- The hierarchy of stacking contexts is a subset of the hierarchy of HTML elements because only certain elements create stacking contexts. 
- We can say that elements that do not create their own stacking contexts are assimilated(同化) by the parent stacking context
- It is important to note that DIV #4, DIV #5 and DIV #6 are children of DIV #3, so stacking of those elements is completely resolved within DIV#3. 
  - Once stacking and rendering within DIV #3 is completed, the whole DIV #3 element is passed for stacking in the root element with respect to its sibling's DIV.

- An easy way to figure out the rendering order of stacked elements along the Z axis is to think of it as a "version number" of sorts, where child elements are minor version numbers underneath their parent's major version numbers.

## Stacking context example

- example 1: 2-level HTML hierarchy, z-index on the last level
  - The only stacking context is the root context.
  - Without z-index, elements are stacked in order of occurrence.
  - If DIV #2 is assigned a positive (non-zero and non-auto) z-index value, it is rendered above all the other DIVs.
  - In this last example you can see that DIV #2 and DIV #4 are not siblings, because they belong to different parents in the HTML elements' hierarchy. 
    - Even so, stacking of DIV #4 with respect of DIV #2 can be controlled through z-index. 
    - It happens that, since DIV #1 and DIV #3 are not assigned any z-index value, they do not create a stacking context. 
    - This means that all their content, including DIV #2 and DIV #4, belongs to the same root stacking context.
    - It is important to remember that assigning an opacity less than 1 to a positioned element implicitly creates a stacking context, just like adding a z-index value.
- example 2: 2-level HTML hierarchy, z-index on all levels
  - It is worth remembering that in general the HTML hierarchy is different from the stacking context hierarchy. 
  - In the stacking context hierarchy, elements that do not create a stacking context are collapsed on their parent.
- example 3: 3-level HTML hierarchy, z-index on the second level
  - The first-level menu is only relatively positioned, so no stacking context is created.
  - The second-level menu is absolutely positioned inside the parent element. In order to put it above all first-level menus, a z-index is used.
  - The problem is that for each second-level menu, a stacking context is created and each third-level menu belongs to the context of its parent. So a third-level menu will be stacked under the following second-level menus
  - This problem can be avoided by removing overlapping between different level menus, or by using individual (and different) z-index values assigned through the id selector instead of class selector, or by flattening the HTML hierarchy.

# What No One Told You About Z-Index

- [What No One Told You About Z-Index_2013](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)
- Every element in an HTML document can be either in front of or behind every other element in the document. This is known as the stacking order.
- When the z-index and position properties aren’t involved, the rules are pretty simple: basically, the stacking order is the same as the order of appearance in the HTML. 
  - (OK, it’s actually a little more complicated than that, but as long as you’re not using negative margins to overlap inline elements, you probably won’t encounter the edge cases.)
- When you introduce the position property into the mix, any positioned elements (and their children) are displayed in front of any non-positioned elements. 
  - (To say an element is “positioned” means that it has a position value other than static, e.g., relative, absolute, etc.)
- Finally, when z-index is involved, things get a little trickier. 
  - At first it’s natural to assume elements with higher z-index values are in front of elements with lower z-index values, and any element with a z-index is in front of any element without a z-index, but it’s not that simple. 
  - First of all, z-index only works on positioned elements. 
  - If you try to set a z-index on an element with no position specified, it will do nothing. 
  - Secondly, z-index values can create stacking contexts, and now suddenly what seemed simple just got a lot more complicated.
- Groups of elements with a common parent that move forward or backward together in the stacking order make up what is known as a stacking context.
- Every stacking context has a single HTML element as its root element. 
- When a new stacking context is formed on an element, that stacking context confines all of its child elements to a particular place in the stacking order. 
- New stacking contexts can be formed on an element in one of three ways:
  - When an element is the root element of a document (the `<html>` element)
  - When an element has a `position` value other than `static` and a `z-index` value other than `auto`
  - When an element has an opacity value less than `1`
  - several newer CSS properties also create stacking contexts.
    - transforms, filters, css-regions, paged media

- Stacking Order Within the Same Stacking Context
- Here are the basic rules to determine stacking order within a single stacking context (from back to front):
1. The stacking context’s root element
2. Positioned elements (and their children) with negative z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML)
3. Non-positioned elements (ordered by appearance in the HTML)
4. Positioned elements (and their children) with a z-index value of auto (ordered by appearance in the HTML)
5. Positioned elements (and their children) with positive z-index values (higher values are stacked in front of lower values; elements with the same value are stacked according to appearance in the HTML)

- Global Stacking Order
- The key to avoid getting tripped up is being able to spot when new stacking contexts are formed. 
- If you’re setting a z-index of a billion on an element and it’s not moving forward in the stacking order, take a look up its ancestor tree and see if any of its parents form stacking contexts. If they do, your z-index of a billion isn’t going to do you any good.

# CSS stacking contexts: What they are and how they work

- [CSS stacking contexts: What they are and how they work](https://tiffanybbrown.com/2015/09/css-stacking-contexts-wtf/index.html)

- A stacking context is an element that contains a set of layers. 
  - This can be a root stacking context, as created by the `html` element. 
  - Or it can be a local stacking context, as created by specific properties and values.
- Within a local stacking context, the z-index values of its children are set relative to that element rather than to the document root. 
- Layers outside of that context — i.e. sibling elements of a local stacking context — can't sit between layers within it.
- Stacking contexts — whether local or root — follow a set of rules that determine the stacking and painting order of elements. Children of a stacking context are painted from bottom to top in the following order.
  1. Elements with a negative stack level, typically elements with z-index: -1
  2. Elements with a position value of static.
  3. Elements with a stack level of 0, typically positioned elements with a z-index value of auto.
  4. Elements with positive stack levels, e.g. a positioned element with a z-index value of 1 or higher.
- Two elements with the same stack level are layered based on their source order. 
- Successive elements stack on top of their predecessors.

# HOW THE CSS STACKING CONTEXT WORKS

- [HOW THE CSS STACKING CONTEXT WORKS](https://www.theguild.nl/how-the-css-stacking-context-works/)

- When stacking contexts are created on an element, that element will become a root stacking context element for its children elements. 
  - Documents can have many stacking contexts, so it is not rare to have stacking contexts inside other stacking contexts. 
  - The problem this creates is that children of the newly created stacking context won’t be able to render on top of an element in a different stacking context. Never ever. Even when the children will become positioned elements. Even with z-index: 999999; .
  - To overcome this problem, you can swap out these child elements in the current DOM hierarchy and bring them to the same level of the root stacking context ( `<html>` element). 
    - Positioned sibling elements can be ordered with the z-index property. 
    - However in more complex DOM structures where many elements live inside each other, this may include some rework of your CSS or even JavaScript and may be more complex.
- Most React applications can consist of those more complex DOM hierarchies, which won’t allow you to swap out elements with their own stacking context so easily. 
  - However, React incorporated a neat addition called “Portals” in v16. Portals will allow you to mount any DOM element at any place in your DOM structure.  
  - A typical use case for portals is when a parent component has an `overflow: hidden` or `z-index` style, but you need the child to visually “break out” of its container. For example, dialogs, hovercards, and tooltips

# Managing Z-Index In A Component-Based Web Application

- [Managing Z-Index In A Component-Based Web Application](https://www.smashingmagazine.com/2019/04/z-index-component-based-web-application/)

- An element can create a stacking context which becomes the root for z-index values of its descendants. 
- If an element is said to create a stacking context, it creates a basis for its children’s z-index values, so they’re never compared with anything outside the stacking context when determining paint order. 
- To put it another way, when an element creating a stacking context is painted, all its children are painted right after it and before any of its siblings.
- The main point of this article, however, is how to deal with z-index when your page is composed of dozens and hundreds of components, each potentially having children with z-index defined.
- One of the most popular articles on z-index proposes grouping all z-index values in one place, but comparing those values doesn’t make sense if they don’t belong to the same stacking context (which might not be easy to achieve in a large application).
- The question is, how are we supposed to come to this solution if we have components within components within components, each having elements with different z-indices? How can we be sure that changing z-index of the header won’t break anything else?
- The answer is a convention that eliminates the need for guesswork: changing z-indices within a component should only affect that component, and nothing else. 
- To put it differently, when dealing with z-index values in a certain CSS file, we should ideally only concern ourselves with other values in that same file.
- Achieving it is easy. We should simply make sure that the root of every component creates a stacking context. The easiest way to do it is to give it position and z-index values other than the default ones (which are static and auto, respectively).

``` CSS
.root__container {
  position: relative;
  z-index: 0;
}
```

- It uses more elements than the previous one, but computation associated with extra DOM elements is cheap whereas developer’s time (a lot of which can sometimes be spent on debugging stacking issues) is definitely not.
- This is the biggest benefit of the proposed approach: 
  - when looking at z-indices, it’s only the component itself that matters, not its context.
- drawbacks
  - you won’t be able to create such overlays inside both the header and the main section
- To recap:
  - Isolate components in terms of z-index values of elements by making the root of each component a stacking context; 
  - You don’t have to do it if no element within a component needs a z-index value other than auto; 
  - Within a component’s CSS file, maintain z-index values any way you like. 
    - It might be consecutive values, or you could give them a step of 10, or you can use variables — it all depends on your project’s conventions and the size of the component (although making components smaller is never a bad thing). 
    - Preferably, only assign z-index to sibling elements. 
    - Otherwise, you may inadvertently introduce more stacking contexts within a component, and you’re faced with the same issue again, luckily on a smaller scale; 
  - Debugging becomes easy. Find the first ancestor component of the two elements that are not stacked correctly, and change z-indices within that component as necessary.

# layerJS: layer based user interfaces

- [layerJS: layer based user interfaces](https://medium.com/layerjs/layerjs-declaring-layer-based-user-interfaces-14a4f9c5db89)
- [Getting started with layerJS](https://medium.com/layerjs/getting-started-with-layerjs-17f679452c8d)

- layerJS introduces the Stage-Frame concept, a new way to build the UI of websites and web apps. 
  - Content is split into fragments (frames) that live on stacked, moveable layers and that are interactively switched within viewports (stages). 
  - layerJS is a lean open source Javascript library that allows rich and intuitive interfaces with just simple HTML markup.

- layerJS introduces the Stage-Frame concept. 
  - Frames are arbitrary HTML fragments - just DIVs containing the content of your site - that can be fit into Stages (also DIVs serving as viewports) dynamically. 
  - The root Stage is usually the browser window and its Frames represent sub pages or app screens. 
  - Frames can be exchanged within Stages using animated transitions like swipes, fades or 3D transitions. 
  - Frames can be placed on overlapping layers allowing effects like floating menus or parallax backgrounds.

- HTML’s page concept and CSS are not sufficient to describe (declare) all possible interactions. 
  - Parts of the content, like menus or slider images need to be exchanged or overlaid dynamically, possibly underlined with animation to create intuitive interfaces. 
- layerJS lets you declare the parts of the interface in the HTML, indicating which content is shown where, when and how, without the need to write Javascript. 
- All content is organized in `frames` which are placed on moveable and overlapping layers. 
- The user navigates between frames by “swiping” specific frames into a viewport (aka `stage` ).
- knowledge from our ancestor project “Webpgr” went into this new open source framework
- A stage in layerJS represents a viewport, a rectangular area within which interaction can happen. What “happens” is that frames — rectangular areas with site content — are be shown and transitions between frames can occur.
- A transition “fits” a particular frame in the stage, moving the new frame into focus and moving the former frame out of focus.
- In the most simple case, if the stage and the frame have the same aspect ratio, fitting means that frame’s top left corner will be at the stage’s top-left corner and frame’s top right corner will be at the stage’s top-right corner and so on for the other two corners. 
  - If the aspect ratios are different, scrolling within the frame will occur.
  - layerJS provides different fitting functions including fit-to-width, fit-to-height, cover, contain and responsive, as well as different positioning modes like top, center or bottom. 
  - Some modes lead to y-scrolling, others to x-scrolling frames.
- Introducing a Layer as organizational level has a number of advantages
  - Layers can overlap and hence create floating elements like menus.
  - Second, transitions in one layer are independent of transitions in the other layers. This allows effects like parallax “swiping” (next level of parallax scrolling)
- On the top level, Frames represent sub pages or app screens. 
- However, Stages and Frames can also be nested.
- A nested stage can be for example used as a slider that exists within another (swipeable) frame.
  - This structure is reflected by nested divs with a special markup that indicates some of the divs as stages, layers or frames. 
  - Data attributes of those divs control the look of the layerJS elements, when they are shown and how they transition.

- Although it may have an initial learning curve, you will be awarded with an intuitive way to build any navigational pattern simply by adding some attributes and links to your HTML.

- Dynamic modifications in a UI are not arbitrary but follow clear patterns
  - interfaces mostly consist of HTML fragments (screens/pages, menus, popups, cards, slides, etc.) which are itself static.
  - in response to user interaction those fragments are dynamically shown, hidden, swapped, moved or transformed — mostly in an animated way.
- Through this separation, the static fragments can clearly be defined by HTML and some CSS, making their creation much more easy and intuitive. 
- The dynamic part of the interface is solely defined by a set of rules which define how the fragments are re-composed upon user interaction. 
- layerJS allows you to define those rules by regular links and HTML attributes.

- layerJS implements this concept as follows:
  - the static HTML fragments are “frames”, which are simply `div` s with the attribute `lj-type="frame"` .
  - “Stages” define where those frames should be shown. 

    - They are kind of “viewport” `div` s identified by the attribute `lj-type="stage"` . 
    - Stages contain one or more “layers” to allow to stack frames on top of each other.

  - The rules to dynamically show/hide frames are simply HTML links like `href="#mylayer.slide1"` which define which frame should be shown where after link click. 

    - Such transitions can also be triggered by gestures or API.

- The above separation of static and dynamic refers to the user interaction / navigation only. 
  - The static fragments could still show dynamic data through frameworks like VueJS, React or Angular. 
  - In this case the fragments would be templates, which still can clearly be defined by declarative HTML and CSS. 
  - From layerJS’ perspective they are nevertheless simply static fragments that can be shown, hidden or animated upon user interaction.

- To start you need to decide whether layerJS should deal with all user navigation (recommended) or should just act in a part of your interface. 
- In the first case you’ll hook up layerJS right at the body, by making it a stage adding `lj-type="stage"` .
- A stage indicates to layerJS that some fragment (frame) should dynamically be fit into it. 
- A stage can contain more than one layer to compose frames on top of each other. 
- Within the layer we added a single frame with id home which will contain the content of the first page/screen. 

# ref

- [zh: 前端项目中有简洁的z-index的约束规则（管理方案）吗？](https://www.zhihu.com/question/24216418)
- [Sass管理复杂的z-index](https://www.w3cplus.com/preprocessor/sassy-z-index-management-for-complex-layouts.html)
  - 使用臭名昭著的99999
  - 使用两位数递增z-index的值
  - 使用Sass管理顺序

- [What the heck, z-index?](https://www.joshwcomeau.com/css/stacking-contexts/)
