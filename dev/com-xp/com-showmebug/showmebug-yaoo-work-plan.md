---
title: showmebug-yaoo-work-plan
tags: [showmebug, work]
created: 2024-05-06T02:54:24.884Z
modified: 2024-05-06T02:54:40.374Z
---

# showmebug-yaoo-work-plan

# guide

# personal
- 工作OKR
  - 业务类: ai编程/pr/自动测试
  - 基建类: 基座工程、代码编辑器
  - 团队类: 测试、运营

- work-xp-pros
  - 产研团队的对齐非常充分
- work-xp-cons
  - 单人项目太多了，维护困难，比如paas和1024code，浪费了很多研发资源

- 研发流程
  - backlog > todo > doing(dev分支) > readyForTest(staging分支) > done
  - 研发负责添加任务，测试负责减少； review属于doing的开发或联调状态
  - 早会: 用户留存/研发排期, 研发质量, 技术专项
# projects

## proj-coding-ai

- develop环境：
  - paas url: https://develop.clackypaas.com
  - agent: https://develop.agent.clackyai.com/demo
  - backend: https://develop.api.clackyai.com
  - app: https://develop.app.clackyai.com
  - website: https://develop.clackyai.com
- staging:
  - paas url: https://staging.clackypaas.com
  - agent: https://staging.agent.clackyai.com/demo
  - backend: https://staging.api.clackyai.com
  - app: https://staging.app.clackyai.com
  - website: https://staging.clackyai.com

- 代码修改或变更的场景, 👀 不能以web系统的数据作为代码数据源，因为外部git系统、ssh、直接在命令行执行命令 也会修改文件内容
  - clacky-webapp操作代码仓库时只会记录当前系统的op
  - vscode-ssh连接代码仓库，操作op未记录
  - git clone + push 直接通过git协议操作代码仓库，操作op未记录
- 在code review或提交pr的场景， 经常需要git pull/rebase远程代码
  - 此时远程修改代码的op在本地无法获取
  - 🤔 变更文件列表必须以git仓库数据为唯一数据源，业务前端变成git的web客户端？

- agent初始化失败时，不影响页面上其他业务的正常使用

- 后端封装api的原因
  - 减少前端的需要传递的参数
  - 减少前端的请求数量
  - disable其他系统的鉴权

- 系统慢的原因
  - clerk认证的token是其他api的前置请求
  - paas 获取ide-server url的api也慢
  - ~~paas旧状态导致渲染异常~~

- 
- 

- resources
  - https://staging.agent.clacky.ai/demo

### draft

- 不支持自动重命名

- 端侧大模型辅助coding，如浏览器内置的ai-api

- docker in docker 的权限问题

- sdk有些文件代码有3000行，打开有点慢，但能忍受

### dev-log

- root-thread项目初始化时，cde环境会生成.1024start/.1024nix文件
  - 第2个thread创建时，若git fetch失败则fetch下来的代码就没有.1024nix文件，第2个thread的terminal就无法使用

- 底部面板的时光机显示隐藏动画
  - 思路1: 使用css transition修改transform
    - 若隐藏前后使用2个面板组件，则需要在动画结束后手动移除dom
  - 思路2: height先减为0再加为新内容高度
    - 可以只用1个面板组件，但效果可能不符设计稿
  - 减少layout计算，面板上方部分元素尽可能减少重绘
  - 动画要考虑进入场景和退出场景

### dev-summary

- 包管理使用apt而不是nix的原因
  - nix安装的包在bash无法检测到执行入口

- bcachefs换回btrfs，因为fork不稳定

- 一台宿主机上创建多个docker容器，实测隔离性不好
  - 采用vm的方案隔离得更彻底

- 
- 
- 

### codebase-collab 🔀

- ai工作时
- 对于新建文件的action类型
  - ai先打开空白文件，sdk前端发送syncOTUpdates，version-0
    - 收到响应latestRevision-0
  - ai改完后
    - sdk前端收到pullOTUpdates，latestRevision-1，
      - updates[0].changes[0]包含ai的修改，即新文件全部内容
      - updates.agentUserId 为 clacky
- 对于修改文件的action类型
  - ai先打开已存在的文件，sdk前端发送syncOTUpdates，version-0 🧐
    - 收到响应latestRevision-0
  - ai改完后
    - sdk前端收到pullOTUpdates，latestRevision-1，
      - updates[0].changes[0]包含ai的修改，即新文件全部内容，包含与
      - updates.agentUserId 为 clacky

- ai编辑文件比多人协同的场景更复杂的原因，ai会发送很多事件导致编辑器多次渲染

- ai执行action时前端收到的事件顺序，场景1，大多数执行流程是这种
  - onTaskUpdated wip
  - file-打开
  - pullOTUpdates
  - onTaskUpdated completed
  - ~~file-更新内容状态~~
