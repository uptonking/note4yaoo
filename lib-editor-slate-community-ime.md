---
title: lib-editor-slate-community-ime
tags: [community, ime, slate-editor]
created: 2023-03-17T21:19:30.341Z
modified: 2023-03-17T21:19:43.592Z
---

# lib-editor-slate-community-ime

# guide

- slate的Editable组件存在会在model数据更新前渲染的问题
  - 在onCompositionStart中setIsComposing导致渲染
  - 在onCompositionEnd中setIsComposing导致渲染，此时slate的model未更新其他组件不会更新，但渲染时renderElements却能拿到最新输入值，就导致了异常

- 可以在应用层的其他组件手动遍历model数据计算来获取最新值
  - 但这可能导致应用层存在过多重复计算，因为其他组件从context获取的editor更新时又会计算一遍
# discuss
- ## 

- ## 

- ## 

- ## 
