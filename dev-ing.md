---
title: dev-ing
tags: [dev, dev-log, dev-xp]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# guide
- 分析核心需求和问题，拆分需求，梳理任务、子任务，排期开发
金瑶 邀请您加入【金瑶的个人会议室】
点击链接直接加入腾讯会议：
https://meeting.tencent.com/p/9606972663
#腾讯会议：960-697-2663

# dev-summary
- module/fwk/server: 灵活的tag/bookmark系统, cms, tables, bi
- 编辑器参考
  - https://atlaskit.atlassian.com/packages/editor/editor-core
  - https://atlaskit.atlassian.com/examples/editor/editor-core/kitchen-sink
  - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-minimal
  - https://atlaskit.atlassian.com/packages/editor/editor-core/example/full-page-with-toolbar
  - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - more-editor
    - https://demo.grammarly.com/

- editor-play
  - https://ckeditor.com/docs/ckeditor5/latest/examples/builds-custom/full-featured-editor.html
  - https://prosemirror.net/examples/
    - https://tiptap.dev/docs/examples/basics/default-text-editor
  - https://codemirror.net/try/
  - https://www.slatejs.org/
  - https://quilljs.com/playground/snow
  - https://playground.lexical.dev/

- code-play
  - https://microsoft.github.io/monaco-editor/playground.html
  - https://play.tailwindcss.com/
  - https://streamlit.io/playground
  - https://arktype.io/playground
  - https://developer.mozilla.org/en-US/play
  - https://play.jqlang.org/
  - https://editor.swagger.io/
  - https://lit.dev/playground/
  - https://playground.solidjs.com/
  - https://angular.dev/playground

- lang-play
  - https://www.typescriptlang.org/play/
  - https://go.dev/play/
  - https://play.rust-lang.org/
  - https://play.kotlinlang.org/
  - https://playground.babylonjs.com/

- ai-play
  - https://www.ibm.com/granite/playground
  - https://playground.liquid.ai/chat
  - https://huggingface.co/chat/
  - https://huggingface.co/playground

- ai-deep-research
  - chat: openai, gemini, mistral, qwen, glm

- play-examples
  - https://playground.powerbi.com/en-us/
# dev-review

```shell
# delete all node_modules folders recursively
rm package-lock.json
find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + && find . -name 'dist' -type d -prune -exec rm -rf '{}' + && find . -name '.next' -type d -prune -exec rm -rf '{}' +
# maybe prefix sudo
find . -name 'node_modules' -type d -prune -exec rm -rf '{}' + 
# 格式化当前包，注意在子文件夹执行命令也会从package.json目录开始格式化整个包
prettier --write '**/*.{js,jsx,ts,tsx,json}' --ignore-unknown
eslint --ext .js,.ts,.tsx --quiet --fix . 
# npm i
  DEBUG=* npm i --no-audit --loglevel silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly
DEBUG=* npm i --legacy-peer-deps --no-audit --loglevel=silly --registry=https://registry.npmmirror.com
npm --registry=https://registry.npmmirror.com install   axios
yarn add axios --registry=https://registry.npmjs.org/  
pnpm install --loglevel=debug --registry=https://registry.npmmirror.com  
export https_proxy=http://127.0.0.1:7890;export http_proxy=http://127.0.0.1:7890;export all_proxy=socks5://127.0.0.1:7890
$$('[contenteditable]')
# 先打开一次discord确保下载了更新
flatpak run com.discordapp.Discord --proxy-server="socks5://127.0.0.1:7897"
betterdiscordctl -i flatpak install
npx create-strapi@latest --ts --use-npm --git-init  --example --skip-cloud --skip-db    --quickstart ./emptyFolder
vite --host 0.0.0.0 --port 8080
serve -p 9000 --cors
HOST=0.0.0.0 PORT=8080 react-scripts start
next dev -H 0.0.0.0 -p 3000
```

- dev-goals 不能在产品中检验的技术不玩，注意产品化
  - rich-editor: text/block, vanillajs
  - pivot-table: editable
  - collaboration, local-first database
  - flowchart/whiteboard/pdf/annotation/comment
  - 事项--截止日期(0730+休整)--重要性(h/m/l/s1-s3)
