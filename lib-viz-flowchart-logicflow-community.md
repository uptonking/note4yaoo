---
title: lib-viz-flowchart-logicflow-community
tags: [community, logicflow]
created: 2024-05-14T19:38:16.523Z
modified: 2024-05-14T19:38:26.376Z
---

# lib-viz-flowchart-logicflow-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-not-yet
- ## 

- ## 

- ## [LogicFlow的浏览器兼容性 _202305](https://github.com/didi/LogicFlow/discussions/1143)
- 目前我们在开发后，只测试了LogicFlow在chrome中的表现效果，不排除在其他浏览器上存在问题。目前我们已知的兼容性信息：
  - 在safari浏览器中，HTML节点可能会出现无法拖动的问题。
  - LogicFlow目前不支持移动端的touch事件，所以会出现无法移动画布、节点。

# discuss-animation
- ## 

- ## 

- ## [动画（animation）明明设置为了只执行一次，却会偶发的再次被触发 _202402](https://github.com/didi/LogicFlow/discussions/1492)
- 这是两种不同的情况。在logicflow中，假如我们拖出两个不同类型的节点A和B，这时在DOM里AB同级，且顺序为AB，在点击A节点之后，A会被重新渲染，顺序变为BA，这是logicflow的渲染机制导致的
  - 在这里，emerge动画是依照时间轴执行的，节点被「重新渲染」，时间轴重置了，动画自然也会重新执行
  - 但是为节点添加class，并不会让对应的时间轴重置

# discuss
- ## 

- ## 

- ## 

- ## 
