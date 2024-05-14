---
title: showmebug-yaoo-work-plan
tags: [showmebug, work]
created: 2024-05-06T02:54:24.884Z
modified: 2024-05-06T02:54:40.374Z
---

# showmebug-yaoo-work-plan

# guide

# plan
- 工作OKR
  - 业务类: ai编程/pr/自动测试
  - 基建类: 基座工程、代码编辑器
  - 团队类: 测试、运营

- draft
  - 在6月中，初步完成生成需求、task、pr的逻辑和流程

- roadmap-研发任务拆解
  - 主要业务流程
  - cde
  - 对标的目标产品不清晰
# more

## proj-idepaas-sdk

- resources
  - https://develop.1024paas.com/
  - https://www.1024paas.com/
  - [DaoPaaS API Options](https://www.1024paas.com/sdk/docs/index.html)
  - [1024PaaS-租户业务接口](https://apifox.com/apidoc/shared-c0c0ebad-15b3-4605-896e-e39879fe6e47/doc-952073)

### not-yet

- paas平台为什么难以落地
  - 功能又多又杂
  - 侧重ai编辑，可以去掉非核心需求

- 
- 
- 
- 

- codemirror相关的代码为什么不通过npm包引入
  - 直接修改github上的源码
- daoPaas的初始化逻辑包含渲染dom吗? 
  - mapRender渲染到dom
- mapRender 有什么问题
  - 未实现按需加载FileTree/Editor/Terminal

### draft

### roadmap

- features-to-dev
  - 多文件打开
  - 多shell
  - 开发多port

- daopaas的框架，在clacky-ai-frontend里面，目前已初步搭建。 
  - 已实现：简单允许和package.json 待实现可以分成两次版本迭代
  - 第一版：原样迁移 把packages/client/src/* 的代码全部迁移到libs/d42paas-biz/client/ 中，并在apps/d42paas_playground/src/app/[locale]/(main)/ 中进行演示（重新使用tailwind+shadcn/ui写）。 
  - 第二版：删除 mapRender 方法

- embed
- 
- ### roadmap

- 
- 
- 

- branching
  - 各分支的 dev-server
  - 各分支的 history、time-travel

- embed
- 
- 

- 考虑轻编辑，通过devcontainer连接远程仓库来进行本地编辑

- 
- 
- 

- 协作迁移到yjs的实现

- 去掉rrweb

- d42paas的 code playgrounds 能否用 d42paas 的sdk实现
  - 用自己的平台开发代码

- 
- 
- 

- 考虑轻编辑，通过devcontainer连接远程仓库来进行本地编辑

- 
- 
- 

- 协作迁移到yjs的实现

- 去掉rrweb

- d42paas的 code playgrounds 能否用 d42paas 的sdk实现
  - 用自己的平台开发代码

- daopaas的框架，在clacky-ai-frontend里面，目前已初步搭建。 
  - 已实现：简单允许和package.json 待实现可以分成两次版本迭代
  - 第一版：原样迁移 把packages/client/src/* 的代码全部迁移到libs/d42paas-biz/client/ 中，并在apps/d42paas_playground/src/app/[locale]/(main)/ 中进行演示（重新使用tailwind+shadcn/ui写）。 
  - 第二版：删除 mapRender 方法

### codebase

- `d42paas_frontend` 项目启动记录
  - cp .env.local.example .env, 可不修改任何配置，但修改配置中queue的名字可方便调试
  - cd packages/demo; pnpm dev
  - cd packages/server; pnpm dev
  - 修改 packages/server/apps/entry/test/filetree_mock_test 末尾文件名为 filetree_mock
  - 在 http://localhost:3010/ api demo的用户名和手机号可随便写

- lazy-load的组件
  - CodeEditor
  - FileTree
  - TerminalComponent
  - Console
  - OutputBrowser

- app-init-dataflow
  - getTicketInit
    - init > `const dao = new DaoPaaS()`;
    - this.daoEditor = new DaoEditor();
    - this.initChannel(data.data);
  - effects
    - getTicketInit
    - updateConfig
    - daoPaasObj.onMessage

### docs

- 本案例的axios为封装后的axios, baseUrl默认为“www.1024paas.com”。

- PART-ONE 请求获取ticket(票)流程
  - 第一步：定义接口
  - 第二步：封装逻辑
  - getEnvironmentsApi
  - getCodeZoneIdApi
  - getPlaygroundIdApi
  - getTicketApi
- PART-TWO 在组件中使用
  - 第一步：引入SDK和样式 import { DaoPaaS, Messages } from 'DaoPaaS.cjs'; 
  - 第二步：初始化实例 
    - const dao = new DaoPaaS({ tenantId: '租户id', ticket: '动态获取的ticket', userInfo: { username: '用户名'} }); 
    - dao.onMessage()
    - dao.mapRender()  // 会把dao内部组件渲染到对应的dom节点
  - 第三步：销毁实例 dao.dispose()
- PART-THREE SDK部分其他方法
  - dao.activePlayground() // 激活容器
  - dao.runPlayground() // 运行容器
- PART-FOUR 基础案例

- 
- 
- 
- 

## proj-1024code

- resources
  - [1024Code](https://1024code.com/~)
  - [1024Code 文档中心](https://docs.1024code.com/)

### not-yet

- questions
  - /ide路由的 CloudIDEPage组件没有在react-devtools显示出来

- 前端项目在打开ide时没有实现运行预览，需要手动点击运行

- 在ide中修改文件后，更新预览太慢

### draft

### codebase

- 左侧图标菜单: fileTree, search, git
  - ActivityPane: 左侧图标菜单对应的面板
  - .tree-section
- Editor: 编辑区 .editor-section
  - EditorPane > `CodeEditor`; 
- Preview: 预览区
  - OpenBrowser
  - Terminal
  - Console

- init-app-dataflow
  - StoreProvider > createStore
    - new CodecubeStore
- init-ide-dataflow
  - codecube.mount()
  - this.ideStore?.mount()
  - const ideCodecube = await getPlaygroundFn(this.slug); 
  - this.initPaaS(); 
    - defaultOpenFiles.push()
    - contextMenu.push
    - aiCodeMenu.push
    - daoEditor?.addHotKeys
  - this.createChatChannel(); 
  - this.createChatgptChannel(); 
  - `dao_paas = await DaoPaaS()`; 

- web项目中的编辑器
  - apps/web/src/store/IDEStore.tsx  接入了daoPaas状态
  - apps/web/src/ui/MarkdownEditor/index.tsx
  - apps/web/src/ui/Codecubes/hooks/AtEditor/index.tsx
  - apps/web/src/pages/community/publish/AtEditor/index.tsx

- 
- 
- 
- 
- 

- `1024code` 注册时要先点击发送验证码，然后在验证码输入框填入6个0就可以注册成功
  - 邀请码测试: hs8MQf, Ukycbf
  - 测试用户是 155572695015和八个一
  - node版本不支持v22，暂时使用v20
  - 编译构建时可通过修改repo文件夹名来避免使用turborepo的cache

## proj-backend

- docker in docker 的权限问题
