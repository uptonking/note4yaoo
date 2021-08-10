---
title: pm-ux-dashboard-admin-docs
tags: [dashboard, docs]
created: '2021-08-10T16:38:29.854Z'
modified: '2021-08-10T16:39:00.631Z'
---

# pm-ux-dashboard-admin-docs

# guide

- 开始使用
- 配置约定
- 路由配置
  - 添加页面、添加链接
- 布局配置
  - 导航条、侧边栏、设置面板
- 内置数据流
  - crud示例
  - 权限管理
  - 注册与登录
- roadmap
  - goal、recent
- faq
# 开始使用

# 配置约定
- 在项目运行前支持的配置项，只作为默认初始值，后续修改不会生效
  - ./config/defaultSettings.ts 配置项很少，暂时只包括标题、主题色
- 在项目运行时支持的配置
  - ./config/routes.ts 配置路由、文件路径
  - ./src/App.tsx 每次initialState改变都会触发rerender
  - initialState可以直接修改globalStore中的值
- 通过设置面板直接在界面中配置，支持的配置项不多
# 路由配置
- 添加页面、添加链接
# 布局配置
- 导航条、侧边栏、设置面板
# 内置数据流
- getInitialState支持异步请求

- 插件/钩子函数
  - 登录时
  - 跳转时

## 权限管理

- 暂时只支持路由级的权限控制，不支持页面内元素的权限控制

- 路由级权限访问控制的实现
  - 从initialState中读取routes数组和isAdmin默认角色
  - 在./src/access.ts中定义并返回多个鉴权函数
  - 在routes中声明access.ts中支持的鉴权函数规则
  - 在创建Route时，对不满足权限规则的重定向到403页面

- ref
- 要配置用户名、还是操作名、还是true/false
  - 考虑最基本的注册登录页面
  - react-acl-router中在每条route配置中指定permissions为角色admin/user，而ant-design-pro中指定操作鉴权函数名
  - 配置用户名更容易理解；配置操作名更容易集成到已有rbac系统
  - react-abac和rbac可用来实现页面内子元素或组件级的访问控制，路由级的访问控制不需要这么复杂

## 网络请求

# roadmap
- goal、recent