- deep into lib/fwk 书籍原理与代码实践要分开, 寻找深入debug的状态, learn-by-debug
  - 学习巩固: 实践练习 > 源码/示例 > 文档/论坛 > 社交分享
  - 不要从一个想法开始，而是从一个真正的问题开始
  - src-code, issues, pr, forks, extensions/alternatives
  - storage, sync/partial, conflicts, consistency
  - 直接根据具体框架或产品搜索解决方案如 airtable-database，不必拘泥于通用方案如event-sourcing/eav, 在产品讨论中常有细节和ideas
  - 解决方案在npm/docker也可以搜到，且更准确; 多关注包管理器上的最新的包
  - github package.json 也能搜索示例
  - 拆分核心内容和周边功能
    - split git-src and issues/pr/wiki, split txt/docx/xlsx and api
    - 将更多精力投入 core content 的创作，以及格式兼容、平台兼容、产品集成
  - 不必执着于vanillajs，常用模式早晚会抽象出工具库或框架，如reactive/effect/ajax/undo
# dev-2026-方向+方法+时间
- 👉🏻 output: 代码产出、产品落地、生态积累
- long-term-support
  - cms, airtable, pdf, lowcode/workflow/auto, drive
- techstack-to
  - async/generator, stream, buffer, binary, scheduler, arrow
  - 样式片段也可在线尝试: codepen, w3schools.com 
- separate storage compute example
  - `Lovefield` uses a plug-in architecture for data stores. All data stores implement `lf.BackStore` interface so that query engine can be decoupled from actual storage technology.
- cache/stream for web storage
  - 参考 tanstack-query, falcor, localforage
- 🤔 支持切换内存和异步数据源的示例
  - tanstack-table external data; ag-grid server-side row model
  - abstract-level, localforage
  - tupledb, tinybase
  - tiddlywiki, react-admin
  - service worker, falcor
- collab-sync, partial-sync
  - string-crdt: ? list-crdt
  - logux: sqlite-persistence, lww-with-hlc
  - verdant/lo-fi: hlc + websocket, no-merkle
  - harika: hlc + sqlite + absurd-sql, no-merkle
  - jaredly/local-first: hlc + rga
  - evolu: hlc + merkle + worker
  - automerge: hypermerge
  - remoteStorage: google-drive、网盘、七牛对象存储
  - 使用hlc: idbsidesync, verdant, harika
  - 结合hlc+crdt: idbsidesync, evolu, rga-crdt
  - 结合hlc+db: piratedb, tinybase, kappa-db-stream, linvodb
  - hypercore: partial-sync
- undo/redo与branching可拆分实现
  - undo与versioning/history基于persistent data structure
  - branching与merge可在应用层实现
  - 多个branching可通过structural sharing共享数据结构
- ui: headless-architecture
  - state + action: 参考autocomplete、search-ui
- headless组件是否表明react将view与logic耦合在一起封装为component的思路是错误的?
  - 与view视图无关的component本身就是个简单的函数或eventemitter-pattern
- 若slate-model层采用扁平化Node(扁平化的思路可参考event-sourcing/orm/tinybase)
  - 如何保持path和key同步，参考 getKeysToPathsTable, getByKey实现上基于getByPath
  - 优化方向可参考tree的crud及协作
  - 协作时还应该考虑 json patch + last-write-win
  - Node定义采用ast, 如 unist
  - lww的字符串改为针对crdt优化的类型
- flat-data-model的示例
  - frontend/in-memory database，如rxdb/pouchdb/tupledb
  - 还可以参考indexeddb相关示例，如dexie
  - sqlite-react: vlcn-orm
  - ast如何扁平化
  - 参考案例: tree、react-admin
- 内容的存储与更新如何与数据库集成
  - 编辑器内容自动保存一般通过在onChange方法中执行saveToDB
    - 也可以在onChange方法中创建内存db、更新索引，通过索引提高计算效率
    - 应该避免维护2份数据
  - 将编辑器的计算密集部分的数据模型不使用普通json对象，而直接用类似数据库模型的设计
  - 为了性能，尽量不要直接读写持久化数据源，要使用缓存object pool
- why use es6 class
  - 运行时类型检查，instanceof
    - 业内主流方案是zod/valibot
  - 既包含类型定义，又包含逻辑工具方法
    - 注意class有时也采用先定义interface再实现，此时ts type也合理了
    - 但应用层业务代码一般不需要定义单独interface
  - 方便调试，可直接log到对象及方法，函数里面的闭包变量更新难以定位
    - 也可提前将需要调试的属性或方法添加到闭包暴露的对象或window上
    - 闭包实现的私有属性更安全
