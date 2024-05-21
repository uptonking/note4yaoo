---
title: lib-utils-layout-docview-dev
tags: [docview, ui-components, window-layout]
created: 2024-05-21T11:44:15.311Z
modified: 2024-05-21T11:45:57.951Z
---

# lib-utils-layout-docview-dev

# guide

- pros
  - Choose from a simple splitview, gridview, collapsable panes or a full docking solution. Combine multiple for complex layouts.
  - Built-in support for floating groups and groups in new windows with a supporting api for progmatic control.
  - Drag and Drop tab to position your layout as well as interacting with external drag events.
  - 支持跨group的keyboard快捷键
  - 支持Nested Dockviews, 即支持多实例、嵌套实例
  - framework-agnostic, 支持react/vue

- cons
  - 不支持rtl

- features
  - Serializable Layouts
  - Customizable Theme
  - Customize header to add additional icons or custom tab
  - high test coverage
  - Exposes native support for both ReactJS components and Vanilla TypeScript

- 基本架构
  - dock > groups/window > panel/tab
# issues
- 如何处理tab中的大文件，比如大于3000行/10M
# dev

# more

# issues-not-yet
- ## 

- ## 

- ## 

- ## 🤔 [Mention how to manage shared state that isn't "params" _202403](https://github.com/mathuo/dockview/issues/543)
- I got something to work using React `Context` . I think this might be the simplest way to do it. Wrap the `<DockviewReact>` in a context that is specifically for that Dockview, and then any prop based data you want to pass down to panels can exist there.

- Correct, dockview doesn't provide a way for you to render React components directly as children because of a number of reasons - mostly because the panels can be deserialized from application state and this requires assigning react components to ids etc etc... described more in Registering and Adding.
  - The purpose of the params that you can provide to each panel are more for static purposes, something you may wish to persist with layout
  - Under the hood though each panel is added to React through React Portals so things like React Context and the React DOM Tree are well preserved.
  - If you have any good examples of sending through application state without using a full state mananger (redux, mobx etc) I would be more than happy to accept PRs - the more examples and docs the better in my opinion.
# discuss
- ## 

- ## 

- ## 

- ## [Need an easy to to know if a panel/group is floating ](https://github.com/mathuo/dockview/issues/583)
- Both the panel and group `api` object expose a `location` property as an object 
  - For example `api.location.type` for floating groups should be equal to `floating` . this may not be well documented

# docs
- Dockview was originally a React-only library which is why the React version maintains the name `dockview` after splitting the core logic into a separate package named `dockview-core`.

- dockview-theme-abyss: Based on Visual Studio Code abyss theme
  - The provided themes are controlled primarily through a long list of CSS variables which can be modified by the user either entirely for a new theme or partial for a modification to an existing theme.

- Each panel has an api which is used to control specific features on that individual panel. 
  - The panel also has access the group api and the container api.
- To open a panel requires a unique id and the name of the component to render.
  - To render a custom tab component you should specify the tabComponent.
- You can position a panel relative to an existing panel, group using direction. 
  - If you do not provide a reference panel or group then the panel will be positioned to the edge of the dock in the specified direction.

- You can update a panel through the Panel API.
  - Use this feature sparingly: Anything you assign to the params options of a panel will be saved when calling api.toJSON(). Only use this to store small amounts of static view data. Do not use this to store application state or dynamic panel state.

- You can move a panel through the Panel API and you can find out how to move a Group here. panel.api.moveTo({ group, position, index }); 

- Rendering type is an important consideration when creating your application and whether your panels should be destroyed when hidden.
- When a panel is selected, all other panels in that group are not visible. 
  - `onlyWhenVisible`: Remove the element from the DOM tree to make space for the new panel.
  - `always`: Keep the DOM tree alive but hide it in order to allow the select panels content to show.
- Both are valid use-cases therefore the dock allows you to choose your rendering mode, the default however is the first option since this is the most memory efficient solution.
- By default `DockviewReact` only adds to the DOM those panels that are visible, if a panel is not the active tab and not shown the contents of the hidden panel will be removed from the DOM.

- The panel instance is only ever destroyed when it is removed from the dock allowing you to still run code associated with the panel when it is not visible. 
  - The renderer only affects what happens to the DOM element.

- Each dock contains groups and each group contains panels. 
  - Logically a user may want to resize a panel but this really translates to resizing the group which contains that panel.
  - The panel resize methods are repeats of the same resize methods found on the group.
- Each Dockview contains of a number of groups and each group has a number of panels. 
  - Logically a user may want to resize a panel, but this translates to resizing the group which contains that panel.

- Dockview supports a wide variety of built-in Drag and Drop possibilities.
  - Merge one group with another group
  - Move both Tabs and Groups in relation to the container

- Dockview fire and intercepts Drag & Drop events extensively however it is indended that the user has ultimate control over all events.
  - External Dnd events can be intercepted through a number of utilities.

- Dockview has built-in support for floating groups. 
  - Each floating container can contain a single group with many panels and you can have as many floating containers as needed. 
  - You cannot dock multiple groups together in the same floating container.

- Locking a group will disable all drop events for this group ensuring no additional panels can be added to the group through drop events. 
  - You can still add groups to a locked panel programatically using the API though.

- Dockview has built-in support for opening groups in new Windows. 
  - Each popout window can contain a single group with many panels and you can have as many popout windows as needed. 
  - You cannot dock multiple groups together in the same window.
  - Popout groups cannot be maximized. Calling maximize function on groups in these states will have no effect.
  - Popout windows require your website to have a blank .html page that can be used, by default this is set to /popout.html but can be configured to match requirements.

- A panel will appear with a scrollbar if the the contents of your view has a fixed height. 
  - If you are using a relative height such as 100% you will need a child container with the appropriate overflow value to allow for scrollbars.

- iFrames required special attention because of a particular behaviour in how iFrames render:
  - Re-parenting an iFrame will reload the contents of the iFrame or the rephrase this, moving an iFrame within the DOM will cause a reload of its contents.
- To ensure iFrames work as expected you should render them in panels with `renderer: 'always'` to ensure they are never removed from the DOM, alternatively set the `defaultRenderer` to `always`.

- 
- 
- 
