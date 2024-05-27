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
  - ~~研发目标对开发产品都不清晰~~
# more

## proj-idepaas-sdk

- resources
  - https://staging.1024paas.com/   (测试数据较多，api较稳定)
  - https://develop.1024paas.com/
  - https://www.1024paas.com/
  - [DaoPaaS API Options](https://www.1024paas.com/sdk/docs/index.html)
  - [1024PaaS-租户业务接口](https://apifox.com/apidoc/shared-c0c0ebad-15b3-4605-896e-e39879fe6e47/doc-952073)
  - https://staging.showmebug.com/  (帐号 01test)
  - [ShowMeBug字节级回放在线笔面试过程实现思路 - 掘金 _202107](https://juejin.cn/post/6985068859099201544)

- sdk设计参考
  - vscode, theia, opensumi
  - [Running the SDK](https://cloud9-sdk.readme.io/docs/running-the-sdk)

### not-yet

- ❓ snapshot数据是如何存储的
  - 切换分支后的回放还能执行吗

- 暂停/继续播放的回调事件未生效

- 获取ticket的api未添加权限校验，header中没有token

- 回放控制的示例，只打印了 onAvailable 事件

- 所有数据的通信都基于channel(websocket)?
  - 获取回放数据没必要用websocket，因为对实时性要求不高

- LSP 的server迁移到worker的方案

- 支持多实例

- paas平台为什么难以落地
  - 功能又多又杂
  - 侧重ai编辑，可以去掉非核心需求

- 给定仓库的url，类似 `/user/repo?task=desc`, 可以访问url查看ai创建pr的过程

- 
- 
- 

### draft

- sdk的主要组件Editor/FileTree/Shell的渲染是独立的 `createRoot(dom).render(<Editor />)`; 

- 
- 
- 

- codemirror相关的代码为什么不通过npm包引入
  - 直接修改github上的源码
- daoPaas的初始化逻辑包含渲染dom吗? 
  - mapRender渲染到dom
- mapRender 有什么问题
  - 未实现按需加载FileTree/Editor/Terminal

### roadmap

- features-to-dev
  - 多文件打开
  - 多shell
  - 开发启动支持多port
  - 考虑2套agent: 前端agent, 后端agent，可切换来节省资源

- embed

#### maybe

- 
- 

- branching
  - 各分支的 dev-server
  - 各分支的 history、time-travel

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

- preview react/vue components

- 
- 
- 

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
  - 在showmebug, 测试帐号为 01test
    - 测试案例: 不能把的笔试, 2023-12-12 17:34， 包括java/python/vue/架构图画板
  - 🌹 亮点
    - ✨ 不同面板的状态能够同时回放，如编辑器界面、预览界面、控制台
      - 回放支持其他面板: 测试用例、题目评分、选择题
    - 回放支持不编辑时的光标位置变化
    - 回放支持shell的操作命令和控制台的输入输出
    - 回放支持debug断点详细数据
    - 回放支持架构图画板
  - 🐛 缺点
    - 文件树在用户操作不同文件时，没有高亮对应的打开文件
    - 👁️ 部分框架的预览视图面板，不支持回放
  - ☑️ to-do
    - 播放进度条的中间节点支持显示预览画面
    - 播放时可并排显示多个shell的输出
    - 录制数据只能有一个用户，如果SMB需要跟随来回切换， 如果切换到面试官录制， 候选人只能停止录制

### codebase-sdk

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

#### LazyEditor/CodeEditor

```JS
// playback
useEffect(() => {
  if (isPlayBack) {
    channel.subscribeForComponent(Events.Editor, {
      onStart: () => {},
      onData, // 监听回放时的帧数据, actions.file.switchFile(), actions.dao.setLatestDocContent
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

- CodeMirrorEditor 通过 useImperativeHandle 对外暴露方法 setState/setView

- channel.addMessageListener(editorMessage); 
  - 监听到消息时，更新编辑器 view.dispatch({changes})

- 在codemirror的collab插件初始化时, initEventWatcher 会注册接收到syncOTUpdates/pushOTUpdates/pullOTUpdates的回调，在回调函数中会执行 store.dao.channel().send('pushOTUpdates', sendData); 
  - 对于syncOTUpdates，会强制执行 this.handleUpdate(true)，发送op到server
  - viewPlugin的update方法，在view更新dom前执行，collab插件这里会push数据到server

- 
- 
- 

#### playback ⌛️

- roadmap
  - 回放时~~不支持浏览器预览面板~~, showMeBug中基于rrweb实现浏览器预览面板的回放
  - 操作op很多时，回放性能差。 考虑snapshot
  - 支持多次编辑的snapshot数据? 多个task?

- 临时方案/待优化
  - 🤔 每个用户导入github仓库到clacky-proj后，每个用户的proj不共享，用户做完需求要提pr到github
    - 多人协同的场景更多是讨论和review，而不是实时协同开发
    - 是否支持每个用户仅回放自己的操作，或者回放时设置仅回放自己的op

- not-yet ❓
- recordBrowser参数似乎未使用
- 回放时拖动进度，是否存在快照来加速拖动
  - 拖动进度时，似乎没有用专门的快照来加速，但 ❓ 已播放过的frame被缓存了
  - this.playbackEngine!.movePosition(start); 
  - findFrameByTimeStamp会查找拖动的进度目标祯
  - 若目标祯不存在，则 this.preFrameTime = Date.now(); + step()

- snapshot数据是如何存储的
  - const { content } = store.file.getFileBaseHistoryByPath(dockerId, openedPath); 
  - 每次获取文件内容，并计算快照挂载到frame, 
  - frame.snapshot = { currentDoc, selection, agentUserId: agentUserId, isChange, changes, }; 

- 回放时，支持修改文件内容，但继续执行很可能失败
  - playback状态时，支持收集操作op

- [回放重构](https://www.notion.so/dao42/0ba448333b3f4740a6e569cefd40f821)
  - 回放的实现原理是sdk从服务端重新加载所有历史事件, 并分发给相应组件(在react项目中可以通过更新state来驱动各组件), 各组件接收到事件进行相应渲染
  - 对于大部分组件, 渲染时并不需要区分是否在回放模式, 只有可输入型组件需要在回放模式时禁止用户操作
  - 现在FileTree和Editor组件中直接注册事件, 不利于实现统一的回放消息重播. 故需要对Dao中的channel做出修改, 关闭on函数不允许组件自己注册事件. 统一由 MessageDispatcher 来分发事件

- syncPlaygroundInfo
  - fileRootPath: /app/data/codeZone/2024/3/5-16/@fad3d6d8-d302-4e29-9c2a-a02f9ca04026/source
  - fileTree: 文件树所有文件名和path, 不包含内容数据

- playbackInfo 结构分析
  - playbackSummerize
    - total 事件events总数
    - start/end 时间戳
  - playbackData 所有events数据
    - timestamp 
    - eventName: fileTree/editor, 决定了此事件归属的组件
    - data 事件相关操作数据
      - editor: openedPath
      - editor: revision, openedPath, updates(changes/sel)
      - fileTree: focus
  - historyBaseData
    - 各文件内容数据 path, content(内容快照)

- PlaybackEngine
  - step是触发播放的核心方法
  - 对于非多祯的场景， this.getPlaybackSnapshot?.(frame.eventName, frame, preFrame) 
  - 每次step方法的末尾，都会执行 gotoNextFrame() 
    - this.preFrameTime = Date.now(); 更新preFrame时间
    - window.requestAnimationFrame(this.step);

```JS
// 本地回放初始化时，ticket是在本地mock的
{
  ticket: Base64.encode('showmebug|662725910453239808|194e9365-4ae3-46fa-be09-a2753887328c|1716202534910|null|')
}
// ${params.tenantCode}|${params.playgroundId}|${userId}|${ Date.now() + 10000 }|null|
```

```JS
{
  // 会触发store.dao.channel().getPlaybackInfo()获取所有事件数据
  const res = await daoPaasObj.preparePlaybackSync();
  messageBox.info('通过同步事件收到回放数据');
  setQuestionsData(res.questionsData);
  if (res.total > 0) {
    setPlayable(true);
    setPlaybackDuration(res.end - res.start);
  }
}

// ;; startRecordBrowser  
// https://d6f47ebf168c8bac0d9048551a99512c-app.staging.1024paas.com null

// http://localhost:3010/ide/replay/664529280084164608/showmebug?showRRwebController=1
// daoPaasObj.preparePlaybackSync()
// 客户端request getPlaybackInfo
// 42 

const playbackInfo = [
  "playbackInfo",
  {
    "playbackSummerize": {
      "total": 49,
      "start": 1716261783156,
      "end": 1716261833013,
      "customize": []
    },
    "playbackData": {
      "playbackData": [{
          "_id": "664c1397e6ca87f076703709",
          "timestamp": 1716261783156,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "ide",
          "data": {
            "action": "REFRESH",
            "fileRootPath": "/app/data/codeZone/2024/3/5-21/@0d04a0b4-3799-4013-9c36-396fb6187ae9/source",
            "payload": {
              "path": ".",
              "name": ".",
              "type": "DIRECTORY",
              "children": [{
                  "type": "FILE",
                  "name": ".1024",
                  "path": ".1024",
                  "children": [],
                  "hide": false,
                  "lock": false,
                  "unittest": false,
                  "isRetainedFile": false
                },
                {
                  "type": "FILE",
                  "name": ".1024nix",
                  "path": ".1024nix",
                  "children": [],
                  "hide": false,
                  "lock": false,
                  "unittest": false,
                  "isRetainedFile": false
                },
                {
                  "type": "FILE",
                  "name": "bs-config.js",
                  "path": "bs-config.js",
                  "children": [],
                  "hide": false,
                  "lock": false,
                  "unittest": false,
                  "isRetainedFile": false
                },
                {
                  "type": "FILE",
                  "name": "index.html",
                  "path": "index.html",
                  "children": [],
                  "hide": false,
                  "lock": false,
                  "unittest": false,
                  "isRetainedFile": false
                }
              ]
            }
          },
          "__v": 0
        },
        {
          "_id": "664c139ae6ca87f07670370e",
          "timestamp": 1716261786399,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "console",
          "agentUserId": "backend",
          "data": {
            "value": "PaasNewLineSign"
          },
          "__v": 0
        },
        {
          "_id": "664c139ae6ca87f076703710",
          "timestamp": 1716261786402,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "PaasNewLineSign"
          },
          "__v": 0
        },
        {
          "_id": "664c139be6ca87f076703712",
          "timestamp": 1716261787595,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\u001b[?2004h"
          },
          "__v": 0
        },
        {
          "_id": "664c139be6ca87f076703714",
          "timestamp": 1716261787595,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "664c13a9e6ca87f076703717",
          "timestamp": 1716261801803,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Tree"
          },
          "__v": 0
        },
        {
          "_id": "664c13a9e6ca87f076703720",
          "timestamp": 1716261801852,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "bs-config.js"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13a9e6ca87f076703721",
          "timestamp": 1716261801853,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "bs-config.js"
          },
          "__v": 0
        },
        {
          "_id": "664c13aae6ca87f076703726",
          "timestamp": 1716261802455,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 2,
            "openedPath": "bs-config.js",
            "updates": [{
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "7ca399c6-8ecb-47e7-a642-f2c2543d5411",
          "__v": 0
        },
        {
          "_id": "664c13aae6ca87f076703731",
          "timestamp": 1716261802759,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "index.html"
          },
          "__v": 0
        },
        {
          "_id": "664c13aae6ca87f076703730",
          "timestamp": 1716261802759,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "index.html"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13abe6ca87f076703736",
          "timestamp": 1716261803225,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 2,
            "openedPath": "index.html",
            "updates": [{
                "changes": [
                  272
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 272,
                    "head": 272
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  272
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 272,
                    "head": 272
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "fb16b3c8-c750-444c-82ea-95f9115fb67e",
          "__v": 0
        },
        {
          "_id": "664c13ace6ca87f07670373e",
          "timestamp": 1716261804424,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "bs-config.js"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13ace6ca87f07670373f",
          "timestamp": 1716261804425,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "bs-config.js"
          },
          "__v": 0
        },
        {
          "_id": "664c13ace6ca87f076703744",
          "timestamp": 1716261804966,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 4,
            "openedPath": "bs-config.js",
            "updates": [{
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "dde48bc7-f187-45cb-85cd-0c2b8b799cb3",
          "__v": 0
        },
        {
          "_id": "664c13aee6ca87f07670374c",
          "timestamp": 1716261806523,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "index.html"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13aee6ca87f07670374d",
          "timestamp": 1716261806524,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "index.html"
          },
          "__v": 0
        },
        {
          "_id": "664c13aee6ca87f076703752",
          "timestamp": 1716261806996,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 4,
            "openedPath": "index.html",
            "updates": [{
                "changes": [
                  272
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 272,
                    "head": 272
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  272
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 272,
                    "head": 272
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "449af58f-0526-48d6-8cac-5fda47739bd4",
          "__v": 0
        },
        {
          "_id": "664c13b3e6ca87f076703755",
          "timestamp": 1716261811907,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 5,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                272
              ],
              "selection": {
                "ranges": [{
                  "anchor": 61,
                  "head": 61
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "48cc1bd7-48ff-4d5c-8cc4-97ae3f95a235",
          "__v": 0
        },
        {
          "_id": "664c13b4e6ca87f076703758",
          "timestamp": 1716261812100,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Editor"
          },
          "__v": 0
        },
        {
          "_id": "664c13b4e6ca87f07670375b",
          "timestamp": 1716261812373,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 6,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                61,
                [
                  0,
                  "",
                  "        "
                ],
                211
              ],
              "selection": {
                "ranges": [{
                  "anchor": 70,
                  "head": 70
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "b07546c6-926b-4fa6-b3ba-5f14434536ca",
          "__v": 0
        },
        {
          "_id": "664c13b5e6ca87f07670375d",
          "timestamp": 1716261813672,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 7,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                281
              ],
              "selection": {
                "ranges": [{
                  "anchor": 249,
                  "head": 249
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "b817119d-c166-4c77-9c9f-8677e79fad4a",
          "__v": 0
        },
        {
          "_id": "664c13b6e6ca87f07670375f",
          "timestamp": 1716261814006,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 8,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                249,
                [
                  0,
                  "",
                  "        "
                ],
                32
              ],
              "selection": {
                "ranges": [{
                  "anchor": 258,
                  "head": 258
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "140ff157-d6c1-496d-b870-0fbe8c592ca9",
          "__v": 0
        },
        {
          "_id": "664c13b6e6ca87f076703761",
          "timestamp": 1716261814861,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 9,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                258,
                [
                  0,
                  "c"
                ],
                32
              ],
              "selection": {
                "ranges": [{
                  "anchor": 259,
                  "head": 259
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "c77985cf-cde3-4ab9-b1b9-749078fb13fa",
          "__v": 0
        },
        {
          "_id": "664c13b7e6ca87f076703763",
          "timestamp": 1716261815161,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 10,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                259,
                [
                  0,
                  "onsole.log("
                ],
                32
              ],
              "selection": {
                "ranges": [{
                  "anchor": 270,
                  "head": 270
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "9efbc495-9cd9-4b64-9897-c67ae9bf099d",
          "__v": 0
        },
        {
          "_id": "664c13b7e6ca87f076703765",
          "timestamp": 1716261815967,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 11,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                270,
                [
                  0,
                  ")"
                ],
                32
              ],
              "selection": {
                "ranges": [{
                  "anchor": 271,
                  "head": 271
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "ec2728cb-28ce-43d8-a991-60329ea7750a",
          "__v": 0
        },
        {
          "_id": "664c13b8e6ca87f076703767",
          "timestamp": 1716261816550,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 12,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                303
              ],
              "selection": {
                "ranges": [{
                  "anchor": 270,
                  "head": 270
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "09b70d89-54b7-43e7-9400-66520f352ed0",
          "__v": 0
        },
        {
          "_id": "664c13b9e6ca87f076703769",
          "timestamp": 1716261817452,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 13,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                270,
                [
                  0,
                  "''"
                ],
                33
              ],
              "selection": {
                "ranges": [{
                  "anchor": 271,
                  "head": 271
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "875e0dfd-9ffb-4d25-b5ff-5b9656051361",
          "__v": 0
        },
        {
          "_id": "664c13b9e6ca87f07670376b",
          "timestamp": 1716261817958,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 14,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                271,
                [
                  0,
                  "a"
                ],
                34
              ],
              "selection": {
                "ranges": [{
                  "anchor": 272,
                  "head": 272
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "8ba26309-cc63-4393-8ff9-27d8214cc2ff",
          "__v": 0
        },
        {
          "_id": "664c13bae6ca87f07670376d",
          "timestamp": 1716261818258,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 15,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                272,
                [
                  0,
                  "a"
                ],
                34
              ],
              "selection": {
                "ranges": [{
                  "anchor": 273,
                  "head": 273
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "a10a2d66-f09a-4cad-8f92-261dcc11171c",
          "__v": 0
        },
        {
          "_id": "664c13bce6ca87f076703771",
          "timestamp": 1716261820277,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Tree"
          },
          "__v": 0
        },
        {
          "_id": "664c13bce6ca87f076703779",
          "timestamp": 1716261820326,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "bs-config.js"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13bce6ca87f07670377a",
          "timestamp": 1716261820327,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "bs-config.js"
          },
          "__v": 0
        },
        {
          "_id": "664c13bce6ca87f07670377f",
          "timestamp": 1716261820773,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 6,
            "openedPath": "bs-config.js",
            "updates": [{
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  2324
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2324,
                    "head": 2324
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "30680c65-61e8-48d2-bd47-dabf4a6b5f23",
          "__v": 0
        },
        {
          "_id": "664c13bee6ca87f076703781",
          "timestamp": 1716261822369,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 7,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2324,
                [
                  0,
                  "",
                  ""
                ]
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2325,
                  "head": 2325
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "cd8dec64-430d-4228-9ebb-bcf28bfc072a",
          "__v": 0
        },
        {
          "_id": "664c13c1e6ca87f076703783",
          "timestamp": 1716261825143,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 8,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2325,
                [
                  0,
                  "c"
                ]
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2326,
                  "head": 2326
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "b3a8d82c-f025-4bc7-a66b-2965938467bd",
          "__v": 0
        },
        {
          "_id": "664c13c1e6ca87f076703785",
          "timestamp": 1716261825701,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 9,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2326,
                [
                  0,
                  "onsole.log("
                ]
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2337,
                  "head": 2337
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "b85d43e8-9409-4442-b91a-e8bb0121b1ce",
          "__v": 0
        },
        {
          "_id": "664c13c2e6ca87f076703787",
          "timestamp": 1716261826480,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 10,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2337,
                [
                  0,
                  ")"
                ]
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2338,
                  "head": 2338
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "9be2f8da-400a-4570-87cf-4ab615ff36f6",
          "__v": 0
        },
        {
          "_id": "664c13c3e6ca87f076703789",
          "timestamp": 1716261827419,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 11,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2338
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2337,
                  "head": 2337
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "4573878a-5eca-4d76-953b-b4db179b11de",
          "__v": 0
        },
        {
          "_id": "664c13c3e6ca87f07670378b",
          "timestamp": 1716261827857,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 12,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2337,
                [
                  0,
                  "''"
                ],
                1
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2338,
                  "head": 2338
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "c54a6005-c77f-47de-bff4-0e746a25d4f3",
          "__v": 0
        },
        {
          "_id": "664c13c4e6ca87f07670378d",
          "timestamp": 1716261828448,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 13,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2338,
                [
                  0,
                  "b"
                ],
                2
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2339,
                  "head": 2339
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "f303e1c9-3de8-4234-a977-4a252571cc23",
          "__v": 0
        },
        {
          "_id": "664c13c4e6ca87f07670378f",
          "timestamp": 1716261828750,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 14,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2339,
                [
                  0,
                  "b"
                ],
                2
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2340,
                  "head": 2340
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "c7e34838-2958-44d7-a8a6-1a5d450977b0",
          "__v": 0
        },
        {
          "_id": "664c13c5e6ca87f076703791",
          "timestamp": 1716261829580,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 15,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2342
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2324,
                  "head": 2324
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "3cf06025-31c0-4d2c-a638-d476fb3a17f6",
          "__v": 0
        },
        {
          "_id": "664c13c5e6ca87f076703794",
          "timestamp": 1716261829770,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Editor"
          },
          "__v": 0
        },
        {
          "_id": "664c13c5e6ca87f076703797",
          "timestamp": 1716261829906,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 16,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2324,
                [
                  0,
                  "",
                  ""
                ],
                18
              ],
              "selection": {
                "ranges": [{
                  "anchor": 2325,
                  "head": 2325
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "4bf00752-cd3f-408a-8a41-29c2d2612d71",
          "__v": 0
        },
        {
          "_id": "664c13c8e6ca87f07670379b",
          "timestamp": 1716261832497,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Tree"
          },
          "__v": 0
        },
        {
          "_id": "664c13c8e6ca87f0767037a3",
          "timestamp": 1716261832554,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "fileTree",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "action": "FOCUS",
            "files": [{
              "type": "FILE",
              "name": "index.html"
            }]
          },
          "__v": 0
        },
        {
          "_id": "664c13c8e6ca87f0767037a4",
          "timestamp": 1716261832555,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "index.html"
          },
          "__v": 0
        },
        {
          "_id": "664c13c9e6ca87f0767037a9",
          "timestamp": 1716261833013,
          "playgroundId": "664529280084164608",
          "dockerId": "664529280126107648",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 17,
            "openedPath": "index.html",
            "updates": [{
                "changes": [
                  307
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 307,
                    "head": 307
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              },
              {
                "changes": [
                  307
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 273,
                    "head": 273
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "959cd8d9-be76-44c5-9610-010d6430809c",
          "__v": 0
        }
      ],
      "historyBaseData": [{
          "_id": "664c13a9636433ffb912046d",
          "dockerId": "664529280126107648",
          "path": "bs-config.js",
          "playgroundId": "664529280084164608",
          "__v": 0,
          "content": "// @see https://browsersync.io/docs/options/\nmodule.exports = {\n    // \"ui\": {\n    //     \"port\": 3001,\n    //     \"weinre\": {\n    //         \"port\": 8080\n    //     }\n    // },\n    \"files\": [\"**/*.css\", \"**/*.html\", \"**/*.js\"],\n    \"watchOptions\": {\n      ignore: '.*',\n      usePolling: true, // 开启轮询监听文件变化\n      interval: 200 // 轮询间隔ms\n    },\n    \"server\": {\n      // baseDir: \"src\"\n    },\n    // \"proxy\": false,\n    \"port\": 8080,\n    // \"middleware\": false,\n    // \"serveStatic\": [],\n    // \"ghostMode\": {\n    //     \"clicks\": true,\n    //     \"scroll\": true,\n    //     \"forms\": {\n    //         \"submit\": true,\n    //         \"inputs\": true,\n    //         \"toggles\": true\n    //     }\n    // },\n    // \"logLevel\": \"info\",\n    // \"logPrefix\": \"Browsersync\",\n    // \"logConnections\": false,\n    // \"logFileChanges\": true,\n    // \"logSnippet\": true,\n    // \"rewriteRules\": false,\n    \"open\": false,\n    // \"browser\": [\"google chrome\"],\n    // \"xip\": false,\n    // \"hostnameSuffix\": false,\n    // \"reloadOnRestart\": true,\n    \"notify\": false,\n    // \"scrollProportionally\": true,\n    // \"scrollThrottle\": 0,\n    // \"scrollRestoreTechnique\": \"window.name\",\n    // \"scrollElements\": [],\n    // \"scrollElementMapping\": [],\n    // \"reloadDelay\": 0,\n    // \"reloadDebounce\": 0,\n    // \"plugins\": [],\n    // \"injectChanges\": true,\n    // \"startPath\": null,\n    // \"minify\": true,\n    // \"host\": null,\n    // \"codeSync\": true,\n    // \"timestamps\": true,\n    // \"clientEvents\": [\n    //     \"scroll\",\n    //     \"scroll:element\",\n    //     \"input:text\",\n    //     \"input:toggles\",\n    //     \"form:submit\",\n    //     \"form:reset\",\n    //     \"click\"\n    // ],\n    // \"socket\": {\n    //     \"socketIoOptions\": {\n    //         \"log\": false\n    //     },\n    //     \"socketIoClientConfig\": {\n    //         \"reconnectionAttempts\": 50\n    //     },\n    //     \"path\": \"/browser-sync/socket.io\",\n    //     \"clientPath\": \"/browser-sync\",\n    //     \"namespace\": \"/browser-sync\",\n    //     \"clients\": {\n    //         \"heartbeatTimeout\": 5000\n    //     }\n    // },\n    // \"tagNames\": {\n    //     \"less\": \"link\",\n    //     \"scss\": \"link\",\n    //     \"css\": \"link\",\n    //     \"jpg\": \"img\",\n    //     \"jpeg\": \"img\",\n    //     \"png\": \"img\",\n    //     \"svg\": \"img\",\n    //     \"gif\": \"img\",\n    //     \"js\": \"script\"\n    // }\n};",
          "createTime": 1716261801845
        },
        {
          "_id": "664c13aa636433ffb912047b",
          "dockerId": "664529280126107648",
          "path": "index.html",
          "playgroundId": "664529280084164608",
          "__v": 0,
          "content": "<html>\n\n<head>\n    <style>\n    h1 {\n        font-size: 30px; \n        color: red;\n    }\n    </style>\n</head>\n\n<body style=\"background-color:white\">\n    <h1>Hello HTML/CSS/JS! Hot reload!</h1>\n    <script>\n        console.log('hello world!')\n    </script>\n</body>\n\n</html>\n",
          "createTime": 1716261802753
        }
      ]
    },
    "agentUsers": [{
        "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
        "userId": "661695283872350209",
        "userInfo": {
          "username": "king",
          "avatarUrl": "https://ui-avatars.com/api/?background=3A3C40&color=fff&rounded=true&uppercase=true&bold=true&length=1&name=king"
        },
        "fileOpened": "index.html",
        "status": "online",
        "followingAgentUserId": "",
        "focusComponent": "Tree",
        "focusXterm": null,
        "editorScroll": 0,
        "cursor": {},
        "wsClientID": "YQona0KWXQtJBRtvABtf",
        "color": "#3091F2"
      },
      {
        "agentUserId": "6e8f9905-1425-4295-8629-ac1307f6ef9f",
        "userId": "194e9365-4ae3-46fa-be09-a2753887328c",
        "userInfo": {
          "username": "king",
          "avatarUrl": "https://ui-avatars.com/api/?background=3A3C40&color=fff&rounded=true&uppercase=true&bold=true&length=1&name=king"
        },
        "status": "online",
        "followingAgentUserId": "",
        "focusComponent": null,
        "focusXterm": null,
        "editorScroll": 0,
        "cursor": {},
        "wsClientID": "i2LiXI_kHLo236lkABth",
        "color": "#5C5CE5"
      }
    ],
    "rrwebDataAllData": {
      "rrwebData": [],
      "customEvents": []
    }
  }
]
```

- 切换文件时
  - 会收到 ["selectedUpdated", {"mapSelection":{}, "path":"bs-config.js"}]

- 
- 
- 

### docs-sdk

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
