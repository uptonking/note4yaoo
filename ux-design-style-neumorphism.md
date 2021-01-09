---
title: ux-design-style-neumorphism
tags: [design-style, neumorphism, ux]
created: '2021-01-09T16:10:51.118Z'
modified: '2021-01-09T16:12:16.423Z'
---

# ux-design-style-neumorphism

# guide

- pros
  - 视觉新鲜感
  - 按钮的层次感提升

- cons
  - 只能用浅白色背景，用其他颜色就难以突出浮雕效果，缺少对比度
  - 产生页面都是按钮的错觉
  - 每个元素都添加了投影，增加了一点渲染计算量

# discuss

- ## [2020年最火的设计趋势Neumorphism，快来了解下](https://www.jianshu.com/p/982fc75f858d)
- 最近流行起了一种叫 Neumorphism 的新风格，也有人称为 Soft UI，这是一种类似于浮雕的效果。
- 三星 Galaxy 系列的发布会宣传海报也使用了这种风格
- 最开始是一位来自乌克兰的设计师 Alexander Plyuto 发布了新的作品「Skeuomorph Mobile Banking」。
  - 这个作品自发布以来就获得了数十万浏览量，数千点赞数，热度持续飙升并登上 Popular 榜首。
  - 评论区就开始了这种风格的讨论，有的人说这是新的拟物风格（New Skeuomorphism）
- 来说说它的前身吧，也就是 Skeuomorphism（拟物）。
  - 这是最早被 Apple 提出的设计概念，就是在界面中模仿现实物体纹理材质的设计，目的是让人们在使用界面时习惯性地联想到现实物体的使用方式。
  - 拟物写实的设计风格曾经风靡全球，当时的 UI 设计师几乎都对拟物作品着迷。
  - 而在2013年的WWDC大会，苹果公司发布的iOS 7系统，系统UI使用更简洁的设计风格
    - 这场大会也使拟物风格逐渐过时，直到现在扁平风格的全面普及，拟物风格就再没有被广泛应用。
  - 从前几年的设计趋势可以看到，扁平风格作为更高效更简洁的风格被设计师推崇，再加上苹果系统 iOS 7 设计风格的面世和谷歌系统规范 Material Design 的普及，扁平风格在 UI 设计中一直占据重要位置。

- 设计
  - 了解一下这个风格的结构
  - 主要有三个样式组成，1 个背景+ 2 个投影。
    - 在这个基础上，通过改变颜色和大小参数来达到不同效果。
  - 我尝试着使用彩色去做这个效果，使用浅色背景时还是有效果的，但使用深一点的颜色时，问题就出现了，效果更像是外发光或者普通投影。
    - 这也可能是为什么大多数作品都采用比较素的颜色作为背景的原因。
- 浏览
  - 这个风格最大的问题就是缺少对比度。
  - 在色彩使用上比较克制，没有大面积的平铺颜色，仅在极少的位置进行色彩点缀，作用是吸引眼球。
  - 从众多设计师的作品可以看出，整体视觉是比较平的，缺少层次。
- 操作
  - 因为在界面中除了文字以外，几乎所有元素都应用了这种效果，导致界面所有内容看起来都是按钮的错觉。
  - 界面中的主要操作按钮也没有被重点提亮。正常态和点击态的对比度并没有拉开，容易造成状态混淆。
  - 点击欲望比较低，不利于引导用户进行下一步操作
- 动画
  - 跟拟物效果的动画有同样的问题，元素动画效果很难做得轻快，更适合按钮的使用
  - 由于视觉层级跟背景没有实际分离开，就像固定在了背景上一样，所以动画效果只要出现移动，就会让人觉得不合理，容易给人一种虫子在皮肤底下蠕动的感觉。
- 开发
  - 问题跟当年的拟物效果的实现类似，要实现这个风格，主要有两个方式
  - 切图
    - 对元素的每个状态（Normal、Hover、Pressed），设计师都需要分别提供一张切图，这个会导致资源库增加大量的图片
  - 代码实现
    - 这个风格的实现效果是对元素增加两个不同方向的投影，通过代码可以实现。
    - 但是需要开发对每个元素添加投影，样式代码增多，繁琐的工作量，开发也不会乐意。
    - 综合分析来看，这种设计风格目前在项目中推广和实现中并不合适。
- 也许扁平风格的多年流行后，设计潮流开始往回走，但并不是直接回到拟物风格，而是在效率和视觉效果中找一个平衡点。
  - 不论这个风格的对错，起码引起了设计师的注意，也激发了很多设计师的灵感，就像当年拟物风格和扁平风格的讨论一样，不分对错，
  - 设计师也不妨多留意一下这个风格，试着做一下效果图，或许会有新的发现。

# tools

- https://github.com/adamgiebl/neumorphism
  - https://neumorphism.io/
  - Generate CSS for your Neumorphism/Soft UI design

- https://github.com/matteobruni/object-gui
  - https://codepen.io/matteobruni/pen/oNxNvja
  - Object GUI is your fully customizable Javascript Object GUI Editor
  - 内置多种主题theming

# examples

- ref
  - https://github.com/mrsaeeddev/awesome-neumorphism

- https://github.com/ismail9k/neomorphism
  - https://ismail9k.github.io/neomorphism/
  - UI components library in the new neomorphism design style
- https://github.com/ajmalhassan/neumogram
  - A neumorphism based minimalist CSS framework.
- https://github.com/BrendaMichellle/NeumorphismExample
  - An example of neumorphism design with pure CSS
- https://github.com/daniruiz/skeuos-css
  - https://drasite.com/skeuos-css
  - CSS library that provides a set of predesigned elements 
  - It follows the latest skeuomorphic design trends, using bright colors and subtle shadows for some depth.
- https://github.com/we-mobius/mobius-ui
  - a neumorphism-style, utility-first UI framework

- https://github.com/themesberg/neumorphism-ui-bootstrap
  - https://demo.themesberg.com/neumorphism-ui/
  - Neumorphism UI has two versions, 
    - one of which is open sourced under the MIT License 
    - and a PRO version which is licensed under the Themesberg EULA license.

- https://github.com/yehuozhili/bigbear-ui
  - 基于React制作的拟物风格组件库
  - 新拟物风格早就存在，但是这种风格受限性很强，特别是对于背景色的要求，
    - 因为只有通过背景色制造的高光和加深才能制作出完美的凸起和凹下。
  - 我将阴影效果进行改造，做出个比较通用的效果，没有实现浅色和深色两种风格
- https://github.com/AKAspanion/ui-neumorphism
  - https://akaspanion.github.io/ui-neumorphism/
  - React component library designed on the "new skeuomorphism" or "neumorphism" UI/UX trend.
- https://github.com/mrsaeeddev/neumorphic-ui
  - https://neumorphic-ui.netlify.com/
  - A library of components based on the concept of neumorphism

 

- https://github.com/gsdeveloper/neudoro
  - A pomodoro clock with a neumorphism design
- https://github.com/RobertPujante/music_player
  - This is a music player with neumorphism user interface

# ref
