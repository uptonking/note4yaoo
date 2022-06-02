---
title: pm-office-siyuan-xp
tags: [office, pm, siyuan, xp]
created: '2022-06-01T18:55:16.290Z'
modified: '2022-06-01T18:55:39.088Z'
---

# pm-office-siyuan-xp


# guide


# changelog

- [Use Protyle instead of Vditor for the editor__202104](https://github.com/siyuan-note/siyuan/issues/1981)
  - Protyle is a brand new editor for SiYuan.


- [1.2.5 文件 (夹) 名称 ID 化，是否与本地化的初衷渐行渐远？__202109](https://ld246.com/article/1629599006639)
  - 思源不是文本编辑器，而是知识管理系统
  - 子文档形式比文件夹形式效率更高，能够充分利用文档树的空间
  - 通过文件实现易变数据的互操作性是一个糟糕和错误的方向，因为多个进程各自直接读写易变文件有概率会导致数据损坏。概括一点讲就是试图通过共享文件、共享内存来实现互操作性的方案都存在一致性问题，正确的方案是通过 API 进行交互，各进程内自己保证一致性
  - 使用人类可读的文本在跨系统平台时存在大小写问题，比如 Linux 上允许同时存在 SiYuan 和 siyuan 文件，但是 Windows 上则不允许，该情况一旦发生数据就可能会被损坏

- 如果确实对 id 和文件名的对应关系有需求，在 sy 文件里面有，随便找个 json 解析工具一提取就搞定了，只是稍微费一点功夫而已。
