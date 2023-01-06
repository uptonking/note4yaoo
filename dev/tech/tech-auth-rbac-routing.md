---
title: tech-auth-rbac-routing
tags: [auth, rbac, react-router, router]
created: 2021-08-11T07:35:28.800Z
modified: 2022-01-06T17:30:03.280Z
---

# tech-auth-rbac-routing

# guide

# rbac-blogs
- 区分3种路由
  - RoutePrivate 未登录不可访问，登录后才可访问
  - RouteUnauthorizedOnly 未登录可访问，登录后不可访问，会自动跳转到指定路由
  - 默认public 未登录可访问，登录后可访问

- 使用 `<Route>` 组件
  - 优点
    - 可读性好
    - 符合React开发模型
  - 缺点
    - 每个私有route都要手动在外面添加组件
      - 但对于统一前缀的路由，可以通过`path='*'`在AuthRedirect里面统一添加跳转
- 使用 `routeObject` 对象
  - 优点
    - 方便批量生成私有路由
  - 缺点
    - 内层路由的可读性差

```JS
 <Route path='id'>
    <Route path='*' element={<AuthRedirect />} />
  </Route>
```

## [react-router v6 官方示例 - 公开路由+私有路由](https://reactrouter.com/docs/en/v6/examples/auth)

- [stackblitz auth routes demo](https://stackblitz.com/github/remix-run/react-router/tree/main/examples/auth?file=src/App.tsx)
  - [routes object demo](https://stackblitz.com/github/remix-run/react-router/tree/main/examples/route-objects?file=src/App.tsx)

```JSX
<Route
  path="/protected"
  element={
    <RequireAuth>
      <ProtectedPage />
    </RequireAuth>
  }
/>

```

- [Role Based Authorization with React Router v6 and Typescript](https://adarshaacharya.com.np/blog/role-based-auth-with-react-router-v6)
  - 简单实用，思路清晰，先验证用户，再检查用户的权限是否符合路由要求
  - PrivateRoute + requiredRoles
  - [示例代码项目参考](https://github.com/adarshaacharya/MentorLabs/blob/main/client/src/router/Router.tsx)

```JSX
<Route
  path={routes.LOGIN}
  element={
    <NonAuthRoute>
      <Login />
    </NonAuthRoute>
  }
/>
<Route
  path={routes.STUDENT_DASHBOARD}
  element={
    <AuthRoute roles={[Role.STUDENT]}>
      <StudentDashboard />
    </AuthRoute>
  }
/>
```

## [Public, private, and role-based routes in React](https://javascript.plainenglish.io/role-based-authorization-role-based-access-control-v-2-in-react-js-cb958e338f4b)

- https://github.com/umair-khanzada/role-based-access-control

- 本方案的优点pros
  - 统一配置userRoles、routes
  - 动态路由

- 本方案的缺点cons
  - 动态路由；子路由不能提前渲染，必须在父路由渲染后才动态渲染；对于嵌套路由的子路由的Layout组件，必须都实现动态渲染子路由组件的逻辑 `<MapAllowedRoutesroutes={allowedRoutes} basePath={basePath}/>`

- 注意children是子路由，子路由并没有提前统一创建，而是传递给页面组件动态创建；
  - 所以页面组件内部必须处理子路由的渲染
  - 优点是动态创建路由
  - 缺点是页面组件结构被污染(在页面中处理子路由的逻辑)

- 实现步骤
  - 定义roles
  - 定义routes
  - 计算allowedRoutes：比较用户权限和各路由权限
  - 动态创建Route： MapAllowedRoutes

```JS
[{
    component: Module1,
    path: '/',
    title: 'Module - 1',
    exact: true,
  },
  {
    component: Module2,
    path: '/module-2',
    title: 'Module - 2',
  }
]
```

- it is my second story on the same topic, there was some reason behind version-2 that are listed below.
  - Version 1 is tightly coupled with the project in which I have introduced this technique.
  - No child/nested route support.
  - No technique to define roles in one place.
  - Updating route access is complicated.
  - Have to maintain common routes for all roles.

- Updates in version-2:
  - I have come up with a more generic approach so it’ll better serve the community.
  - Added child/nested route support.
  - Define roles in one place so it’s easy to maintain.
  - Easy to update route access just by adding or removing role.
  - If you skip the permission, it’ll automatically accessible to everyone.

- The idea is simply prevent the app to generate unnecessary routes, rather checking the role on each route and showing fallback UI
  - it would be a great idea to generate only the routes in which user have access, 
  - so if the user navigate manually to a route ie: (typing in the address bar), he/she will get 404 Not Found screen because route is not registered.

- Because we are looking for a role-based solution, so let’s define the roles first, roles are nothing just a plain javascript object having key-value pairs
- Define the private routes configuration, route config object supports all the react-router’s route component props with some additional props ie: (title/name, permission, children)
- we have a utility method `getAllowedRoutes` in which we can pass routes array and it’ll return filtered routes array and pass that array into routes mapping component MapAllowedRoutes
- the last step is to render the filtered routes

- Benefits
  - Check route access only once when parent route renders
  - Generate only routes that user have access
  - Central roles and private routes configuration file
  - Easy to add/remove a role
  - Easy to add/remove route access from user role
  - Synchronization between routes and navigation
  - Single + Multiple role support
# rbac-api
- https://github.com/HiWayne/rainbow-bridge
  - nestjs+mysql+typeorm实现的，高安全性用户账号系统、基于RBAC的权限系统
  - 用户系统采用加盐 SHA512 哈希+10000 次派生算法加密，保证了密码存储的高安全性。用户身份使用双 token (access token + refresh token) 验证，非对称加密算法使用 HS512。权限系统基于 RBAC 设计。
# rbac-blogs-more
- [RBAC权限系统分析、设计与实现](https://juejin.cn/post/6844903940752932878)
  - 简洁概括了rbac模型的原理
- [设计-RBAC数据库的设计与使用](https://www.jianshu.com/p/1d20fd8c3029)
  - 权限模型 rbac、acl、abac、pbac
  - 数据库设计：核心五张表

- [How to Role Based Access Control (RBAC) ?](https://dev.to/thearvindnarayan/how-to-role-based-access-control-rbac-2935)
  - Route Guarding 
  - Restricting access to a part of the page
  - Securing Backend Endpoints
  - 只列举了使用场景和组件api设计，未给出实现

- [React - Role Based Authorization Tutorial with Example](https://jasonwatmore.com/post/2019/02/01/react-role-based-authorization-tutorial-with-example)
  - https://github.com/cornflourblue/react-role-based-authorization-example
  - 请求api时用到了 rxjs BehaviorSubject
  - 还提供了express后端示例
  - https://github.com/cornflourblue/node-role-based-authorization-api
    - [Node.js - Role Based Authorization Tutorial with Example API](https://jasonwatmore.com/post/2018/11/28/nodejs-role-based-authorization-tutorial-with-example-api)

- [React-router authorization based on user roles](https://www.nafrontendzie.pl/autoryzacja-react-router-role-uzytkownika)
  - [Role-based authorization using React-Router](http://web.archive.org/web/20170529015710/http://frontendinsights.com/role-based-authorization-using-react-router/)
  - 限制路由访问的实现，所有需鉴权的页面组件都继承自AuthorizedComponent，里面实现了role的比较判断
  - 不同role显示不同页面元素的实现，所有需鉴权的子元素组件都继承自RoleAwareComponent，里面实现了role的比较判断
  - 可作为通用的授权方案，没有强调rbac
  - https://github.com/burczu/react-router-role-authorization
  - what I wanted to achieve
    - limit the access to some routes to specific roles. 
    - different roles have access to different functionality so I wanted to show different components on the home page.

- [6 种 Vue 权限路由实现方式总结(最全)](https://cloud.tencent.com/developer/article/1449210)
  - 使用全局路由守卫
  - 登录页与主应用分离
  - 使用 addRoutes 动态挂载路由
  - 菜单与路由分离，菜单由后端返回
  - 菜单与路由完全由后端返回
  - 不使用全局路由守卫，手动添加路由
    - 前面几种方式，除了 登录页与主应用分离，每次路由跳转，都在全局路由守卫里做了判断
    - 应用初始化的时候只挂载不需要权限控制的路由
    - 若没有初始化，则调用远程接口获取菜单和路由等，然后处理后端返回的路由，将 component 赋值为真正的组件，接着调用 addRoutes 挂载新路由，最后跳转路由即可
