---
title: lib-excel-luckysheet-dev
tags: [excel, grid, lib, luckysheet]
created: 2020-10-19T16:48:46.206Z
modified: 2022-08-21T09:57:46.814Z
---

# lib-excel-luckysheet-dev

# guide

- pros
  - 支持插件，如excel导入导出、chartMix

- cons
  - 代码混乱

- resources
  - [Luckysheet 兔小巢支持论坛](https://support.qq.com/products/288322/)
  - [梦数科技开源平台](http://www.lashuju.com/)

## features

- 表格设置
  - 冻结行列、合并单元格、
  - 筛选、排序、查询、
  - 条件格式、批注; 
- 支持数据分析
  - 包括透视表、分列、矩阵操作、
  - 内置385个计算函数; 
- 复制为json数据
  - excel与luckysheet之间数据的复制粘贴; 
- 共享编辑
- 增强功能
  - 支持一键截图
  - 如excel导入、插入图片、数据验证、行内样式
- 支持移动端查看

- 格式设置
  - 样式 (修改字体样式，字号，颜色或者其他通用的样式)
  - 条件格式 (突出显示所关注的单元格或单元格区域；强调异常值；使用数据栏、色阶和图标集（与数据中的特定变体对应）直观地显示数据)
  - 文本对齐及旋转
  - 支持文本的截断、溢出、自动换行
  - 数据类型
  - 货币, 百分比, 数字, 日期
  - Custom，和excel保持一致

- 单元格
  - 拖拽选取来修改单元格 (对选区进行操作，可以拖动四边来移动选区，也可以在右下角对选区进行下拉填充操作)
  - 选取下拉填充 (对于一个1, 2, 3, 4, 5的序列，将会按照间隔为1进行下拉填充，而对2, 4, 6, 8将会以2作为间隔。支持等差数列，等比数列，日期，周，天，月，年，中文数字填充)
  - 自动填充选项 (下拉填充后，会出现填充选项的菜单，支持选择复制，序列，仅格式，只填充格式，天，月，年的选择)
  - 多选区操作 (可以按住Ctrl键进行单元格多选操作，支持多选区的复制粘贴)
  - 查找和替换 (对内容进行查找替换，支持正则表达式，整词，大小写敏感)
  - 定位 (可以根据单元格的数据类型进行自动定位并选中，选中后可以批量进行格式等操作)
  - 合并单元格

- 行和列操作
  - 隐藏，插入，删除行或列
  - 冻结行或列 (支持冻结首行和首列，冻结到选区，冻结调节杆可以进行拖动操作)
  - 文本分列 (可以把文本根据不同符号进行拆分，和excel的分列功能类似)

- 操作体验
  - 撤销/重做
  - 复制/粘贴/剪切操作 (支持luckysheet到excel和excel到luckysheet带格式的互相拷贝)
  - 快捷键支持 (快捷键操作保持与excel一致，如果有不同或者缺失请反馈给我们)
  - 格式刷 (与google sheet类似)
  - 任意选区拖拽 (选择单元格，输入公式，插入图表，会与选区相关，可以通过任意拖动和放大缩小选区来改变与之关联的参数)

- 公式和函数
  - 内置公式
    - 数学 (SUMIFS, AVERAGEIFS, SUMIF, SUM, etc.)
    - 文本 (CONCATENATE, REGEXMATCH, MID)
    - 日期 (DATEVALUE, DATEDIF, NOW, WEEKDAY, etc.)
    - 财务 (PV, FV, IRR, NPV, etc.)
    - 逻辑 (IF, AND, OR, IFERROR, etc.)
    - 查找和引用 (VLOOKUP, HLOOkUP, INDIRECT, OFFSET, etc.)
    - 动态数组 (Excel2019新函数，SORT,FILTER,UNIQUE,RANDARRAY,SEQUENCE)
  - 公式支持数组 (={1, 2, 3, 4, 5, 6}, Crtl+Shift+Enter)
  - 远程公式 (DM_TEXT_TFIDF, DM_TEXT_TEXTRANK)
  - 自定义公式 (根据身份证识别年龄，性别，生日，省份，城市等)

- 表格操作
  - 筛选 (支持颜色、数字、字符、日期的筛选)
  - 排序 (同时加入多个字段进行排序)

- 数据透视表
  - 字段拖拽 (操作方式与excel类似，拖动字段到行、列、数值、筛选等4个区域)
  - 聚合方式 (支持汇总、计数、去重计数、平均、最大、最小、中位数、协方差、标准差、方差等计算)
  - 筛选数据 (可对字段进行筛选后再进行汇总)
  - 数据透视表下钻 (双击数据透视表中的数据，可以下钻查看到明细，操作方式与excel一致)
  - 根据数据透视表新建图表 (数据透视表产生的数据也可以进行图表的制作)

- 图表
  - 支持的图表类型 (目前折线图、柱状图)
  - 关于图表插件 (图表使用了一个中间插件ChartMix)
  - Sparklines小图 (以公式的形式进行设置和展示)

- 分享及写作
  - 评论 (评论的删除、添加、修改、隐藏)
  - 共享编辑 (支持多用户共享编辑，内置API)

- LuckySheet专有
  - 矩阵计算 (通过右键菜单进行支持：对选区内的数据进行转置、旋转、数值计算)
  - 截图 (把选区的内容进行截图展示)
  - 复制到其他格式 (右键菜单的"复制为", 支持复制为json、array、对角线数据、去重等)
  - EXCEL, CSV, TXT 导入及导出 (专为luckysheet打造的导入导出插件，支持密码、水印、公式等的本地导入导出)
  - 插入图片和svg形状 (支持JPG, PNG, SVG, Pen tool的插入、修改和删除，并且随表格的变动而产生变化)
  - 数据验证(表单功能) (支持Checkbox, drop-down list, datePicker)
  - 单元格内多样式 (Alt+Enter单元格内换行、上标、下标、单元格内科定义每个文字的不同样式)

- 未来开发计划
  - 打印及设置 (像excel一样进行打印设置，并导出为图片或者PDF)
  - 树形菜单 (类似excel中的分级显示（分组）)
  - 表格新功能 (类似excel中表格的筛选器和切片器)
  - 文档 (完善文档和API)

## ui结构层次

- `<div id="luckysheet" style="margin:0px;padding:0px;position:absolute;width:100%;height:100%;left: 0px;top: 0px;"></div>`
- `<div id="luckysheet-sheettable_0" class="luckysheet-cell-sheettable" style="height: 936px; width: 2072px; cursor: default;"></div>`

```CSS
.luckysheet-cell-sheettable {
  position: relative;
  text-align: left;
  font-size: 11pt;
  color: #000;
  text-decoration: none;
}

.luckysheet * {
  box-sizing: initial;
  outline: 0;
}
```

# blogging

## [LuckySheet源码分析目录_舟翁_202011](https://blog.csdn.net/u010593516/article/details/109604358)

1. 源代码项目结构
2. core.js源码分析
3. 函数实现原理
4. 页面加载过程
5. 主界面绘制draw.js
6. 界面刷新策略fresh.js

## [MiniSheet开发记录目录_舟翁_202102](https://blog.csdn.net/u010593516/article/details/113743472)

- https://gitee.com/zhouweng/mini_sheet

Day 1 为什么会有mini_sheet
Day 2 Win10系统配置开发环境
Day 3 如何看源码学习
Day 4 编译工具说明
Day 5 第一个最小化系统
Day 6 让表格动起来
Day 7 选择一个单元格
Day 8 双击单元格编辑
Day 9 编辑单元格回写内存
Day10 点亮单元格行列标题
Day11 拖动选择单元格区域
Day12 从excel文件复制粘贴
Day13 鼠标右键菜单复制粘贴
Day14 在页面顶部显示工具条
Day15 一次规模比较大的重构
Day16 单元格样式(背景色/下划线/删除线等)
Day17 工具条设置单元格样式
Day18 工具条设置字体大小
Day19 如何做合并单元格
Day20 左右对齐、上下对齐
Day21 工具条设置单元格颜色
【完结篇】Day22 行高和列宽的设置
