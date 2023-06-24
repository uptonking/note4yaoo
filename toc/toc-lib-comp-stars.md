---
title: toc-lib-comp-stars
tags: [components, toc, widget]
created: 2020-12-19T10:12:11.212Z
modified: 2021-01-12T18:49:07.422Z
---

# toc-lib-comp-stars

# guide

# calendar
- https://github.com/nhn/tui.calendar /ts
  - http://ui.toast.com/tui-calendar
  - available when using the Plain JavaScript, React, Vue Component.
  - 依赖tui-date-picker、tui-time-picker、preact、immer
  - date依赖moment、moment-timezone

- https://github.com/fullcalendar/fullcalendar
  - https://fullcalendar.io/
  - Full-sized drag & drop event calendar in JavaScript

- https://github.com/Zertz/tempocal
  - https://tempocal.pierluc.io/
  - Highly flexible building blocks to craft calendars with Temporal API

- https://github.com/wojtekmaj/react-date-picker
  - A date picker for your React app.
- https://github.com/wojtekmaj/react-time-picker
  - A time picker for your React app.
- https://github.com/wojtekmaj/react-calendar
  - Ultimate calendar for your React app.
- https://github.com/gpbl/react-day-picker
  - Lightweight date picker component for React

## calendar-heatmap

- https://github.com/grubersjoe/react-activity-calendar
  - https://grubersjoe.github.io/react-activity-calendar/
  - A React component to display activity data in a calendar (heatmap)
  - 依赖date-fns, tinycolor2, react-tooltip
- https://github.com/uiwjs/react-heat-map
  - https://uiwjs.github.io/react-heat-map/
  - 依赖react
  - 长期维护

- https://github.com/arunghosh/react-grid-heatmap
  - A react component for heatmap visualisation in grid layout

- https://github.com/kevinsqi/react-calendar-heatmap
  - https://www.kevinqi.com/react-calendar-heatmap/
  - An svg calendar heatmap inspired by github's contribution graph
  - 依赖 memoize-one

- https://github.com/g1eb/reactjs-calendar-heatmap
  - https://rawgit.com/g1eb/reactjs-calendar-heatmap/master/
  - 依赖d3 v4, moment

- https://github.com/wa0x6e/cal-heatmap
  - https://cal-heatmap.com/
  - a javascript module to create calendar heatmap to visualize time series data, a la github contribution graph
  - 依赖d3 v3
- https://github.com/DKirwan/calendar-heatmap
  - A d3 heatmap for representing time series data similar to github's contribution chart
  - 依赖d3 v3
# timeline
- https://github.com/prabhuignoto/react-chrono /ts
  - https://5f985eb478dcb00022cfd60e-wfennyutax.chromatic.com/
  - Modern Timeline Component for React
  - Render timelines in three different modes (Horizontal, Vertical, Vertical-Alternating).
  - Auto play the timeline with the slideshow mode.
  - Nested timelines
  - Styled with emotion.

- https://github.com/visjs/vis-timeline /js
  - https://visjs.github.io/vis-timeline/
  - customizable, interactive timelines and 2d-graphs with items and ranges.

- TimelineJS /2.6kStar/MPLv2/202303/js
  - https://github.com/NUKnightLab/TimelineJS3
  - http://timeline.knightlab.com/
  - A Storytelling Timeline built in JavaScript.
