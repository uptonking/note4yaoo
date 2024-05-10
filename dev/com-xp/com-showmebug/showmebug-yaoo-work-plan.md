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
  - 业务类: ai编程/pr/测试
  - 基建类: 基座工程、代码编辑器
  - 团队类: 测试、运营

- bug
  - 在6月中，初步完成生成需求、task、pr的逻辑和流程
# more

## proj-idepaas

### not-yet

- codemirror相关的代码为什么不通过npm包引入
  - 直接修改github上的源码
- daoPaas的初始化逻辑包含渲染dom吗? 
  - mapRender渲染到dom
- mapRender 有什么问题
  - 未实现按需加载FileTree/Editor/Terminal

- 
- 
- 
- 
- 

### draft

### roadmap

- daopaas的框架，在clacky-ai-frontend里面，目前已初步搭建。 
  - 已实现：简单允许和package.json 待实现可以分成两次版本迭代
  - 第一版：原样迁移 把packages/client/src/* 的代码全部迁移到libs/d42paas-biz/client/ 中，并在apps/d42paas_playground/src/app/[locale]/(main)/ 中进行演示（重新使用tailwind+shadcn/ui写）。 
  - 第二版：删除 mapRender 方法

- embed
- 
- 

- 协作迁移到yjs的实现

- 去掉rrweb

- d42paas的code playgrounds能否用 d42paas 的sdk实现

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
  - getTicketInit > init-DaoPaaS
    - this.daoEditor = new DaoEditor();
    - this.initChannel(data.data);
  - effects
    - getTicketInit
    - updateConfig
    - daoPaasObj.onMessage

- 
- 
- 
- 
- 
- 

## proj-1024code

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
  - dao_paas = await DaoPaaS()

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
