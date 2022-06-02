---
title: web-ui-comp-design-usecase
tags: [components, design-style, usecase]
created: '2021-04-11T10:23:39.124Z'
modified: '2021-04-11T17:38:41.941Z'
---

# web-ui-comp-design-usecase

# b2b vs b2c

- 企业应用的特点
  - 对responsive ui要求低，多是桌面操作，移动端以浏览为主
  - 对高并发的要求较低，多是内部管理或控制台
  - 对兼容性、稳定性、容错性要求高，对新技术要求低
  - 好招人：如java后端好招、node后端难招

# text-editor

- toc 目录

# code-editor

- 行号显示
- 在行号位置能折叠代码块中的方法、类、json等
- 语法高亮
- 顶部显示鼠标所在位置的面包屑路径


- [radix-ui Code blocks, but better](https://ped.ro/writing/code-blocks-but-better)
# mobile-first 移动优先

- 默认纵向布局显示
  - 每个组件能够在大屏幕横向展示、在小屏幕纵向展示，最好能根据屏幕大小/方向自动切换
- 尽量不用水平滚动条
  - 水平滚动条不适合移动端下滑的操作
  - 水平和竖直滚动条在页面中间**都**比较刺眼
- media query多用min-width
- mobile event
  - no hover
  - less drag
  - more touch

- mobile-ime-输入法
  - 会自动弹出来挡住半屏

- ref
  - ios
  - android
  - miui

- examples
  - https://generative.parts/responsive

- ## Tinkering with layout components. How about `<Stack axis="x|y" space={…}>` where the axis should default to "y" for a mobile-first experience.
- https://twitter.com/kripod97/status/1263393651000049665
  - Responsive props could also be supported, e.g. to make the component expand horizontally on tablets and up
  - With this pattern, there would be no need for a separate `<Inline>/<HStack> and <Stack>/<VStack>` component.
  - I’m wondering if there are any valid use-cases for `flex-direction: *-reverse`. Would love to hear the opinion of accessibility experts about that.
  - stacks should not wrap at any time. A separate `<Cluster>` component could fulfill that use-case, serving as a horizontal stack which wraps automatically on overflow.
- I usually go for `inline` flag as it’s always about two possible directions
  - That’s also fine, but I don’t see how it could support responsive props.
  - Same approach as yours,  `inline={{md: true}}` or what others do with arrays: `inline=[false, true, true]`
- What about HStack and VStack like SwiftUI?
  - I tried those concepts at first and currently building a project with them. 
  - However, I feel like they’re too rigid for responsiveness while being a bit redundant, too.
  - You need to switch the axis dynamically/responsively?
  - Yeah, exactly. The `axis` provides that functionality, being a responsive prop.

- ## When designing websites these days, how do you start working on your mock-ups? Mobile first, then desktop? 
- https://twitter.com/smashingmag/status/1205455057539477504
- Always component-level; always mobile-first. 
  - I've taken the habit of creating a pattern library of all components even if it's not "officially" part of the project; it makes cross-browser testing easier, too.
- Depends on the analytics, if most visits are mobile I'll start with mobile. 
  - Projects I work on are generally desktop-heavy though, so rarely happens.
- Same as some others have said, I create section by section, and for each one I have an idea how it will look at each size before I begin.
- We start with desktop/laptop/tablet, with "mobile-in-mind" rather than mobile-first.
- I prefer mobile-first but increasingly I am starting with desktop and then refactoring my stylesheet for mobile-first styles. It is just easier to work things out when I only have desktop mockups.
- Sadly, mobile layouts don't have the same "Wow" factor as desktop. Client's often don't understand the concept of scrolling. Therefore a lot of cases, I have to start with desktop so the client understands the product, then go to mobile (time permitting)
- I’ve done all of the above, but I’ve returned to Desktop-first, then mobile. It’s been more efficient for me to start with desktop and then to simplify it for mobile.
- I use a different approach, I design for the highest available resolution (7680 by 4320 pixels) and let the presentation scale down to any screen display device.

- ## When building a CSS component mobile-first, do you use min-width or max-width mostly 
- https://twitter.com/smashingmag/status/902839994880053248
- I usually have only min-widths for mobile first. components tend to get more complex on bigger screens, so fewer overrides this way.
- Mobile-first means it starts changing behavior as the screen gets bigger (technically speaking) so I use min-width.
- min-width. I start with default styles and as the viewport gets wider, additional styles can be applied. This keeps properties to a minimum.
- Min-width. With HTTP/2, split CSS to files by min-width, use mq in `<link>` ➡️ browser will prioritize download
- Min-widths, then group and sort them with mqpacker @PostCSS plugin
- I can't stand building mobile first. I find it much easier building the most complex layout first then simplifying it for mobile.
- When a property changes over the different breakpoints we were explicit declare it for every breakpoint. So min and max every mediaquery.
- Way easier to min-width and add on flex/grid props then to max-width and remove them. Also using flex/calc to avoid MQs altogether is best!

# discuss

- ## "Avoid global state — Colocate with Uncontrolled Compound Components" This might help shed light on some of the design decisions made for the @radix_ui Primitive APIs.
- https://twitter.com/jjenzz/status/1384158245556690945
