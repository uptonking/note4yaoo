---
title: lib-utils-layout-dockview-dev
tags: [dockview, ui-components, window-layout]
created: 2024-05-21T11:44:15.311Z
modified: 2024-05-27T11:39:14.886Z
---

# lib-utils-layout-dockview-dev

# guide

- pros
  - 🪟 Choose from a simple splitview, gridview, collapsable panes or a full docking solution. Combine multiple for complex layouts.
  - Built-in support for floating groups and groups in new windows with a supporting api for pragmatic control.
  - dockview doesn't interfer with any drag and drop logic for other controls
    - Drag and Drop tab to position your layout as well as interacting with external drag events
  - 支持keyboard快捷键，导航到其他group的tab
  - ✨ 支持Nested Dockviews, 即支持多实例、嵌套实例
  - framework-agnostic, 支持react/vue

- cons
  - drag拖拽体验差，拖拽结束到视图更新的等待时间太长
  - 不支持rtl

- features
  - Serializable Layouts
  - Customizable Theme
  - Customize header to add additional icons or custom tab
  - high test coverage
  - Exposes native support for both ReactJS components and Vanilla TypeScript
  - ✨ 内置丰富的拖拽功能: 可折叠面板accordion拖拽改变顺序，tab改变顺序

- dev-xp 简单场景没必要上复杂的库
  - 基本架构: dock > groups/window > panels/tab
  - 容易实现dock标签页元素的交互效果
  - 💡 dockview最适合的场景是标签页拖拽，不需要拖拽的场景使用简单sidebar即可
    - 容易实现将标签页拖到左中右的位置，左中右位置一般是并列关系
    - 适合实现将浮动面板的标签拖拽到主区域, 如果不需要可不用dockview
    - dockview/splitpanel容易实现拖拽调整宽度

