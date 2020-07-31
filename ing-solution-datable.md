---
title: ing-solution-datable
tags: [pm, solution, table]
created: '2019-05-15T03:30:55.244Z'
modified: '2020-07-14T10:25:13.843Z'
---

# ing-solution-datable

- A handy/efficient data table to pivot your data
  - 用更加灵活的表格来透视数据

## table-xp

- animation
  - 类似包含gif图的网页，可预设数据滚动动画，非常interactive
- features
  - 链接预览标题、图片
  - 类似ide的同时打开多标签页并编辑
  - 记住不同tab的上次编辑位置
  - 单列选择
- globalOptions
  - defaultViewMode/defaultEditMode
  - indentationSpace

## grape-trellis

- kbd键盘字母特殊显示

## Excelbox

- A tool for fast pivoting data list in memory. 快速进行数据分组聚合的工具库

## todo

## reference

### jackson-core & jackson-databind

- 通过JsonFactory创建parser和generator
  - `createParser(InputStream in)`
  - The input stream will not be owned by the parser
  - 解析器不直接拥有stream，通过拥有IOContext来操作流
