---
title: ux-usecase-pattern
tags: [pattern, pm, usecase, ux]
created: 2019-11-18T12:37:41.447Z
modified: 2021-01-01T20:10:11.503Z
---

# ux-usecase-pattern

# guide

# 界面类
- 数字展示不直观，可以考虑百分比进度条
- 类似medium和zhihu的图片先显示模糊轮廓再逐渐变清晰的效果如何实现
  - 基本思路：数据库存两张图片，然后用清晰替换模糊
- 缺少预览图时，自动生成文字logo图或[文字像素图](https://svelte.dev/contributors.jpg)
- 类似掘金个人资料修改界面的列表修改体验，没有excel的网格，很简洁
- div或一块组件不要全部为空，提示已完成或未开始更友好
- 少用context menu右键菜单，应用跨平台且体验尽量一致
  - 扩展鼠标的作用
  - 要做好触摸屏等无右键的适配
- ribbon menu vs text menu
  - good
    - 选项卡分类及图标，跨设备体验更友好，更一致
  - bad
    - text menu is easier to learn the shortcut
    - text menu tends to be more rigid and heirarchical
    - ribbon menu takes more space and hides deeper than text menu
    - 宽屏时代，侧边大量空白，占用了有限的垂直空间
    - 大量使用频率低的冗余菜单，从哪里进去找菜单不明确
    - 切换菜单不便
  - 建议
    - 竖向的ribbon menu
    - 自定义工具条
    - VS针对编程人员因为效率会使用快捷键，所以无需
    - Office面对的大部分是小白，所以需要简单易用的图形化操作界面。Adobe Creative Cloud系列软件面向专业设计人员，他们更倾向于使用快捷键完成操作
# 主题功能类
- bilibili
  - 回复内容可以包含类似 `01:30` 这样的时间数字，点击时间数字会直接跳转到视频指定位置
# 通用类
- 搜索记录多端同步：google、B站
# [Laws of UX](https://lawsofux.com/)

> a collection of best practices that designers can consider when building user interfaces.

## principle 定律原则

- [Pareto Principle](https://lawsofux.com/pareto-principle/)
- The Pareto principle states that, for many events, roughly 80% of the effects come from 20% of the causes.

- [Postel’s Law](https://lawsofux.com/postels-law/)
- Be liberal in what you accept, and conservative in what you send.
- Be empathetic to, flexible about, and tolerant of any of the various actions the user could take or any input they might provide.
- Anticipate virtually anything in terms of input, access, and capability while providing a reliable and accessible interface.
- The more we can anticipate and plan for in design, the more resilient the design will be.
- Accept variable input from users, translating that input to meet your requirements, defining boundaries for input, and providing clear feedback to the user.

- [Tesler’s Law](https://lawsofux.com/teslers-law/)
- Tesler’s Law, also known as The Law of Conservation of Complexity, states that for any system there is a certain amount of complexity which cannot be reduced.
- All processes have a core of complexity that cannot be designed away and therefore must be assumed by either the system or the user.
- Ensure as much as possible of the burden is lifted from users by dealing with inherent complexity during design and development.

- [Occam’s Razor](https://lawsofux.com/occams-razor/)
- Among competing hypotheses that predict equally well, the one with the fewest assumptions should be selected.

- [Doherty Threshold](https://lawsofux.com/doherty-threshold/)
- Productivity soars when a computer and its users interact at a pace (<400ms) that ensures that neither has to wait on the other.

## heuristic 启发式的

- [Aesthetic-Usability Effect](https://lawsofux.com/aesthetic-usability-effect/)
- Users often perceive aesthetically pleasing design as design that’s more usable.

- [Fitts’s Law](https://lawsofux.com/fittss-law/)
- The time to acquire a target is a function of the distance to and size of the target.
- Touch targets should be large enough for users to accurately select them.
- Touch targets should have ample spacing between them.
- Touch targets should be placed in areas of an interface that allow them to be easily acquired.

- [Goal-Gradient Effect](https://lawsofux.com/goal-gradient-effect/)
- The tendency to approach a goal increases with proximity to the goal.

- [Hick’s Law](https://lawsofux.com/hicks-law/)
- The time it takes to make a decision increases with the number and complexity of choices.
- Minimize choices when response times are critical to increase decision time.
- Break complex tasks into smaller steps in order to decrease cognitive load.
- Avoid overwhelming users by highlighting recommended options.
- Use progressive onboarding to minimize cognitive load for new users.

- [Jakob’s Law](https://lawsofux.com/jakobs-law/)
- Users spend most of their time on other sites. 
- This means that users prefer your site to work the same way as all the other sites they already know.
- Users will transfer expectations they have built around one familiar product to another that appears similar.

- [Miller’s Law](https://lawsofux.com/millers-law/)
- The average person can only keep 7 (plus or minus 2) items in their working memory.
- Don’t use the “magical number seven” to justify unnecessary design limitations.
- Organize content into smaller chunks to help users process, understand, and memorize easily.

- [Parkinson’s Law](https://lawsofux.com/parkinsons-law/)
- Any task will inflate(膨胀；鼓吹；涨价) until all of the available time is spent.

## gestalt 格式塔/一个体系的一系列思想

- [Law of Common Region](https://lawsofux.com/law-of-common-region/)
- Elements tend to be perceived into groups if they are sharing an area with a clearly defined boundary.
- Adding a border around an element or group of elements is an easy way to create common region.
- Common region can be created by defining a background behind an element or group of elements.

- [Law of Proximity](https://lawsofux.com/law-of-proximity/)
- Objects that are near, or proximate to each other, tend to be grouped together.
- Proximity helps to establish a relationship with nearby objects.

- [Law of Similarity](https://lawsofux.com/law-of-similarity/)
- The human eye tends to perceive similar elements in a design as a complete picture, shape, or group, even if those elements are separated.
- Elements that are visually similar will be perceived as related.
- Color, shape, and size, orientation and movement can signal that elements belong to the same group and likely share a common meaning or functionality.
- Ensure that links and navigation systems are visually differentiated from normal text elements.

- [Law of Prägnanz](https://lawsofux.com/law-of-pr%C3%A4gnanz/)
- People will perceive and interpret ambiguous or complex images as the simplest form possible, because it is the interpretation that requires the least cognitive effort of us.
- The human eye likes to find simplicity and order in complex shapes because it prevents us from becoming overwhelmed with information.
- Research confirms that people are better able to visually process and remember simple figures than complex figures.

- [Law of Uniform Connectedness](https://lawsofux.com/law-of-uniform-connectedness/)
- Elements that are visually connected are perceived as more related than elements with no connection.
- Group functions of a similar nature so they are visually connected via colors, lines, frames, or other shapes.
- Alternately, you can use a tangible(可触摸的，可感知的；有形存在的) connecting reference (line, arrow, etc) from one element to the next to also create a visual connection.
- Use uniform connectedness to show context or to emphasize the relationship between similar items.

## cognitive bias 认知偏向/偏好

- [Peak-End Rule](https://lawsofux.com/peak-end-rule/)
- People judge an experience largely based on how they felt at its peak and at its end, rather than the total sum or average of every moment of the experience.
- Pay close attention to the most intense points and the final moments (the “end”) of the user journey.
- Identify the moments when your product is most helpful, valuable, or entertaining and design to delight the end user.
- Remember that people recall negative experiences more vividly than positive ones.

- [Serial Position Effect](https://lawsofux.com/serial-position-effect/)
- Users have a propensity to best remember the first and last items in a series.
- Placing the least important items in the middle of lists can be helpful because these items tend to be stored less frequently in long-term and working memory.
- Positioning key actions on the far left and right within elements such as navigation can increase memorization.

- [Von Restorff Effect](https://lawsofux.com/von-restorff-effect/)
- The Von Restorff effect, also known as The Isolation Effect, predicts that when multiple similar objects are present, the one that differs from the rest is most likely to be remembered.
- Make important information or key actions visually distinctive.

- [Zeigarnik Effect](https://lawsofux.com/zeigarnik-effect/)
- People remember uncompleted or interrupted tasks better than completed tasks.
- Invite content discovery by providing clear signifiers of additional content.
- Providing artificial progress towards a goal will help to ensure users are more likely to have the motivation to complete that task.
- Provide a clear indication of progress in order to motivate users to complete tasks.