- examples
  - [经典ide三栏布局 GridviewReact ](https://github.com/mathuo/dockview/tree/master/packages/docs/sandboxes/editor-gridview)
  - [Dockview demos](https://dockview.dev/demo/)
  - [Floating Groups DockviewReact ](https://dockview.dev/docs/core/groups/floatingGroups)
  - 最大化 ~~最小化~~ [Maximized Groups DockviewReact ](https://dockview.dev/docs/core/groups/maxmizedGroups)
  - [Window-like mananger with tabs ](https://dockview.dev/docs/advanced/)
  - [iframes ](https://dockview.dev/docs/advanced/iframe)
  - [Nested Instances ](https://dockview.dev/docs/advanced/nested)
  - 💡 将外部元素拖到dockview [External Dnd Events ](https://dockview.dev/docs/core/dnd/external)
  - 🌲 文件树的拖拽 [Dnd ](https://dockview.dev/docs/core/dnd/dragAndDrop)
  - [Dockview Framework Wrappers (Vue.js, Angular, JavaScript etc.) ](https://github.com/mathuo/dockview/issues/562)
  - https://codesandbox.io/u/mathuo
  - [Search - CodeSandbox](https://codesandbox.io/search?query=dockview&page=1&configure%5BhitsPerPage%5D=12&refinementList%5Bnpm_dependencies.dependency%5D%5B0%5D=dockview)
  - dockview + codemirror

- resources
  - https://github.com/search?type=code&q=dockview+path%3Apackage.json%20NOT%20is:fork
# draft
- default-width
  - 👀 宽度要在所有panel都addPanel后再统一设置，不能addPanel后立即设置, 且要在setVisible后设置
- 浏览器窗口resize时，自动更新各panel宽度

- maximize-panel时，支持占满指定元素的宽高，而不是占满整个Dockview(避免挡住标题栏)

- 动态添加/关闭面板的数据驱动方式，官方示例使用的是api.addPanel命令式操作

- floating-panel
  - 支持设置默认width/height
  - Floating groups cannot be maximized
  - `addFloatingGroup` only accepts existing panels and groups

- tab
  - disable dnd

- 未实现将折叠面板中的文件拖拽到编辑区的交互

- panel的滚动条自动显示隐藏

- Gridview不支持floating-panels, 仅Dockview支持floating-panels

- replace watermark with placeholder

- props.api.getParameters() 无法获取到参数, 但 props.params可以

- drag
  - how to disable drag of a tab or group, not drop

- 当拖拽导致面板宽度变化时，希望显示不同的内容
  - 可结合container query实现

- 
- 
- 

# dev-xp
- 💡 旧版文档中包含更多的api使用示例, 可在github仓库查看旧版文档markdown

- 显示隐藏groups的处理
  - ✅ 官方api已支持

- ⚠️ 使用dockview首先要确定布局的位置逻辑和最大化窗口的显示范围
  - 如果左侧边栏不希望被最大化挡住，那么左侧边栏就不必用dockview实现

- disableDnd={true}
  - tab能drag, 不能drop
- locked={true}
  - 宽度不能resize
- panel.group.locked = 'no-drop-target'
  - 不能drop

- ide示例基于Gridview实现， 编辑区面板的初始数据 `size: 100` 很重要, 若注释掉，则无法显示left/right
  - 🧐 Gridview暂不支持floating，实现floating推荐使用Dockview
  - Dockview也可以实现Gridview的分屏拖拽的效果

- left-sidebar最好不要放在DockviewReact里面实现，因为实现below不好实现
  - 变通思路是先创建中间区域的panels，再通过左右方向添加2个侧边栏

- 🤔 面板配置方式
  - 设置同一个group多个panel的显示隐藏，必须先设置要显示的，再隐藏不需要显示的panel，才能符合预期
  - 要先setVisible，再setSize，这样宽高才会生效

- 
- 
- 

- 根据业务场景的需求，panel的渲染模式需要采用onlyWhenVisible/always的组合
  - 兼顾内存占用和渲染性能

- tab内容懒加载的最佳实践
  - gridview的面板逐个懒加载

```JS
// 动态添加任意panel组件
layoutApi.current?.addPanel({
  id: panel.id,
  component: 'default',
  title: panel.tabTitle || `Untitled`,
  tabComponent: 'tabEphemeral',
  params: {
    type: panel.panelType || 'general',
    renderType: panel.renderType,
    panelId: panel.id,
  },
  position: {
    referencePanel: 'mainEditor',
  },
})
```

# codebase 🔡🧮

- 
- 
- 
- 
- 
- 
- 
- 

# examples
- https://github.com/lyonbot/onebox /MIT/202401/ts/inactive
  - https://lyonbot.github.io/onebox/
  - a Draft Notebook for Developers
  - Run JS/TS in Browser: Execute JavaScript and TypeScript code directly in your browser, supporting ES modules import/export. Integrated a Chrome DevTools Frontend for inspecting.
  - 支持创建html/js并执行js，但打开打开的chrome-devtools不支持预览html
  - 支持从文件树拖拽文件到标签页
  - 嵌入了chrome-devtools
  - 依赖monaco-editor、dexie、localforage、solid-js、markdown-it

- https://github.com/kosaj/dockview-iframe-plugin /202308/ts/inactive
  - iframe

- https://github.com/prashantpaddune/CDE /202310/ts/inactive
  - CDE powered by StackBlitz's WebContainer
  - Monaco + DockView + Xterm + YJS + React Complex Tree

- https://github.com/Oneirocom/Magick /apache2/202405/ts
  - https://magickml.com/
  - a cutting-edge toolkit for a new kind of AI builder
  - Magick is a groundbreaking visual AIDE (Artificial Intelligence Development Environment) for no-code data pipelines and multimodal agents.

- https://github.com/DB-Insight/DBInsight /MIT/202402/ts
  - open source database management tool

- https://github.com/umstek/listen-next /202402/ts
  - https://listen-next.vercel.app/
  - A simple web based audio player for offline files.
# issues
- 如何处理tab中的大文件，比如大于3000行/10M
# more

# issues-not-yet
- ## 

- ## [How to set constraints for floating groups? ](https://github.com/mathuo/dockview/discussions/568)

- ## [How can i prevent group from removing after the last panel was closed? ](https://github.com/mathuo/dockview/discussions/587)

- ## [Save group restrictions as a part of layout object ](https://github.com/mathuo/dockview/issues/493)
- Group constraints currently come with quite a few limitations including the fact they are not persisted. It would need some careful though into how this might work if it was added.

- ## [Unable to persist fullscreen / maximized mode ](https://github.com/mathuo/dockview/issues/494)

- ## 💡 [Implement default width and height for Dockview panels ](https://github.com/mathuo/dockview/issues/589)
  - When adding a new panel to the top/right/bottom/left of a panel in a Dockview component, the available space is evenly distributed between the two panels. This is not always a desirable default.
  - I see that the underlying GridView can handle fixed widths/heights when adding panels.
  - It should be nice if we could define default widths and/or heights for panels. 
- @mathuo created an experiment in PR #592 for it.
  - [feat: priority experiments _202404](https://github.com/mathuo/dockview/pull/592)
  - preferredWidth and preferredHeight works very-very well, but priority seemingly did not work. And it breaks down when two or more panels are grouped together, the preferredWidth/preferredHeight info is lost.

- ## [Set exact width in addPanel ](https://github.com/mathuo/dockview/discussions/339)

```JS
event.api.addPanel({
  id: 'default',
  component: 'default'
}).api.setSize({
  width: 250
})·
```

- ## [Linking the states of nested dock instances ](https://github.com/mathuo/dockview/issues/532)
- When we dynamically add a panel inside a nested dockview, it cannot save to local storage.
  - I guess the problem is because when we create a nested dockview, it will create a new API instance. However when we save the state by calling toJson we just handled the parent/container API. But I'm not sure how to merge/combine these apis into one and save to localstorage.

- By creating another dock within the panel of an existing dock you are creating a new instance of the dock component. They are not linked internally in any way and do not know about each other.
  - Currently it is expected that the if the user creates a nested dock, they save that nested dock state seperately and use their application state (perhaps associate that nested layout with the `id` of the panel it's nested within) to link everything back together. 
  - Think of the nested dock JSON as just some application state you would associate with that panel within your application.

- ## 🤔 [Mention how to manage shared state that isn't "params" _202403](https://github.com/mathuo/dockview/issues/543)
- I got something to work using React `Context` . I think this might be the simplest way to do it. Wrap the `<DockviewReact>` in a context that is specifically for that Dockview, and then any prop based data you want to pass down to panels can exist there.

- Correct, dockview doesn't provide a way for you to render React components directly as children because of a number of reasons - mostly because the panels can be deserialized from application state and this requires assigning react components to ids etc etc... described more in Registering and Adding.
  - The purpose of the params that you can provide to each panel are more for static purposes, something you may wish to persist with layout
  - Under the hood though each panel is added to React through React Portals so things like React Context and the React DOM Tree are well preserved.
  - If you have any good examples of sending through application state without using a full state mananger (redux, mobx etc) I would be more than happy to accept PRs - the more examples and docs the better in my opinion.

- ## [How can I share data between panels? ](https://github.com/mathuo/dockview/discussions/593)
- I managed to solve it myself using React Context

# discuss
- ## 

- ## 

- ## [setConstraints on gridview / enable size locking _202303](https://github.com/mathuo/dockview/issues/210)
  - Im not sure if i understand the setConstraints method from here, but it does seem not to work - no restrictions applied. setSize works, but to keep the group's size in required range, i need to call it repeatedly.

- When using the DockviewReact component a user adds panels which are added to groups. Internally what's being resized when you drag the resize handles is the group, the group resizes which then forces the panel to resize with the group.

- ## [Locked mode: prevent all mouse resizing _202401](https://github.com/mathuo/dockview/issues/460)
- I guess there are two features here:
- Disable mouse-interaction based resizing
  - I think this could be achieved entirely through CSS making it a fairly small change that is required.
- Disable the dnd drop functionality
  - This one is more involved but actually seems to be fairly similar to an existing issue here which I have been doing some work on which is to expose a function allowing control of whether dnd overlays are shown, in your case this function would just disable all overlays.

- 
- 
- 

- ## [Feature request: Adding a gap around panels ](https://github.com/mathuo/dockview/issues/447)
- 

- ## [Enhance onDidLayoutChange Behavior ](https://github.com/mathuo/dockview/issues/520)
- I'm using the onDidLayoutChange change from DockviewApi to detect changes in my layout so I can persist the layout to a database. 
  - It looks like onDidLayoutChange gets fired even when the layout itself hasn't necessarily changed, but the active panel has. The result is that the user gets many spurious calls-to-action to save their layout, even though the only thing that's changed is which panel is currently active.

- 202403: In version 1.10.0 several enhanements have been make to the events dockview fires, reducing duplicate events substancially. 

- ## [Adding element/icon to title ](https://github.com/mathuo/dockview/discussions/423)
- There are currently two ways to alter the behaviour of the header tabs. 
  - You can provide an alternative default template which will be used instead of the provided one 
  - or you can provide a template per panel when adding those panels.

- ## 🌰 [Actions in paneview ](https://github.com/mathuo/dockview/issues/335)
- I've tried with little time to do an example here: codesandbox.io/s/simple-paneview-forked-qrklqh?file=/src/app.tsx
  - It works, but I have my doubts about the performance of passing a component to `updateParameters` .

- ## [How to keep group remain after last child has been removed?  ](https://github.com/mathuo/dockview/issues/402)
- 
- 
- 

- ## [Incorrect Positioning of floating Panel in addPanel and fromJson Methods ](https://github.com/mathuo/dockview/issues/318)
- I've got a sandbox below which is a dockview-core example creating some floating and non-floating groups. 
  - https://codesandbox.io/s/broken-tdd-7jd9v7?file=/src/app.ts

- ## 🪟 [Is it possible to create a "grid" layout programmatically with add panel? ](https://github.com/mathuo/dockview/discussions/420)
- There are some docs on the `addPanel` method you may find useful here
  - you can provide a position object which takes a couple of arguments which help position the panel. 
  - You can position the new panel relative to an existing panel by providing `referencePanel` or an existing group by providing `referenceGroup` . 
  - You can also provide a `direction` which will be relative to the referencePanel or referenceGroup if provided and if not provided the direction is absolute
- you could achieve the same layout with many alternative positioning configurations 

- ## 🌰 [Horizontally spanned panel ](https://github.com/mathuo/dockview/discussions/478)
- you can provide a position object which takes a couple of arguments which help position the panel. You can position the new panel relative to an existing panel by providing referencePanel or an existing group by providing referenceGroup. 

- ## [Gready rendering mode  ](https://github.com/mathuo/dockview/issues/397)
- The standard behaviour of dockview is to "de-render" any hidden panels (those panels that are not active). 
  - This is and will remain the default behaviour however there are some circumstances where it would be more beneficial to leave all panels rendered but hidden (display: none) to preserve certain DOM specific state such as scroll position.
  - If you want to change the default behaviour you can specify a defaultRenderer at the component level. This information is not persisted as a part of any serialized layout.

- ## [Option to prevent closing tabs ](https://github.com/mathuo/dockview/issues/563)
- You can use custom tab components and, in that way, remove the close icon

- [Add 'hideClose' to DockviewDefaultTab component ](https://github.com/mathuo/dockview/issues/321)

- ## [How to remove a panel programmatically ? ](https://github.com/mathuo/dockview/discussions/292)
- There actually isn't a removePanel method directly exposed currently so to pragmatically remove you would need to do this via the panels api methods. For example you can close a panel by calling .close().

- ## [Set exact width in addPanel ](https://github.com/mathuo/dockview/discussions/339)
- I discovered that I can do it inside the component itself with the API, and I think I can also do

- ## [Move between tabs ](https://github.com/mathuo/dockview/discussions/343)
- There is support to switch the active panel pragmatically in the dockview api.

- ## [Possible to stop floating windows being dragged outside visible dockview area? ](https://github.com/mathuo/dockview/discussions/325)
- You can include both `snap` and `priority` when adding items to the Gridview through `.addPanel()` . Those flags don't exist on the Dockview since they don't make sense in that context. I will make sure I add all this to the gridview docs.

- ## 💡 [[BUG] dockview craches when changing from excalidraw ](https://github.com/mathuo/dockview/issues/317)
- When you switch tabs in dockview the panel that becomes hidden is removed from the dom but the React component remains active (so that if you was to return to that panel the component would be as left) however this only works if some assumptions are obeyed, one of which being that component doesn't try to access the window because whilst hidden it has been removed from the window and has no access to it.
- If you find that you do not want to destory the component and you want it to remain active even when not visible, it may be worth reading how dockview allows you to work with iframes too here since this would allow a particular component to remain attached to the dom even when not visible.
  - This approach is suitable when you are ok with the underlying React component being unmouted when the panel is hidden.

- and another link using a similar approach where the panel is absolutely positioned and hidden as required but never removed from the dom, based on the iframe examples found on dockview.dev
  - This approach keeps the panel attached to the dom at all times but will hide the element as and when required.

- ## [Need an easy to to know if a panel/group is floating ](https://github.com/mathuo/dockview/issues/583)
- Both the panel and group `api` object expose a `location` property as an object 
  - For example `api.location.type` for floating groups should be equal to `floating` . this may not be well documented

# docs
- v1.10.0 has a few substancial changes around how events are fired and how things are made "active" and focused.

- Dockview was originally a React-only library which is why the React version maintains the name `dockview` after splitting the core logic into a separate package named `dockview-core`.

- dockview-theme-abyss: Based on Visual Studio Code abyss theme
  - The provided themes are controlled primarily through a long list of CSS variables which can be modified by the user either entirely for a new theme or partial for a modification to an existing theme.

- Each panel has an api which is used to control specific features on that individual panel. 
  - The panel also has access the group api and the container api.
- To open a panel requires a unique id and the name of the component to render.
  - To render a custom tab component you should specify the tabComponent.
- 💡 You can position a panel relative to an existing panel, group using `direction`. 会在direction指定的方向添加一个group。
  - If you do not provide a reference panel or group, then the panel will be positioned to the edge of the dock in the specified direction.
 
- You can update a panel through the Panel API.
  - Use this feature sparingly: Anything you assign to the params options of a panel will be saved when calling api.toJSON(). Only use this to store small amounts of static view data. Do not use this to store application state or dynamic panel state.

- You can move a panel through the Panel API and you can find out how to move a Group here. panel.api.moveTo({ group, position, index }); 

- Rendering type is an important consideration when creating your application and whether your panels should be destroyed when hidden.
- When a panel is selected, all other panels in that group are not visible. 
  - `onlyWhenVisible`: Remove the element from the DOM tree to make space for the new panel.
  - `always`: Keep the DOM tree alive but hide it in order to allow the select panels content to show.
- Both are valid use-cases therefore the dock allows you to choose your rendering mode, the default however is the first option since this is the most memory efficient solution.
- By default `DockviewReact` only adds to the DOM those panels that are visible, if a panel is not the active tab and not shown the contents of the hidden panel will be removed from the DOM.

- > The panel instance is only ever destroyed when it is removed from the dock allowing you to still run code associated with the panel when it is not visible. 
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
- 🧐 `addFloatingGroup` only accepts existing panels and groups

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
