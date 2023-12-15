---
title: lib-saas-nocobase-community
tags: [community, lowcode, nocobase]
created: 2023-03-31T02:09:10.677Z
modified: 2023-12-15T17:03:40.487Z
---

# lib-saas-nocobase-community

# guide

# not-yet
- [How can I create Search functionality?](https://github.com/nocobase/nocobase/discussions/1535)
  - not-yet

- [预期会支持多租户的功能吗？或者说个人如果想开发一个多租户插件的话，应该从哪些地方开始入手？](https://github.com/nocobase/nocobase/discussions/1380)
  - 目前有多租户插件，在线 demo 就是。后续需要继续完善

- [建议：增加图表的定时刷新功能或者在图表上方增加刷新按钮，目前无法处理实时交互的数据图表](https://github.com/nocobase/nocobase/discussions/704)
# discuss-stars
- ## [服务器端字段目前没有校验功能](https://github.com/nocobase/nocobase/issues/303)
  - 有一个名为 email 的字段，需要做邮件格式校验，在界面添加是有校验的，但如果用 api 形式调用发现服务器端目前还没有做校验。

- NocoBase 的默认设定，对字段并不做后端校验，暂时所有的校验只是前端有效。如果有服务端校验需要可以参考这里的配置
  - 完整的校验模块会独立出来考虑，有计划，但是优先级不高。

- 使用 sequelize 的 validation 是可以的
# discuss
- ## 

- ## 

- ## [官网的开通体验站点怎么实现的？](https://github.com/nocobase/nocobase/discussions/559)
- NocoBase 支持多应用模式，以及目前比较具备代表性的两个场景：
  - 独立 context：demo 站
  - 共享 context：连接第三方数据库插件

- ## [未来是否会支持生成代码](https://github.com/nocobase/nocobase/discussions/435)
- NocoBase 的无代码/低代码是配置化驱动的，配置保存在数据库里，通过后端动态驱动，而并非代码生成器的思路（代码生成器比较适用于低代码，无代码场景不太适合）。
- NocoBase 是插件化设计的，一些复杂的模块都可以通过编写插件来实现，插件是需要写代码的，可发挥的空间巨大。写好的插件，再通过简便的方式提供给用户使用。
- 另外，在项目的 packages/app 文件夹里也可以添加个性化的业务代码。

# discuss-lowcode-design
- ## [Webstudio vs. Webflow](https://webstudio.is/blog/webstudio-vs-webflow)
- Some platforms, like Framer Sites, focus on making it as easy as possible to make a website. 
  - However, the farther you get from the logic and structure of HTML & CSS, the less creative freedom and power you have to work with.
- On the other end of the spectrum, we have tools like Webflow and Webstudio that give users a visual way to interact directly with HTML & CSS
- At Webstudio, we prioritize performance, creative freedom, and extensive collaboration.