- dev-xp-editor
  - 不仅要保持编辑器内容和视图同步，还要保持选区和内容同步
  - 编辑器外部相关面板的协同产品较少，如评论

## ing

- yaoo-proj
  - ~~prosemirror/codemirror + comfyui~~
  - ~~codemirror-devtools~~
- not-yet
  - ~~elmesque-editor~~, 基于immutable思想实现的编辑器大多采用redux/elm风格
  - branching/versioned-doc
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - 做完tailwind-table就面试
- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
# dev-01

```log //dev-xp
console.log('; ; task ', taskState, runningTaskAction, task?.task_steps)
^((?!(42\["heartbeat|resourceMonit|refreshXtermCols)).)*$
^(?!42\["resourceMonit).* 
/syncUpdates|syncOTUpdates/

```
```log //ai
- provide a brief overview of reactjs in less than 90 words
- provide a brief overview of reactjs with hello world code example
- count from 1 to 80, every number on a separate line
- count from zz1 to zz40, every item on a separate line  /no_think
- when did deepseek v3.1 model release?
- when did qwen3-coder model release?
- what's the weather in guangzhou china? give me some food and outdoor-activities suggestions according to weather temperature
- what's the dom api compatibility in common browsers

- explain code at ./playground/quick-sort.js
- for file ./playground/quick-sort.js, add a simple test case

- image-lawn
  - a big park for resting and relaxing, there are little trees around a big lawn, some birds are resting in the lawn, The lawn and the trees around it both need pruning
- image-logo-excel-like
  - create a product logo for my excel-like webapp, 
  - the logo brand color should be like green/teal/indigo/..., or any good color that giving a cold and formal feeling, 
  - the logo should express rows or columns or grid, but logo should not be complicated,
add action to add datetime at top of readme.md
add action to create quickSort1.mjs and try to implement quick sort algorithm in less than 60 lines
<!-- 🛝 -->
use vanilla html/css/javascript to create a simplistic personal profile landing page: homepage shows a big welcoming greeting, then shows 2 example personal projects, then a simple get in touch example email below it
use vanilla html/css/javascript to create a personal profile landing page: homepage shows a cool welcoming animation, then shows 4 example personal projects, then a simple get in touch form below it
use react to create a homepage shows a list of frontend frameworks like react/vue/angular, when clicking the framework, navigate to the route to show its introduction

- You are a professional python/typescript/nodejs fullstack developer.
  - provide a comprehensive overview of this project. analyze the project architecture and primary user journey use cases. then find some important source code to explain the core architecture and data flow.
  - i want more details about rag ingest/chunking/embedding/persistence logic
  - how to refactor related source code to support more vector db including qdrant/chromadb/pgvector? show me some code and explain the architecture migration

- You are a professional python/typescript/nodejs fullstack developer and a system administrator.
  - I want to run this project fully locally without docker and nginx for local development and debugging.
  - please read setup-related files like docker-compose.yaml and README.md, and tell me step by step how to configure and run frontend/backend locally.
  - i have already installed python/uv/npm/chromadb/Ollama/postgresql/mysql/redis on my local macos.
  - just tell me steps and commands to set up backend/frontend, i will start services like db/redis later.

- 你是一个专业且友善的 AI 助手。你的回应应该： 1. 使用简体中文回答 2. 当需要展示代码时，使用适当的语法高亮（如 typescript, python, javascript 等） 3. 当需要解释复杂概念时，可以使用 Mermaid 图表 4. 当涉及数学公式时，使用 LaTeX 语法 5. 保持回应简洁明确，适时使用列表和表格来组织信息. 
  - 请按以上要求介绍reactjs前端框架

- the northwinds excel contains the sales data for a company called Northwind Traders, which imports and exports specialty foods from around the world. 
  - The sales team wants to identify for which month they perform well and bad in 2014.
  - please give me the result with tables and plots

```

