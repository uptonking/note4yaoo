---
tags: [pm, yaoo]
title: note-pm-dataplayer
created: '2019-05-15T03:31:43.740Z'
modified: '2019-08-21T14:09:10.312Z'
---

# note-pm-dataplayer

## target

## todo

## design
- dashboard = list + chart

## 1.datable
- excelbox + handsontable + swing/javafx/java-cef

### 功能设计
- 广义的表格制作器
    - 类似表格类网页制作
- 表格数据的定位
    - 行业大类+标签小类，标签尽可能扁平化
    - 用户名+表格数据名
    - 一套表格原始数据 > 衍生透视表 > 数据分析报告  <==>  数据立方
- 表格元数据类
    - 可选择默认显示3表头+2行数据或者表格缩略图
- 表格操作类
    - 两表对比视图，相同部分灰色
- 冲突处理
   - 如何处理编辑冲突，类似维基百科的热门条目
        - 通过缩小编辑范围避免冲突，开始编辑时必须指定编辑类型，编辑一行/指定行范围/全部
            - 若编辑范围不冲突，则自动合并多人修改后的内容
            - 引入标记【冲突热点】【中立客观】
            - 编辑冲突费时费感情，限制每人热点条目的编辑次数和门槛，鼓励编辑冷门条目
            - 管理员直接处理编辑战，处理原则是回退不过三的3RR
                - 该原则是指编辑者在24小时之内，不得对同一页面进行超过三次的回退动作。回退是指撤销另一编者的编辑动作，违反者可能会被封禁
            - 预防恶意破坏，删除全部的内容的编辑需要24小时生效
        - 大范围先提交先确认的原则，修改内容较少的或后提交的到生效需要前一位作者1小时内的合并
            - 若多人修改内容都很大，则到生效的冷却时间延长12小时，分别发给各人比较及确定版本
        - 通过历史版本支持回退3个最近版本及3个stable版本，默认保存最原始的版本
            - 每人重复编辑需要间隔10分钟
    - 政治冲突
        - 网站本身保持中立客观，不参与政治话题
        - 对政治敏感内容进行国际化处理，同一页面对不同地区提供不同内容
    - 移动冲突
        - 停止移动页面，单独作为表格
    - 版权冲突
        - 参考维基条目所有权 https://zh.wikipedia.org/wiki/Wikipedia:%E6%9D%A1%E7%9B%AE%E6%89%80%E6%9C%89%E6%9D%83
        - 维基百科所有内容是协同编辑的。无论一个编者再怎么熟练，或在社群的地位有多高，都无权声称对条目的所有权
        - 一旦将自己的作品放上维基百科，就不能阻止任何人修改您编写的内容。每个编辑页面已清楚表明了：维基百科内容均容许他人编辑、使用和重制
            - 好处是其他人能扩展数据及想法，也能稍微限制广告
        - 不鼓励条目签名或编辑修改签名
        - 不鼓励用于扭曲事实和广告宣传的独占条目
    - 榜单类数据的交流冲突    
        - 交流讨论统一在社区进行，数据展示页面只展示高质量评论
    - 疑难冲突
        - 预谋的恶意破坏，由仲裁会员会或交流社区裁定
- 政治相关处理
    - 新闻
    - 地区

### extension
- 投票活动
- 维基百科表格内容提取导出
- toc内容提取导出

### feature
- wps sheet复制一块区域的数据粘贴时，没有样式

## 2.data-chart
- d3

## 3.data-map
- leaflet/mapboxgl

## 4.data-etl
- datax

## 5.data-ecosystem

### extensions
- h5ds

### open api / datalking
- dataverse 

#### datapi

- 榜单类数据容易引战的问题
    - 关闭评论？

##### 文档类型产品
- 基本功能：标题、列表、代码块、图片、链接、字体、表格、函数、toc
- Markdown (github 56,333 results)
    - https://www.appinn.com/markdown/
        - 功能：标题、列表、代码块、图片、链接、字体
    - [GitHub Flavored Markdown Spec](https://github.github.com/gfm/)
        - Syntax highlighting
        - Task Lists(checkbox)
        - Tables
        - Issue references & commit references
        - Username @mentions
        - Automatic linking for URLs
        - Strikethrough(crossed out) text
        - [github emoji](https://github.com/ikatyang/emoji-cheat-sheet/blob/master/README.md)
        - https://guides.github.com/features/mastering-markdown/
- reStructuredText (github 600 results)
    - https://docutils-zh-cn.readthedocs.io/zh_CN/latest/ref/rst/restructuredtext.html
    - 功能：基本功能、表格、注释、目录索引、脚注、替换、函数、单位
- AsciiDoc (github 1,846 results)
    - https://asciidoctor.cn/docs/asciidoc-syntax-quick-reference/
    - https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/
    - 功能：基本功能、表格、注释、目录索引、脚注、替换、UI Macros


