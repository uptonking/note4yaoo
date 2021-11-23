---
title: lib-editor-ckeditor5-dev
tags: [ckeditor, editor]
created: '2021-10-25T09:33:19.901Z'
modified: '2021-10-25T09:33:39.528Z'
---

# lib-editor-ckeditor5-dev

# 2021

- 路由权限和http取数权限都要验证
  - ❓️路由权限要检查返回的用户对象要包含`role`属性，通过后才跳转路由；需要新的查询接口，或者直接在前端配置规则
  - http请求权限要在请求头中带上 authorization，检查返回值是否包含成功标志，返回值包含成功标志才直接使用，否则鉴权失败

- [Role-Based Routing with Next.js](https://spin.atomicobject.com/2019/12/11/role-based-routing-with-next-js/)
  - 每次跳转page时检查 router.pathname.startsWith("/employee") && role !== "employee"

- 解决用户权限的2个维度
  - 路由级权限控制，定义路由配置对象时，声明访问该路由需要的role
  - http请求级权限控制，访问敏感数据或执行敏感操作时需要检查role
  - 其他参考
    - 动态添加路由
    - 菜单与路由分离，菜单由后端返回菜单
    - 或者 菜单与路由完全由后端返回
# guide
- features

- who is using ckeditor 5
  - drupal
