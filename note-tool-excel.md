---
tags: [table, tool]
title: note-tool-excel
created: '2019-08-01T16:03:46.394Z'
modified: '2019-10-24T14:15:27.369Z'
---

# note-tool-excel

## 问题

- 支持存储和分析的数据量有限  
    - 2007格式的excel支持16,384 columns and 1,048,476 rows
- 不支持并行修改
- 打开大文件速度慢
- 输入数据费时
- Excel撤销和恢复是全局的。在多个工作簿、工作表中的操作相互干扰。
    - 例如在a中删除操作，b中输入操作。在a中撤销必须先清除b中的操作。
- Excle经常出现空白列。例如，从A表复制一列到一个新表B中，本来表A只有5行，可到了B表中
- 数据有宏和非宏两种编辑状态，非宏时记录操作结果
- 表格太多时，搜索困难
    - 通过数据库，提供单元格粒度的搜索
- 统计挖掘能力不足，比不上spss, sas
    - excel的定位本身就是入门级的工具，不是专业全面的工具

## faq

- 多人协作冲突解决
    - OT  http://www3.ntu.edu.sg/home/czsun/projects/otfaq/

### 特定需求
- 一批数据制作多表时，各表有同样的数据，存在冗余
- 横向排版不能分栏
- 不统计则不能分组显示

## 优点
- 简单清晰
- 使用广泛
- 数据和样式保存在一个文件
- 可视化的数据编辑和样式编辑

## feature

- tip of the day
    - 最常用和最实用的表格操作技巧

## excel 格式说明

- 默认情况下，Excel for Windows使用1900日期系统，而Excel for Macintosh使用1904日期系统，Excel for Windows 也支持使用1904时间系统。
    - https://support.microsoft.com/zh-cn/help/214330/differences-between-the-1900-and-the-1904-date-system-in-excel
    - 1900日期系统有一小错误，即其包含了1900年2月29日（1900年不是闰年）所对应的序列值，早期 Macintosh 计算机的设计，不支持 1904 年 1 月 1 日之前的日期，是为了防止与 1900 年不是闰年相关的问题
    - 如果两个工作簿使用不同的日期系统，则可能会遇到问题，当链接或复制工作簿之间的日期。具体而言，日期会移动四年零一天。
- 存储方式  
    - xls采用的是一种名为BIFF8(BinaryInterchangeFileFormat)的文件格式
    - xlsx则是采用OOXML(Office open Xml)的格式存储数据

### xlsx格式的Excel
- .xlsx其实是个压缩包，解压后目录结构如下
    - `_rels/`
        - `_rels`：记录描述excel整体的元信息文件的位置关系，包括app.xml,core.xml,workbook.xml
    - `docProps/`
        - `app.xml`：记录各sheet的heading和title名称
        - `core.xml`：记录excel的创建和修改时间
        - `custom.xml`：记录自定义属性信息，如KSOProductBuildVer
    - `xl/`
        - `_rels/`
            - `workbook.xml.rels`：记录sheet数据和样式文件的位置关系，包括sheet1.xml,sharedStrings.xml,styles.xml,theme1.xml   
        - `theme/`
            - `theme1.xml`：记录excel使用的主题样式，包括字体、颜色、格式
        - `worksheets/`
            - `sheet1.xml`：记录sheet的元信息和各单元格值的索引号，元信息包括sheet中数据的行列范围、列宽、行列样式、页边距
        - `sharedStrings.xml`：记录excel所有单元格的字符串的值
        - `styles.xml`：记录excel整体样式和各单元格样式
        - `workbook.xml`：记录excel所有sheet的name和sheetId，还有默认显示宽高
    - `[Content_Types].xml`：记录其他各文件所对应的openxmlformats的具体类型ContentType


