---
title: job-coding-faq-open
tags: [coding, faq, job]
created: 2021-09-22T16:30:42.668Z
modified: 2021-09-22T16:31:13.438Z
---

# job-coding-faq-open

# guide

# open
- 判断DOM标签的合法性，标签的闭合，span里面不能有div，写一个匹配DOM标签的正则
# 跨文件排序的方法
- 一台2G内存的电脑，硬盘里有10个1G的文件，每个文件里都是乱序的数值，通过这台电脑对这10个1G的文件跨文件进行数值大小的排序。

- 每次对每个文件分配排序，比如快排，因为每个文件都是1g，所以2g内存够了，排好后重写写入覆盖当前文件
- 然后对10个排好序的文件，做归并排序
- 每次只能顺序读每个文件的一部分（防止10个文件超出内存2G), 只有当文件内容用完了，才读取文件下一段。
- 每次归并，取出数据都要顺序存到磁盘上

- ref
  - https://leetcode-cn.com/circle/discuss/PIJQ1i/
# frameworks
-  Vue自定义指令懒加载
