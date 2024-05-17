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
  - [ShowMeBug字节级回放在线笔面试过程实现思路 - 掘金 _202107](https://juejin.cn/post/6985068859099201544)

### not-yet

- paas平台为什么难以落地
  - 功能又多又杂
  - 侧重ai编辑，可以去掉非核心需求

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

### draft

- sdk的主要组件Editor/FileTree/Shell的渲染是独立的 `createRoot(dom).render(<Editor />)`; 

- 
- 
- 

### roadmap

- features-to-dev
  - 多文件打开
  - 多shell
  - 开发启动支持多port
  - 考虑2套agent: 前端agent, 后端agent，可切换来节省资源

- embed
  - 

#### maybe

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
- 
- 

#### replay

- roadmap
  - 回放时不支持预览视图
  - 支持多次编辑的snapshot数据

- not-yet ❓
  - recordBrowser参数似乎未使用

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

// http://localhost:3010/ide/replay/662725910453239808/showmebug?showRRwebController=1
// daoPaasObj.preparePlaybackSync()
// 客户端request getPlaybackInfo
// 42 

const playbackInfo = [
  "playbackInfo",
  {
    "playbackSummerize": {
      "total": 35,
      "start": 1715831830251,
      "end": 1715832045082,
      "customize": []
    },
    "playbackData": {
      "playbackData": [{
          "_id": "66458416e6ca87f076702c89",
          "timestamp": 1715831830251,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "fileTree",
          "agentUserId": "ide",
          "data": {
            "action": "REFRESH",
            "fileRootPath": "/app/data/codeZone/2024/3/5-16/@fad3d6d8-d302-4e29-9c2a-a02f9ca04026/source",
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
          "_id": "66458418e6ca87f076702c8e",
          "timestamp": 1715831832648,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "console",
          "agentUserId": "backend",
          "data": {
            "value": "PaasNewLineSign"
          },
          "__v": 0
        },
        {
          "_id": "66458418e6ca87f076702c8f",
          "timestamp": 1715831832649,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "PaasNewLineSign"
          },
          "__v": 0
        },
        {
          "_id": "66458419e6ca87f076702c92",
          "timestamp": 1715831833933,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\u001b[?2004h"
          },
          "__v": 0
        },
        {
          "_id": "66458419e6ca87f076702c94",
          "timestamp": 1715831833933,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "6645841fe6ca87f076702c96",
          "timestamp": 1715831839991,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\r\u001b[K\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "66458421e6ca87f076702c98",
          "timestamp": 1715831841336,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\r\u001b[K\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "66458422e6ca87f076702c9a",
          "timestamp": 1715831842894,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\r\u001b[K\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "66458439e6ca87f076702c9c",
          "timestamp": 1715831865818,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\r\u001b[K\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "66458485e6ca87f076702c9f",
          "timestamp": 1715831941702,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Tree"
          },
          "__v": 0
        },
        {
          "_id": "66458485e6ca87f076702ca9",
          "timestamp": 1715831941732,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "bs-config.js"
          },
          "__v": 0
        },
        {
          "_id": "66458485e6ca87f076702ca8",
          "timestamp": 1715831941732,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
          "_id": "66458486e6ca87f076702cae",
          "timestamp": 1715831942203,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
          "uuid": "d540235b-6196-44d1-8d22-2bc549f5390e",
          "__v": 0
        },
        {
          "_id": "66458487e6ca87f076702cb9",
          "timestamp": 1715831943182,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "index.html"
          },
          "__v": 0
        },
        {
          "_id": "66458487e6ca87f076702cb8",
          "timestamp": 1715831943182,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
          "_id": "66458487e6ca87f076702cbe",
          "timestamp": 1715831943640,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
                    "anchor": 71,
                    "head": 71
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "b9c7b9eb-e74b-4920-9df1-ed75aeda1d32",
          "__v": 0
        },
        {
          "_id": "66458498e6ca87f076702cc1",
          "timestamp": 1715831960139,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "terminal",
          "agentUserId": "backend",
          "data": {
            "value": "\r\u001b[K\u001b[01;34m~/app\u001b[00m$ "
          },
          "__v": 0
        },
        {
          "_id": "664584c6e6ca87f076702cc3",
          "timestamp": 1715832006370,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 3,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                272
              ],
              "selection": {
                "ranges": [{
                  "anchor": 35,
                  "head": 35
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "5dbf4085-0dcc-48af-83fa-55d1f2087b16",
          "__v": 0
        },
        {
          "_id": "664584c6e6ca87f076702cc6",
          "timestamp": 1715832006523,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Editor"
          },
          "__v": 0
        },
        {
          "_id": "664584dde6ca87f076702cca",
          "timestamp": 1715832029265,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
                  "anchor": 61,
                  "head": 61
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "6a4129fe-6a53-493d-9dbe-9c8a573eb558",
          "__v": 0
        },
        {
          "_id": "664584dee6ca87f076702ccc",
          "timestamp": 1715832030226,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 5,
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
          "uuid": "0837fce4-4113-40ab-bf9d-978b424deb25",
          "__v": 0
        },
        {
          "_id": "664584dee6ca87f076702cce",
          "timestamp": 1715832030775,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 6,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                62,
                [
                  8,
                  "",
                  "        "
                ],
                211
              ],
              "selection": {
                "ranges": [{
                  "anchor": 71,
                  "head": 71
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "ffa010a7-234b-4dea-9c2e-d32e0db31d33",
          "__v": 0
        },
        {
          "_id": "664584e1e6ca87f076702cd0",
          "timestamp": 1715832033339,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 7,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                282
              ],
              "selection": {
                "ranges": [{
                  "anchor": 250,
                  "head": 250
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "78d6a9ce-1399-406f-a63f-57e1d815c378",
          "__v": 0
        },
        {
          "_id": "664584e2e6ca87f076702cd2",
          "timestamp": 1715832034319,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 8,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                250,
                [
                  0,
                  "",
                  "        "
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
          "uuid": "5f5d6133-9231-4f9b-8450-f238835111da",
          "__v": 0
        },
        {
          "_id": "664584e3e6ca87f076702cd5",
          "timestamp": 1715832035412,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 9,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                259,
                [
                  0,
                  "c"
                ],
                32
              ],
              "selection": {
                "ranges": [{
                  "anchor": 260,
                  "head": 260
                }],
                "main": 0
              },
              "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
            }]
          },
          "uuid": "a70924fb-7ddd-489d-8b16-c1bd227a5164",
          "__v": 0
        },
        {
          "_id": "664584e3e6ca87f076702cd7",
          "timestamp": 1715832035884,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 10,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                260,
                [
                  0,
                  "onsole.log("
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
          "uuid": "94b69841-42d1-41b4-ac5a-c457006341d2",
          "__v": 0
        },
        {
          "_id": "664584e5e6ca87f076702cd9",
          "timestamp": 1715832037089,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 11,
            "openedPath": "index.html",
            "updates": [{
              "changes": [
                271,
                [
                  0,
                  ")"
                ],
                32
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
          "uuid": "1febf6e2-30f0-4f7f-ba17-4648bdd748a3",
          "__v": 0
        },
        {
          "_id": "664584e8e6ca87f076702cdd",
          "timestamp": 1715832040432,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "focusChange",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "componentName": "Tree"
          },
          "__v": 0
        },
        {
          "_id": "664584e8e6ca87f076702ce5",
          "timestamp": 1715832040450,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
          "_id": "664584e8e6ca87f076702ce6",
          "timestamp": 1715832040451,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "openedPath": "bs-config.js"
          },
          "__v": 0
        },
        {
          "_id": "664584e8e6ca87f076702ceb",
          "timestamp": 1715832040854,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
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
          "uuid": "9cb7a6a3-6793-4899-9e4b-5c0bbc6a8fae",
          "__v": 0
        },
        {
          "_id": "664584ebe6ca87f076702ced",
          "timestamp": 1715832043138,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 5,
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
          "uuid": "130e90dd-7426-4b6f-ac84-caca27a3e144",
          "__v": 0
        },
        {
          "_id": "664584ebe6ca87f076702cf3",
          "timestamp": 1715832043442,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 7,
            "openedPath": "bs-config.js",
            "updates": [{
                "changes": [
                  2325,
                  [
                    0,
                    "",
                    ""
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
              },
              {
                "changes": [
                  2326,
                  [
                    0,
                    "c"
                  ]
                ],
                "selection": {
                  "ranges": [{
                    "anchor": 2327,
                    "head": 2327
                  }],
                  "main": 0
                },
                "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea"
              }
            ]
          },
          "uuid": "096b9270-c9be-4cc4-9214-046a09a09e7e",
          "__v": 0
        },
        {
          "_id": "664584ebe6ca87f076702cf5",
          "timestamp": 1715832043910,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 8,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2327,
                [
                  0,
                  "onsole.log("
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
          "uuid": "e2401ff6-1e7e-40e5-95fe-5ae7183fc29b",
          "__v": 0
        },
        {
          "_id": "664584ede6ca87f076702cf7",
          "timestamp": 1715832045082,
          "playgroundId": "662725910453239808",
          "dockerId": "662725910495182848",
          "eventName": "editor",
          "agentUserId": "63ba7a74-e3d4-4efd-9558-0fdd47a2d3ea",
          "data": {
            "revision": 9,
            "openedPath": "bs-config.js",
            "updates": [{
              "changes": [
                2338,
                [
                  0,
                  ")"
                ]
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
          "uuid": "ea96f1b7-ccf0-4b42-b389-5dbec83eebf0",
          "__v": 0
        }
      ],
      "historyBaseData": [{
          "_id": "66458485636433ffb90f3d07",
          "dockerId": "662725910495182848",
          "path": "bs-config.js",
          "playgroundId": "662725910453239808",
          "__v": 0,
          "content": "// @see https://browsersync.io/docs/options/\nmodule.exports = {\n    // \"ui\": {\n    //     \"port\": 3001,\n    //     \"weinre\": {\n    //         \"port\": 8080\n    //     }\n    // },\n    \"files\": [\"**/*.css\", \"**/*.html\", \"**/*.js\"],\n    \"watchOptions\": {\n      ignore: '.*',\n      usePolling: true, // 开启轮询监听文件变化\n      interval: 200 // 轮询间隔ms\n    },\n    \"server\": {\n      // baseDir: \"src\"\n    },\n    // \"proxy\": false,\n    \"port\": 8080,\n    // \"middleware\": false,\n    // \"serveStatic\": [],\n    // \"ghostMode\": {\n    //     \"clicks\": true,\n    //     \"scroll\": true,\n    //     \"forms\": {\n    //         \"submit\": true,\n    //         \"inputs\": true,\n    //         \"toggles\": true\n    //     }\n    // },\n    // \"logLevel\": \"info\",\n    // \"logPrefix\": \"Browsersync\",\n    // \"logConnections\": false,\n    // \"logFileChanges\": true,\n    // \"logSnippet\": true,\n    // \"rewriteRules\": false,\n    \"open\": false,\n    // \"browser\": [\"google chrome\"],\n    // \"xip\": false,\n    // \"hostnameSuffix\": false,\n    // \"reloadOnRestart\": true,\n    \"notify\": false,\n    // \"scrollProportionally\": true,\n    // \"scrollThrottle\": 0,\n    // \"scrollRestoreTechnique\": \"window.name\",\n    // \"scrollElements\": [],\n    // \"scrollElementMapping\": [],\n    // \"reloadDelay\": 0,\n    // \"reloadDebounce\": 0,\n    // \"plugins\": [],\n    // \"injectChanges\": true,\n    // \"startPath\": null,\n    // \"minify\": true,\n    // \"host\": null,\n    // \"codeSync\": true,\n    // \"timestamps\": true,\n    // \"clientEvents\": [\n    //     \"scroll\",\n    //     \"scroll:element\",\n    //     \"input:text\",\n    //     \"input:toggles\",\n    //     \"form:submit\",\n    //     \"form:reset\",\n    //     \"click\"\n    // ],\n    // \"socket\": {\n    //     \"socketIoOptions\": {\n    //         \"log\": false\n    //     },\n    //     \"socketIoClientConfig\": {\n    //         \"reconnectionAttempts\": 50\n    //     },\n    //     \"path\": \"/browser-sync/socket.io\",\n    //     \"clientPath\": \"/browser-sync\",\n    //     \"namespace\": \"/browser-sync\",\n    //     \"clients\": {\n    //         \"heartbeatTimeout\": 5000\n    //     }\n    // },\n    // \"tagNames\": {\n    //     \"less\": \"link\",\n    //     \"scss\": \"link\",\n    //     \"css\": \"link\",\n    //     \"jpg\": \"img\",\n    //     \"jpeg\": \"img\",\n    //     \"png\": \"img\",\n    //     \"svg\": \"img\",\n    //     \"gif\": \"img\",\n    //     \"js\": \"script\"\n    // }\n};",
          "createTime": 1715831941725
        },
        {
          "_id": "66458487636433ffb90f3d16",
          "dockerId": "662725910495182848",
          "path": "index.html",
          "playgroundId": "662725910453239808",
          "__v": 0,
          "content": "<html>\n\n<head>\n    <style>\n    h1 {\n        font-size: 30px; \n        color: red;\n    }\n    </style>\n</head>\n\n<body style=\"background-color:white\">\n    <h1>Hello HTML/CSS/JS! Hot reload!</h1>\n    <script>\n        console.log('hello world!')\n    </script>\n</body>\n\n</html>\n",
          "createTime": 1715831943176
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
        "fileOpened": "bs-config.js",
        "status": "online",
        "followingAgentUserId": "",
        "focusComponent": "Tree",
        "focusXterm": null,
        "editorScroll": 0,
        "cursor": {},
        "wsClientID": "S7jW17KeCKn4rfNiABrD",
        "color": "#3091F2"
      },
      {
        "agentUserId": "6e8f9905-1425-4295-8629-ac1307f6ef9f",
        "userId": "194e9365-4ae3-46fa-be09-a2753887328c",
        "userInfo": {
          "username": "king",
          "avatarUrl": "https://ui-avatars.com/api/?background=3A3C40&color=fff&rounded=true&uppercase=true&bold=true&length=1&name=king"
        },
        "fileOpened": null,
        "status": "online",
        "followingAgentUserId": "",
        "focusComponent": null,
        "focusXterm": null,
        "editorScroll": 0,
        "cursor": {},
        "wsClientID": "rGC3Hlapfh762yA1ABrH",
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

#### FileTree

```JS
useEffect(() => {
  store.dao.channel().subscribeForComponent(Events.FileTree, {
    onStart: () => {
      actions.file.expandedFolders([]);
      setTreeData({});
      actions.file.setFileTree(null);
    },
    onData,
    getPlaybackSnapshot,
  });
}, [onData]);
```

- 切换文件时
  - 会收到 ["selectedUpdated", {"mapSelection":{}, "path":"bs-config.js"}]

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
