---
title: yaooking-resume-v202508
created: 2025-07-15T16:17:50.422Z
modified: 2025-07-15T16:17:50.422Z
---

# 金 瑶

## 个人信息

* 性 别：男 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &nbsp; &nbsp; &nbsp; 年 龄：32  
* 专 业：测绘工程 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; 岗 位：前端工程师 或 Nodejs全栈
* 手 机：15527519292  &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &nbsp; 邮 箱：jinyaoo86@outlook.com  
* 其 他：[个人网站](https://uptonking.github.io/yaoo-showcase-profile-v202404/) &emsp; [Github](https://github.com/uptonking)

## 技术栈

* 熟练掌握 React/Redux/Mobx/JS/CSS/HTML 的原理和生态，能够快速开发组件库、Web/H5应用，了解Nextjs、Vue的开发
* 熟悉 ProseMirror/Tiptap/CodeMirror/Slate/Quill 的原理和富文本编辑器的研发，了解基于OT/CRDT的协作算法及开发
* 熟悉 Nodejs 和 PostgreSQL/SQLite 的CRUD，了解Strapi CMS的原理，能够快速开发内容管理、用户权限、低代码平台
* 熟练使用 JavaScript/TypeScript，了解 Java、Python
* 对编辑器和表格领域的技术仍具有很高的热情，还会继续投入精力

## 工作及教育经历

* 深圳至简天成 云端AI Coding产品Clacky  &emsp; &emsp; &nbsp; 2024.05~2025.08 &emsp; 全栈工程师(偏前端) 
* 个人项目 CRDT/Noseditor编辑器/StrapiCMS &nbsp; &nbsp; 2022.09~2024.04 &emsp; 全栈工程师 
* 杭州投光编辑器 Affine协同办公 &emsp; &emsp; &emsp; &emsp; &nbsp; &nbsp; &nbsp; 2021.10~2022.07 &emsp; 全栈工程师(偏前端) 
* 个人项目 React-Dashboard/KnowledgeBase  &emsp; 2019.12~2021.08 &emsp; 前端工程师(偏React) 
* 湖北地信科技 实习+工作 &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &nbsp; 2015.09~2019.10 &emsp; GIS地图研发工程师 
* 武汉大学 硕士&emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &nbsp; 2015.09~2017.07 &emsp; 测绘工程 
* 武汉大学 本科&emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &nbsp; 2011.09~2015.07 &emsp; 资源环境与城乡规划管理 

## 项目经历

1. IDE SDK的维护与云端AI Coding产品Clacky的开发 - 2024.05~2025.08
   - 结合AI Coding的业务需求，开发自定义插件扩展CodeMirror代码编辑器的能力，主要是Diff视图与代码内的嵌入式聊天框，基本达到了竞品Cursor的用户体验
   - 扩展IDE Server的能力，基于CodeMirror的类似OT的算法，实现了AI流式写代码和AI全文写代码2种方案，满足不同的业务场景。此外，还对接LSP Server实现了语法跳转、Hover卡片等功能来增强IDE的基础能力。

2. 基于Strapi CMS的内容管理系统 - 2023.12~2024.04
   - 日常业务开发需要一个可复用、可扩展的脚手架，提供开箱即用的内容管理、用户权限、api自动生成等功能
   - 基于Strapi CMS的插件系统，使用自研Noseditor/Nosontable编辑器和表格扩展了Strapi的自定义字段，还实现了版本历史和撤销回退，可作为低代码平台的基础

3. Noseditor Notion-like 块级编辑器 - 2023.02~2023.09
   - 富文本编辑器是使用广泛、可复用性高的模块，前端领域缺少一个开源的支持拖拽的Notion-like编辑器
   - 基于Slate实现了block style可拖拽的编辑器，还基于yjs的CRDT数据结构实现了部分协同功能

4. 投光编辑器的维护和Affine编辑器的研发 - 2021.10~2022.07
   - 维护基于CKEditor的投光编辑器，开发学术版相关功能，包括数学公式、BibTeX参考文献等，并交付业务项目
   - 参与新产品Affine编辑器的研发，负责富文本模块，开发了图片、工具条、评论相关功能，交付demo帮助公司拿到融资

5. Materials 资料库/知识库 - 2021.05~2021.09 
   * 基于Markdown/MDX的在线文档资料库系统，对标语雀、飞书知识库
   * 基于ProseMirror实现了文档查看器，为实现文档编辑做好了准备，文档渲染到DOM后，会在右侧自动创建toc标题目录，监听滚动事件，在右侧高亮当前标题

6. Dashboard 仪表板 - 2021.02~2021.06
   * 基于React实现的轻量、可定制的纯前端控制台/仪表板，对标 Ant Design Pro
   * 为了快速添加页面，实现了基于配置文件的动态路由，结合React的懒加载和代码拆分，同时也提高了首屏加载速度

7. 其他项目或玩具(详见 GitHub)
   * 基于CRDT的可协作Todo-list小玩具 (2022.09~2022.12): 基于G-Set和LWW-Map实现了数据的CRUD和同步逻辑，可作为协作系统的基础
   * Prospect Garden Design 组件库 (2020.09～2021.01): themeable, design-token based design system
   * 其他玩具：tanstack-table，ag-grid, handsontable, electron, echarts

## 项目展示

- [Noseditor Notion-like 块级编辑器 (在线预览)](https://uptonking.github.io/yaoo-showcase-noseditor-slate/)
- [基于Strapi CMS的内容管理系统 (可在Nodejs环境下运行源码)](https://github.com/uptonking/nostalgia-studio/tree/main/cms-strapi/strapi-awesome)
- [Materials 资料库 (无在线预览，有部分文档)](https://github.com/uptonking/nostalgia-studio-v2023/tree/main/packages/materials-repo)
- [Dashboard 仪表板 (在线预览)](https://uptonking.github.io/pgd-dashboard-showcase)

