---
title: toc-lib-comp-timeline-undo
tags: [components, time-travel, timeline, toc, ui, undo]
created: 2023-11-23T17:56:29.394Z
modified: 2023-11-24T18:41:26.906Z
---

# toc-lib-comp-timeline-undo

# guide
- tips
  - timeline的使用范围很广，可以是内容的变化历史，可以是独立的component时间轴组件
  - undo/history类产品的形态可参考git commits的交互和设计
  - 考虑侧重静态展示，还是动态展示和操作
  - pause/resume的方案: redux, logic-flow

- time-travel的实现方案
  - redux/event-sourcing
  - git的实现基于snapshot，而不是es

- usecase-branching
  - testing/drafting
  - form editing
# redux-like
- https://github.com/reduxjs/redux-devtools/tree/main/packages/redux-devtools-slider-monitor /MIT/202404/ts
  - A custom monitor for use with Redux DevTools.
  - It uses a slider based on `react-slider` to slide between different recorded actions. 
  - 不依赖redux-toolkit
  - 依赖react-redux、styled-components
  - 支持play/pause/resume, 支持设置播放倍速
  - It also features play/pause/step-through, which is inspired by some very cool Elm examples.
  - [redux-devtools integrations for js and non-js frameworks](https://github.com/reduxjs/redux-devtools/blob/main/extension/docs/Integrations.md)
  - https://github.com/calesce/redux-slider-monitor /201706/js/inactive
    - https://calesce.github.io/redux-slider-monitor/
    - A custom monitor for Redux DevTools to replay recorded Redux actions
    - This package was merged into redux-devtools monorepo

- https://github.com/inakianduaga/redux-state-history /MIT/201608/ts/inactive
  - https://inakianduaga.github.io/redux-state-history-example/
  - Redux store enhancers for tracking and visualizing state changes
  - 依赖react-redux、jsondiffpatch、react-dropzone
  - todomvc在页面上展示op时间轴的示例，可自动播放，无需devtools，直接在页面上展示
  - 不支持设置播放倍速
  - Inspired by the redux devtools and redux slider monitor, this package provides state recording/playback (i.e. "time travel") abilities for redux applications.
  - Only state diffs are stored for each state change (performance untested for large state/long running applications).
  - Decoupled recording/debugging code
  - Import/Export histories: Play them back locally, including realtime speed.
  - Time-travel is "pure": That is, state history changes without refiring the actual actions that produced said change (so still works for impure/async actions).
  - A store enhancer provides the history tracking on each state change, recording the state change, the timestamp of the change, and the action type that produced said change.

- https://github.com/joshwcomeau/redux-vcr /MIT/201610/js/inactive
  - A Redux devtool that lets you replay user sessions in real-time
  - ReduxVCR consists of 4 individual packages:
    - Capture The capture layer is responsible for watching the stream of actions, selecting the ones that you'd like to record, and augmenting them with timestamps and metadata.
    - Persist The persist layer receives the data from Capture and persists it to Firebase. It handles all anonymous authentication concerns.
    - Retrieve The retrieve layer, meant to be used in development only, fetches the data from Firebase, and handles all admin authentication concerns.
    - Replay Finally, the replay layer is your interface to navigating and watching the recorded cassettes.
  - [Introducing ReduxVCR. The adorable tool that lets you record and re-watch user sessions _201610](https://medium.com/@joshuawcomeau/introducing-redux-vcr-cad57b37540a)
  - https://github.com/joshwcomeau/redux-vcr-todomvc /201609/js
    - ReduxVCR integrated into TodoMVC.
  - https://github.com/joshwcomeau/key-and-pad /201803/js
    - Fun experiment with the Web Audio API 

- https://github.com/zalmoxisus/mobx-remotedev /MIT/201902/js/inactive
  - MobX DevTools extension
  - Remote debugging for MobX with Redux DevTools extension
  - 🍴 forks
    - https://github.com/hlhr202/mobx-remotedev /MIT/202107/js/inactive
  - [MobX 6 (Cannot obtain atom from undefined) ](https://github.com/zalmoxisus/mobx-remotedev/issues/55)
    - I've switched from Redux devtools to a simple browser logger: kubk/mobx-log ; I am going to add Redux devtools support but for me it's no longer needed, because the logger already covers most of its usecases like inspecting store, calling actions and computeds.
  - [Roadmap _201607](https://github.com/zalmoxisus/mobx-remotedev/issues/1)
    - Support for non-browser environment (unify with remotedev)
    - As far as I know the Slider monitor just reverts to a previous state and then reapplies actions after that point. That's all what replaying does.
  - https://github.com/zalmoxisus/remotedev /MIT/201812/js/inactive
    - Remote debugging for any flux architecture.
    - https://github.com/zalmoxisus/remotedev/tree/master/examples
    - 示例包括 redux/flux/alt/rxjs/reflux
  - https://github.com/zalmoxisus/remotedev-app /MIT/201812/js/inactive
    - Web, Electron and Chrome app for monitoring remote-redux-devtools. Can be accessed on remotedev.io

- https://github.com/klauspaiva/redux-replayable /GPLv3/202010/ts
  - A small Redux utility to collect actions for replaying and logging, with built-in whitelisting and GDPR-friendly controls
- https://github.com/ezefattori/redux-replay /MIT/201905/js/inactive
  - A Redux middleware that records and replays actions in a timely manner. 
  - Works with the local storage of the browser or with a remote server.
  - 和replay产品结合使用的示例
- https://github.com/danislu/redux-action-replay-middleware /201608/js
  - Middleware for storing redux actions in localstorage and replaying them later. Usefull for QA reproducing bugs etc.

- https://github.com/JannicBeck/undox /MIT/202103/ts/inactive
  - Redux Implementation of Undo/Redo based on storing actions instead of states.
  - Actions are stored in an array named history. 
  - 🐛🆚️ The most popular and used library to add undo/redo functionality to redux is without a doubt `redux-undo`. It stores whole states instead of actions. This is great for small states and fat actions, but does not scale well if the state tree grows and especially if state is persisted.
  - It really just boils down to if your state is fat and your actions are thin or your state is thin and your actions are fat.
- https://github.com/omnidan/redux-undo /202001/js
  - higher order reducer to add undo/redo functionality to redux state containers
- https://github.com/StephenHaney/redux-time-travel /MIT/201809/js/inactive
  - A scalable undo redo time travel implementation that leaves your original state intact
  - powered by diffs and merges.

- https://github.com/onceup/redux-toolkit-history-example /202211/ts
  - Simple example of history undo-redo implementation with redux-toolkit

- https://github.com/recruit-tech/redux-action-replay /201710/js
  - Replay your redux actions in your application by puppeteer. 
  - Get renderer metrics and take screenshots.
  - good way to integrate test. This is a weak e2e

- https://github.com/clarus/redux-ship /MIT/201710/js
  - https://clarus.github.io/redux-ship-devtools/
  - Redux Ship is a side effects handler for Redux with a built-in system of snapshots for: 
    - live debugging thanks to a graphical visualization of the side effects;
    - simpler unit tests with snapshot testing.
  - 多用于测试
# timeline
- https://github.com/squarechip/timeline /202002/js/NoDeps/inactive
  - https://squarechip.github.io/timeline/
  - vanilla JavaScript horizontal/vertical timeline
  - 支持横竖向

- react-chrono /3.8kStar/MIT/202403/ts
  - https://github.com/prabhuignoto/react-chrono
  - https://react-chrono.prabhumurthy.com/
  - https://5f985eb478dcb00022cfd60e-wfennyutax.chromatic.com/
  - Modern Timeline Component for React
  - 依赖dayjs、styled-components
  - 示例丰富，支持自定义icon、动态请求、
  - Render timelines in three different modes (Horizontal, Vertical, Vertical-Alternating).
  - Auto play the timeline with the slideshow mode.
  - Nested timelines
  - Styled with emotion.

- https://github.com/steven-mercatante/react-timeline /201910/js
  - https://react-timeline.com/
  - add responsive and customizable timelines to React apps.
  - 支持alternate间隔布局、日期事布两列局件

- https://github.com/rcdexta/react-event-timeline /201905/js/仅竖向
  - https://rcdexta.com/react-event-timeline
  - React component to generate a responsive vertical event timeline
  - 支持card、collapsible

- https://github.com/lizashkod/react-timeline-range-slider /MIT/202104/js
  - https://codesandbox.io/p/sandbox/react-timeline-range-slider-ve7w2
  - 过于简单, 拖拽设置时间范围的边界

- https://github.com/visjs/vis-timeline /1.5kStar/MIT/202311/js
  - https://visjs.github.io/vis-timeline/
  - https://visjs.github.io/vis-timeline/examples/timeline/
  - customizable, interactive timelines and 2d-graphs with items and ranges
  - 鼠标滚动时会缩放日期范围
  - 示例丰富
  - 依赖moment、vis-data、vis-util，代码量不大
  - https://github.com/razbensimon/react-vis-timeline
  - https://github.com/visjs/vis-data
    - Manage unstructured data using DataSet. 
    - Add, update, and remove data, and listen for changes in the data.

- TimelineJS /2.8kStar/MPLv2/202309/js/inactive
  - https://github.com/NUKnightLab/TimelineJS3
  - http://timeline.knightlab.com/
  - https://timeline.knightlab.com/examples/houston/index.html
  - A Storytelling Timeline built in JavaScript.
  - TimelineJS works on any site or blog.
  - https://github.com/NUKnightLab/TimelineJS /8.8kStar/201507/js

- https://github.com/twitter/labella.js /201705/js
  - https://twitter.github.io/labella.js/
  - Placing labels on a timeline without overlap.
  - If you try to place labels for points on a timeline (or any 1D space), one common problem is the labels often overlap.
  - Force is the main engine that takes your nodes (labels) and figures out where to place them on the screen. 
    - There are actually two steps in this process: distribute and remove overlap(s)
    - In the distribute step, the nodes are split into multiple layers if all nodes cannot fit within one layer. 
    - In the remove overlap(s) step, Labella employs a constraint-based layout algorithm and uses special quadratric programming solver called VPSC to find the best location to place the nodes. 
  - labella.js does not require D3 to function though. It is a standalone library with no dependency. D3 was only used in the examples for demoing purpose
  - https://github.com/kristw/d3kit-timeline /201802/js/依赖d3-scale-axis
    - https://d3kit-timeline.vercel.app/
    - reusable timeline component built on top of D3, d3Kit and Labella.js

## play-pause

# gantt
- https://github.com/guiqui/react-timeline-gantt /202112/js
  - https://guiqui.github.io/react-timeline-gantt/index.html
  - a component built to display and manage calendar gantt charts. 
  - It use virtual rendering to be reactive an efficient.
  - 依赖moment
  - Three Zoom levels: day, week, month
  - Infinite calendar scrolling
  - Support all CRUD operations.
  - build to be use under a Flux architecture, this means that the component should not be managing the state of the application, is up the store and only the store to modify the state of the application. 
  - What our component does is to give you callbacks to know when the component is asking for a change.

- https://github.com/neuronetio/gantt-schedule-timeline-calendar /NonOpen/Paid
  - https://gantt-schedule-timeline-calendar.neuronet.io/examples
  - all-in-one component that you can use in different scenarios.

- https://github.com/JSainsburyPLC/react-timelines /202006/js/archived
  - https://jsainsburyplc.github.io/react-timelines/
  - React Timelines Library
  - 典型的gantt，左边是tasks，右边是时间轴

- https://github.com/React9k/react-timeline-9000 /202209/js/简陋
  - http://react-timeline-9000.s3-website-ap-southeast-2.amazonaws.com/
  - A performance focused timeline component in react

- https://github.com/clayrisser/react-gantt /202002/js/inactive
  - https://clayrisser.github.io/react-gantt/
  - gantt chart for react

- https://github.com/CrowdStrike/ember-timetree /201509/js/archived
  - http://crowdstrike.github.io/ember-timetree
  - Visualize hierarchical timeline data. Built with Ember.js and D3.js.
  - 左边文件树，右边时间轴
# branching
- https://github.com/nicoespeon/gitgraph.js /2.9kStar/MIT/202209/ts/inactive
  - https://www.nicoespeon.com/gitgraph.js
  - https://www.nicoespeon.com/gitgraph.js/stories/
  - 🌵 A JavaScript library to draw pretty git graphs in the browser
  - core无依赖，支持vanillajs、React，基于svg实现
  - core contains the main logic for manipulating git-like API and compute the graph that should be rendered.

- https://github.com/sdq/history-tree /201901/js
  - https://sdq.github.io/history-tree/
  - An interactive history tree for undo/redo/reset/revisit in javascript

- https://github.com/mikolalysenko/version-tree /201404/js/inactive
  - A data structure for maintaining a tree of versions. 
  - This can be useful when implementing fully persistent data structures using the DTSS method. 
  - Works in both node.js and browserify. 
  - All operations use amortized O(1) space and time.

- https://github.com/JasonStoltz/branch-js /201510/js
  - A utility to track and apply changes to javascript objects as if they were git branches.
  - "branching" lets you make changes to an object without directly affecting the original object until you are ready to "merge" those changes back in.
  - The most applicable use case for this is probably forms.

- https://github.com/dxinteractive/dendriform /202207/ts
  - Build performant, reactive data-editing UIs for React.js
  - Dendriform is less specific and far more adaptable, to be used to make entire UIs where allowing the user to edit data is the goal. 
  - Use `.branch()` to deeply access parts of your form's value. This returns another form, containing just the deep value.
  - "Dendriform" means "tree shaped", referencing the tree-like manner in which you can traverse and render the parts of a deep data shape.
# examples
- https://github.com/gonnavis/Timeline /202101/js
  - http://gonnavis.com/timeline/
  - 直观地显示各个历史时间段及历史地图
  - 时间轴是朝代，可显示不同朝代的地名
# time-travel/track-changes
- https://github.com/loro-dev/loro-time-travel-demo /202311/ts
  - https://loro-dev.github.io/loro-time-travel-demo/
  - demonstrate Loro's high performance and time travel capabilities. 
  - The entire code is only about 100 lines.

- https://github.com/haydn/use-state-snapshots /MIT/201906/js/NoDeps/inactive
  - https://codesandbox.io/s/use-state-snapshots-i6fuq
  - A React hook to keep track of state changes for undo/redo functionality
  - Drop-in replacement for `useState` including support for functional updates and lazy initial state.
  - 示例是简单画板，画笔渲染使用svg，下方显示多个时刻快照
  - ⌛️ Three ways to track changes:
    - Automatically create new snapshots at regular intervals.
    - Automatically create a snapshot for every single change to state.
    - Only create snapshots for specific changes to state.
  - Configurable limit for the number of snapshots to keep.
  - Snapshots include timestamps and ID's so you can display a timeline of changes.

- https://github.com/nytimes/ice /GPLv2/201402/js/NoDeps/inactive
  - https://nytimes.github.io/ice/demo/
  - Ice is a track changes implementation, built in javascript, for anything that is `contenteditable` on the web. 
  - Conceived(想出；构思) by the CMS Group at The New York Times, ice is powering the editor used for writing articles in the newsroom.
  - [Online Contract Editor problem](https://github.com/nytimes/ice/issues/146)
    - as someone who has contributed quite a bit to this library in the past, I feel obliged to tell you that this library is quite out of date and in many ways unfixable due to the way it is structured as browsers are changing those parts that this library touches all the time.
    - I would recommend going with an editing library that maintains its own model of the content - such as ProseMirror or CKEditor 5 and build tracked changes on top of that.

- https://github.com/open-source-labs/reactime /2.1kStar/MIT/202310/ts
  - https://www.reacti.me/
  - an open-source Chrome developer tool for time travel debugging and performance monitoring in React applications. 
  - enables developers to record snapshots of application state, jump between and inspect state snapshots, and monitor performance metrics such as component render time and render frequency.
  - Whenever the state is changed (whenever setState, useState is called), this extension will create a snapshot of the current state tree and record it
  - jump to any previously recorded snapshots
# diff
- https://github.com/MrWangJustToDo/git-diff-view /MIT/202404/ts
  - https://mrwangjusttodo.github.io/git-diff-view/
  - A Diff View component for React/Vue, just like Github
  - core只依赖lowlight
  - https://github.com/wooorm/lowlight /MIT/202310/js
    - Virtual syntax highlighting for virtual DOMs and non-HTML things
    - This package uses `highlight.js` for syntax highlighting and outputs objects (ASTs) instead of a string of HTML.
    - This package is useful when you want to perform syntax highlighting in a place where serialized HTML wouldn’t work or wouldn’t work well. 
    - You can use the similar `refractor` if you want to use `Prism` grammars instead. 
    - If you’re looking for a really good (but rather heavy) alternative, use `starry-night`.
# utils/undo
- https://github.com/philipmendels/undomundo /202204/ts/inactive
  - https://github.com/philipmendels/undomundo-multiplayground
  - https://philipmendels.github.io/undomundo-multiplayground/
  - a library for managing an action-based undo history, with support for time travel and branching. 
  - 依赖fp-ts
  - 🔀 It can be used in a multi-user setting because it allows for modification of the history at the time of undo/redo, as visually explained in this blog article from Figma.
  - Undomundo does not enable you to declare in advance which actions should be grouped/skipped and under which circumstances. You can however skip actions on a per-call basis
  - https://github.com/philipmendels/use-flexible-undo /MIT/202204/ts/inactive
    - React hook that lets you use undomundo's branching undo/redo functionality independently of how you structure your application state
  - https://github.com/philipmendels/overboard
    - https://philipmendels.github.io/overboard/
    - Example repo for using the library use-flexible-undo together with an interactive board. 
    - 示例画布基于dom实现
    - The board itself is built from scratch in React. The list with draggable items/layers uses react-beautiful-dnd.
    - Desktop only. No touch support yet.

- https://github.com/plantain-00/composable-editor-canvas /MIT/202404/ts
  - https://plantain-00.github.io/composable-editor-canvas/
  - A composable editor canvas library.
  - 提供了多种编辑场景示例
  - 提供了多种render target:react, react-canvas, react-svg, react-webgl
  - 实现了2种undo: undo, patch-based-undo-redo

- https://github.com/ArthurClemens/JavaScript-Undo-Manager /424Star/MIT/202305/js/NoDeps/单文件
  - https://codesandbox.io/s/undo-manager-color-sliders-z4myoj
  - Simple undo manager to provide undo and redo actions in JavaScript applications.
  - Actions (typing a character, moving an object) are structured as command pairs: one command for destruction (undo) and one for creation (redo). Each pair is added to the undo stack

- https://github.com/gliese1337/command-history /201903/ts
  - A typed undo-redo system based on the Command Object pattern
  - type ICommand = { execute, redo, undo, coalesce }
- https://github.com/ubie-oss/historian-js /202006/ts
  - History manager with undo and redo capabilities

- https://github.com/iMrDJAi/UndoRedo.js /MIT/202105/js
  - https://imrdjai.github.io/UndoRedo.js/
  - 示例参考 https://www.cssscript.com/demo/undo-redo-history/
  - simple JavaScript library provides a history for undo/redo functionality
  - 示例用的textarea，一次undo会删除多个文字

- https://github.com/propero-oss/action-history /202201/ts
  - Extensible history for reversible actions (undo/redo)
- https://github.com/BeardScript/history-actions /201903/ts
  - provides a simple and flexible pattern to define user actions that can be done and undone through the historyManager
  - You can record multiple actions within a single ChangeLog and undo them all in one call.

- https://github.com/zaboople/klonk /Klonk/202309/java
  - A text editor with an sort-of-unusual undo/redo algorithm
  - [Resolving the great undo-redo quandary | Hacker News _202211](https://news.ycombinator.com/item?id=33560275)
# graphics
- https://github.com/metricsgraphics/metrics-graphics /7.3kStar/MPLv2/202004/ts/inactive
  - http://metricsgraphicsjs.org/
  - a library built for visualizing and laying out time-series data
  - currently supports line charts, scatterplots and histograms, as well as features like rug plots.
# more
- https://github.com/xzdarcy/react-timeline-editor /MIT/202401/ts
  - https://zdarcy.com/
  - 基于react开发的，用于快速搭建 时间线编辑能力的组件
  - 可用于构建动画编辑器、视频编辑器等。
  - 提供强解藕的运行器能力，可脱离编辑器独立运行。
  - 依赖interactjs、react-virtualized

- [MyLens - One Timeline, Many Histories.](https://mylens.ai/)