- ai执行action时前端收到的事件顺序，场景2，这种流程也较多
  - onTaskUpdated wip
  - file-打开
  - pullOTUpdates
  - ~~file-更新内容状态~~
  - onTaskUpdated completed
- ai执行action时前端收到的事件顺序，场景3，很少
  - onTaskUpdated wip
  - file-打开
  - onTaskUpdated completed
  - pullOTUpdates
  - ~~file-更新内容状态~~
- ai执行action时前端收到的事件顺序，场景4，很少
  - onTaskUpdated wip
  - file-打开
  - ~~pullOTUpdates~~, 缺少了此事件
  - onTaskUpdated completed
  - ~~file-更新内容状态~~

```JS
[
  "pullOTUpdates",
  {
    "updates": [{
      "changes": [
        2,
        [
          0,
          "z"
        ],
        250
      ],
      "selection": {
        "ranges": [{
          "anchor": 3,
          "head": 3
        }],
        "main": 0
      },
      "agentUserId": "a9db200d-f439-4687-94c3-d905890baaae"
    }],
    "lastRevision": 51,
    "latestRevision": 52,
    "path": "README.md",
    "id": "c555f900-cb62-4e1b-9f2f-dac9dcbbed29",
    "mapSelection": {
      "a9db200d-f439-4687-94c3-d905890baaae": {
        "ranges": [{
          "anchor": 3,
          "head": 3
        }],
        "main": 0
      },
      "1f381fbe-d91e-46b5-ba5d-66511ebdb681": {
        "ranges": [{
          "anchor": 249,
          "head": 249
        }],
        "main": 0
      }
    }
  }
]
```

### ✨ feat-ai-writing-with-diff

- 打字动画的问题与优化方案
- 每行打字效果是从下向上的，体验不好
  - 调整打字动画的实现
- 对于某些类型的action如新增文件，跟随有明显延迟
  - 新增文件时，希望ai能尽快打开文件，而不是写完再打开

- 其他优化
  - 缓存diff视图的快照数据，不需要每次发起真实请求
  - 打开关闭diff视图不需要刷新文件

- 
- 
- 

- 时光机
  - ~~开启关闭diff视图, 配置在业务层~~
  - ~~切换diff视图的布局, 上下、左右，配置在业务层~~
  - ~~执行计划时计算diff-op，op的内容和时机~~
  - ~~回放~~模式获取diff-op
  - ~~回放~~模式支持编辑，内容和光标选区的变化
  - changed-files-list

- ai-coding的动画编码效果的技术方案
  - 不能使用纯css实现打字效果，css难以控制暂停继续，
    - 但符合ai按行写代码的主流实现方式, 且ai打字一般从左到右只打一遍
  - 思路1: 修改unifiedMergeView的源码，默认只渲染红色旧代码，新代码先通过decoration隐藏再通过逐个插入字符实现
  - 思路2: 逐个插入行, 插入行可以使用 line-decoration
  - 思路3: 绿色部分每一行默认折叠，然后依次展开
  - 其他思路
    - 先通过类似code-fold隐藏代码，当需要显示时，渲染打字机效果的文本
    - ~~不断传入newDoc，不断计算diff~~
  - 参考案例
    - folded-code也是隐藏代码的一种思路
    - 控制进度需要自动移动到下一个changedLine
- diff视图开启关闭动画的配置放在业务层还是state-field
  - 动画执行的进度可以放在state-field, 因为会随着editorState的更新而更新

- preOpenFile
  - 检查参数 diffMode, originalContent，newContent，title

- 技术实现确认0731
- 如何获取agent返回的修改后的代码并开始编辑
  - ~~agent切换并打开文件时，paas检查isAgentWriting，然后计算diff-op~~
  - ~~然后通过**类似**封装replayCodeByRange的modifyCode方法，以打字机的效果渲染diff，支持一次性将ai的修改全撤销~~
  - action进度条处于激活时，且用户打开了这个文件
- agent执行计划时，暂停播放后，停止在哪个字符
  - 暂停也是写全文
- 等待ai返回或计算diff很慢时，需要loading
  - 提示用户，限制大小
- 支持打开已删除的文件，显示diff
  - originalContent
- 如何判断op是来自ai还是真实用户，agentUserId
  - 由业务方判断，paas不关心agent
- 何时以及如何获取2个帧之间的所有op, 需要测试自定义帧
- 插入自定义帧的时机是执行计划或追加步骤开始前，存储十几个文件快照的数据量可能很大，确定要存吗
  - agent写代码时一个action一个自定义帧，数据量不大
  - 快照数据是否保存在historyBaseData更合理

- agent执行时，动态计算agent返回内容对应的op，渲染diff
  - 回放时，直接从ideServer获取op，渲染diff

- 由AI负责插入数据帧(考虑插入快照内容), 如果有新的action, 也是正常插入帧
  - 自定义事件帧可通过自定义eventName添加

- 快照文件什么时候显示
  - 只有追加步骤修改同一文件才显示只读的快照文件，否则显示可编辑的diff视图

