---
title: note-web-layer
tags: [layout, viz, web]
created: '2020-07-17T11:55:40.790Z'
modified: '2020-07-17T11:56:26.797Z'
---

# note-web-layer

## faq

- app图层设计是整体思维，是否与局部component的设计相矛盾
  - 那就从全局角度设计Component，考虑使用context api

## solution-catalog-layers

- popper.js /MIT/15.4kStar/202007
  - https://github.com/popperjs/popper-core
  - https://popper.js.org/
  - https://github.com/popperjs/react-popper
  - https://popper.js.org/react-popper/
  - It will position any UI element that "pops out" from the flow of your document and floats near a target element
- layerJS /MIT/1.8kStar/202002
  - https://github.com/layerJS/layerJS
  - https://layerjs.org/
  - https://github.com/layerJS/layerJS/wiki
  - Javascript UI composition framework
  - No dependencies.
- layer-for-layui /MIT/7.9kStar/201712
  - https://github.com/sentsin/layer
  - https://layer.layui.com/
  - 丰富多样的Web弹出层组件
  - [layui](https://github.com/sentsin/layui)
- react-layer-stack /MIT/152Star/201903
  - https://github.com/chain-police/react-layer-stack
  - Layering system for React. 
  - Useful for popover/modals/tooltip/dnd application
- react-layers-manager /MIT/107Star/201904 
  - https://github.com/giuseppeg/react-layers-manager
  - Manage layers and z-index in React applications using context and createProtal
  - render your layers as siblings of your application root
  - This way layers are guaranteed to always be on top of your application
- ref
  - https://github.com/sdgluck/react-z-index
    - Manage zIndex values in one place
    - wrap Modal component with ZIndex component
  - https://github.com/pieterv/react-layers
    - inspired by the work done on the react-bootstrap's [Overlay](https://react-bootstrap.github.io/components/overlays/)
    - Overlays rely on the third-party library Popper.js

## layerJS: layer based user interfaces

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

## Understanding CSS z-index

## z-index

- When the `z-index` property is not specified on any element, elements are stacked in the following order ( from bottom to top )
  - background and borders of the root element
  - Descendant non-positioned blocks, in order of appearance in the HTML
  - **Floating blocks**
  - Descendant non-positioned inline elements
  - Descendant positioned elements, in order of appearance in the HTML
- stack tips
  - applying a opacity value creates a new stacking context
-  Floating blocks are placed between non-positioned blocks and positioned blocks
  -  the background and border of non-positioned block  is completely unaffected by floating blocks，but the content is affected
-  If you want to create a custom stacking order, you can use the z-index property on a `positioned` element. 
  - z-index只能用在非static定位元素上，若用在static定位元素上则无效果
- When no z-index property is specified, elements are rendered on the default rendering layer 0 (zero)
- when z-index value is auto, the box does not establish a new local stacking context. The stack level of the generated box in the current stacking context is the same as its parent's box
-  the rendering order of certain elements is influenced by their z-index value. This occurs because these elements have special properties which cause them to form a stacking context.
- A stacking context is formed, anywhere in the document, by any element in the following scenarios
  - Root element of the document ( `<html>` ).
  - Element with a position value absolute or relative and z-index value other than auto.
  - Element with a position value fixed or sticky 
  - Element that is a child of a flex (flexbox) container, with z-index value other than auto.
  - Element that is a child of a grid (grid) container, with z-index value other than auto.
  - Element with a opacity value less than 1
  - Element with the following properties with value other than none
    - tranform
    - filter
    - clip-path
- Within a stacking context, child elements are stacked according to the same rules previously explained. Importantly, the z-index values of its child stacking contexts only have meaning in this parent. Stacking contexts are treated atomically as a single unit in the parent stacking context.
- Stacking contexts can be contained in other stacking contexts, and together create a hierarchy of stacking contexts.
- Each stacking context is completely independent of its siblings: only descendant elements are considered when stacking is processed.
- Each stacking context is self-contained: after the element's contents are stacked, the whole element is considered in the stacking order of the parent stacking context.
- The hierarchy of stacking contexts is a subset of the hierarchy of HTML elements because only certain elements create stacking contexts. We can say that elements that do not create their own stacking contexts are assimilated by the parent stacking context
- ref
  - https://developer.mozilla.org/en-US/docs/Web/CSS/z-index
  - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index
  - https://philipwalton.com/articles/what-no-one-told-you-about-z-index/
