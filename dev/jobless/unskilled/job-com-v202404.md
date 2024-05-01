---
title: job-com-v202404
tags: [company, interview, job]
created: 2024-04-23T14:56:51.814Z
modified: 2024-04-23T15:38:13.307Z
---

# job-com-v202404

# guide

- 待改进
  - 学术编辑器开发的难点未介绍清楚，可以考虑介绍Notion-like编辑器的难点、版本控制的难点
  - 能为公司产品或团队带来什么？ 没有将自己的作品融入公司产品作为卖点，比如拖拽组件、多维表格、流程自动化、历史版本

- 
- 
- 

# 面试记录

# com-深圳君璟科技
- [深圳君璟科技有限公司 - 天眼查](https://www.tianyancha.com/company/6147670320)
  - 成立日期：2023-05-11
  - 法定代表人：李镇
  - 位于广东省深圳市，是一家以从事软件和信息技术服务业为主的企业
  - [深圳君璟科技有限公司 - 爱企查](https://aiqicha.baidu.com/company_detail_43931763153659)
- [海口君诺科技有限公司 - 天眼查](https://www.tianyancha.com/company/5621585281)
  - 成立日期：2022-07-21
  - 法定代表人：李镇
  - [海口君诺科技有限公司 - 爱企查](https://aiqicha.baidu.com/company_detail_87619388628567)

- [「君璟科技招聘」2024年君璟科技招聘信息-BOSS直聘](https://www.zhipin.com/gongsi/job/7c0df181113fa1ca1XN53967F1M~.html)

- 面试
- 第三方支付的接口容易变动，是完全自己实现，还是用的开源的

- 
- 
- 

# com-至简天成
- 结果

- 一面
- showMeBug的代码编辑器是根据codesandbox的sandpack修改得到的吗
  - 不是，根据codemirror自研
- 协作基于codemirror内置？
  - 协作基于yjs
- 版本回放为什么不基于内置功能去做
  - 基于rrweb实现很快
- 代码内容是不是存在数据库的一个字段
  - 待深入
- daopass sdk 是纯前端的吗
  - 是很薄的一层封装

- 二面
- 产品大类划分，与研发人力投入
- 产品市场以tob为主，还是以toc为主
- 新产品方向：为什么选择ai-agent，为什么不研发类似linear的issue管理系统，为什么不做招聘市场、在线会议
- 研发人员的一般离职时间

- 面试结果一拖再拖，已放弃

## 简介

- [深圳至简天成科技有限公司 - 天眼查](https://www.tianyancha.com/company/3202670111)
  - 法定代表人：李亚飞
  - 注册时间：2018-06-19
  - 分公司: 上海、北京、杭州、广州
  - [深圳至简天成科技有限公司 - 爱企查](https://aiqicha.baidu.com/company_detail_10142142014981)

- 融资信息
  - 2021-07-07	A轮	1亿元
  - 2021-01-27	Pre-A轮	1000万元
  - 2020-09-03	天使轮	数百万元

- [1024paas.com](https://www.1024paas.com/)
  - Create accessible Rapps with speed, modular and accessible component library that gives you the building blocks you need to build your Editor applications.
  - 基础应用
  - 分享协作
  - 跟随模式
  - 切换题目
  - 测试用例
  - 操作回放
  - 编辑器配置
  - [DaoPaaS API Options](https://www.1024paas.com/sdk/docs/index.html)
    - 本文是DaoPaaS的一个简单使用示例。
    - [主要流程 - 1024PaaS-租户业务接口](https://apifox.com/apidoc/shared-c0c0ebad-15b3-4605-896e-e39879fe6e47/doc-952073)

- 创建实例
  - dao = new DaoPaaS()
  - dao.onMessage
# com-沃尔玛外包-failed
- 低代码实施工程师 base地: 福田区 偏前端(不需要搭建应用)、偏前端6年以上经验，至少两年以上React开发经验，技术型
  - VIJAYAN VENKATESHAN 邀请你加入沃飞书视频会议 会议主题：面试-金瑶 会议时间：4月24日 (明天) 14:00 - 14:30 (GMT+8) 会议 ID：309 167 225 会议链接：https://vc.feishu.cn/j/309167225
  - 沃尔玛这个低代码前端开发是在平台上进行二次开发的，是用明道云。
  - 比较喜欢沟通能力好的，喜欢沃尔玛平台，稳定性好的
  - 表达能力好的，思路清晰的

### 二面_20240426

- 介绍下你做过的项目
  - 编辑器、表格
  - strapi cms的生态、插件

- 挑一个你所做过的项目，介绍下难点
  - 学术编辑器，参考文献

- 明道云流程自动化
  - 内置了一些自动化流程
  - 提供了第三方集成

- 面试小结
- 要点
  - 业务开发的流程、细节、难点
- 不足
  - 学术编辑器开发的难点未介绍清楚，可以考虑介绍Notion-like编辑器的难点、版本控制的难点
  - 🧐 没有将自己的作品融入公司产品作为卖点，比如拖拽组件、多维表格、流程自动化、历史版本

### 一面_20240424

- 微软power platform的rpa模块
  - [Microsoft Power Automate – Process Automation Platform | Microsoft](https://www.microsoft.com/en-us/power-platform/products/power-automate)
  - A comprehensive, end-to-end cloud automation platform powered by low code and AI.
  - Use robotic process automation (RPA) to automate legacy systems with prebuilt or custom user-interface actions.
  - Manage peaks and optimize resources with hosted infrastructure that automatically scales and dynamically balances loads.

- react的jsx、hooks原理

- redux的原理
  - single source of truth, immutable state, functional reducer

- webpack打包编译输出的原理
  - 识别入口文件，逐级递归识别依赖，构建依赖图谱，将代码转化成AST抽象语法树，把AST抽象语法树变成浏览器可以识别的代码， 然后输出
# more