- ai变更文件列表 不显示非计划内的文件更改

- 
- 
- 
- 

- 基于indexeddb存储编辑op的问题
  - 需要实现同步到其他协作者
  - 同步编辑op，计算plan时间段文件的全部改动
  - 新增删除文件的op
  - 同步进度

- indexeddb的存储逻辑放在业务层还是paas层
  - 业务层-pros
    - 可绕过paas直接与agent通信, agent > web > idb
  - 业务层-cons
    - 业务代码的复杂度会变高
  - paas层-pros
    - 与agent通信的逻辑会变复杂，业务触发action，接着 agent > ideServer > paas > web
  - paas层-cons
    - 部分通用性不强的功能不适合放在paas，不适合的如review评论，适合的如变更文件列表、diff

- 回放
  - 是否支持协同回放
  - 回放模式仅展示已完成的action，未完成的不展示，追加步骤的action会展示
  - 撤销后的文件要支持取消撤回
  - 撤销后的文件进度条上的action会变灰，取消撤回会变绿

- 是否要支持内部cde仓库的合并
  - git有冲突
  - crdt无冲突

- Editor
  - 切换diff视图的api

- 本地llm架构

- 
- 
- 
- 

#### 业务数据结构设计

- 业务操作
  - 撤销文件
  - 切换文件

- 协同编辑的数据结构
  - 目前基于ot
  - agent编辑、用户编辑
  - 用户编辑行号范围、agent编辑范围

- 操作op
  - 所属文档id，执行时间
  - 🤔 所属步骤，根据time确认

- 变更文件列表
  - 文件类型、文件名、文件路径、变更代码行数、操作类型、操作人头像和用户名

- paas现有持久化数据结构(mongodb的表)

```JS
// mongodb的historycrdts表存储编辑器、文件树的操作数据
[
  // custom event/frame
  {
    "_id": {
      "$oid": "66a9bdf2cc8eccde2db14a2e"
    },
    "data": {
      "action": "beforeSteps",
      "value": "steps1416",
      "uuid": "1722400242698"
    },
    "eventName": "customize",
    "playgroundId": "690273537138839552",
    "__v": 0,
    "agentUserId": "9cc647d3-e2f1-4dde-ae3b-8b97680b1ee7",
    "dockerId": "690273537168199680",
    "timestamp": 1722400242699
  },

  // delete file
  {
    "_id": {
      "$oid": "66ba003949c463e87f872df0"
    },
    "timestamp": 1723465785685,
    "playgroundId": "694744266697789440",
    "dockerId": "694744266731343872",
    "eventName": "fileTree",
    "agentUserId": "2d7317e4-ec19-4f27-b7bd-ba92b9750af4",
    "data": {
      "action": "DELETE",
      "files": [{
        "type": "FILE",
        "name": "hello.go"
      }],
      "fileRootId": "@dfbbaecc-27a0-4545-a986-c259e4a6ede0",
      "result": true
    },
    "__v": 0
  },

  // fileTree
  {
    "_id": {
      "$oid": "66a38107fabfd7026f68dfd8"
    },
    "timestamp": 1721991431081,
    "playgroundId": "688546823149174784",
    "dockerId": "688546823174340608",
    "eventName": "fileTree",
    "agentUserId": "ide",
    "data": {
      "action": "REFRESH",
      "fileRootPath": "/Users/yaoo/Documents/repos/com2024-showmebug/clacky-ai-paas-frontend/packages/server/apps/entry/test/filetree_mock",
      "url": "becbf0df199be859138c5a5d6778d595-app.develop.clackypaas.com",
      "payload": {
        "path": ".",
        "name": ".",
        "type": "DIRECTORY",
        "children": [{
            "type": "FILE",
            "name": "hello.c",
            "path": "hello.c",
            "children": [],
            "hide": false,
            "lock": false,
            "unittest": false,
            "isRetainedFile": false
          },
          {
            "type": "FILE",
            "name": "hello.go",
            "path": "hello.go",
            "children": [],
            "hide": false,
            "lock": false,
            "unittest": false,
            "isRetainedFile": false
          },
          {
            "type": "FILE",
            "name": "hello.rb",
            "path": "hello.rb",
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
          },
          {
            "type": "FILE",
            "name": "index.js",
            "path": "index.js",
            "children": [],
            "hide": false,
            "lock": false,
            "unittest": false,
            "isRetainedFile": false
          },
          {
            "type": "DIRECTORY",
            "name": "root",
            "path": "root",
            "children": [{
              "type": "FILE",
              "name": "1.txt",
              "path": "root/1.txt",
              "children": [],
              "hide": false,
              "lock": false,
              "unittest": false,
              "isRetainedFile": false
            }],
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

  // editor
  {
    "_id": {
      "$oid": "66a3840ffabfd7026f68dffa"
    },
    "timestamp": 1721992207807,
    "playgroundId": "688546823149174784",
    "dockerId": "688546823174340608",
    "eventName": "editor",
    "agentUserId": "9cc647d3-e2f1-4dde-ae3b-8b97680b1ee7",
    "data": {
      "openedPath": "index.html"
    },
    "__v": 0
  }

  // editor-
  {
    "_id": {
      "$oid": "66a38413fabfd7026f68e005"
    },
    "timestamp": 1721992211304,
    "playgroundId": "688546823149174784",
    "dockerId": "688546823174340608",
    "eventName": "editor",
    "agentUserId": "9cc647d3-e2f1-4dde-ae3b-8b97680b1ee7",
    "data": {
      "revision": 3,
      "openedPath": "index.html",
      "updates": [{
        "changes": [
          280
        ],
        "selection": {
          "ranges": [{
            "anchor": 109,
            "head": 109
          }],
          "main": 0
        },
        "agentUserId": "9cc647d3-e2f1-4dde-ae3b-8b97680b1ee7"
      }]
    },
    "uuid": "0340dc0b-ec3d-4294-b3d4-a1d407264621",
    "__v": 0
  }

  // focusChange
  {
    "_id": {
      "$oid": "66a38411fabfd7026f68e002"
    },
    "timestamp": 1721992209938,
    "playgroundId": "688546823149174784",
    "dockerId": "688546823174340608",
    "eventName": "focusChange",
    "agentUserId": "9cc647d3-e2f1-4dde-ae3b-8b97680b1ee7",
    "data": {
      // "componentName": "Editor"
      "componentName": "Tree"
    },
    "__v": 0
  }

]
```