# react-list-keyboard
- react-window默认显示滚动条，但可通过css隐藏滚动条同时使内容支持滚动
  - [Add option to FixedSizeList for hiding scrollbar](https://github.com/bvaughn/react-window/issues/375)
    - scrollbar-color: transparent transparent;
- mui默认的list就支持键盘操作
- [Hide scroll bar, but while still being able to scroll](https://stackoverflow.com/questions/16670931)

- https://github.com/lukasbach/react-accessible-menu
  - https://lukasbach.github.io/react-accessible-menu/storybook/
  - 只依赖uuid
  - Accessible keyboard-friendly interactive list/menu component
  - 提供了丰富的示例，包括 vertical、horizontal、grid、imperative、virtualized
  - 长列表的示例支持向下方向键自动滚动
  - virtualized的示例基于 react-virtualized

- https://github.com/dzucconi/use-keyboard-list-navigation
  - A React hook to navigate through lists with your keyboard.

- https://github.com/taniarascia/react-hooks /js
  - https://taniarascia.github.io/react-hooks/
  - [Build a CRUD App in React with Hooks](https://www.taniarascia.com/crud-app-in-react-with-hooks/)
  - a simple CRUD app that can add, update, or delete users.

- https://github.com/exivity/react-crud-hook
  - make it easier to perform CRUD-operations while also providing methods to set attributes and relationships on a record. 
  - Records should conform to the JSON: API specs

- https://github.com/bezkoder/react-typescript-api-call
  - https://github.com/bezkoder/react-hooks-crud-web-api /js
  - Build a React Hooks CRUD Application to consume Web API with Axios, display and modify data with Router & Bootstrap.

- https://github.com/candraKriswinarto/react-crud-context-api
  - Create CRUD application using react hooks and context api, Reactstrap
# keyboard-shortcuts
- https://github.com/pacocoursey/cmdk
  - https://cmdk.paco.me/
  - Fast, unstyled command menu React component.

- https://github.com/ssleptsov/ninja-keys
  - https://ninja-keys-demo.vercel.app/
  - hits ⌘+k (or ctrl+k) and a search UI dialog appears.
  - Keyboard shortcut interface for your website that works with Vanilla JS, Vue, and React.
  - [You can now use the cmd-k / ctrl-k keyboard shortcut to navigate around GitHub without taking your hands off the keyboard](https://twitter.com/github/status/1453389061478043652)
    - IMO something like `^j` and `^k` for ⬇️ and ⬆️, respectively, would be great 
    - Ctrl K is a browser shortcut to the address bar, why hijack that?

- https://github.com/timc1/kbar
  - https://kbar.vercel.app/
  - React component to add a fast, portable, and extensible command + k (command palette) interface to your site.

- https://github.com/harshhhdev/kmenu
  - https://kmenu.hxrsh.in/
  - An animated and accessible command menu
# gesture
- https://github.com/rcbyr/keen-slider /4.1kStar/MIT/202212/ts/NoDeps/vanillajs
  - https://keen-slider.io/
  - Easily create sliders, carousels and much more.
  - Library Agnostic: Works well in JavaScript, TypeScript, React, Vue, Angular
  - Mobile First: Supports multi touch and is fully responsive

- https://github.com/Splidejs/splide /202210/ts/NoDeps
  - https://splidejs.com/
  - flexible and accessible slider/carousel written in TypeScript.

- https://github.com/FormidableLabs/nuka-carousel
  - https://formidable.com/open-source/nuka-carousel/
  - accessibility-first React carousel library with an easily customizable UI 
# media
- https://github.com/cookpete/react-player
  - React component for playing a variety of URLs, including file paths, YouTube, Facebook, Twitch, SoundCloud, Streamable, Vimeo, Wistia, Mixcloud, DailyMotion and Kaltura.
  - If you aren’t using React, you can still render a player using the standalone library
- https://github.com/Collaborne/media-player
  - A media player build in React on top of CookPete/react-player.
  - It supports the MUI theming and components and own functionality of the Picture-in-Picture and Fullscreen API
  - You can play both: audio and video files.
# highlight
- https://github.com/FormidableLabs/prism-react-renderer
  - Renders highlighted Prism output to React (+ theming & vendored Prism)
  - This library tokenises code using Prism and provides a small render-props-driven component to quickly render it out into React.
  - It's bundled with a modified version of Prism that won't pollute the global namespace and comes with a couple of common language syntaxes.
# embeddable-widget
- https://github.com/shobhitsharma/embedo
  - It adds a layer on top of third party embed APIs while ensuring best practices and native guidelines for each component. 
  - It takes cares of resizing the container, emitting necessary events and with support for native and external options to be pass along.
  - currently support Twitter URLs, YouTube videos URLs
- https://github.com/ritz078/embed-js /2017
  - A lightweight JavaScript plugin to embed emojis, media, maps, tweets, code and services.
  - creating a custom plugin is also few lines of code.

- https://github.com/seriousben/embeddable-react-widget
  - https://seriousben.github.io/embeddable-react-widget
  - Create an embedable js widget with react
- https://github.com/okor/justice /2015
  - Embeddable script for displaying web page performance metrics bar with a streaming FPS graph
- https://github.com/pipwerks/PDFObject
  - https://pdfobject.com/
  - A lightweight JavaScript utility for dynamically embedding PDFs in HTML documents.
- https://github.com/paulirish/lite-youtube-embed
  - https://paulirish.github.io/lite-youtube-embed/
  - Provide videos with a supercharged focus on visual performance. 
  - This custom element renders just like the real thing but approximately 224× faster.
- https://github.com/umap-project/umap
  - lets you create maps with OpenStreetMap layers in a minute and embed them in your site.
  - It uses django-leaflet-storage and Leaflet. Storage, built on top of Django and Leaflet.

- https://github.com/timekit-io/booking-js
  - version 2 of booking.js that supports the new projects model and uses App Widget Key for authentication
# more-components
- https://github.com/ashwinbabus/react_comments /js
  - https://hardcore-cray-d3cab1.netlify.app/
  - A simple react-app (no backend) that demonstrates nested comments feature.
  - 依赖只有redux；支持无限嵌套的评论组件
