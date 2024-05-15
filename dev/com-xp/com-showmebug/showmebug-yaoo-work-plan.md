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

- work-xp-pros
  - 研发进度给了开发者较多空间
  - 产品团队的对齐比较充分
- work-xp-cons
  - 单人项目太多了，交接困难
  - 研发流程cicd，lint、pr流程不完整
  - 研发目标对开发产品都不清晰
# more

## proj-idepaas-sdk

- resources
  - https://staging.1024paas.com/   (测试数据较多，api较稳定)
  - https://develop.1024paas.com/
  - https://www.1024paas.com/
  - [DaoPaaS API Options](https://www.1024paas.com/sdk/docs/index.html)
  - [1024PaaS-租户业务接口](https://apifox.com/apidoc/shared-c0c0ebad-15b3-4605-896e-e39879fe6e47/doc-952073)
  - https://staging.showmebug.com/  (帐号 01test)

### not-yet

- paas平台为什么难以落地
  - 功能又多又杂
  - 侧重ai编辑，可以去掉非核心需求

- 
- 
- 

- codemirror相关的代码为什么不通过npm包引入
  - 直接修改github上的源码
- daoPaas的初始化逻辑包含渲染dom吗? 
  - mapRender渲染到dom
- mapRender 有什么问题
  - 未实现按需加载FileTree/Editor/Terminal

- 所有数据的通信都基于channel(websocket)?
- 
- 
- 
- 

### draft

- sdk的主要组件Editor/FileTree/Shell的渲染是独立的 `createRoot(dom).render(<Editor />)`; 
- 
- 
- 

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

### dev-xp

- `d42paas_frontend` 项目启动记录
  - cp .env.local.example .env, 可不修改任何配置，但修改配置中queue的名字可方便调试
  - cd packages/demo; pnpm dev
  - cd packages/server; pnpm dev
  - 修改 packages/server/apps/entry/test/filetree_mock_test 末尾文件名为 filetree_mock
  - 在 http://localhost:3010/ api demo的用户名和手机号可随便写

- ⌛️ 回放示例(环境支持sdk-staging/sdk-localhost-3010/showmebug)
  - 在sdk demo界面，需要指定代码处理为 showmebug
    - 在basic示例点击 录制数据 和 停止录制
    - 复制basic示例url中的playgroundId, 可在操作回放中指定租户为 showmebug 和 playgroundId
  - 在showmebug，测试帐号为 01test
    - 测试案例: 不能把的笔试, 2023-12-12 17:34， 包括java/python/vue/架构图画板
  - 🌹 亮点
    - ✨ 不同面板的状态能够同时回放，如编辑器界面、预览界面、控制台
    - 回放支持其他面板: 测试用例、题目评分、选择题
    - 回放支持不编辑时的光标位置变化
    - 回放支持shell的操作命令和输入输出
    - 回放支持debug断点详细数据
    - 回放支持架构图画板
  - 🐛 缺点
    - 文件树在用户操作不同文件时，没有高亮对应的打开文件
    - 部分框架的预览视图面板，不支持回放
  - ☑️ to-do
    - 在播放进度条直接显示预览界面
    - 播放时可并排显示多个shell的输出
    - 录制数据只能有一个用户，如果SMB需要跟随来回切换， 如果切换到面试官录制， 候选人只能停止录制，

### codebase

- lazy-load的组件
  - CodeEditor
  - FileTree
  - TerminalComponent
  - Console
  - OutputBrowser

- app-init-dataflow
  - getTicketInit
    - init > `const dao = new DaoPaaS()`;
      - this.daoEditor = new DaoEditor(); // DaoEditor封装很少
      - requestChannelPathFromTicket
      - this.initChannel(data.data);
      - window.addEventListener('message',fn)
      - store.dao.channel().startChannel()
    - dao.onMessage()
    - dao.subscribe()
    - dao.mapRender() 渲染编辑器、预览、shell面板
  - effects
    - getTicketInit
    - updateConfig
    - daoPaasObj.onMessage

#### LazyEditor

```JS
// playback
useEffect(() => {
  if (isPlayBack) {
    channel.subscribeForComponent(Events.Editor, {
      onStart: () => {},
      onData, // 监听数据变化(回放时的帧数据)
      getPlaybackSnapshot, // 获取快照数据
    });
  }
}, [channel, isPlayBack]);

// 监听全局消息(处理自定义帧)
useEffect(() => {
  if (channelAvailable && channel) {
    channel.removeMessageListener(handleMessageListener);
    channel.addMessageListener(handleMessageListener);
  }

  return () => channel.removeMessageListener(handleMessageListener);
}, [channel, channelAvailable]);
```

#### CodeEditor

- CodeMirrorEditor 通过 useImperativeHandle 对外暴露方法 setState/setView

- channel.addMessageListener(editorMessage); 
  - 监听到消息时，更新编辑器 view.dispatch({changes})

- 
- 
- 
- 
- 
- 

#### replay

- 
- 
- 
- 

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