- [guide : running gpt-oss with llama.cpp · ggml-org/llama.cpp · Discussion _202508](https://github.com/ggml-org/llama.cpp/discussions/15396)

```sh /llm

ollama run --verbose gemma3:4b
OLLAMA_DEBUG=2 ollama serve gemma3:4b

# llama-server -m model.gguf --port 8080 --alias name

./build/bin/llama-server -m ~/.lmstudio/models/ 

# llama-cli -m model.gguf -cnv --chat-template chatml

./build/bin/llama-cli -m ~/.lmstudio/models/mradermacher/merged-mermaid-7b-GGUF/merged-mermaid-7b. Q6_K.gguf
llama-cli -hf ggml-org/gemma-3-1b-it-GGUF

VLLM_LOGGING_LEVEL=debug VLLM_CONFIGURE_LOGGING=1 vllm serve RUC-DataLab/DeepAnalyze-8B --max-num-batched-tokens 40000 --max-model-len 28000 --enable-log-requests --enable-log-outputs --enable-prompt-tokens-details --uvicorn-log-level debug 

```

```sh /image
cd ~/Documents/opt/compiled/zimage && ./ZImageCLI -m mzbac/Z-Image-Turbo-8bit -o ~/Pictures/test11.png -W 512 -H 512 -s 7 -p "一位帅哥和他的宠物狗穿着配套的服装参加狗狗秀节目，室内灯光，背景中有观众。"

cd ~/Documents/opt/compiled/zimage && ./ZImageCLI -m mzbac/Z-Image-Turbo-8bit -o ~/Pictures/test11.png -W 1024 -H 1024 -s 9 -p "
```

- goal-to 增强特色
  - editor
  - crud
  - 业务系统与架构增强: lasuite-docs, knowledgebase, cms

- dev-log
  - ?
- dev-to
  - ?

## 0106

- i want to run ocr llm model locally. why does llama.cpp not support deepseek-ocr gguf, but ollama supports deepseek-ocr since ollama uses llama.cpp under the hood? 
- [Ollama's new engine for multimodal models · Ollama Blog _202505](https://ollama.com/blog/multimodal-models)
  - Ollama has so far relied on the ggml-org/llama.cpp project for model support and has instead focused on ease of use and model portability.
  - As more multimodal models are released by major research labs, the task of supporting these models the way Ollama intends became more and more challenging.
  - We set out to support a new engine that makes multimodal models first-class citizens, and getting Ollama’s partners to contribute more directly to the community via the GGML tensor library.
  - Today, ggml/llama.cpp offers first-class support for text-only models. For multimodal systems, however, the text decoder and vision encoder are split into separate models and executed independently. Passing image embeddings from the vision model into the text model therefore demands model-specific logic in the orchestration layer that can break specific model implementations.
  - Within Ollama, each model is fully self-contained and can expose its own projection layer, aligned with how that model was trained. This isolation lets model creators implement and ship their code without patching multiple files or adding cascading if statements. They no longer need to understand a shared multimodal projection function or worry about breaking other models—they can focus solely on their own model and its training.

## 0104

- 🤔 https://huggingface.co/datalab-to/chandra this model uses [OpenRAIL ](https://huggingface.co/blog/open_rail) license. if i use this model locally on ocr saas webapp, is it free to use? is OpenRAIL license commercial friendly? 
  - 此问题deepseek回答无法访问网页而拒绝，gemini/grok/chat-glm幻觉，chatgpt询问是否要fetch license文件的内容因而最准确
  - https://huggingface.co/datalab-to/chandra/blob/main/LICENSE
  - check the exact OpenRAIL variant and its prohibited-use clauses. OpenRAIL licenses are explicitly designed to permit reuse, distribution and commercialization of models while adding responsibility / prohibited-use rules.
  - it’s a Modified OpenRAIL-M license, with explicit restrictions
  - Attachment A - USE RESTRICTIONS
    - Commercial and broader use licenses may be available from Licensor
    - for any purpose if You (your employer, or the entity you are affiliated with) generated/raised more than two million US Dollars

- 65风格发言指的是什么
  - “65风格发言”源自中国 CS: GO（反恐精英） 圈子，特指知名主播QUQU的老板/队友 B65（人称B哥、65）的说话方式。
  - 要掌握或识别“真正的65风格”，你需要抓住以下几个核心要素：极度的自信、独特的口头禅、对“游戏理解”的自我吹捧，以及一种“老板”特有的指点江山的气质。
  - 真正的65风格离不开这几个词，如果缺少了它们，就没有那个味儿： 
  - “常规”：这是65风格的灵魂。无论做什么操作（哪怕是白给），都要说是“常规操作”。
  - “顶级”：形容自己的意识、道具或枪法。
  - “理解”：指游戏阅读能力。
  - “满昏”：即“满分”，口音梗。
  - “甚至”：用来递进吹嘘自己的操作。
  - “拿下”：表示胜利或击杀。