### ✨ feat-时光机的任务执行

- 🤔 时光机打字动画的时机不采用pullOTUpdates事件的原因
  - pullOTUpdates事件虽然包含了用户id，但ai进行其他操作时顺便修改文件此时也会打开diff视图，而业务侧只想要ai在action对应的文件才打开打字动画(非计划内的文件不打开打字动画)，在业务侧难以控制和定制diff视图的打开时机
  - 多人协同时，其他用户编辑会影响diff-view的originalContent的值，没有使用稳定可靠的mongodb里的快照值
  - ot事件的触发频率过高，计算diff视图影响性能

- ai修改文件的逻辑20241216
  - 🚩 u<<all: taskUpdated, {'id': '2-1', 'title': 'Modify index.html to include progressbar.mjs script', 'action': <ActionType. MODIFY_FILE: 'modify_file'>, 'status': <ActionStatus. IN_PROGRESS_STATUS: 'in_progress'>, 'result': None
  - >>IDEserver: `file`, args=`{'path': 'index.html', 'timestamp': 1734337154, 'loadType': 'default', 'readOnly': False}`.
    - 可能会打开不存在的文件，对不存在的文件不需要打快照，但快照为空字符串时不影响
  - >>IDEserver: `appendCustomizeFrameData`, args=`{'action': 'snapshot_file', 'value': {'path': 'index.html', 'content': 
  - >>IDEserver: `queryCustomizeFrameData`, args=`{'action': 'snapshot_file', 'uuid': '41dba51a-42fa-4aa1-a501-bc7d81c93a61', 'value': {'path': 'index.html'}}`
  - >>IDEserver: `file`, args=`{'path': 'progressbar.mjs', 'timestamp': 1734337154, 'loadType': 'default', 'readOnly': True}`
    - 为什么会读取非本action的文件, readonly 静默打开不影响前端，是在读references
  - >>IDEserver: `agentWriteFile`, args=`{'path': 'index.html', 'content': 
  - >>IDEserver: `file`, args=`{'path': 'index.html', 'timestamp': 1734337158, 'loadType': 'default', 'readOnly': False}`
  - 🚩 u<<all: taskUpdated, {'id': '2-1', 'title': 'Modify index.html to include progressbar.mjs script', 'action': <ActionType. MODIFY_FILE: 'modify_file'>, 'status': <ActionStatus. COMPLETED_STATUS: 'completed'>, 
    - 为什么有时action的taskUpdated事件没了，还是在很后面?
  - 等2s
  - u<<all: taskStateUpdated, done

- 时光机的ui视觉只限制在底部面板，但有些逻辑不能只写在底部面板组件中
  - 自动打开隐藏底部时光机面板的逻辑必须写在组件之外，否则组件未render执行就不会自动打开隐藏
  - 时光机与侧边栏共享联动的状态也必须写在组件之外
  - 🧐 时光机相关的ui操作只局限在进度条，打开文件需要额外处理

- 引入task-engine的好处
  - 可细粒度控制打字动画的暂停和action执行的时序
  - 可单独控制回放的长度，不必回放全部action

- live模式下action的暂停与恢复
  - 完全由agent控制，agent在未执行完action时点暂停会将当前action视为未执行
  - 打字动画在暂停时会立即打完，当前action视为已执行
  - task状态变化 inited > planning > working > pausing > working > done/canceled/appended 
  - action状态变化 inited > in_progress > completed/abandoned/canceled

- playback模式下action的暂停与恢复
  - 完全由业务前端控制, 在未执行完action时点暂停会立即将该action执行完且暂停
  - 打字动画在暂停时会立即打完，当前action视为已执行
  - task状态变化 waitingActions为空时回放完成
  - action状态变化 running > played，按顺序执行
  - 回放时点击action会立即暂停到点击的action，然后更新waitingActions，不能清空否则丢失pause状态
  - 暂停后点播放会从下一个action开始播放

### ✨ feat-cmdk

- improve
  - migrate to StateField
  - cmdk-undo有时需要undo两次的逻辑可以通过传入参数定制 `history({joinToEvent: tr=>boolean})` 来实现

- 🚧 开发实现记录
  - reject后undo的流程通过 isCmdkDiffRejected 的 1/0/-1 三种状态控制，由于场景的特殊性，1/0不表示true/false，而是before/after
  - 在undo时输入框恢复正确位置可通过 tr.startState.field() 找到旧值，而不是tr.state
  - 快捷键ac/rj的逻辑不一定要import各种逻辑和文件，可以使用已有的dom事件， acceptBtn.click() 可直接触发已注册的事件，可在一定程度上通过dom对象减少实现的复杂度

- ✨ cmd+k， 主流程是用户输入需求，agent返回建议的代码
  - 对于不清晰的用户需求，cmd+k如何处理，需不需要澄清, ui交互是否要补充
  - agent工作编辑时是否禁用cmd+k快捷键
  - 用户点击下面的部分接受时，上面是否出现 accept selected数量，类似3/5
  - 部分accept的接受拒绝，和diff工具条同时出现吗？
  - 点击Stop停止生成后，仍保持diff视图，显示未写完的代码，此时accept是否显示消耗积分
  - 部分accept后，cmd+z回到原文件与最新文件的diff，还是回到原文件与agent返回的文件的diff视图
  - addToChat发送到驾驶舱的消息接口，agent做什么响应
  - 对话框消失后再显示需要恢复prompt吗
- cmd+k api需要支持 uRemakeFile, uStopRemakingFile, uRegenerateAlternative?
  - 需要单独发送selectedContent对应的代码字符串吗
  - accept/reject在前端给用户操作, 用户reject后agent需要知道吗，目前操作的粒度是全部
    - 由前端接受拒接且agent不需要知道， 修改粒度为每个变更块suggestedBlock
  - 追加修改需要新增单独的uFollowUpRemakeFile事件吗，追加的范围默认是上次修改的范围
    - 追加需要追加的提示词
  - 需要新增单独的uRegenerateAlternative的事件吗, 可以一次返回多个
  - regenerate是否需要切换回旧版代码的ui 
    - 暂时不做新的ui交互
  - sdk和前端的通信方式，弹出框如何让paas和agent通信

- cmd+k交互细节
  - diff内容滚动到窗口之外时，会作为悬浮框固定显示在顶部
  - 打字动画的diff，不会滚动页面
  - followup不是按钮，而是输入框

- diff工具条显示的条件时机和位置
  - regenerate 什么
  - edit
  - undo

## proj-idepaas-sdk

- resources
  - https://staging.1024paas.com/   (测试数据较多，api较稳定)
  - https://develop.1024paas.com/
  - https://www.1024paas.com/
  - https://app.apifox.com/project/3335675
  - [DaoPaaS API Options](https://www.1024paas.com/sdk/docs/index.html)
  - [1024PaaS-租户业务接口](https://apifox.com/apidoc/shared-c0c0ebad-15b3-4605-896e-e39879fe6e47/doc-952073)
  - https://staging.showmebug.com/  (帐号 01test)
  - [ShowMeBug字节级回放在线笔面试过程实现思路 - 掘金 _202107](https://juejin.cn/post/6985068859099201544)

- sdk设计参考
  - vscode, theia, opensumi, replit, codesandbox
  - [Running the SDK](https://cloud9-sdk.readme.io/docs/running-the-sdk)

### not-yet

- 

- 初始化cde时处理并发初始化的问题

- ❓ snapshot数据是如何存储的
  - 切换分支后的回放还能执行吗

- 回放的示例，暂停/继续播放的回调事件未生效
- 回放的示例，只打印了 onAvailable 事件
- 回放更适合纯前端实现? 
  - 纯前端的回放不支持协同调试，所以需要
- 回放要支持其他面板: terminal/browser

- 为什么不需要创建单独的回放编辑器
  - 回放时需要在快照的基础上支持直接编辑
- 回放及播放控制需要实现在服务端吗
  - 为了协同调试，需要

- 获取ticket的api未添加权限校验，header中没有token

- sdk的主要组件Editor/FileTree/Browser/Shell的渲染是独立的 `createRoot(dom).render(<Editor />)`; 

- editor
  - 支持多实例
  - 行级 code-comment
  - ai切换文件时，没有销毁中间层CodeEditor

- ❓ 为什么要将editorView对象挂在全局state的file下
  - actions.file.editorView(view)
- 如何复用idepaas-sdk的编辑器组件，一种思路是使用readonly版本

- fileTree
  - 大文件无法打开， 如package-lock.json
  - 文件树未实现懒加载， 点击时再请求文件夹的数据而不是一次请求整棵树
  - 部分文件再次打开光标会跳到文件尾
  - fileChangeLogs的变更列表无法区别修改删除
  - 搜索排除了node_modules目录吗
- ideServer无法检测并广播file-delete事件

- collab
  - 在有用户上下线时会全量广播当前协作的所有用户信息，存在数据量大且频次高的问题

- 跟随模式，假设用户A正在跟随用户B
  - 用户A自己切换文件时，头像仍停留在用户B的文件

- 
- 

#### bugs-in-prod

- 
- 

#### bugs-in-prod-unstable

- console有时渲染空白，大多数时候能正常渲染

- 
- 

### draft

- 
- 
- 
- 

- codemirror-themes

- 所有数据的通信都基于channel(websocket)?
  - 获取回放数据没必要用websocket，因为对实时性要求不高

- LSP的server迁移到worker的方案

- 给定仓库的url，类似 `/user/repo?task=desc`, 可以访问url查看ai创建pr的过程

- paas平台为什么难以落地
  - 功能又多又杂
  - 可以去掉非核心需求

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
  - 考虑2套agent: 前端agent, 后端agent，可切换来节省资源，类似apple的3级llm架构
  - 支持统一浏览器不同标签页打开不同ide

- 用一个程序监听所有客户端的文件写入导致的文件变化，会导致监听经常崩溃

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

- d42paas的 demo playgrounds 能否用 d42paas 的sdk实现
  - 用自己的平台开发代码

- preview react/vue components

- 持久化用户安装的包可以快速fork和复用，一个用户安装了，其他用户可直接用

- 
- 
- 

### dev-xp

- `d42paas_frontend` 项目启动记录
  - pnpm的版本必须是v9，不能是v8
  - cp .env.local.example .env, 可不修改任何配置，但修改配置中queue的名字可方便调试
  - cd packages/demo; pnpm dev
  - cd packages/server; pnpm dev
  - 修改 packages/server/apps/entry/test/filetree_mock_test 末尾文件名为 filetree_mock
  - 在 http://localhost:3010/ demo的用户名和手机号可随便写

- pros-paas 🌹
  - 在业务中使用时，可通过单独的playgroundId在demo页面进行测试，隔离性较好，且不影响业务
  - 后端业务通过tenantCode隔离，方便测试人员、agent组、其他项目组单独测试
  - 以websocket作为主要数据通信方式

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
  - 🔲 to-do
    - 播放进度条的中间节点支持显示预览画面
    - 播放时可并排显示多个shell的输出
    - 录制数据只能有一个用户，如果SMB需要跟随来回切换， 如果切换到面试官录制， 候选人只能停止录制

- paas平台的注册只需要name和任意secret就会返回token
  - 甚至校验时只需要ticket，不需要token

- 变更文件列表之前通过在服务端跑 `git status` 命令获取，但对服务器性能影响太大
  - 编辑器系统若支持外部命令行的git push/pull操作，则必须以git仓库数据作为唯一数据源，不能以web系统的数据作为代码数据源

- idepaas的打字机效果实现, 支持一次将ai的修改全撤销

- 🏠 paas的diff视图开启方式，通过配置属性diffConfig无法支持自身文件树打开时是否开启diff
  - 可将配置属性diffConfig变为配置方法detectDiff，这样支持文件树，还能在业务侧定制具体的开启细节和请求其他数据
  - 为了支持添加和取消，不建议初始化时传入配置，通过registerDetectDiff和unregister方法可以更灵活地实现

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

- 各视图组件都可以从全局状态中拿到socket状态 发送消息
  - store.dao.channel().send('updateAiCodeInfo', {})
  - store.dao.channel().send('syncOTUpdates', {})
- 各视图组件都可以从全局状态中拿到socket状态 注册事件
  - store.dao.channel().on('removeAiCodeInfo', cb)

#### LazyEditor/CodeEditor

- 三层editor结构
  - LazyEditor: 注册socket事件
  - CodeEditor: 计算content, 准备extensions， LSP
  - CodeMirrorEditor: 初始化codemirror, 设置menu, 不关心filePath

- CodeEditor 编辑器初始化时计算配置和插件，注册外部事件
  - CodeMirrorEditor(useCodeMirror) 编辑器初始化时注册各类菜单事件

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

#### playback ⌛️

- roadmap
  - 回放时~~不支持浏览器预览面板~~, showMeBug中基于rrweb实现浏览器预览面板的回放
  - 若操作op很多，则回放性能差。 考虑snapshot
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

// 插入自定义帧
const res: any = await daoPaasObj?.appendCustomizeFrameDataSync({
  action: 'startQuestion',
  value: id,
  uuid,
});
```

- 回放时，支持修改文件内容，但继续执行很可能失败
  - playback状态时，支持收集操作op

- [回放重构](https://www.notion.so/dao42/0ba448333b3f4740a6e569cefd40f821)
  - 回放的实现原理是sdk从服务端重新加载所有历史事件, 并分发给相应组件(在react项目中可以通过更新state来驱动各组件), 各组件接收到事件进行相应渲染
  - 对于大部分组件, 渲染时并不需要区分是否在回放模式, 只有可输入型组件需要在回放模式时禁止用户操作
  - 现在FileTree和Editor组件中直接注册事件, 不利于实现统一的回放消息重播. 故需要对Dao中的channel做出修改, 关闭on函数不允许组件自己注册事件. 统一由 MessageDispatcher 来分发事件
  - 有两种subscriber, 一种是播放控制组件的subscriber叫PlayControlSubscriber, 另一种是普通数据组件的subscriber叫 ComponentSubscriber
  - 可以在组件初始化时调用DaoPaaS的方法订阅相应的事件
- 新增浏览器协同和回放功能（RRWEB）v0.9.159

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
// 回放拖动卡顿的问题示例如下
// https://www.1024paas.com/ide/replay/672251935319277568/showmebug?showRRwebController=1

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

#### rrweb

- 跟随浏览器的交互基于rrweb实现
  - cde初始化时，syncPlaygroundInfo会包含 supportRRWeb: true
  - 点击跟随用户时，会发送 `followingAgentUser/liveBrowser` 2个事件， 然后收到following和followBrowser2个响应事件
    - 被跟随的用户会还收到liveBrowser事件
  - 跟随模式ui交互的鼠标和候选人名称渲染在iframe之外，跟随时的浏览器界面和内容不是原本iframe内的真实dom元素，而是渲染在iframe之外的`.replayer-wrapper canvas`元素
  - 小结: 跟随浏览器的feature不依赖浮动在浏览器面板之上的图标反而造成困惑，可以以后再联调rrweb的完整功能

#### browser

- 依赖ide-server的只有 followBrowser 事件
- 
- 
- 

#### fileTree

- 视图组件基于 react-complex-tree 的 ControlledTreeEnvironment 和 Tree 实现
  - renderItem定义在顶层

- 通过鼠标点击切换文件时会执行click事件的openFile()逻辑
  - 先设置跟随 store.dao.channel().followingFocusComponent('Tree'); 
  - setOpenPath(''); 
  - onSelectFileOrFolder([src]); + `onCustomSelect?.([src], type)`; 
  - setSelectedFilePath(items[0] as string); 
- 在useEffect里面，每次`selectedFilePath`变化，都会请求文件内容并更新编辑器(收到服务端的创建文件事件时也会这样)
  - channel.loadFile(selectedFilePath); 
  - actions.file.setDocLoading(true); 
  - this.send(Commands. File, { path }) 向ideServer请求文件内容
  - 当收到ideServer返回的文件内容时 this.socket.on(Events. File, 
  - switchFile(event.data) 更新 fileStore.doc
  - this.transitionFileInfo({ openedPath: event.data.openedPath }); 触发`fileInfo`事件到sdk前端
  - this.dispatchDataEvent('editor', event); 触发初始注册事件
  - 每次 fileStore.doc.openedPath 变化都会触发`CodeEditor`组件强制unmount再mount重渲染
  - `CodeEditor`在EditorView初始化完成后会执行 setEditorSelection，触发 `fileOpenDone` 事件

- 
- 
- 
- 
- 

### codebase-collab 🔀

- 

### codebase-ideServer 🔡

- init-dataflow 前提是sdk已经获取到ideServer的socket连接地址url了
  - AppService使用setInterval发送ideServerHeartBeat到manager
  - AppGateway初始化 new PlaygroundChannel(this.i18n, client, this.server)
  - AgentUserService
  - PlaygroundManagerService

- plyground支持切换容器环境
  - 切换时playgroundId不变，但fileRootPath和dockerId都可能变，dockerId名字取得不好它代表的是容器环境而不是docker
  - 容器失活后再激活，dockerId不会变

- playgroundLayer的设计是为了解决切换环境时通信中断的问题，
  - 方法是先在layer层更新数据，然后一次性更新playgroundItem的属性

- paas-sdk-client通过manager动态获取到ide-server的url，不是固定的
  - manager负责docker容器的管理和分配

- 什么时候用本地ide-server
  - 本地ide-server启动时会向manager注册id/code，manager收到sdk请求ide-server的url时，会检查code，若存在则返回本地ide-server连接ws://localhost:3012，否则返回线上ide-server连接
- 录制用户操作，什么时候开始
  - 整个playground的期间

- fileTree
  - playgroundItem.getPlaygroundInfo()
    - 直接使用playgroundItem.fileTree缓存，未做重新计算
  - registerFileTreeEvent
    - 每次都去构建文件树, 操作过重, 需要细分
- registerFileEvent
  - 若非大文件，读内容使用 await this.currentPlaygroundItem. FileTree_readFile( path, fileRootPath ); 
  - 打开文件时，便要初始化文件的基础信息写入数据库，用于回放
    - this.currentPlaygroundItem.playgroundHistoryCRDT.initialBaseFileByPath( path, { currentDoc } );
    - this.currentPlaygroundItem.playgroundHistoryCRDT.initCachedOTMap( path, loadType === 'refresh', { currentDoc }, );
  - OTInfo = await this.currentPlaygroundItem.playgroundHistoryCRDT.queryEditorOTInfoByPath( path, ); 
    - queryEditorOTInfoByPathFromCache
  - this.broadcastAll('file', { data:{ content: OTInfo.currentDoc } }, true); 

- PlaygroundChannel 监听getPlaybackInfo
  - 从mongodb表获取编辑操作数据 playgroundHistoryCRDT.loadAllData(); 
  - 获取代码文件数据 playgroundHistoryBase.findSourceByPlaygroundId()

- 🔊 mq通信逻辑
- 在收到manager发过来的playgroundInfo事件时，ideServer会缓存部分状态如console/terminal-history，对发给前端的业务数据用的是先缓存再更新的逻辑然后发给前端
  - this.playgroundLayerMap.set(playgroundInfo.dockerId, layer); 
  - await layer.updatePlaygroundInfo(playgroundInfo); 
  - this.playgroundItem.consumerLayer(data.dockerId); 
  - this.playgroundItemInfo = cloneDeep(layer.playgroundItemInfo); 
- 在playground未创建时，通信使用toManager
  - 在playground创建后，通信使用toPlayground

- Events. ForceRefreshFile
  - const isFileExist = await this.currentPlaygroundItem.checkIfThePathExists(
  - if (!isFileExist), not exist
  - let OTInfo = this.currentPlaygroundItem.playgroundHistoryCRDT.queryEditorOTInfoByPathFromCache( path, ); 
  - if (fileByte / (1024 * 1024) >= 16), this.transmit('file', fileJson); largeSuffix = 'd42.large'
  - this.broadcastAll('file', fileJson, true); 

- 
- 
- 
- 
- 
- 
- 

#### not-yet

- ideServer对于文件树的crud操作没有用类似chokidar的方式实现，而是直接使用node.fs操作或依赖外部事件来更新，是什么原因
  - 20250217: goAgent在移动文件到子文件夹后，git stash导致文件消失，golang的fsnotify无法捕获子文件夹的文件变更，变更事件只包含非移动文件的变更
  - 思路1: ideServer自身移动文件后，立即touch moved-file.md让其他监听系统能监听到事件
  - 思路2: ideServer自身移动文件后，手动通知manager/goAgent变化的路径，让监听方自己去更新
  - NFS自身没有监听文件变更的能力，需要依赖第三方

- 
- 
- 
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
  - [1024Code](https://1024code.com/)
  - [1024Code 文档中心](https://docs.1024code.com/)

### not-yet

- questions
  - /ide路由的 CloudIDEPage组件没有在react-devtools显示出来, 因为懒加载？ 

- 前端项目在打开ide时没有实现运行预览，需要手动点击运行

- 在ide中修改文件后，更新预览太慢

### draft

### dev-xp

- `1024code` 注册时要先点击发送验证码，然后在验证码输入框填入6个0就可以注册成功
  - 已注册用户可直接在发送验证码后输入6个0
  - ⚠️ node版本不支持v22，暂时使用v20
  - 编译构建时可通过修改repo文件夹名来避免使用turborepo的cache

### codebase

- init-app-dataflow
  - StoreProvider > createStore
    - new CodecubeStore
    - 初始化socket连接，基于rails-action-cable
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

- OpenAIStream
  - new ReadableStream

```JS
// stream response (SSE) from OpenAI may be fragmented into multiple chunks
// this ensures we properly read chunks and invoke an event for each SSE event stream
const parser = createParser(onParse);
// https://web.dev/streams/#asynchronous-iteration
for await (const chunk of res.body as any) {
  parser.feed(decoder.decode(chunk));
}
```

- 左侧图标菜单: fileTree, search, git
  - ActivityPane: 左侧图标菜单对应的面板
  - .tree-section
- Editor: 编辑区 .editor-section
  - EditorPane > `CodeEditor`; 
- Preview: 预览区
  - OpenBrowser
  - Terminal
  - Console

- web项目中的编辑器
  - apps/web/src/store/IDEStore.tsx  接入了daoPaas状态
  - apps/web/src/ui/MarkdownEditor/index.tsx
  - apps/web/src/ui/Codecubes/hooks/AtEditor/index.tsx
  - apps/web/src/pages/community/publish/AtEditor/index.tsx

- ai聊天是输出的代码使用highlightjs高亮
- 
- 
- 
