---
title: pm-ux-dashboard-admin-devlog
tags: [dashboard, devlog, pm]
created: '2021-08-08T08:38:41.856Z'
modified: '2021-08-08T08:39:17.347Z'
---

# pm-ux-dashboard-admin-devlog

# todo
- 支持配置路由对应的左侧边栏菜单
  - 隐藏某个菜单项及children，hideInMenu
  - 隐藏自身和children，不配置name
  - 隐藏children，hideChildrenInMenu
  - optional
    - 隐藏自身，只展示children，子菜单上移，flatMenu
    - isHeader/FooterShown
    - isMenuShown 不展示菜单
    - isMenuHeaderShown 不展示菜单顶栏

- 左侧导航子目录
  - 在侧边栏折叠到只显示图标时，不管侧边栏内部的菜单，显示固定图标
  - [x] shortcut link外部链接，以 http(s) 开头
  - [x] 支持同时打开多个子目录
  - optional
    - 高亮鼠标所在的菜单项
    - 不能默认展开
    - 通过引入perfect-scrollbar暂时解决了左侧边栏会出现水平滚动条的问题
    - collapse: false时，子菜单项不可展开
  - 鼠标位于左侧边栏滚动时，只滚动左侧边栏，不应该滚动内容区

- 配置左侧边栏
  - width，配置宽度容纳更长文本，甚至支持拖拽修改宽度
  - mini-sidebar icons: 只显示一级菜单的icon

- 配置右侧配置面板
  - dockable
  - 右侧面板的顶部显示在导航条底部之下，不要遮挡

- 配置navbar
  - 添加shadow，区分白色导航条和白色侧边栏
  - 快速连接菜单项

- 配置routes
  - 本项目的404页面，考虑无权访问的提示词
    - 全局404很难实现，因为动态路由无法预知是否存在；path为`*`放在末尾时，只能匹配当前层级，无法匹配嵌套层级
  - 各个path、各个嵌套层级的404路由跳转如何实现
    - config/routes.ts配置部分只定义了开发者需要的routes
    - 可考虑自动生成当前层级
  - role-based-access-control给出的思路是只渲染有权限的菜单；问题是导航菜单就不能完整显示了
  - 测试以slash /结尾的url是否正常跳转
  - 处理double slash的情况

- 自定义布局
  - 顶部一级菜单，左侧二级菜单
  - 支持隐藏所有布局区域：顶部导航条、内容区页脚、侧边菜单、logo区域

- 其他
  - 根据路由修改页面title
  - ajax要处理race condition，添加 isDone 标记
    - 注册未完成时就点击 `去登录` 会导致内存泄露
  - 登录时记住密码

- auth
  - 客户端用户登录状态的判断：token + isLoginAuthed
  - 退出登录后回到登录界面，但登录按钮是active的；validate的逻辑要重写
  - ~~debounce 提交按钮的网络请求~~，正在提交了直接在前端拒绝再次提交
  - 提交按钮无法用tab键focus和选择

- test
  - fetch-mock to msw(Mock Service Worker)

- search
  - 搜索菜单
  - 搜索内容

- 中文etl优化
  - routing url不使用文件名，而使用层级信息如/intro/1, /background/2/1，具体编号大小由文件创建时间确定

- discuss
  - 分享
  - 对于左侧菜单项，使用懒加载而不是直接导入组件时，修改routes.ts配置文件不会自动刷新，拖慢开发速度
# dev

## pages文件夹下的文件名和路由的url如何对应

- 暂时不做转换，直接将文件名原名作为路由url中的路径
  - pages文件夹下，不推荐使用PascalCase作为react组件所在的文件名
  - 实现起来简单
  - 规则明确，不存在隐式转换

- ref
  - [Transform PascalCase files to lowercase routes on nextjs](https://www.reddit.com/r/reactjs/comments/a2zb0y/transform_pascalcase_files_to_lowercase_routes_on/)
