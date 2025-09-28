---
title: dev-ing
tags: [dev, dev-log, dev-xp]
created: 2022-05-24T17:52:58.048Z
modified: 2022-05-24T17:53:08.400Z
---

# dev-ing

# guide
- 分析核心需求和问题，拆分问题，梳理任务、子任务，排期开发
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
# dev-2025-方向+方法+时间
- 👉🏻 output: 代码产出、产品落地、生态积累
- eg-tanstack-table-v8
  - [ ] 方便接入已有的外部数据源
  - [x] 内存数据: nedb, blinkdb
  - [x] 流式数据: linvodb, tingodb; 可参考kappa架构
  - 支持内存和持久化: tupledb, tinybase, tiddlywiki
- db-sync/collab
  - db+crdt的参考: piratedb, evolu, triplitdb, mithic
    - 不必执着于基于indexeddb的实现，只是作为一种持久化的方式
  - base: level/rocksdb/foundationdb, hypercore, ipfs, kappadb
  - sqlite: rust_sqlite, extension
  - pouchdb: doc-db, incremental view
  - crsqlite, hypermerge: crdt + db
  - triplitdb: crdt + tupledb + eav
  - fireproof: ipld, live-sync, replication, branching-prolly-tree
  - tinybase: reactive
  - kappa + lsm => kdtree/r-tree
  - 基于oplog的研发方向, 架构设计时考虑放在数据库层解决还是应用层解决
    - 实现db，还是sourcing based framework
    - 基于log能提升write性能，基于materialized-view能提升read性能
    - 基于oplog实现partial-sync
  - pijul: crdt + vcs
- long-term-support
  - cms, airtable, lowcode
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
  - prosemirror/codemirror + comfyui
  - ~~codemirror-devtools~~
- not-yet
  - ~~elmesque-editor~~, 基于immutable思想实现的编辑器大多采用redux/elm风格
  - branching/versioned-doc
  - pouchdb + kappa-crdt + eav => pouchdb-crdt-eav
  - 做完tailwind-table就面试
- dev-to 提炼核心`需求+产出`工作流，不能在产品中检验的技术不玩
# dev-09
- dev-log
  - ?
- dev-to
  - ?
 
```log //dev-xp
console.log('; ; task ', taskState, runningTaskAction, task?.task_steps)
^((?!(42\["heartbeat|resourceMonit|refreshXtermCols)).)*$
^(?!42\["resourceMonit).* 
/syncUpdates|syncOTUpdates/

```
```log //ai
- give an brief intro to reactjs in less than 90 words
- when did deepseek v3.1 model release?
- when did qwen3-coder model release?
- what's the weather in guangzhou china? give me some food and outdoor-activities suggestions according to weather temperature
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
```

## 0928

- [Why am I getting a permission denied error for schema public on pgAdmin 4? - Stack Overflow](https://stackoverflow.com/questions/67276391/why-am-i-getting-a-permission-denied-error-for-schema-public-on-pgadmin-4)
  - ✅ ALTER DATABASE my_database OWNER TO my_database_user; 
  - GRANT USAGE ON SCHEMA public TO your_user; 

- [PGError: ERROR: source database "template1" is being accessed by other users - Stack Overflow](https://stackoverflow.com/questions/4977171/pgerror-error-source-database-template1-is-being-accessed-by-other-users)
  - `CREATE DATABASE` works by copying an existing database. PostgreSQL won't let you copy a database if another session is connected to it. If `template1` is being accessed by other users, CREATE DATABASE will fail.
  - The question you need to answer: Why are other sessions connected to template1?
  - At the point you initialize a database cluster, template0 and template1 are the same. if you add the procedural langauge PL/python to template1, every database you create later will include PL/python.
  - The database template0 is intended to be a "virgin" template. It should contain only standard database objects--the ones created by initializing the cluster. As a "virgin" template, it should never be changed. Never.
  - 💡 Solution: Restart posgres service.

## 0924

- [Diff syntax highlighting in Github Markdown - Stack Overflow](https://stackoverflow.com/questions/40883421/diff-syntax-highlighting-in-github-markdown)

```diff
public class Hello1
{
   public static void Main()
   {
-      System.Console.WriteLine("Hello, World!");
+      System.Console.WriteLine("Rock all night long!");
   }
}
```

## 0923

- authentik + https://github.com/authts/react-oidc-contex
  - Access to fetch at 'http://localhost:9000/application/o/aktest3000/.well-known/openid-configuration' from origin 'http://localhost:3001' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.

## 0922

- what's the filesystem for macos, ntfs or xfs ?
  - `diskutil info /` will show `File System Personality:   APFS`, Protocol: Apple Fabric.
  - APFS — default since macOS High Sierra(10.13/2017 and later) for SSDs and for most modern macOS (supports snapshots, cloning, encryption, space sharing).
  - HFS+ (Mac OS Extended, Journaled) — older macOS used this (spinning HDDs / legacy systems).
  - exFAT / FAT32 — supported both read/write by macOS and Windows; good for cross-platform external drives.
- ext4 (Fourth Extended Filesystem)
  - Commonly used as the default filesystem for general-purpose storage on Linux systems.
  - Supports large files (up to 16 TB) and file systems (up to 1 exabyte).
- XFS (eXtensible Filesystem)
  - Designed for high performance and scalability.
  - Supports very large files (up to 8 exabytes) and file systems (up to 16 exabytes).
  - Copy-on-write for metadata operations (improves performance and data integrity).
- Unix/BSD: May use UFS, ZFS, or other filesystems, but not ext4/XFS by default.
- [GNU make - Options Summary](https://ftp.gnu.org/old-gnu/Manuals/make-3.79.1/html_node/make_93.html)
  - `-C dir ` / `--directory=dir` Change to directory dir before reading the makefiles.

## 0920

- [Add cli switch to show generation time and tokens/sec output time · Issue · ollama/ollama](https://github.com/ollama/ollama/issues/1806)
  - ollama run qwen3 --verbose
  - it'll dump the token counts and timing info after each message.
- [Error: EACCES: permission denied, mkdir '/usr/local/lib/node\_modules/node-sass/build' - Stack Overflow](https://stackoverflow.com/questions/49679808/error-eacces-permission-denied-mkdir-usr-local-lib-node-modules-node-sass-b)
  - [EACCES: permission denied in VS Code MAC - Stack Overflow](https://stackoverflow.com/questions/38980338/eacces-permission-denied-in-vs-code-mac)
  - sudo chown -R $(whoami) .
  - 最后采用的方法是手动在 .bashrc/.zshrc 设置 `TMPDIR` 的值

## 0919

- 🤔 for a laptop, gpu vs apu vs npu
- Laptops can feature two types of GPUs: integrated, which is built into the central processing unit (CPU), and discrete, which is a separate, more powerful chip.
- GPU (discrete GPU) — a separate, much more powerful processor for parallel work (gaming, graphics, heavy ML training/inference).
- APU — a CPU with an integrated GPU on the same chip (AMD coined the term). 
  - AMD's marketing term for a CPU that has a powerful integrated GPU on the same chip.
  - Good for everyday use, much better battery/thermals than a discrete GPU, ok for light gaming and GPU-accelerated web/dev tasks. 
- NPU (Neural Processing Unit) — a specialized accelerator (also called AI accelerator or “Neural Engine”) built to run neural networks efficiently on-device. 
  - Extremely power-efficient and fast for inference, but not as general-purpose as a GPU. 
  - Common in smartphone and modern SoC designs (Apple, some Intel/Android SoCs).
  - Apple’s Neural Engine (M1/M2 chips), Intel Meteor Lake AI Accelerators, or AMD Ryzen AI.
- 💡 [Cline + LM Studio: the local coding stack with Qwen3 Coder 30B - Cline Blog _202508](https://cline.bot/blog/local-models)
  - 🧩 KV Cache Quantization: Leave unchecked. The KV cache setting is important. While it can be an optimization for some processes, it will persist context between tasks and create unpredictable behavior. Keep it off for consistent performance.
  - You can now run Cline completely offline.
  - LM Studio provides the runtime, Qwen3 Coder 30B provides the intelligence, and Cline orchestrates the work
  - Qwen3 Coder 30B, especially in its optimized MLX format on Apple Silicon, delivers performance that's genuinely useful for real coding tasks. The model brings 256k native context, strong tool-use capabilities, and repository-scale understanding.
  - Combined with Cline's compact prompt system (designed specifically for local models at 10% the length), you get an agent that can handle substantial coding tasks without ever touching the cloud.
  - Choose the right quantization depending on your hardware. For my 36B RAM Mac, this meant the 4-bit quantized model
  - In Cline's settings, select LM Studio as your provider and qwen/qwen3-coder-30b as your model. Don't set a custom base URL if you're using the default local endpoint.
  - Match your context window to LM Studio's setting: 262, 144 tokens. This gives you maximum working space for large repositories and complex tasks.
  - Enable "Use compact prompt." This is crucial for local models. The compact prompt is roughly 10% the size of Cline's full system prompt, making it much more efficient for local inference. The tradeoff is that you lose access to MCP tools, Focus Chain, and MTP features, but you gain a streamlined experience optimized for local performance.
  - Qwen3 Coder 30B performs well on modern laptops, especially Apple Silicon machines. The MLX optimization makes inference surprisingly fast for a 30B parameter model.
  - Large context ingestion will slow down over time -- this is inherent to long-context inference. If you're working with massive repositories, consider breaking work into phases or reducing the context window.
  - If the model seems unresponsive, confirm "Use compact prompt" is enabled in Cline and "KV Cache Quantization" is disabled in LM Studio. These settings are critical for proper operation.
  - If performance degrades during long sessions, try reducing the context window by half or reloading the model in LM Studio. Very long contexts can strain local inference.
- [LLMLoadModelConfig | LM Studio Docs](https://lmstudio.ai/docs/typescript/api-reference/llm-load-model-config)
  - `llamaKCacheQuantizationType`: Quantization type for the Llama model's key cache. 
    - This option determines the precision level used to store the key component of the attention mechanism's cache. 
    - Lower precision values (e.g., 4-bit or 8-bit quantization) significantly reduce memory usage during inference but may slightly impact output quality. 
    - The effect varies between different models, with some being more robust to quantization than others.
    - Set to `false` to disable quantization and use full precision.
  - `llamaVCacheQuantizationType`: Quantization type for the Llama model's value cache.
    - Similar to the key cache quantization, this option controls the precision used for the value component of the attention mechanism's cache. Reducing precision saves memory but may affect generation quality. 
    - This option requires Flash Attention to be enabled to function properly.

## 0918

- [What does YMMV mean? : r/TooAfraidToAsk](https://www.reddit.com/r/TooAfraidToAsk/comments/bhzxqc/what_does_ymmv_mean/)
  - YMMV. also ymmv. written abbreviation for `your mileage may vary`: used, for example on social media and in text messages and emails, to mean that you understand people may have a different opinion or experience to yours: Their first album is better, but of course YMMV.

## 0917

- 🧩 [MLX Quantization · ml-explore/mlx-lm](https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/LEARNED_QUANTS.md)
  - To reduce the quality loss from quantization MLX LM has several options:
  - DWQ(Distilled Weight Quantization) fine-tunes non-quantized parameters (including quantization scales and biases) using the non-quantized model as a teacher.
  - AWQ(Activation-aware Weight Quantization) scales and clips the weights prior to quantization. 
  - Dynamic quantization estimates the sensitivity of a model's outputs to each layer and uses a higher precision for layers which have higher sensitivity. 
  - GPTQ(GPT Quantization) finds quantized weights which minimize the squared error of each layer's output given the provided input.
- Dynamic quantization is the fastest to run. 
  - DWQ takes longer but typically yields better results.
- DWQ (Distilled Weight Quantization): 
  - This method is more complex. By using the original, larger model as a "teacher, " it fine-tunes the smaller, quantized model to behave more like its powerful predecessor. 
  - This often results in a model that retains more of the original's nuance and accuracy, even at a lower bit-rate. 
  - The goal is to get closer to the performance of a less quantized model while keeping the file size small.
- AWQ (Activation-aware Weight Quantization): 
  - This method is more direct. It intelligently analyzes which weights are most important for the model's performance and protects them during the quantization process. 
  - It's a very effective and efficient way to reduce model size without a catastrophic loss in quality, focusing on preserving the most critical parts of the model's "knowledge."
  - AWQ is designed for hardware efficiency and faster inference, making it suitable for resource-constrained environments . However, it may require adjustments (e.g., reducing max-model-len or using enforce-eager mode) to avoid OOM errors on limited VRAM 
- 🤔👾 i want to download llm in lm studio to use it on my mac with 32GB unified RAM. 
  - for a model like qwen3-32b, which quant should i use: Q6_K_S, Q4_K_S, Q4_K_M, Q4_K_L, Q3_K_L, Q3_K_M ?
  - which model is faster with good quality ?

## 0912

- 英译中:  Qwen is excellent. I wish they had a version with reasoning. “Reasoning” seems like mostly smoke and mirrors to me.
  - "smoke and mirrors"采用意译"故弄玄虚"，既保留原比喻意象又确保中文读者理解
  - 也可翻译为: 虚有其表
- [Make changes to node_modules files with patch-package - DEV Community](https://dev.to/roshangm1/make-changes-to-nodemodule-files-with-patch-package-30h4)
  - Track the patch files in git `git add patches/*`

## 0911

- a ULID is 26 characters long. 
  - The first 10 characters encode the timestamp (48-bit, milliseconds since Unix epoch) in Crockford Base32; Timestamp resolution: milliseconds.
  - the remaining 16 characters are 80 bits of randomness/entropy. 
  - Total bits: 128 bits = 48 bits timestamp + 80 bits randomness.
  - That layout is what makes ULIDs both globally unique and lexicographically sortable by creation time.
- 10 chars × 5 bits/char = 50 bits are used for the timestamp field (the top 2 bits are unused for typical 48-bit timestamps).
  - Crockford Base32: 0123456789ABCDEFGHJKMNPQRSTVWXYZ (no I, L, O, U to avoid confusion). Case-insensitive, but uppercase is canonical.

## 0910

- `q4ks` and `q4km` are shorthand for the specific GGUF (Georgi Gerganov Universal Format) quantization applied to the model.
  - q4: This indicates that the model has been quantized to 4-bit precision. Quantization is a process that reduces the memory footprint and computational cost of a model by representing its weights with fewer bits.
  - k: This refers to the "k-quant" method. It's a more advanced quantization technique compared to older legacy methods.
- "s" for small and "m" for medium, denote the specific variant of the k-quant method used. The primary difference between them lies in how they handle different layers within the neural network. 
  - The `q4_k_m` version typically uses a higher precision (like 6-bit) for some of the more important layers of the model, such as the attention and feed-forward network layers, while the rest of the layers are quantized to 4-bit.
  - In contrast, the `q4_k_s` version is more uniformly quantized to 4-bit across all layers, making it slightly smaller but with a greater potential for quality degradation.
  - `q4_k_m` is generally the superior choice as it offers a better-balanced quantization, preserving more of the model's original accuracy and reasoning capabilities

## 0909

- what does zero-shot mean in the text embedding model leaderboard below?
  - On the Massive Text Embedding Benchmark (MTEB) leaderboard, the term "zero-shot" refers to a model's ability to perform tasks on datasets it has not been explicitly trained on. It serves as a crucial indicator of a model's true generalization capabilities, moving beyond performance on familiar data.
  - In general, zero-shot learning refers to a model's ability to handle tasks involving categories or classes it hasn't seen during training—without requiring additional task-specific fine-tuning or labeled examples
  - In MTEB, "zero-shot" indicates the model is being assessed on tasks that it hasn’t been fine-tuned for.

## 0905

- [How to print out a dictionary nicely in Python? - Stack Overflow](https://stackoverflow.com/questions/44689546/how-to-print-out-a-dictionary-nicely-in-python)
  - print(json.dumps(dictionary, indent=4, sort_keys=True))

## 0904

- Sync Settings: Error: error: gpg failed to sign the data: [GNUPG:] KEY_CONSIDERED 1C4A85B3737F 2 [GNUPG:] BEGIN_SIGNING H10 [GNUPG:] PINENTRY_LAUNCHED 65844 curses 1.3.1 not a tty - - ? 501/20 0 gpg: signing failed: No such file or directory [GNUPG:] FAILURE sign 83918929 gpg: signing failed: No such file or directory fatal: failed to write commit object
  - 变通的解决方案是，commit前手动将 `~/.gitconfig`文件中 `commit.gpgsign` 改为false, commit后再改回true

## 0902

- 下面是一个有异常的curl脚本，异常位置是包含单引号的`what's`

```sh
curl http://localhost:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-coder-30b",
    "messages": [
      { "role": "system", "content": "append important Chinese history events around the date." },
      { "role": "user", "content": "What's the date today?" }
    ],
    "temperature": 0.7,
    "max_tokens": -1,
    "stream": false
}'
```

- ai改了几遍都没改对
  - 由于整个 JSON 被包裹在 Shell 单引号中，反斜杠（\）被视为字面量字符，而不是转义字符。
  - 因此，JSON 实际接收到的内容是 What\'s the date today?，其中包含无效的转义序列 \'。
  - JSON 解析器遇到 \' 时会报错，因为 JSON 标准只允许特定的转义序列（如 \"、\\ 等），而 \' 不是其中之一。这导致 cURL 请求失败。
  - 解决方案 B 使用 What\'s，这在 Shell 的单引号字符串中会被视为字面量反斜杠和单引号，导致 JSON 中包含无效的转义序列 \'。JSON 标准不允许 \' 作为转义序列（有效的转义序列是 \"、\\ 等），因此 JSON 解析失败。

```sh
# solution B 
curl http://localhost:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-coder-30b",
    "messages": [
      { "role": "system", "content": "append important Chinese history events around the date." },
      👇 若写在.sh文件中作为脚本执行时可以有#注释，但copy到terminal执行执行时不能有#注释
      { "role": "user", "content": "What'\''s the date today?" }  # 注意内部单引号的转义
    ],
    "temperature": 0.7,
    "max_tokens": -1,
    "stream": false
}'
```

- 在执行命令前，可以使用 `echo` 命令预览 Shell 实际解析的内容：
  - 解决方案 A 使用 What'\''s，这是 Shell 中在单引号字符串内嵌入单引号的正确方式。它通过退出单引号模式、插入转义的单引号（\'），然后重新进入单引号模式来确保 JSON 内容正确。
  - In POSIX shells (bash, zsh) a single-quoted literal starts with `'` and ends with the next `'`. Inside those single quotes nothing is special — backslash has no escape meaning. To include a single-quote character (') in a single-quoted string you must close the quote, put an escaped single-quote, then re-open the quote.
  - In ZSH (and Bash), when you want to include a single quote within a single-quoted string, you need to end the single-quoted string, add an escaped single quote (`\'`), and then start a new single-quoted string.
  - 如果 JSON 较复杂，考虑使用 `Heredoc` 或临时文件来避免 Shell 转义问题

```sh
# 💡 echo后的内容可以直接copy执行 ✅
# solution A
echo curl http://localhost:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-coder-30b",
    "messages": [
      { "role": "system", "content": "append important Chinese history events around the date." },
      { "role": "user", "content": "What'\''s the date today?" }
    ],
    "temperature": 0.7,
    "max_tokens": -1,
    "stream": false
}'
```

## 0901

- The most popular model is ChatGPT. The second most popular model is Claude
- 🆚 what's different between the following 2 models? what does awq mean? 
  - [mlx-community/DeepSeek-Coder-V2-Lite-Instruct-4bit-AWQ · Hugging Face](https://huggingface.co/mlx-community/DeepSeek-Coder-V2-Lite-Instruct-4bit-AWQ) 
  - [mlx-community/DeepSeek-Coder-V2-Lite-Instruct-4bit-mlx · Hugging Face](https://huggingface.co/mlx-community/DeepSeek-Coder-V2-Lite-Instruct-4bit-mlx)
- TL; DR: the two repos are the same base model converted to MLX format with different quantization settings/tools.
  - …4bit-AWQ was quantized with AWQ (Activation-Aware Weight Quantization) and includes explicit AWQ calibration parameters (group-size, embed-bits, etc.)
  - 4bit-mlx is a 4-bit MLX conversion made with an earlier mlx-lm converter (default MLX quantization), without the AWQ-specific calibration notes
- AWQ = Activation-Aware Weight Quantization. It’s a 4-bit weight-only quantization method that tries to keep the important weights (and account for activation magnitudes) so model quality drops much less than naive 4-bit quantization. In practice AWQ aims for near-FP16 quality at 4 bits by using activation-aware scaling and targeted preservation/calibration.
  - 强调通过 AWQ 技术在低比特（4-bit）下保持较高精度。
- 🤔 when i download …4bit-mlx-like model, I can use it instantly in LM Studio without configuration 
  - if i download …4bit-AWQ-like model in LM Studio, is it required to config the awq parameters explicitly? if yes, how can i configure it in LM Studio?
- usually no — you don’t need to type AWQ flags into LM Studio.
  - AWQ hyper-parameters (--group-size, --embed-bits, --num-samples, etc.) are conversion-time settings used by the quantizer (mlx-lm / autoawq) and are baked into the MLX quantized files. LM Studio ships an MLX engine and will load MLX/AWQ quantized models directly using the quantization data stored in the model
  - so in normal cases you can drop the …4bit-AWQ MLX model into LM Studio and run it without manually re-entering AWQ params.
- LM Studio is designed to automatically detect and handle AWQ-quantized models without requiring manual parameter configuration
# dev-08-mirror-editor-upgrade-&-aisdk-&-comfyui-upscale/anime-&-comfyui-examples

## 0831

- [Cannot find module 'librechat-data-provider' · danny-avila/LibreChat _202505](https://github.com/danny-avila/LibreChat/discussions/7416)
  - 🐛 Failed to resolve entry for package "@librechat/client"
  - Try running what the commands do manually. Please note any errors at any step.
  - I ran `npm run frontend` first which built the `librechat-data-provider` component and that seemed to fix the error on my system.
  - 实测多次碰到vite编译子项目时部分子包编译失败而未生成`dist`目录，此时按依赖顺序手动在子包执行 `npm run build` ，可以让项目运行成功
- [Why does "npm install" rewrite package-lock.json? - Stack Overflow](https://stackoverflow.com/questions/45022048/why-does-npm-install-rewrite-package-lock-json)
  - `npm install` honors package-lock.json only if it satisfies the requirements of package.json.
  - If it doesn't satisfy those requirements, packages are updated & package-lock is overwritten.
  - If you want the install to fail instead of overwriting package-lock when this happens, use `npm ci`.

## 0828

- [openrouter的Gemini 2.5 Pro Preview调用报错 - 开发调优 - LINUX DO _202504](https://linux.do/t/topic/536770)
  - (Google AI Studio) Provider returned error: {"error":{"code":400, "status":"FAILED_PRECONDITION"}}
  - 换成美国节点试试，谷歌限制地区

## 0826

- [convolution_overrideable not implemented. · Issue · comfyanonymous/ComfyUI _202401](https://github.com/comfyanonymous/ComfyUI/issues/2532)
  - I checked the dimensions of my original drawing and realized it was too big, when I changed it to the dimensions recommended by the model, I didn't have that problem anymore
  - I have tried different python version(3.10, 3.11, 3.12) met same problem as here. but when I reduce the size of image, will pass the VAE Encode and success.

## 0821

- [Huggingface docs - Understand caching](https://huggingface.co/docs/huggingface_hub/en/guides/manage-cache)
  - huggingface_hub utilizes the local disk as two caches, which avoid re-downloading items again. 
  - The first cache is a file-based cache, which caches individual files downloaded from the Hub and ensures that the same file is not downloaded again when a repo gets updated. 
  - The second cache is a chunk cache, where each chunk represents a byte range from a file and ensures that chunks that are shared across files are only downloaded once.
  - The Hugging Face Hub cache-system is designed to be the central cache shared across libraries that depend on the Hub.
  - File-based caching: The default `<CACHE_DIR>` is `~/.cache/huggingface/hub`. 
  - In order to have an efficient cache-system, huggingface-hub uses symlinks. However, symlinks are not supported on all machines. This is a known limitation especially on Windows. 
  - Chunk-based caching (Xet): hf_xet adds a `xet` directory to the existing huggingface_hub cache, creating additional caching layer to enable chunk-based deduplication
    - located at `~/.cache/huggingface/xet` by default, contains two caches, utilized for uploads and downloads.
    - This cache holds chunks (immutable byte ranges of files ~64KB in size) and shards (a data structure that maps files to chunks). 
    - `chunk-cache` contains cached data chunks that are used to speed up downloads.
    - `shard-cache` contains cached shards that are utilized on the upload path.
    - `staging` is a workspace designed to support resumable uploads.
    - The `chunk_cache` is limited to 10GB in size while the `shard_cache` has a soft limit of 4GB. 
  - If you need to reclaim the space utilized by either cache or need to debug any potential cache-related issues, simply remove the `xet` cache entirely by running `rm -rf ~/<cache_dir>/xet`.
  - At the moment, cached files are never deleted from your local directory: when you download a new revision of a branch, previous files are kept in case you need them again.
- [Fix Codeium Taking Too Much Space on Ubuntu (VS Code Users Must Read) - Duck Cloud _202507](https://www.duckcloud.info/post/fix-codeium-taking-too-much-space-on-ubuntu-vs-code-users-must-read)
  - If you're using Codeium on Ubuntu with VS Code, chances are you've noticed a surprising storage spike
  - Codeium stores local AI model embeddings — and over time, these files can swell to gigabytes of data.
  - delete the ai file, Codeium will rebuild it as needed.

```sh
du -ah ~/.codeium/database | sort -hr | head -n 20
rm -rf ~/.codeium/database/9c0694567290725d9dcba14ade58e297
```

## 0814

- [Error loading model: missing text_projection.weight · Issue · comfyanonymous/ComfyUI _202410](https://github.com/comfyanonymous/ComfyUI/issues/5222)
  - clip missing: ['text_projection.weight']
  - No action needed. The message is just informational.
- How can it be "just informational"? If the weights are missing, the CLIP-textencoder will not work properly.
  - `text_projection` is used in the CLIP model and does not exist structurally in T5 text encoder.
  - FLUX uses both CLIP and T5, so the message appears during the process of loading T5.
- Exactly, it uses both and CLIP will fail due to the missing weights.
  - It's an issue with the CLIP-L textencoder. If replaced with a another one like ViT-L/14 there is no error message.
- `text_projection.weight` is a key associated with the projected pooled output, and many diffusion models do not use this.
  - For this reason, some diffusion models exclude unnecessary keys from the text encoder model when releasing their weights.
  - This is why text_projection.weight is not included in some versions of CLIP-L.

## 0810

- [No response is returned from route handler (Response differs due to polyfill!) · Issue · vercel/next.js _202311](https://github.com/vercel/next.js/issues/58611)
  - Error: No response is returned from route handler '/.../auth0-nextjs-repro/app/api/auth/[auth0]/route.ts'. Ensure you return a `Response` or a `NextResponse` in all branches of your handler.
  - my problem was that I hadn't fully adapted the `@auth0/nextjs-auth0` example to the app router. I needed to return `handleLogin`, not just await it.

## 0809

- ### why do you use `a` html element? why do you not use nextjs `Link` component?
- why I should have used Link:
  - Client-side navigation - Next.js Link provides faster navigation by avoiding full page reloads
  - Prefetching - Link automatically prefetches linked pages in the background for better performance
  - Consistency - The existing code already imports and uses Next.js components like Image, so using Link would be more consistent with the project's patterns
  - SEO and accessibility - While both work, Link is optimized for Next.js routing

## 0804

- ["parserOptions.project" has been set for @typescript-eslint/parser - Stack Overflow](https://stackoverflow.com/questions/58510287/parseroptions-project-has-been-set-for-typescript-eslint-parser)
  - ESLint legacy config (version <= 8): update your ESLint config to use TypeScript rules only on TypeScript files
  - [Relative TSConfig Projects with `parserOptions.project = true` | typescript-eslint](https://typescript-eslint.io/blog/parser-options-project-true/)
    - As of typescript-eslint 5.52.0, we now support providing true for parserOptions.project
    - Doing so indicates that each source file being linted should use type information based on the nearest tsconfig.json in its directory.
    - For each file, @typescript-eslint/parser will check that file's directory, then the parent directory, and so on - until a tsconfig.json file is found.

## 0803

- [fix: Remove `clone-deep` dependency in favor of native `structuredClone` · Pull Request · survivejs/webpack-merge _202407](https://github.com/survivejs/webpack-merge/pull/214)
  - I imagine there's some subtle difference between `structuredClone` and `clone-deep` and there was some structure in your configuration `structuredClone` wasn't able to handle.
  - `async function terserMinify(input, sourceMap, minimizerOptions, extractComments) { }` could not be cloned.
- [quilt(1) - Linux manual page](https://www.man7.org/linux/man-pages/man1/quilt.1.html)
  - Quilt is a tool to manage large sets of patches by keeping track of the changes each patch makes.  
  - Patches can be applied, unapplied, refreshed, and so forth.  
  - The key philosophical concept is that your primary working material is patches
  - Quilt manages a stack of patches.  Patches are applied incrementally on top of the base tree plus all preceding patches.
  - Patch files are located in the patches subdirectory of the source tree
  - Before a patch is applied, copies of all files the patch modifies are saved to the `.pc/patch-name` directory, where patch-name is the name of the patch

## 0802

- [log in error · Issue #884 · TGX-Android/Telegram-X](https://github.com/TGX-Android/Telegram-X/issues/884)
  - 出现此错误后，不要继续多次尝试了；停止尝试48小时；
  - 更换你使用的vpn节点，登录手机版的Telegram X，然后验证码会发送到你的电脑版Telegram上面，输入即可登录手机版。
  - 核心问题就是你的vpn节点有问题了，比如协议不完整，或者以ipv6为优先等情况。
# dev-07-pullOTUpdates/syncOTUpdates-editor-flickering-&-vscode-hover-marked-&-lasuite-local-dev-&-ollama-comfyui

```log //com-showmebug/clacky
console.log('; ; task ', taskState, runningTaskAction, task?.task_steps)
console.log('; ; act-file-o ', currentOpenedActionId, shouldForceOpenFile, actionPath, currentFilePath)
console.log('; ; taskActions', currentActionId, path, store.cdePlay.enableDiffView(), currentAction, taskActions)
console.log('; ; open-diff ', enableDiffAnimation, store.cdePlay.enableDiffView(), store.cdeReplay.isMachinePaused())
console.log('; ; qryDiffSnap ', snapshotFrameResult)
console.log(

          ';; 📝 ',
          filePath,
          event.data?.revision,
          store.file.latestRequestFilePath(),
          Boolean(isFollow),
          Boolean(event.data?.isRefresh),
          Boolean(event.data?.isAfterWrite),
          Boolean(isOtherUserOpened),
          event,
        );
        

^((?!(42\["heartbeat|resourceMonit|refreshXtermCols|42\["multiTerminal|42\["terminalStatus|42\["activeTerminal|42\["ragStatus|42\["initAiCodeInfo)).)*$
^((?!(42\["heartbeat|resourceMonit|refreshXtermCols|42\["multiTerminal|42\["terminalStatus|42\["activeTerminal|42\["ragStatus|42\["initAiCodeInfo|42\["fileChange|42\["pullOTUpdates)).)*$
^((?!(42\["heartbeat|resourceMonit|refreshXtermCols|42\["multiTerminal|42\["terminalStatus|42\["activeTerminal|42\["ragStatus|42\["initAiCodeInfo|42\["fileChange)).)*$
^((?!(42\["heartbeat|resourceMonit|refreshXtermCols)).)*$
^(?!42\["resourceMonit).* 
/syncUpdates|syncOTUpdates/
<!-- 观测云搜索 ide-server -->
-multiTerminalHeartBeat -all\:multiTerminal -"[fromMQ] multiTerminal" -"[toMQ]paas:multiTerminal" -"] multiTerminal, {" -all\:activeTerminal -"] activeTerminal, {"  -"[toMQ]paas:multiTerminalCmd" -"[fromMQ] terminalStatus" -"appendMultiTerminalProcessName res" -"appendMultiTerminalCmdReply res" -all\:multiTerminalProcessName -all\:multiTerminalCmdReply -all\:initAiCodeInfo -"[fromMQ] lspStatus" -all\:lspStatus -all\:updateDebugSupport -all\:availablePorts -"[fromMQ] portsChanged" -"[fromMQ] availablePorts" -"availablePorts, {}" -"[fromMQ] ragStatus" -"] ragStatus data: [" -"all:ragStatus" -"[fromMQ] vncStatus" -"[fromMQ] config" -"[followingFocusComponent]"
-"toMQ fileContentUpdate begin" -"[toMQ]paas:filePull"  
-agentAppendFile -"[FileTree_writeFile] fs.writeFile prepared" -"[FileTree_writeFile] success"
<!-- 观测云搜索 frontend -->
-chunkMessage -richMessage -messageSuggestion -toolCallStatusUpdated

```
```log //ai
- when did deepseek v3.1 model release?
- when did qwen3-coder model release?
- what's the weather in guangzhou china? give me some food and outdoor-activities suggestions according to weather temperature
- lawn
  - a big park for resting and relaxing, there are little trees around a big lawn, some birds are resting in the lawn, The lawn and the trees around it both need pruning
- prompts-logo-excel-like
  - create a product logo for my excel-like webapp, 
  - the logo brand color should be like green/teal/indigo/..., or any good color that giving a cold and formal feeling, 
  - the logo should express rows or columns or grid, but logo should not be complicated,
add action to add datetime at top of readme.md
add an action to run "npm install -ddd" and another action to add datetime at top of readme.md
add action to create a route /nextjs with nextjs changelog content in it , and show nextjs link in home page, when clicking the link, jump to /nextjs route
add action to create quickSort1.mjs and try to implement quick sort algorithm in less than 60 lines
<!-- 🛝 -->
use create-react-app to create a react-router v6 example webapp in typescript: homepage shows a list of frontend frameworks like react/vue/angular, when clicking the framework, navigate to the route to show its introduction
use vanilla html/css/javascript to create a personal profile landing page: homepage shows a cool welcoming animation, then shows 4 example personal projects, then a simple get in touch form below it
use vanilla html/css/javascript to create a simplistic personal profile landing page: homepage shows a big welcoming greeting, then shows 2 example personal projects, then a simple get in touch example email below it
- line 290 in file  is not tested, please write unit tests to test it
- line 160-174, 181-185 in file apps/webapp/src/utils/paas-playground.ts
 is not tested, please write unit tests to test it
- ensure tests pass by auto run terminal commands  npx nx run webapp:test  src/__tests__/hooks/use-time-machine.test.tsx
- ensure tests pass by auto run terminal commands  npx nx run shared-utils:test __tests__/env-browser.test.ts
- ensure tests pass by auto run terminal commands  cd packages/client && pnpm test  src/lib/codemirror-languageserver/src/__tests__/utils.spec.ts
- ensure tests pass by auto run terminal commands cd packages/server && pnpm test apps/entry/__tests__/fileUtils.spec.ts
- you can mock state/store/data/websocket/external-dependencies, especially you can refer to this test file apps/webapp/src/__tests__/components/chat-box/action-panel.test.tsx to mock store/useTrackedStore/actions
- you can mock state/store/data/external-dependencies/modules, especially you can refer to this test file apps/webapp/src/__tests__/components/cde-header/run-status-button.test.tsx to mock store/useTrackedStore/actions
- you can use jest and @testing-library/react, 
- Each unit test should be independent of other tests. Avoid sharing state or dependencies between tests by using beforeEach/beforeAll/afterEach/afterAll
- you had better write only in test files and not modify original source code
- Handle asynchronous code correctly 
- 👾
- tests failed, run test command again and fix issues
- yes, auto fix issues to make tests pass, donnot ask me again
- you can mock codemirror-related packages, like @codemirror/view
- you only need to test  line  715-732 , donnot write tests for more lines
test('mock test', () => {
  expect(true).toBe(true);
});
```

## 0731

- [Running on CPU only · Issue · comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI/issues/718)
  - `python main.py --cpu`
- [Failed to initialize database. · Issue · comfyanonymous/ComfyUI](https://github.com/comfyanonymous/ComfyUI/issues/8764)
  - for macos, go to folder `/Applications/ComfyUI.app/Contents/Resources/ComfyUI`, and create a folder named `user` inside it .

## 0720

- [Working with the Alpine Package Keeper (apk) - Alpine Linux Documentation](https://docs.alpinelinux.org/user-handbook/0.1a/Working/apk.html)
  - apk is the Alpine Package Keeper - the distribution’s package manager. 

## 0717

- [Install VSCode extensions in Windsurf](https://www.nisanthchunduru.com/posts/Install-VSCode-extensions-in-Windsurf)

```JSON
{
  "windsurf.marketplaceExtensionGalleryServiceURL": "https://marketplace.visualstudio.com/_apis/public/gallery",
  "windsurf.marketplaceGalleryItemURL": "https://marketplace.visualstudio.com/items"
}
```

## 0715

- makefile
  - `=` (recursive expansion): Variables are evaluated each time they are used; Can lead to circular dependencies if not careful
  - `:=` (immediate expansion): Evaluates variables immediately when the Makefile is read

## 0710

- hover浮窗尺寸限制: w-400, h-240
- YARD has become the de‑facto standard for Ruby documentation—and most IDEs will show these docstrings on hover. 
  - You simply put `#` lines immediately above your method or class, optionally using `@param/@return` tags
- RDoc-style comments
  - You can use a block comment with `=begin/=end`, but note that not every editor will pick it up for hovers 

## 0709

```JS
import 'highlight.js/styles/atom-one-dark.css'
```

```jsx
<link
  id="el"
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
  rel="stylesheet"
  <!-- 👇  -->
  disabled
  crossorigin="anonymous" />
```

- If `disabled` attribute is specified in the HTML when it is loaded, the stylesheet will not be loaded during page load. 
  - Instead, the stylesheet will be loaded only when the `disabled` property is set to `false` or removed. 
  - Setting the `disabled` property using JavaScript causes the stylesheet to be removed from the document's `Document.styleSheets` list.
  - It only has an effect with style sheet links (`rel` property set to `stylesheet`).
- rel=preload
  - specifying resources that your page will need very soon, which you want to start loading early in the page lifecycle, before browsers' main rendering machinery kicks in.
  - Even though the name contains the term load, it doesn't load and execute the script but only schedules it to be downloaded and cached with a higher priority.

## 0707

- The standard JavaScript Error object and its descendants (like TypeError, ReferenceError, etc.) have properties like message, name, and stack. However, these properties are not enumerable.
  - JSON.stringify() only includes an object's enumerable properties in the resulting JSON string. Since stack, message, and name are not enumerable, JSON.stringify() ignores them completely.
- [typescript - Why Catch clause variable type annotation must be any? - Stack Overflow](https://stackoverflow.com/questions/69021040/why-catch-clause-variable-type-annotation-must-be-any)
  - unknown type exists as a safe alternative to any, because operations with unknown type are illegal, so you are forced to type check your unknown variable before doing anything.

## 0703

- The versions of `base64` and head on macOS do not support the same options as their Linux counterparts.
  - linux: base64 -w 0 /dev/urandom | head -c 2M > textfile.txt
  - macos: base64 /dev/urandom | head -c 2097152 > textfile.txt
  - brew install coreutils
  - gbase64 -w 0 /dev/urandom | ghead -c 2M > textfile.txt
- The size property returned by `fs.statSync` in Node.js is in **bytes** 
# dev-06-agentAppendFile-jank-&-LSP-def-jump-back/forward-&-codemirror-tooltip-merged-&-colanode-webapp
- lsp支持的语言排查
  - 鼠标放上去就消失lint了
  - 让settings开关联动
- 文件树M标记的处理
  - 清理标记的时机， fork时和commit时，提供手动删除.1024feature-file的能力
    - goAgent去删，ideServer不关心git操作和文件操作
  - A/D标记不支持
  - goAgent触发的时机不太确定，计算资源占用大
  - gitignore的文件不应该显示M
- 🔲 🔜
  - terminal放大缩小折叠展开后，光标自动聚焦在terminal
  - 编辑器行号宽度样式优化
  - 修复文件树将文件夹拖到文件夹不work的问题
  - 变更列表 accept-all, reject-all
  - ~~terminal在follow时自动打开，在非follow时显示更新的红点~~
  - ~~terminal在执行时需要自动滚到末尾，方便显示最新输出信息~~
  - ~~编辑器打开时自动跳到diff视图第一个变更块的位置~~
  - ~~action路径超出卡片宽度~~
  - ~~webview自动打开, 刷新时保持打开~~
  - ~~cmdk工具条无法触发，快捷键可以~~

## 0628

- [What is the purpose of `.PHONY` in a Makefile? - Stack Overflow](https://stackoverflow.com/questions/2145590/what-is-the-purpose-of-phony-in-a-makefile)
  - By default, Makefile targets are "file targets" - they are used to build files from other files.
  - However, sometimes, you want your Makefile to run commands that do not represent physical files in the file system.
  - These special targets are called phony and you can explicitly tell Make they're not associated with files
  - The special target . PHONY: allows to declare phony targets, so that make will not check them as actual file names: it will work all the time even if such files still exist.

## 0624

- [StatusCodes. Status499ClientClosedRequest Field (Microsoft. AspNetCore. Http) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.http.statuscodes.status499clientclosedrequest?view=aspnetcore-9.0)
  - HTTP status code 499. This is an unofficial status code originally defined by Nginx and is commonly used in logs when the client has disconnected.

## 0623

- [CSS Triangle with border trick | CSS-Tricks](https://css-tricks.com/snippets/css/css-triangle/)
- [One of the most ubiquitous CSS tricks. How do you implement this arrow? : r/webdev _202308](https://www.reddit.com/r/webdev/comments/164kvpu/one_of_the_most_ubiquitous_css_tricks_how_do_you/)
  - these days I'd likely use a `clip-path` because it seems to alias better.
  - What do you mean by alias better?
  - Sometimes the border trick can leave a subpixel gap on certain screen resolutions or zoom levels. The gap is because the position of the element vs. the pseudoelement is calculated slightly differently, so it has a noticeable gap. This is called aliasing. It's the same effect in video games when a 3d model's edges have sharp pixels, and to smooth it out you use anti-aliasing.

## 0619

- [Failed to save 'file': A system error occured (EACCES: permission denied, open 'file path') · Issue #17860 · microsoft/vscode](https://github.com/Microsoft/vscode/issues/17860)
  - i know what was the problem : i'm working with angular cli, when i generate a component using the ng g c name, if in the terminal iam as root, then the generated files belongs to the root user, when after i go to edit them using vscode as a non root i have this error !
  - The solution is that i created the main project's folder as 'root' and then given it permissions so that i can create files in it. Those files don't have the root as the owner so it doesn't gives an error of permission denied when we try to save/create files in the editor.
  - `sudo chmod -R <user_name> <directory_name>`
  
- lsp跳转到根目录外失败
  - "file:///home/runner/app/home/runner/.nvm/versions/node/v22.16.0/lib/node_modules/typescript/lib/lib.dom.d.ts"
  - "file:///home/runner/.cache/typescript/5.8/node_modules/%40types/node/console.d.ts"
  - "file:///home/runner/.nvm/versions/node/v22.16.0/lib/node_modules/typescript/lib/lib.dom.d.ts"
- go/python/java/ruby挂载的目录在 dependency/ 
- .nvm及操作系统默认的目录如.cache挂载在 容器 dependency/home/ 对应 操作系统 ~/home/
- lsp-ts跳转失败路径
  - /home/runner/.nvm/versions/node/v22.16.0/lib/node_modules/typescript/lib/lib.dom.d.ts

## 0618

- Static imports of lazy-loaded libraries are forbidden. Library is lazy-loaded in these files
  - 在jest + nx的测试代码出现此问题
  - 解决方法是， 不使用 const utils = require('@clacky-ai/utils')
    - 而用 全局变量 mockCheckIsAppleOs = jest.requireMock('@clacky-ai/utils').checkIsAppleOs
- [how do I make the test wait for useEffect's update to be called first - Stack Overflow](https://stackoverflow.com/questions/76824340/how-do-i-make-the-test-wait-for-useeffects-update-to-be-called-first)

```jsx
// __tests__/App.test.tsx
import { render, screen, waitFor } from "../test-utils";
import App from "../App";
test("loads and displays greeting", async () => {
  // Render your APP to the DOM
  render(<App />);
  
  // Wait for the DOM to update
  await waitFor(() => {
    expect(screen.getByText("1")).toBeInTheDocument();
  });
});
```

## 0617

- 无法跳转的场景: 普通切换文件
- 未失焦的场景下，刷新页面不能恢复光标位置
- [How do you put api routes in the new app folder of Next.js? - Stack Overflow](https://stackoverflow.com/questions/75418329/how-do-you-put-api-routes-in-the-new-app-folder-of-next-js)
  - app\api\routes.ts
- [error TypeError: Cannot read properties of undefined (reading '') when using Next.js runtime edge on turborepo or Nx · Issue #53562 · vercel/next.js](https://github.com/vercel/next.js/issues/53562)
  - I got it fixed. Seems like every app requires the dev script to be: "dev": "next dev --turbo" instead of "dev": "next dev"
- [Organization repo + hobby plan in Vercel - DEV Community](https://dev.to/algoorgoal/deploying-organization-repo-to-vercel-with-a-hobby-plan-2f3h)
  - Vercel doesn't support deploying an organization repository for free, you will need some workaround if you want to stay on the hobby plan. 
  - In this post, I'll talk how you can do it with github actions. 

## 0616

- 去掉自动滚动，ai滚动到某一行的事件, 调整diff动画的逻辑
- 流式输出/修改文件，的ui上要显示diff绿色
- git diff计算:  输入 时间戳， 返回 时间戳的内容变化

```js
// 查询文件初始内容
// 对新创建的文件，一直是空文件
// 对于0-1项目， historyBaseData:[]
stts.dao.channel().send('getPlaybackInfo')
// ⬆️ [ "getPlaybackInfo", {}, { "currentDockerId": "806278374774525952" } ]
// ⬇️ playbackInfo
{
  "playbackSummerize": {
    "total": 80,
    "start": 1749440495981,
    "end": 1749441018099,
    "customize": []
  },
  "playbackData": {
    "playbackData": [],
    "historyBaseData": [{
        "_id": "684657f4d808bf3cbf5e43f3",
        "dockerId": "803690894141677568",
        "path": "README.md",
        "playgroundId": "803690894095540224",
        "__v": 0,
        "content": "# profile-landing-page 0327\nA Pen created on CodePen.io. Original URL: [https://codepen.io/uptonking/pen/QWdqEmr](https://codepen.io/uptonking/pen/QWdqEmr).\n\nfirst pass at an avatar animation for my personal portfolio\n\n- open http://localhost:9000/\n\n# tests 1527\n\n- aa\n- bb\n\naa\n    ",
        "createTime": 1749440500984
      },
      {
        "_id": "684659f2d808bf3cbf5e4dc6",
        "dockerId": "803690894141677568",
        "path": "script.mjs",
        "playgroundId": "803690894095540224",
        "__v": 0,
        "content": "export const hello = 'world '\nconsole.log('; log ', hello)\n\nexport const hello2 = 'world '\nconsole.log('; log ', hello2)\n\nexport const hello3 = 'world '\nconsole.log('; log ', hello3)\n\nexport const hello4 = 'world'\nconsole.log('; log ', hello4)\n\nexport const hello5 = 'world'\nconsole.log('; log ', hello5)\n\n\n",
        "createTime": 1749441010390
      }
    ]
  },
  "agentUsers": [{
      "agentUserId": "clacky",
      "userId": "728372792453660672",
      "userInfo": {
        "username": "Clacky",
        "avatarUrl": "https://assetscdn.clacky.ai/clacky/marvin_avatar_common.svg",
        "userId": "clacky"
      },
      "status": "online",
      "followingAgentUserId": "",
      "focusComponent": "Editor",
      "focusXterm": null,
      "editorScroll": 0,
      "cursor": {},
      "wsClientID": "gf8kAoVDp01-H9SrAAGp",
      "color": "#3091F2"
    },
    {
      "agentUserId": "b10985e2-97a9-4fa2-a8fb-c5f19758f4c8",
      "userId": "705965668918861825",
      "userInfo": {
        "userId": "user_2ly7xQ9AdCaUU4i23Ta55Y51Mpv",
        "username": "uptonking",
        "avatarUrl": "https://img.clerk.com/eyJ0eXBlIjoicHJveHkiLCJzcmMiOiJodHRwczovL2ltYWdlcy5jbGVyay5kZXYvb2F1dGhfZ2l0aHViL2ltZ18ybHk3eFdIeGxNaEl1SjlZYVFYV0ZTOVhFZlQifQ"
      },
      "fileOpened": "script.mjs",
      "status": "online",
      "followingAgentUserId": "",
      "focusComponent": "Editor",
      "focusXterm": null,
      "editorScroll": 0,
      "cursor": {},
      "wsClientID": "0aAR-tc-rUq0CvOCAAGt",
      "color": "#5C5CE5"
    }
  ],
  "rrwebDataAllData": {
    "rrwebData": [],
    "customEvents": []
  }
}
```

## 0614

- dev-to
  - 支持跳转定义时不click聚焦也能正常回退
  - editor tab显示文件名

## 0613

- [Is it possible to simulate key press events programmatically? - Stack Overflow](https://stackoverflow.com/questions/596481/is-it-possible-to-simulate-key-press-events-programmatically)
  - `element.dispatchEvent(new KeyboardEvent('keydown', {'key': 'a'}));`

## 0612

- [how to implement back and forward functionality like browser - Stack Overflow](https://stackoverflow.com/questions/6869476/how-to-implement-back-and-forward-functionality-like-browser)
  - 一种思路是使用2个栈， backStack/forwardStack
- 🤔 i want to implement jumping backward and forward in custom text editor written in typescript.
  - solution 1:  use 2 array stacks.  const backStack=[]; const forwardStack=[]; when user clicks in the editor, the cursor position is pushed into backStack. when user click backward/forward button, position is popped from backStack then pushed into forwardStack.
  - solution 2: use 1 array to store history positions, and a currentPos as array index. when user click backward/forward button, just move the currentPos backward/forward to get the cursor position. 
  - which solution is better ?
  - 如果要让其他组件在stack为空时更新ui，需要在状态变化时通知外界，另一种思路是当业务侧每次更新stack时业务侧主动查询最新的stack是否为空
- 👾 Solution 1 (Dual Stacks) is Better
  - Matches standard editor/browser history semantics
  - Back/forward operations are true O(1) (single pop/push)
  - No array slicing/reallocations needed
  - No expensive truncation operations during recording
  - Doesn't retain obsolete forward history (automatically clears when new actions occur)
  - Solution 1 is superior due to its constant-time operations, memory efficiency, and industry-standard approach.
  - 🤔 Combine with edit history for full undo/redo system
- solution2: Single-array + index model 
  - Easy to dump full history at once (no need to merge two stacks).
  - State Management and API (The Biggest Win for Solution 2)
  - Splice on each new navigation (to drop the “forward” tail) is O(N) in the worst case.
  - Every jump still requires bounds-checking and index arithmetic.

## 0611

- 流式输出闪烁的原因，是 fileChange事件引发的ideServer读磁盘文件与mongo文件内容不一致产生的pullOTUpdates事件 与 agentAppendFile引发的pullOTUpdates事件 的编辑器内容不一致，前端编辑器无法处理，导致前端主动多次打开文件获取最新内容
  - ~~方案1: agentAppendFile不触发文件持久化，事件开始和结束时添加标记，开始时写到内存缓存，结束时自动持久化到磁盘，也能减少lint计算等操作~~
  - ~~方案2: agentAppendFile不触发文件持久化，由ai手动触发持久化~~
  - 💡 讨论后采用方案， 对于ideServer主动告知goAgent文件变化的场景，不需要goAgent再次发送fileChange事件通知ideServer文件内容变了，这样ideServer发送给前端的文件更新事件pullOTUpdates只剩下一个，此方案更简单且能满足需求
- 流式输出时编辑器闪烁，似乎不是ot事件导致的问题，实测在36s写文件300次都是正常的
  - 🤔 receiveOTUpdates 的直接原因是 pullOTUpdates 的版本号少了一次
    - 进一步确认，当触发了 `[vitualOT]mock filechange` 逻辑的文件才异常闪烁, 把doc.version打印出来看看
  - ideServer收到的 [fromMQ] fileChange  33/42次，似乎也正常
- 🤔 另一个角度， agentAppendFile 的逻辑应与 pushOTUpdates 的逻辑保持一致

```JS
async function aa() {
  for (let i = 0; i < 300; i++) {
    await new Promise((resolve, reject) => setTimeout(resolve, 120));
    console.log("hi ", i);
    stts.dao.channel().send('agentAppendFile', { path: 'append2.md', text: `${i} - ${(Math.random() + 1).toString(36).substring(3)}\n` })
  }
}
```

## 0610

- receiveOTUpdates 的异常事件流
  - agentAppendFile 向ideServer发送了 ? 次写文件事件
  - 21:21:21  -  8
  - 21:21:22  -  8
  - 06/10 21:21:22.152781 [vitualOT]mock filechange
  - 06/10 21:21:23.155993 refresh 强制刷新文件
  - 实测 agentAppendFile 向ideServer写代码的频率为 4-8次/s, 即 4-8行/s
    - 在异常场景下， 由于fileChange事件通知ideServer有文件变化，ideServer不停持久化、计算变化op 处理出现异常
- 用户A手动输入字符b时，用户B接收事件的时序
  - 1024paas的旧版事件只有3个
    - 42["pullOTUpdates",{"updates":[{"changes":[14]
    - 42["pullOTUpdates",{"updates":[{"changes":[14,[0,"b"]]
    - 42["fileChange",{"data":["README.md"]}]

```JS
// ⬇️ pullOTUpdates
{
  "updates": [{
    "changes": [
      13
    ],
    "selection": {
      "ranges": [{
        "anchor": 13,
        "head": 13
      }],
      "main": 0
    },
    "agentUserId": "5c38ff4b-b93d-4ce1-b74a-05c2baaf8d28"
  }],
  "lastRevision": 39,
  "latestRevision": 40,
  "path": "README.md",
  "id": "344eff48-6e2a-45cc-8936-7da2e41adeb7",
  "mapSelection": {
    "9962289e-a28e-49fd-8dc8-aef08d263c20": {
      "ranges": [{
        "anchor": 13,
        "head": 13
      }],
      "main": 0
    },
    "5c38ff4b-b93d-4ce1-b74a-05c2baaf8d28": {
      "ranges": [{
        "anchor": 13,
        "head": 13
      }],
      "main": 0
    },
    "12cdfe61-72ca-4046-be33-9c2af5d23af4": {
      "ranges": [{
        "anchor": 5,
        "head": 5
      }],
      "main": 0
    }
  }
}
// ⬇️ pullOTUpdates
{
  "updates": [{
    "changes": [
      13,
      [
        0,
        "a"
      ]
    ],
    "selection": {
      "ranges": [{
        "anchor": 14,
        "head": 14
      }],
      "main": 0
    },
    "agentUserId": "5c38ff4b-b93d-4ce1-b74a-05c2baaf8d28"
  }],
  "lastRevision": 40,
  "latestRevision": 41,
  "path": "README.md",
  "id": "073ff2ad-7da6-4fe3-aff6-547ec4785237",
  "mapSelection": {
    "9962289e-a28e-49fd-8dc8-aef08d263c20": {
      "ranges": [{
        "anchor": 13,
        "head": 13
      }],
      "main": 0
    },
    "5c38ff4b-b93d-4ce1-b74a-05c2baaf8d28": {
      "ranges": [{
        "anchor": 14,
        "head": 14
      }],
      "main": 0
    },
    "12cdfe61-72ca-4046-be33-9c2af5d23af4": {
      "ranges": [{
        "anchor": 5,
        "head": 5
      }],
      "main": 0
    }
  }
}
// ⬇️ 42["fileChange",{"data":["README.md"]}] , 2次相同
// ⬇️ fileTree, 2次 create + feature
{
  "eventName": "fileTree",
  "agentUesrId": "shell",
  "playgroundId": "804065174448644096",
  "dockerId": "804065174519947264",
  "data": {
    "action": "CREATE",
    "files": [{
      "type": "FILE",
      "name": "README.md"
    }],
    "result": true
  },
  "timestamp": 1749538196784
}
```

- [Why I keep getting ECONNRESET error on proxy calls in MAC OSX only, totally arbitrary with some successful calls (Pretty desperate) - Stack Overflow](https://stackoverflow.com/questions/54096937/why-i-keep-getting-econnreset-error-on-proxy-calls-in-mac-osx-only-totally-arbi)
  - Found the fix for this after trying all other methods including giving a timeout duration, only keep connection alive option solved it for me.
  - Added below to to the api object

```JS
"headers": {
  "Connection": "keep-alive"
}
```

## 0609

- ai执行task时，多次打开文件的异常事件，ide-server的日志
  - ⬇️ file, {"path":"heapSort.mjs", "timestamp":1749459434122, "fileRootId":"home", "loadType":"refresh", "fileRootPath":"", "readOnly":false} 
  - ⬆️ self[b10985e2-97a9-4fa2-a8fb-c5f19758f4c8] file, {"agentUserId":"b10985e2-97a9-4fa2-a8fb-c5f19758f4c8", "data":{"revision":72, "openedPath":"heapSort.mjs", 👉 "isRefresh":true, "isBinary":false, "ext":"mjs", "mapSelection":{}, "content":"
  - ⬇️ openFileByFollow, {"fileOpened":"heapSort.mjs"}
- editor闪烁是由于多次打开文件，相关日志如下

```log
receiveOTUpdates error  heapSort.mjs RangeError: Applying change set to a document with the wrong length
    at ChangeSet.apply (DaoPaaS.cjs:33891:13)
    at get newDoc (DaoPaaS.cjs:34829:51)
    at EditorState.applyTransaction (DaoPaaS.cjs:35060:31)
    at get state (DaoPaaS.cjs:34836:23)
    at Array.eval (DaoPaaS.cjs:110298:36)
    at extendTransaction (DaoPaaS.cjs:34962:35)
    at resolveTransaction (DaoPaaS.cjs:34921:10)
    at EditorState.update (DaoPaaS.cjs:35031:12)
    at receiveUpdates (DaoPaaS.cjs:88235:16)
    at Object.receiveOTUpdates (DaoPaaS.cjs:104339:36)
    at eval (DaoPaaS.cjs:104446:48)
    at new Promise (<anonymous>)
    at Object.onPullUpdates (DaoPaaS.cjs:104435:16)
    at eval (DaoPaaS.cjs:104379:36)
    at eval (DaoPaaS.cjs:104270:15)
    at TaskList.run (DaoPaaS.cjs:104263:16)
    at Socket.eval (DaoPaaS.cjs:104380:21)
    at Emitter$1.emit (DaoPaaS.cjs:10085:21)
    at Socket.emitEvent (DaoPaaS.cjs:11681:16)
    at Socket.onevent (DaoPaaS.cjs:11669:12)
    at Socket.onpacket (DaoPaaS.cjs:11646:14)
    at Emitter$1.emit (DaoPaaS.cjs:10085:21)
    at eval (DaoPaaS.cjs:12004:12)
```

## 0608

- ai执行task的数据流
  - ⬆️ "followingAgentUser", "clacky"
  - ⬇️ following, { "agentUserId": "a67ab9fd-b0f6-48be-8945-80c9452a3991", "userId": "705965668918861825", "userInfo": { "userId": "user_2ly7xQ9AdCaUU4i23Ta55Y51Mpv", "username": "uptonking", "avatarUrl": "https://img.clerk.com/eyJ0eXBlIjoicHJveHkiLCJzcmMiOiJodHRwczovL2ltYWdlcy5jbGVyay5kZXYvb2F1dGhfZ2l0aHViL2ltZ18ybHk3eFdIeGxNaEl1SjlZYVFYV0ZTOVhFZlQifQ" }, "fileOpened": "collab.js", "status": "online", "followingAgentUserId": "clacky", "focusComponent": "Tree", "focusXterm": null, "editorScroll": 0, "cursor": {}, "wsClientID": "96aYj58LTtiDzPehAAb0", "color": "#2ACC96" }
    - 有问题, { "status": "online", "wsClientID": "lmx1IScYa75bkIUoAABN", "fileOpened": "collab.js", "focusComponent": "Tree", "followingAgentUserId": "clacky" }

## 0605

- ai工作状态变化， 会触发 ide-server 和 sdk前端 相关事件
  - action init > in-progress: sdk前端会先打开跟随文件，但sdk内存状态的跟随文件还是旧文件
- ai刚开始工作时，打开文件错误的问题
  - sdk的user-fileOpened是旧状态
- ai写完后，编辑器闪烁的问题
- ai写完后，再次打开diff的问题
- ai工作时的主要事件时序, 流式输出
  - ⬆️ "followingAgentUser", "clacky"
  - //////
  - ⬇️ [ "fileTree", { "playgroundId": "802656873768951808", "eventName": "fileTree", "agentUserId": "clacky", "data": { "action": "CREATE", "files": [ { "type": "FILE", "name": "mergeSort.mjs" } ], "result": true, "message": "success"  } } ]
  - ⬆️ file, { "path": "mergeSort.mjs", "timestamp": 1749194085630, "fileRootId": "home", 🇺🇳 "loadType": "default", "fileRootPath": "", "readOnly": false }
  - ⬇️ file, { "revision": 0, "openedPath": "mergeSort.mjs", 👉 "isRefresh": false, "isBinary": false, "ext": "mjs", "mapSelection": {}, "content": "" }
  - ⬆️ file, { "path": "mergeSort.mjs", "timestamp": 1749194113927, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
  - //////
  - ⬆️ file, { "path": "heapSort.mjs", "timestamp": 1749194116519, "fileRootId": "home", 🇺🇳 "loadType": "default", "fileRootPath": "", "readOnly": false }
  - ⬆️ file, { "path": "heapSort.mjs", "timestamp": 1749194129709, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
  - ⬆️ file, { "path": "heapSort.mjs", "timestamp": 1749194146606, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
  - //////
  - ⬆️ { "path": "testSort.mjs", "timestamp": 1749194148960, "fileRootId": "home", 🇺🇳 "loadType": "default", "fileRootPath": "", "readOnly": false }
  - ⬆️ { "path": "testSort.mjs", "timestamp": 1749194170868, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
  - ⬆️ { "path": "testSort.mjs", "timestamp": 1749194173066, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
  - ⬆️ { "path": "testSort.mjs", "timestamp": 1749194195435, "fileRootId": "home", 🚩 "loadType": "refresh", "fileRootPath": "", "readOnly": false }
- ai工作时的主要事件时序, 非流式输出
  - ⬆️ "followingAgentUser", "clacky"
  - //////
  - ⬆️ [ "file", { "path": "progressbar.mjs", "fileRootId": "home", 👉 "loadType": "follow", "fileRootPath": "", "readOnly": false }  ]
    - 有时sdk会请求ai上一次访问的文件，而不是正在创建的文件
  - ⬇️ [ "file", { "agentUserId": "307b71ba-6fbf-46c8-b7a8-13a1b8f30f07", "data": { "revision": 0, "openedPath": "progressbar.mjs", "isRefresh": false, "isBinary": false, "ext": "mjs", "mapSelection": {}, "content": "" } } ]
    - 有时会缺失这一次打开文件的事件
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 1, "openedPath": "progressbar.mjs", 👉 "isRefresh": true, "isBinary": false, "ext": "mjs", "mapSelection": {}, "content": "xxx" }, "timestamp": 1749126857060 } ]
  - //////
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 0, "openedPath": "index.html", "isRefresh": false, "isBinary": false, "ext": "html", "mapSelection": {}, "content": "xxx" } } ]
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 1, "openedPath": "index.html", 👉 "isRefresh": true, "isBinary": false, "ext": "html", "mapSelection": {}, "content": "xxx y" } } ]
  - //////
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 0, "openedPath": "style.css", "isRefresh": false, "isBinary": false, "ext": "css", "mapSelection": {}, "content": "xxx" }  } ]
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 1, "openedPath": "style.css", 👉 "isRefresh": true, "isBinary": false, "ext": "css", "mapSelection": {}, "content": "xxx y“ }, "timestamp": 1749126885851 } ]
  - //////
  - 执行结束后，有时sdk会请求再次打开最后一个文件
- ai工作时的主要事件时序, 流式状态
  - ⬆️ [ "followingAgentUser", "clacky" ]
  - ⬆️ [ "file", { "path": "style.css", "fileRootId": "home", "loadType": "follow", "fileRootPath": "", "readOnly": false }  ]
  - ⬇️ ai工作的文件 [ "file", { "agentUserId": "clacky", "data": { "revision": 0, "openedPath": "index.html", "isRefresh": false, "isBinary": false, "ext": "html", "mapSelection": {}, "content": "<body> </body>  " } } ]
  - ⬆️ [ "file", { "path": "style.css", "timestamp": 1749114832648, "fileRootId": "home", "loadType": "default", "fileRootPath": "", "readOnly": false }  ]
  - 做完一个action
  - ⬆️ [ "file", { "path": "progressbar.mjs", "timestamp": 1749114853704, "fileRootId": "home", "loadType": "default", "fileRootPath": "", "readOnly": false } ]
  - ai打字动画
  - ⬆️ [ "file", { "path": "progressbar.mjs", "timestamp": 1749114861342, "fileRootId": "home", "loadType": "refresh", "fileRootPath": "", "readOnly": false }  ]
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 0, "openedPath": "style.css", "isRefresh": false, "isBinary": false, "ext": "css", "mapSelection": {}, "content": "body " }  } ]
  - ⬇️ [ "file", { "agentUserId": "clacky", "data": { "revision": 1, "openedPath": "style.css", "isRefresh": true, "isBinary": false, "ext": "css", "mapSelection": {}, "content": "body " }, "timestamp": 1749117449758 } ]

## 0604

.rbenv
.sdkman
- go-to-definition 容器中执行pwd、lsp返回的地址
  - `/home/runner/.nvm/versions/node/v22.16.0/lib/node_modules/typescript/lib/lib.dom.d.ts`.
    - 实际地址 /app/data/codeZone/2025/1/6-19/@5c32b7b0-d171-4c22-b755-29697210f00d/dependency/home/.nvm/versions/node/v22.16.0/lib/node_modules/typescript/lib/lib.dom.d.ts
  - `/home/runner/.pyenv/versions/3.12.8/lib/python3.12/site-packages/fastapi/applications.py`.
    - 实际地址 /app/data/codeZone/2025/dependency/.pyenv/versions/3.12.8/lib/python3.12/site-packages/fastapi/applications.py
  - `/home/runner/.gvm/pkgsets/go1.23/global/pkg/mod/github.com/gin-gonic/gin@v1.9.0/gin.go`.
    - 实际地址  /app/data/codeZone/2025/dependency/.gvm/pkgsets/go1.23/global/pkg/mod/github.com/gin-gonic/gin@v1.9.0/gin.go
  - `/home/runner/app/main.go`
- ide-server 通过node fs.readFile读取的地址
  - /app/data/codeZone/2025/1/6-4/@f0e6d0c4-04e5-4706-b230-980466466a1b/dependency/ home/app/main.go
  - dependency/home on /home/runner type nfs
  - 因为文件系统自身不需要 User 目录，为了模拟操作系统，就加了runner

```JS
// read-request
{
  "path": "README.md",
  "timestamp": 1749030891398,
  "fileRootId": "home",
  "loadType": "default",
  "fileRootPath": "",
  "readOnly": false
}
```

## 0603

- [expect(jest.fn()).toHaveBeenCalled() fails even though the function has been called - Stack Overflow](https://stackoverflow.com/questions/67538405/expectjest-fn-tohavebeencalled-fails-even-though-the-function-has-been-cal)
  - 箭头函数每次都是新函数  store: { dao: { isPlayBack: () => false, channel: () => ({ loadFile: mockLoadFile, 
  - const mockLoadFile = jest.fn(() => console.log('; ; loadFile')); 
- [Service mocked with Jest causes "The module factory of jest.mock() is not allowed to reference any out-of-scope variables" error - Stack Overflow](https://stackoverflow.com/questions/44649699/service-mocked-with-jest-causes-the-module-factory-of-jest-mock-is-not-allowe)
  - The problem is that all `jest.mock` will be hoisted to the top of actual code block at compile time, which in this case is the top of the file. At this point VocabularyEntry is not imported. You could either put the mock in a `beforeAll` block in your test or use `jest.mock` like this
  - const VocabularyEntry = require("../../../src/model/VocabularyEntry"); 

## 0602

- [Adding a directory to the PATH in macOS - Apple Community](https://discussions.apple.com/thread/254226896?sortBy=rank)
  - `export PATH=".:$PATH:/opt/xyz/bin"`
  - `export PATH=".:$PATH:$HOME/xyz/bin"`
# dev-05-LSP-def-docs-&-filechange-fileTree-sync-&-ideServer-jump-to-external-file-&-agentAppendFile-OT-events

## 0530

- [How is setTimeout called in a for loop js? - Stack Overflow](https://stackoverflow.com/questions/63076634/how-is-settimeout-called-in-a-for-loop-js)
  - 💡 You don't call `setTimeout()` inside a for loop. You replace the for loop with setTimeout(). This is the traditional way of doing it. 
  - You can use a Promise with async/await in modern js to use the for loop again

```JS
// async/await
async function test() {
  for (let i = 0; i < 3; i++) {
    await new Promise((resolve, reject) => setTimeout(resolve, 1000));
    console.log("hi ", i);
  }
}
test();
// traditional
let loop = 0;

function loop() {
  console.log("hi");
  x++;
  if (x < 3) {
    setTimeout(loop, 10000);
  }
}
loop();
```

- [setTimeout in for-loop does not print consecutive values - Stack Overflow](https://stackoverflow.com/questions/5226285/settimeout-in-for-loop-does-not-print-consecutive-values)
  - `for (var i = 1; i <= 2; i++) { setTimeout( () => { console.log(i) }, 100); }`  // 3, 3
  - The function argument to `setTimeout` is closing over the loop variable. The loop finishes before the first timeout and displays the current value of `i`, which is 3.
  - Because JavaScript variables only have function scope, the solution is to pass the loop variable to a function that sets the timeout.
  - `for (var i = 1; i <= 2; i++) {  (function (x) { setTimeout(function () { console.log(x); }, 100); })(i);  }`  // 仍然会同时全输出
  - You can use an immediately-invoked function expression (IIFE) to create a closure around setTimeout

## 0528

- [ByTestId | Testing Library](https://testing-library.com/docs/queries/bytestid/)

```JSX
import {screen} from '@testing-library/dom'
<div data-testid="custom-element" />
const element = screen.getByTestId('custom-element')
```

**昨天完成:** 
- [ ]  补充单元测试， 进度60%
- [x]  增强ux，打开根目录外文件显示全路径且支持点击copy
**今日计划:** 
- [ ]  补充单元测试
- [ ]  增强ux，打开根目录外文件，编辑文件前显示弹窗提示
- [ ]  编辑器支持前进后退快捷键
**思考总结:** 
- 测试覆盖率未达标的代码，如果合到develop环境，会影响别人提测
- 还会影响自测，对于测试一些服务端相关的功能，如果依赖develop的其他服务如manager/mq/lsp，那不发到develop环境实测都无法确定实现对不对

## 0523

```JS
// file request
[
  "file",
  {
    "path": "conduit/app.py",
    "fileRootId": "home",
    "fileRootPath": "",
    "readOnly": false,
    "loadType": "default",
    "timestamp": 1747992586816,
  },
  {
    "currentDockerId": "794044105415118848"
  }
]
// file response
{
  "agentUserId": "12cdfe61-72ca-4046-be33-9c2af5d23af4",
  "data": {
    "revision": 54,
    "openedPath": "conduit/app.py",
    "isRefresh": false,
    "isBinary": false,
    "ext": "py",
    "mapSelection": {},
    "content": "from fastapi import FastAPI\nfrom  "
  },
  "timestamp": 1747992587884,
  "aiCodeInfo": [],
  "requestTimestamp": 1747992586816
}
```

## 0521

- [EACCES: permission denied on yarn install · Issue · yarnpkg/yarn](https://github.com/yarnpkg/yarn/issues/1806)
  - `sudo chmod -R 777 node_modules` just fine
  - sudo npm i yarn --global

## 0520

- [Using async/await with a forEach loop - Stack Overflow](https://stackoverflow.com/questions/37576685/using-async-await-with-a-foreach-loop)
  - await y.forEach(async (x) => {})
  - await Promise.all(y.map(async (x) => {}))
  - Promise.all will run all the promises concurrently. 
  - A for loop is meant to be sequential

## 0519

- [fs - I need to create a 'touch' function in node.js - Stack Overflow](https://stackoverflow.com/questions/55342795/i-need-to-create-a-touch-function-in-node-js)
  - `fs.utimesSync(filename, time, time)`; 

```JS
// <=[fromMQ] fileChange change1-add/2-del, type0-file
// 在terminal cp文件夹 
{
  "messageId": "cd80c091-3527-11f0-8fb0-0242ac110004",
  "timestamp": 1747710551,
  "replyMessageId": "",
  "dockerId": "796427839766491136",
  "fileChanges": [{
      "path": "ffo1111",
      "change": 1,
      "type": 1
    },
    {
      "path": "ffo1111/ffo12",
      "change": 1,
      "type": 1
    }
  ]
}
// cp时包含文件
{
  "messageId": "f71f6ccd-3529-11f0-8fb0-0242ac110004",
  "timestamp": 1747711480,
  "replyMessageId": "",
  "dockerId": "796427839766491136",
  "fileChanges": [{
      "path": "ffo1333",
      "change": 1,
      "type": 1
    },
    {
      "path": "ffo1333/ffo12",
      "change": 1,
      "type": 1
    },
    {
      "path": "ffo1333/ffo12/qqqzzz.md",
      "change": 1,
      "type": 0
    }
  ]
}
// 在terminal移动文件夹 - 包含文件
{
  "messageId": "55b06fba-3529-11f0-8fb0-0242ac110004",
  "timestamp": 1747711209,
  "replyMessageId": "",
  "dockerId": "796427839766491136",
  "fileChanges": [{
      "path": "ffo1111",
      "change": 2,
      "type": 1
    },
    {
      "path": "",
      "change": 2,
      "type": 0
    },
    {
      "path": "ffo1222",
      "change": 1,
      "type": 1
    }
  ]
}
// 在terminal移动文件夹 
{
  "messageId": "cc543ff4-3524-11f0-8fb0-0242ac110004",
  "timestamp": 1747709261,
  "replyMessageId": "",
  "dockerId": "796427839766491136",
  "fileChanges": [{
      "path": "ffo12",
      "change": 2,
      "type": 0
    },
    {
      "path": "ffo11/ffo12",
      "change": 1,
      "type": 1
    }
  ]
} {
  "eventName": "fileTree",
  "agentUesrId": "shell",
  "playgroundId": "796427839711965184",
  "dockerId": "796427839766491136",
  "data": {
    "action": "CREATE",
    "files": [{
      "type": "DIRECTORY",
      "name": "ffo11/ffo12"
    }],
    "result": true
  },
  "timestamp": 1747709261188
}
// 在terminal重命名文件夹 
{
  "messageId": "40e04d09-34df-11f0-ac1b-0242ac110005",
  "timestamp": 1747679391,
  "replyMessageId": "",
  "dockerId": "796297186127343616",
  "fileChanges": [{
      "path": "ffo11",
      "change": 2,
      "type": 0
    },
    {
      "path": "ffo112",
      "change": 1,
      "type": 1
    }
  ]
}
// 手动在文件树创建文件
[
  "fileTree",
  {
    "action": "CREATE",
    "files": [{
      "type": "FILE",
      "name": "aa.md"
    }],
    "fileRootId": "home"
  },
  {
    "currentDockerId": "795083519319052288"
  }
]
```

## 0518

- [RC Config files. What are RC config files? | by Aadish N | Medium](https://medium.com/@aadishazzam/rc-files-403a2b7c80a9)
  - .bashrc
  - .npmrc
  - .eslintrc

## 0514

**昨天完成：**
- [x]  对于LSP体验增强的需求，根据review反馈和产品调整需求细节，调整技术文档
- [x]  review时光机折叠需求的技术文档
- [x]  尝试复线近一周未处理的2个issue，一个找到了方法，另一个未能复现，先停下来处理紧急issue
- [x]  测试language server的响应时间     [LSP Language Server 事件检查清单](https://www.notion.so/LSP-Language-Server-1e0a0f93102280e1abdcee39d3642010?pvs=21)
- [ ]  处理紧急issue，在terminal删除多个文件`rm *.js`时，文件树未更新，未定位到问题需要继续分析日志和代码逻辑
**今日计划：**
- [ ]  集中精力处理3个文件树同步相关的紧急issue，避免阻塞双ide需求的调研和架构分析
- [ ]  补充测试本地vscode LSP事件的响应时间
- [ ]  为clacky-ai-paas-frontend接入测试覆盖率

## 0510

- [error: the 'cargo' binary, normally provided by the 'cargo' component, is not applicable to the '1.78.0-x86\_64-unknown-linux-gnu' toolchain · Issue #12763 · rust-lang/rust-clippy](https://github.com/rust-lang/rust-clippy/issues/12763)
  - I would guess this is rust-lang/rustup#988, where e.g. rust analyzer runs at the same time you run a cargo command after updating the toolchain file.

## 0509

- [My beloved Ruby Cheat Sheet - DEV Community _202012](https://dev.to/ericchapman/my-beloved-ruby-cheat-sheet-208o)
  - full_name = 'Mike Taylor'
  - active? = true
  - fruits = ['Appel', 'Orange', 'Banana']
  - fruit_color = { apple: 'red' }
  - number.round 2.68
- [test coverage at ci · Pull Request · clacky-ai/clacky-ai-frontend](https://github.com/clacky-ai/clacky-ai-frontend/pull/913)

## 0506

- 今天计划
  - 继续调研并完成LSP体验增强的设计文档
  - 评审并修改设计文档
- 实际完成
  - 梳理了需求细节并完善了设计文档70%的内容，还要画几张架构图
  - 解决了今天刚反馈的高优先级问题，使用vim在命令行修改文件时编辑器未更新的问题
# dev-04-iframe-postMessage-&-LSP-protocol-&-codemirror-lsp-client-transport-&-lsp-def/underline-js/go/python/java

## 0428

- 今天计划
  - 解决Java代码按住ctrl不显示下划线的问题

## 0427

- 今天计划
  - 调研和开始开发hover信息卡片的交互和ui

```sh
java -Declipse.application=org.eclipse.jdt.ls.core.id1 -Dosgi.bundles.defaultStartLevel=4 -Declipse.product=org.eclipse.jdt.ls.core.product -Dlog.level=ALL -Dosgi.dev -Dsocket.stream.debug=true -DCLIENT_PORT=4000 -DCLIENT_HOST=localhost -noverify -Xmx1G --add-modules=ALL-SYSTEM --add-opens java.base/java.util=ALL-UNNAMED --add-opens java.base/java.lang=ALL-UNNAMED -jar  /Users/yaoo/Documents/active/opt/env/jdt-language-server-1.46.1-202504011455/plugins/org.eclipse.equinox.launcher_1.7.0.v20250331-1702.jar -configuration /Users/yaoo/Documents/active/opt/env/jdt-language-server-1.46.1-202504011455/config_mac -data /Users/yaoo/Documents/active/opt/env/jdtls-data
```

## 0425

- 今天计划
  - 修复测试反馈的语法跳转低优先级问题
- lsp-definition-dev-to
  - Java/Ruby 代码按住cmd/ctrl时没有显示下划线但可跳转，原因是language server的相关事件没返回，需要修复language server的配置
  - hover代码时显示类型信息或语法提示
  - 存在多个定义候选项时的交互优化
  - 查找引用， 跳转到符号

## 0424

- 今天计划
  - 优化语法跳转的细节，修复测试反馈的问题
  - 修复影响发版的问题

## 0423

- [What is the difference between decodeURIComponent and decodeURI? - Stack Overflow](https://stackoverflow.com/questions/747641/what-is-the-difference-between-decodeuricomponent-and-decodeuri)
  - encodeURIComponent("&") returns "%26".
  - decodeURIComponent("%26") returns "&".
  - encodeURI("&") returns "&".
  - decodeURI("%26") returns "%26".
  - Even though encodeURIComponent does not encode all characters, decodeURIComponent can decode any value between %00 and %7F.

## 0421

- 今天计划
  - 继续实现go语言的语法跳转
  - 优化语法跳转的功能和交互，与产品设计核对部份交互细节
    - 对于多个定义候选项的查看交互，是否采用popover(只读编辑器)
    - 跳转后自动展开并定位到文件树对应文件，隐藏文件夹下的不跳转
    - 多语言项目的LSP不支持非当前LSP语言的跳转
- 实际完成

## 0418

- 今天计划
  - 继续完善python语言的语法跳转，特别是处理Any类型和Unknown类型的提示
  - 开始实现go语言的语法跳转
- 实际完成
  - python语言的Any类型点击会居中，但没有位置跳转
  - 开始实现go语言的跳转

## 0417

- 昨天
  - 实现 ctrl + click 的下划线交互
  - 开始处理 definition事件返回多个定义项时的交互
- 今天
  - 继续处理 definition事件返回多个定义项时的交互
  - 实现和测试python语言的语法跳转

## 0416

- 昨天
  - 开始在sdk实现语法跳转功能， 处理跳转到隐藏目录如 node_modules 下的文件
  - 开始实现 ctrl + click 的下划线交互
- 今天
  - 继续实现 ctrl + click 的下划线交互
  - 测试和优化 .ts/.js 类型文件语法跳转的整体功能

## 0415

- 昨天
  - 尝试 node_modules 下的文件的自动补全和语法跳转, 处理named import和default import的差异
- 今天
  - 继续实现 node_modules 场景下，跨文件的语法跳转 demo
  - 开始在sdk实现语法跳转功能

## 0414

- terminate和revert导致action的cancel状态
- CodeEditor的逻辑为什么要和action状态相关
- 上周
  - 熟悉sdk中LSP相关的代码，理解实现原理
  - 实现了js类型文件 文件内的语法跳转， 跨文件的语法跳转demo还在实现中
  - 解决影响发版的问题，如root-thread未关闭时也能聊天、追加步骤的diff视图异常
  - 排查紧急issue，包括action执行完后文件不可编辑
- 本周
  - 在sdk，实现js/ts文件的 语法跳转、跨文件的语法跳转
  - 实现python类型文件的 语法跳转、跨文件的语法跳转
  - 尽量实现go类型的语法跳转
- 今天
  - 继续实现跨文件的语法跳转demo

## 0413

- 昨天
  - 调整quick thread的入口及交互
  - 解决root thread未close时， 聊天输入框可输入可发送信息的问题
  - 解决 追加步骤时，第一个action的diff显示异常的问题
- 今天
  - ~~处理执行命令一个打开多个端口时，webview的url会多次变化的问题~~
  - 继续跨文件的语法跳转demo实现

## 0411

- 昨天
  - 处理发版相关问题，增强端口转发的稳定性，对于一个命令开启多个端口的场景，默认在webview打开小端口
  - 排查执行task时网络断开后再恢复连接，点击action时diff视图未显示且文件不可编辑的问题
- 今天
  - 处理昨晚测试反馈的影响发版的问题，包括root-thread未关闭时可聊天、追加步骤时action的diff显示异常
  - 继续跨文件的语法跳转demo实现

## 0410

- 昨天
  - 跨文件的语法跳转demo实现，进行中80%，处理hover时按住cmd显示下划线的ux
- 今天
  - 跨文件的语法跳转demo实现

## 0409

- 昨天
  - 配合quick thread的需求， 更新了驾驶舱的快捷键引导
  - 跨文件的语法跳转demo实现，进行中70%
- 今天
  - 在sdk实现 js 文件内的语法跳转

## 0407

- 上周
  - 调研agent获取浏览器信息的方案，根据产品初步需求确定不使用rrweb的方案
  - 熟悉sdk中LSP相关的代码，尝试js类型文件的语法跳转
- 本周
  - 深入LSP的实现，修复LSP插件的现有问题
  - 尝试实现js/ts文件的语法跳转
- 今天
  - 深入LSP的实现，修复LSP插件的现有问题

## 0405

- [[@types/node] Compiler error: Cannot find module 'undici-types' · DefinitelyTyped/DefinitelyTyped · Discussion #67406](https://github.com/DefinitelyTyped/DefinitelyTyped/discussions/67406)
  - The suggestion to set `"moduleResolution": "node"` makes the error go away. However my project contains both server-side (Node) and client-side TS code, and obviously I cannot set "moduleResolution": "node" for the client-side portion. Because simply having @types/node installed is enough to trigger the issue, regardless of if the types are actually used, I'm stuck.
  - For now I've downgraded @types/node to avoid the issue. I guess I could start maintaining two separate node_modules for server- and client-side, but that seems like an inconvenient workaround for this bug.
  - 👷🏻: 最后解决方案是，手动删除 node_modules, 然后使用.nvmrc指定的版本执行npm install
- [Missing module `undici-types` · Issue #1664 · pop-os/shell](https://github.com/pop-os/shell/issues/1664)
  - The only solution I've found so far is to downgrade @types/node from 20.10.6 to `20.0.0`. (forced the downgrade using yarn's "resolutions" feature)
  - Kind of weird, I fixed this error by deleting node_modules directory.
- [[node] After running "ncu -u" and "npm install", then "tsc --project lib/typescript/cmdline/tsconfig.json" gives "node_modules/@types/node/module.d.ts:106:13 - error TS2386: Overload signatures must all be optional or required." · DefinitelyTyped/DefinitelyTyped · Discussion #70562](https://github.com/DefinitelyTyped/DefinitelyTyped/discussions/70562)
  - if you are using the v16 or v18 branches of @types/node and want to upgrade to TypeScript 5.6, then you will also need to upgrade @types/node to a compatible version (^16.18.102 or ^18.19.41)

## 0404

- [Detect network connection in React Redux app - if offline, hide component from user - Stack Overflow](https://stackoverflow.com/questions/40248639/detect-network-connection-in-react-redux-app-if-offline-hide-component-from-u)
  - `navigator.onLine` will return the status whether it is online or offline but it wont check internet connectivity is there or not.
  - The reason behind sending the get request to `google.com` instead of any random platform is because it has great uptime. The idea here is to always send the request to a service that is always online. If you have a server, you could create a dedicated route that can replace the google.com domain but you have to be sure that it has an amazing uptime.

```JS
// Check for internet connectivity
fetch('https://www.google.com/', {
    mode: 'no-cors',
  })
  .then(() => {
    console.log('CONNECTED TO INTERNET');
  }).catch(() => {
    console.log('INTERNET CONNECTIVITY ISSUE');
  })
```

## 0403

- 昨天
  - hotfix紧急修复影响发版的问题，task执行时点击已完成的action未显示diff
  - 熟悉sdk中LSP连接代码和补全相关的逻辑
- 今天
  - 修复sdk中LSP补全相关的逻辑，尝试js类型文件的语法跳转

## 0402

- 昨天
  - 微调 webview 的 loading 时间与浏览器保持一致，在 loading 时点击 refresh 会重新开始 loading
  - 调研 agent 获取浏览器信息的方案，初步方案不需要采用 rrweb，但需要采用注入脚本的方案
- 今天
  - 验证agent获取浏览器信息的方案细节，主要是iframe跨域相关操作，给出开发排期计划
  - 整理ide-server相关的问题形成文档，交接给天平

## 0401

- [can I catch exception of Iframe in parent window of Iframe - Stack Overflow](https://stackoverflow.com/questions/6327128/can-i-catch-exception-of-iframe-in-parent-window-of-iframe)
  - If it's not the same domain but you have control of the iframe content (both domains are under your control), you can communicate with the outer frame by using a cross domain communication 
- [What are the differences between normal and slim package of jquery? - Stack Overflow](https://stackoverflow.com/questions/35424053/what-are-the-differences-between-normal-and-slim-package-of-jquery)
  - The short answer taken from the announcement of jQuery 3.0 Final Release :
  - Along with the regular version of jQuery that includes the ajax and effects modules, we’re releasing a “slim” version that excludes these modules. All in all, it excludes ajax, effects, and currently deprecated code.
  - The file size (gzipped) is about 6k smaller, 23.6k vs 30k.
  - In the jquery.slim.js, the following features are removed: jQuery.fn.extend jquery.fn.load jquery.each
- 昨天
  - 微调 webview 的 loading 时间与浏览器保持一致，在 loading 时点击 refresh 会重新开始 loading
  - 调研 agent 获取浏览器信息的方案，初步方案不需要采用 rrweb，但需要采用注入脚本的方案
- 今天
  - 验证agent获取浏览器信息的方案细节，主要是iframe跨域相关操作，给出开发排期计划
  - 整理ide-server相关的问题形成文档，交接给天平
# dev-03-codemirror-EditContext-steals-rename-input-key-&-webview-iframe-onload-&-vite-routes-proxy-path-on-win-&-nodejs-utf16le

## 0331

- agent获取浏览器相关信息的需求
- [C-1444 静态代码分析方案测试调研](https://linear.app/clackyai/issue/C-1444/)
  - treesitter + Semgrep 自动修复（不可靠，强依赖Sem云端）
    - 使用 Tree-sitter 生成代码的语法树，以检测代码的语法问题和错误。
    - 静态分析与修复：使用 Semgrep 根据预定义或自定义的规则，对代码进行分析，并应用自动化修复。
    - 验证结果：再次使用 Tree-sitter 解析修复后的代码，以确认是否存在剩余的语法错误。
  - ruff/golangci-lint/eslint/rubocop + AI 片段修复
    - 为 Python、Go、TypeScript、JavaScript 和 Ruby 提供统一的语法检查方案，遵循 Ruff 的 "快速 + 结构化输出" 原则。以下是各语言工具选择和 Python 集成实现
    - 前置安装：确保所有工具已安装并加入 PATH
- 上周
  - 提测 revert后打开文件自动定位到未被revert的action
  - 提测 优化webview组件，减少白屏时间，刷新时loading反馈
  - 调研进一步减少白屏时间的方法
  - 调研LSP的原理
- 本周
  - 调研agent获取浏览器信息的方案，特别是基于rrweb的实现
  - 深入LSP的实现，修复LSP插件的现有问题
  - 尝试实现js/ts文件的语法跳转
- 今天
  - webview loading 与浏览器保持一致
  - 调研agent获取浏览器信息的方案，特别是基于rrweb的实现
  - 深入LSP的实现，修复LSP插件的现有问题

### 多标签设计与实现-快速方案

- limitations
  - 不支持超过2个分栏布局
  - 不支持一个分栏内创建tab-group
  - 支持将webview标签页自由拖拽到任意标签旁
- 单人多标签的场景，只需要在内存保存多个文件的数据，但要支持多个编辑器显示和编辑同一份数据
- 协同多标签的场景，
- 跟随模式下会自动切换标签页，
  - 大多数场景下，切换标签页时先save再切换
  - 特殊场景如用户处于cmdk或regenerate或search的输入框且修改了提示词但还没有点击send或执行，此时切换会造成用户数据丢失
    - 在cmdk未accept时切换的场景
- 更改布局的操作如浮动驾驶舱或split-editor-right是否要支持协同
  - vscode会将光标自动切换到新tab内容的对应位置
  - 标签页的其他数据如何协同，如image放大比例
- 非编辑器的页面如何协同如图片查看页、浏览器页
  - 在标签页头部显示用户头像？
  - 最好能同步光标位置，iframe内容上光标的位置难以准确确定

### 删除移动文件的设计与实现-快速方案

- action-删除文件
  - live模式显示弹窗
  - 回放模式显示红色背景的文件快照

## 0328

- 昨天
  - 修复一些测试反馈的问题
  - 在刷新页面时，自动恢复ports标签页
  - 点击action打开文件时，调整为自动打开AI Diff
- 今天
  - 继续处理测试反馈的问题，减少发版相关issue
  - 优化编辑器的抖动问题

## 0327

- 昨天
  - 提测 webview的loading反馈和优化
- 今天
  - 修复一些影响发版的问题
  - 深入调研LSP的实现原理，和在paas中的实现细节，分析现有实现的问题

## 0325

- iframe的`onload`事件发生在iframe的html的`<script>`脚本执行后
- [HTMLElement: load event - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/load_event)
  - The load event fires for elements containing a resource when the resource has successfully loaded. 
  - Currently, the list of supported HTML elements are: `<body>, <embed>, <iframe>, <img>, <link>, <object>, <script>, <style>, and <track>`.
  - The error and load events fired on `<iframe>`s could be used to probe the URL space of the local network's HTTP servers. 
  - Therefore, as a security precaution user agents do not fire the `error` event on `<iframe>`s, and the `load` event is always triggered even if the `<iframe>` content fails to load.
- 邮件子帐号
  - `username+1/2/2@gmail.com` ， gmail支持子邮箱，但业界不推荐
  - 在产品上，如果按user email收费就会存在漏洞
- 昨天
  - 测试 revert后打开文件自动定位到未被revert的action, 今天会提测
  - 修复一些影响发版的问题
- 今天
  - 完善webview刷新时的loading状态和交互细节

## 0324

- 上周
  - 完成了入职流程剩余的子需求并提测
  - 插入子需求，在thread close后，允许编辑文件
  - 优化webview组件，减少白屏时间，刷新时loading反馈未做完
  - 开始实现插入的需求，revert后打开文件自动定位到未被revert的action
- 本周
  - 提测 revert后打开文件自动定位到未被revert的action
  - 提测 优化webview组件，减少白屏时间，刷新时loading反馈
  - LSP的优化
- 今天
  - 测试diff视图的逻辑，保证准确性
  - 完善webview刷新时的loading状态和交互细节
- 昨天
  - 调整 revert后打开文件自动定位到未被revert的action，基本改完了，本地测试中

## 0323

- 昨天
  - 清理sdk的浏览器组件，将未实现完的loading隐藏
  - 与茜茜确定revert后打开文件，diff视图的对比逻辑 和 revert/restore工具条 的需求变更，调整了一部份代码
- 今天
  - 继续调整 revert后打开文件自动定位到未被revert的action
  - 测试diff视图的逻辑，保证准确性

## 0321

- 昨天
  - 在thread close后，允许编辑文件
  - 设计webview刷新时的loading状态，今天会继续完善
- 今天
  - 进一步清理sdk的浏览器组件，减少rerender的次数，来减少白屏时间

## 0319

- 昨天
  - 完成子需求，创建root-thread时添加二次确认的指引
  - 测试和检查入职流程的整体需求，已经合到staging
- 今天
  - 进一步清理sdk的浏览器组件，减少rerender的次数，来减少白屏时间
  - 和佳路讨论优化场景，打开多个端口时，webview是否要自动切换到展示最新port

## 0318

- 昨天
  - 给thread列表添加了树形ui
  - 开始入职流程最后一个子需求，创建root-thread时添加二次确认的指引
- 今天
  - 完成子需求，创建root-thread时添加二次确认的指引
  - 测试和检查入职流程的整体需求，今天应该可以合到staging

## 0317

- [[Tooltip] tooltips are shown for disabled buttons but documentation says it shouldn't happen · Issue · radix-ui/primitives](https://github.com/radix-ui/primitives/issues/1914)
  - Indeed, setting `pointer-events: auto !important` (`!pointer-events-auto` in Tailwind) allows to show the tooltip even when disabled is true
- [margin - Spacing - Tailwind CSS](https://tailwindcss.com/docs/margin)
  - Use `space-x-<number> or space-y-<number>` utilities like space-x-4 and space-y-8 to control the space between elements
- 上周
  - 开发P0级的需求，入职流程引导，实现了6个子需求，还剩2个
  - 处理用户反馈的一些问题，如路由跳转、diff不一致、文件打不开等，花费时间较多，导致入职流程需求未按时完成
  - 清理了sdk的webview的一些废弃代码和逻辑
- 本周
  - 快速完成P0级的需求，入职流程引导
  - 大概花3天开发P0级的需求, webview减少白屏时间、增加loading反馈
- 今天
  - 继续完善入职流程子需求，给thread列表添加树形ui
  - 测试和检查入职流程的整体需求，尽快上线

## 0314

- how to create terminal, send input, get result  in linux , show me dev tips and  some code examples in nodejs
  - Use `child_process.spawn` for real-time interaction
  - Use `child_process.exec` for simple commands
  - Use `stdin, stdout, and stderr` streams: to interact with the child process programmatically.
  - Use asynchronous methods to avoid blocking the Node.js event loop.
- 昨天
  - 解决用户反馈的 requirements.txt打不开的问题，已合入develop
  - 排查了用户反馈的问题，ai-diff 与 github-pr的diff不一致的问题，是产品设计问题，已反馈给佳路
  - 排查了内部反馈的一些问题，如makePlan的数据是否是修改过的数据
- 今天
  - 继续处理onboarding入职项目流程的剩余2个半需求，树形ui需要花费较多时间

## 0313

- [What is the most efficient way to read only the first line of a file in Node JS? - Stack Overflow](https://stackoverflow.com/questions/28747719/what-is-the-most-efficient-way-to-read-only-the-first-line-of-a-file-in-node-js)

```JS
const fs = require('fs');
const readline = require('readline');
// 🚨 This won't work with zero length file. The promise will wait for resolve call forever.
// Seems to work fine with a zero length file, but may be due to an update. I'm running Node v16.2.0.
async function getFirstLine(pathToFile) {
  const readable = fs.createReadStream(pathToFile);
  const reader = readline.createInterface({ input: readable });
  const line = await new Promise((resolve) => {
    reader.on('line', (line) => {
      reader.close();
      resolve(line);
    });
  });
  readable.close();
  return line;
}
```

- 昨天
  - 提测了onboarding入职项目流程的5个半子需求，还剩2个半
  - 排查了用户反馈的 requirements.txt打不开的问题，原因是ide-server读取utf16文件时识别为二进制，昨天改了这一块的逻辑但打开后乱码，今天需要继续改读写文件的逻辑
- 今天
  - 继续处理onboarding入职项目流程的剩余2个半需求，手动关闭root thread需要陈越这边更新下后端的逻辑
  - 继续处理requirements.txt打不开的问题

## 0312

- 昨天
  - 实现了onboarding入职项目流程的4个issue，还剩2个优先级高的
  - 在状状的协助下，排查了用户反馈的路由跳转未生效的问题，是用户业务侧问题，不是clacky平台问题
- 今天
  - 处理onboarding入职项目流程的剩余2个高优先级issue，涉及树形ui要花费较多时间
- 排查ai执行action结束后，打开文件ai-diff没有红绿块的问题
  - 因为ai在用户执行前的thinking阶段就自己把文件改了，这是非预期的

## 0311

- 在html中显示同向斜引号
  - `{' '} <span className='font-["Inter_Variable",_"SF_Pro_Display",_-apple-system,_BlinkMacSystemFont,_sans-serif]'> “Root Thread” </span>{' '}`

```CSS
.quotes {
  font-family: "Inter Variable", "SF Pro Display", -apple-system, BlinkMacSystemFont, sans-serif;
}
```

- 昨天
  - 清理webview react组件的一些已废弃的逻辑，减少rerender的次数，优化白屏时间
  - 进行了onboarding入职项目流程的需求评审
- 今天
  - 根据设计稿调整webview的交互细节，提升体验
  - 优化webview的loading反馈

### 💊 排查记录0311

- 🐛 问题: 用户点击 "登陆聚合页" 时，没有自动跳转到登陆界面的ui
- 💡 原因: vite在从路由 https://5800-5af768f8d191-web.clackypaas.com/ais 跳转到 https://5800-5af768f8d191-web.clackypaas.com/ais/portal.html 时，由于proxy中的路径替换没有匹配到正确的 portal.html 文件，导致这个url下前端vue组件及vue-router都未执行
  - windows下路径替换用 `\\`, clacky的cde默认是linux环境，路径替换要用`\/`
  - 解决方案如下，修改文件 `proxy/common.js`

```diff
-        const module = dir.split('\\')[1]
+        const module = dir.split('\/')[1]
```

## 0310

- 上周
  - 上线了导入知识库的需求，并修复相关问题
  - 排查ai写代码相关问题，包括重复片段、打快照超时
  - 处理文件重命名时光标跳入编辑器的问题，增加重命名时支持ESC快捷键退出
- 本周
  - 大概花3天开发P0级的需求, webview减少白屏时间、增加loading反馈
  - 会开始另一个p0级需求，LSP的优化
  - 伟强讨论后，有调整为高优先级的需求和issue也会先处理
- 昨天
  - 测试文件重命名时光标跳入编辑器的问题，已合到staging
  - 清理webview react组件的一些已废弃的逻辑，减少rerender的次数，来减少白屏时间
- 今天
  - 继续优化webview的渲染逻辑
  - 开始给webview添加loading反馈

## 0309

- 昨天
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，本地修改已完成，今天会合到staging
- 今天
  - terminal打开文件的diff视图选择非revert的action
  - 开始处理p0需求，给webview添加loading反馈

## 0308

- [Use Chrome's Developer Tools to Track Element Focus, by John Kavanagh](https://johnkavanagh.co.uk/articles/use-chrome-developer-tools-to-track-element-focus/)

## 0307

- 昨天
  - 花了点时间排查群里反馈的激活失败 DOCKER_INFO_LOST的问题
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，分析代码逻辑后没有找到快速解决的方法
- 今天
  - 换其他方法解决文件重命名时光标跳入编辑器的问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0306

- 🐛 文件重命名时光标跳入编辑器的问题
  - contenteditable的事件触发顺序: onblur > onfocusout
  - 重命名时 react input的事件触发顺序:  onKeydown(旧值) > onInput(新值) > focus
  - input连续输入字符时正确的时序: onkeydown > oninput > renderTree > ref-cb x2
- 💡 不算完美的解决方案
  - ~~对于重命名非当前打开的文件，可以将文件设为editable=false~~(非重命名的打开文件支持edit)
  - 重写重命名的逻辑
- 昨天
  - 排查ai写的代码与diff展示的代码不一致的问题，定位到是用户特殊的操作流程导致的，不是bug
  - 排查ai写文件时打快照超时的问题，根据日志可判断打快照的逻辑并未超时，由于观测云agent日志缺失，再观察看能否复现
  - 处理urgent紧急issue，文件重命名时光标跳入编辑器的问题，ai给出修改方案不work，还需要分析代码逻辑
- 今天
  - 解决文件重命名时光标跳入编辑器的问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0305

- [Why doesn't the try catch block catch the promise exception? - Stack Overflow](https://stackoverflow.com/questions/66119982/why-doesnt-the-try-catch-block-catch-the-promise-exception)

```JS
const test = async function() {
  throw new Error('Just another error')
}
// ❌ error not caught
try {
  test().then()
} catch (err) {
  alert('error: ' + err.toString())
}
// ✅ the following 2 pattern works
test()
  .then(result => {
    // ...use `result` here...
  })
  .catch(error => {
    // ...handle/report error here...
  });
try {
  const result = await test();
  // ...use `result` here...
} catch (err) {
  // ...handle/report error here...
}
```

- 昨天
  - 排查ai写的代码包含重复片段的问题，定位到问题是ai生成的代码质量有待提高
  - 排查导入知识库在develop环境能工作，但在staging环境不工作的问题，可能是提示词不好
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题，ai给出修改方案不work，还需要分析代码逻辑
- 今天
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题
  - terminal打开文件的diff视图选择非revert的action
  - 处理git stash后文件树与文件系统的同步

## 0304

- 排查rename时编辑器`view.focus()`触发的原因和位置
- [Find and replace with a newline in Visual Studio Code - Stack Overflow](https://stackoverflow.com/questions/30351529/find-and-replace-with-a-newline-in-visual-studio-code)
  - when search in file, Check the regular exp icon `.*`
- 昨天
  - 导入知识库在本地与 @陈旭东 联调完毕，前端已合入develop，agent部分昨天还没合入develop，今天会推进合到staging
  - 添加一个文件树搜索同步调用形式的api，但不work
- 今天
  - 处理git stash后文件树与文件系统的同步
  - 处理urgent紧急issue，主要是文件树重命名输入框相关问题
  - webview的loading交互及其他优化

## 0303

- [CursorList - .cursorrule files and more for Cursor AI](https://cursorlist.com/)
  - [awesome-cursorrules/rules/react-typescript-nextjs-nodejs-cursorrules-prompt-/.cursorrules at main · PatrickJS/awesome-cursorrules](https://github.com/PatrickJS/awesome-cursorrules/blob/main/rules/react-typescript-nextjs-nodejs-cursorrules-prompt-/.cursorrules)
- 上周
  - 排查用户反馈的问题，主要包括，排查 Console 输出 Cannot write file 的异常， ai写代码后在编辑器显示重复代码的问题，花了较多时间但没有找到原因
  - 优化了cde的体验细节，包括terminal打开文件路径支持显示diff，减少webview和ports出现的频率
  - 处理ide-server在监控告警上的噪音日志
  - 开发P0级的需求-导入知识库，前端进度80%
- 本周
  - 推进需求-导入知识库上线
  - webview的loading交互及其他优化
  - LSP语法跳转的修复和增强
- 今天
  - 本地测试导入知识库的需求，尽快合入staging
  - 处理git stash后文件树与文件系统的同步
  - 确定下一个开发任务
- 迭代需求重点
  - webview关闭打开逻辑优化
  - 语法跳转 (LSP跳转)
  - 编辑器 - TS 项目支持 Lint
  - Tab代码补全 - 迭代一
# dev-02-logging-to-guance-&-fix-folder-crud-loading-&-user-issues-fixes-&-ai-rules-cursorrules

## 0228

- 昨天
  - 开发P0级的需求-导入知识库，与产品设计确定了交互细节，在clacky前端实现了导入知识库的cde tools
- 今天
  - 在paas实现了placeholder占位符，完成需求开发，与意如在develop环境核对交互，与 陈旭东 联调导入知识库的完整流程，合入staging
- [Difference between DOM parentNode and parentElement - Stack Overflow](https://stackoverflow.com/questions/8685739/difference-between-dom-parentnode-and-parentelement)
  - In most cases,  `parentElement` is the same as `parentNode`. The only difference comes when a node's `parentNode` is not an element. If so,  `parentElement` is null.

```JS
document.body.parentNode; // the <html> element
document.body.parentElement; // the <html> element
document.documentElement.parentNode; // the document node
document.documentElement.parentElement; // null 👈
(document.documentElement.parentNode === document); // true
(document.documentElement.parentElement === document); // false
```

- [Is there a CSS parent selector? - Stack Overflow](https://stackoverflow.com/questions/1014861/is-there-a-css-parent-selector)
  - The W3C's Selectors Level 4 Working Draft includes a :has() pseudo-class that provides this capability
  - The pseudo element `:focus-within` allows a parent to be selected if a descendent has focus.
- [VIM: how to go to exact line on Ubuntu - Stack Overflow](https://stackoverflow.com/questions/6380635/vim-how-to-go-to-exact-line-on-ubuntu)
  - :1500
  - try `150G` to get to line 150. which is less key strokes then `:150Enter`

## 0227

<!---

# Best Practices
  - Define Rule Objectives
  - Define coding Standards & Style
  - Avoid Rule Conflicts
  - Provide Examples
  - Key Conventions
  - Organize and Tag
-->
- 昨天
  - 处理了ide-server的监控告警噪音日志
  - 优化了cde的体验细节，包括terminal打开文件路径支持显示diff，减少webview和ports出现的频率
- 今天
  - 开发P0级的需求，开发导入知识库，与 陈旭东 联调和对接
  - 处理影响发版的问题

## 0226

- 昨天
  - 修复了暂停时只剩下一个action的场景下，无法开始执行的问题
  - 协助排查agent连接ide-server超时的问题，是ide-server cpu占用高导致的
  - 下午排查ai写代码后在编辑器显示重复代码的问题，通过回放确定是OT逻辑异常导致代码写入多次，今天会通过mongodb查询ot数据来进一步确认问题的原因
- 今天
  - 继续排查编辑器显示重复代码的问题
  - ide-server的噪音处理
  - 开始分析paas现有LSP的实现逻辑和梳理现有问题
- [What is the point of finally in a try..catch? - Stack Overflow](https://stackoverflow.com/questions/73813509/what-is-the-point-of-finally-in-a-try-catch#)
  - `finally` basically runs even if you have an early-return from try-catch or even if you don't handle the error in the try-catch. 

```JS
function myFunction() {
  try {
    console.log('inside "try"');
    return
  } finally {
    console.log('inside "finally"');
  }
  console.log("after try-finally");
}
myFunction()
// inside "try"
// inside "finally"
```

- [Error: ENOENT: no such file or directory, scandir '../commands' discord.js - Stack Overflow](https://stackoverflow.com/questions/71982181/error-enoent-no-such-file-or-directory-scandir-commands-discord-js)

## 0225

- 昨天
  - 上午排查通过ssh打开clacky-cde时，ports端口转发列表包含很多端口的问题，上午时间有限没什么结论
  - 下午排查ai写代码后在编辑器显示重复代码的问题，通过日志大致确定是OT逻辑异常导致代码写入多次，今天会通过回放和mongodb查询ot数据来进一步确认问题的原因
- 今天
  - 继续排查编辑器显示重复代码的问题
  - 开始分析paas现有LSP的实现逻辑和梳理现有问题

## 0224

- 上周
  - 集中处理用户反馈的issue
- 本周
  - 继续处理cde高优先级的issue
  - 开始ports端口转发和webview的优化
- 昨天
  - 排查用户反馈的问题, Console 输出 Cannot write file 错误, 在本地ubuntu系统和clacky-ubuntu系统能复现，在本地mac不能复现
  - 和 @刘天平 排查git stash后文件系统和文件树数据不同步相关的fileChange事件，文件操作的现有实现考虑非常不全面，要花时间继续改
- 今天
  - 快速开发近期反馈的2个小优化: ide server的断连与恢复提示ui、排查白屏问题
  - 修复完和 @廖伟强 确定下一个任务的优先级，先做 ports优化，还是其他的issue

```sh
run_command: npx concurrently "cd backend && npm run start:dev" "cd admin-frontend && pnpm dev:arco"
# 对于concurrently执行的命令如何stop
```

## 0223

- 掉线提示
  - terminal光标不要闪了
- 大白屏异常排查
- webview关闭按钮
- 昨天
  - 测试用户反馈的 Run button 一直 loading 的问题，分为3个子issue，解决了2/3，剩下的 @刘天平 进一步排查
  - 修复影响发版的问题
- 今天
  - 修复用户反馈的高优先级问题, 如Console 输出 Cannot write file 错误
  - git stash后文件系统和文件树数据不同步，需要配合 @刘天平 排查fileChange事件为什么缺失部分路径
  - 修复完和 @廖伟强 确定下一个任务的优先级，先做 ports优化，还是其他的issue

## 0221

- 昨天
  - 排查用户反馈的 Run button 一直 loading 的问题，分为3个子issue，解决了1/3，剩下的需要和 @刘天平 @胡状状 讨论
  - 修复了偶尔会出现的底部时光机多个 action 进度条同时loading的问题，昨晚合入了staging
- 今天
  - 修复用户反馈的高优先级问题, 如文件树数量限制，ide异常loading时任务没有restart按钮，Console 输出 Cannot write file 错误
  - 测试和修复fileChange事件和文件树的更新逻辑
  - 测试用户反馈的开关AI Diff后编辑器出现loading的问题，已合入staging

## 0220

- 昨天
  - 测试用户反馈的开关AI Diff后编辑器出现loading的问题，已合入staging
  - 排查用户反馈的webview每隔十几秒自动刷新的问题，定位到是旧版本vite的问题，已反馈给用户
  - 协助排查用户反馈的Run button一直loading的问题，发现主流程上出现异常的不停发送激活事件但manager激活不成功及心跳异常的问题，后面主要由天平在排查
- 今天
  - 修复用户反馈的高优先级问题, 如文件树数量限制，ide异常loading时任务没有restart按钮，Console 输出 Cannot write file 错误
  - 优化ports启动白屏时间过长的问题、loading反馈
  - 进一步测试和修复fileChange事件和文件树的更新逻辑

## 0219

- 昨天
  - 测试反馈 git stash 时文件树ui和文件系统不一致的问题经常出现，需要进一步测试和修复fileChange事件和文件树的更新逻辑
  - 和测试确定语法跳转的需求范围和实现方案
  - 修复用户反馈的开关AI Diff后编辑器出现loading的问题，待进一步测试
- 今天
  - 进一步测试和修复fileChange事件和文件树的更新逻辑
  - 修复用户反馈的高优先级问题
  - 优化ports启动白屏时间过长的问题、loading反馈

## 0218

- 昨天
  - 修复了用户反馈的文件树不显示文件的问题 
  - 修复过程中发现了文件树里移动操作的实现有很大缺陷，fileChange事件不包含移动的文件，修复完待测试
- 今天
  - 优化ports启动白屏时间过长的问题、loading反馈
- [`stat` command in Linux with examples - GeeksforGeeks](https://www.geeksforgeeks.org/stat-command-in-linux-with-examples/)
  - `stat -x aa.md`; 
  - Birth: The time at which the file was created. 对于NFS系统，属性值为空
  - Change: The last time the at which file’s attribute or content was changed(the last time the file's metadata or contents were changed. Metadata includes file permissions, ownership, link count, etc.)
  - Modify: The last time at which file was modified(the last time the contents of the file were modified)
  - Access: The last time at which the file was accessed.
  - 在本地ubuntu系统，在vscode中拖拽移动文件时或通过mv移动文件时，只有ctime会变化
  - 在NFS系统，Birth一直为空, 通过mv移动文件时只有ctime会变化
- [stat(1)](https://man.freebsd.org/cgi/man.cgi?query=stat&sektion=1)
  - The -x option in the stat command is not a standard option in Linux's GNU stat utility
  - This flag is typically associated with the BSD version of stat (e.g., on macOS or BSD-based systems), where -x displays file metadata in a more verbose, "human-readable" format

## 0217

- 上周
  - 修复删除文件和新建文件夹类型的action时编辑器一直loading的问题
  - 编辑器支持.slim文件语法高亮
  - 修复cmd+p打开文件不显示diff视图的问题
  - 定位到用户反馈的文件树不显示文件的问题，原因是用户特殊的操作以及sdk文件树组件的更新逻辑异常，确定了解决方案
- 本周
  - 优化端口转发的实现细节、优化白屏时间
  - 处理未完成的cde细节优化的相关issues
- 今天
  - 快速解决文件树不显示文件的问题
  - 优化ports启动白屏时间过长的问题，增加loading的ui反馈

## 0214

- 昨天
  - 协助排查ports频繁自动断开连接且自动恢复的问题
  - 排查用户反馈的执行新建文件类型action时文件树不显示文件的问题，最后发现不是因为30个文件的限制，今天还需要继续画点时间分析日志
  - 根据反馈为了减少对服务端的影响，在playground status处于异常状态时，将每隔5s自动发动激活事件的事件间隔调整为15s-30s的随机数
  - 编辑器支持.slim文件语法高亮已上线develop环境，在develop环境测试能正常语法高亮和diff视图下正常编辑，但昨天提测的功能有点多测不过来，所以这个发版先不发这个
- 今天
  - 继续排查用户反馈的执行新建文件类型action时文件树不显示文件的问题
  - 优化ports启动白屏时间过长的问题，增加loading的ui反馈

## 0213

- 昨天
  - 在本地测试删除文件和新建文件夹类型的action，尽快合到staging
  - 修复cmd+p打开文件不显示diff视图的问题
- 今天
  - 排查ports频繁自动断开连接且自动恢复的问题
  - 执行新建文件类型action时，文件树不显示文件
  - 编辑器支持.slim文件语法高亮

## 0212

- 昨天
  - 🚧 修复执行新建文件夹类型的action时，编辑器一直loading的问题，基本修复完成还需要本地测试
  - 🚧 排查用户进入cde时卡在第3个进度条的问题，没有从底层定位到原因，在业务侧调整了发送激活事件的逻辑
- 今天
  - 在本地测试测试删除文件和新建文件夹类型的action，尽快合到staging
  - 修复cmd+p打开文件不显示diff视图的问题
  - ai执行时，ai和用户头像没有定位到文件树对应文件的问题

## 0211

- 昨天
  - 测试跟随时打开已删除文件时遇到异常大弹窗的问题，今天会合到staging
  - 修复与上面类似的问题，执行新建文件夹时编辑器一直loading
- 今天
  - 修复执行新建文件夹时编辑器一直loading
  - ai执行时，ai和用户头像没有定位到文件树对应文件的问题

## 0210

- 上周
  - 调整前端日志接入观测云的方式，补充主要流程节点的日志，方便排查用户反馈
  - 处理近期反馈的高优先级issues，如扩容提示消息、cmdL改为cmdShiftL
- 本周
  - 继续处理近期反馈的高优先级issues
  - 开发本次迭代规划的需求
- 今天
  - 测试跟随时打开已删除文件时遇到异常大弹窗的问题
  - 最近又收到新建文件类型的action执行后在文件树不显示的反馈，找到了稳定复现的方法，今天会解决此问题
  - 处理近期反馈的高优先级issues
- [Feat/fix bugs 0116 time-machine action click enhancement by huisnotacouncillor · Pull Request #491 · clacky-ai/clacky-ai-frontend](https://github.com/clacky-ai/clacky-ai-frontend/pull/491)
- [get the second to last item of an array? - Stack Overflow](https://stackoverflow.com/questions/6499012/get-the-second-to-last-item-of-an-array)

```JS
array_fragment[array_fragment.length - 2]
path.split('/').slice(-2)[0];
path.split('/').slice(-2).reverse().pop()
path.split('/').reverse()[1];
```

## 0208

- 昨天
  - 和壮壮一起补充完善了前端关键流程节点的日志，方便排查用户反馈
  - 部分实现了自定义现有的toast提示消息组件，解决机器扩容时toast消息显示多条的问题
    - 使用现有组件逻辑不方便，因为每次都会创建新的toast
  - 又收到新建文件类型的action执行后在文件树不显示的反馈，并且找到了稳定复现的方法，排查了一部分日志发现没有触发fileTree事件，今天会尽快解决此问题
- 今天
  - 解决新建文件类型的action执行后在文件树不显示的问题
  - 处理近期反馈的高优先级issues

## 0207

- 昨天
  - 因为有些紧急issue无法复现也没有日志，在clacky前端给pass初始化流程和重要事件添加了日志
  - 将前端日志从rum迁移到和后端统一的查看位置，并在文档上记录了clacky日志的格式约定
- 今天
  - 处理cde高优先级的issues，解决影响近期发版的问题
- [Typescript: No index signature with a parameter of type 'string' was found on type '{ "A": string; } - Stack Overflow](https://stackoverflow.com/questions/56568423/typescript-no-index-signature-with-a-parameter-of-type-string-was-found-on-ty)
  - (this. DNATranscriber as any)[character]; 

## 0206

- 昨天
  - 优化了机器扩容时的异常提示消息体验，今天会尽快合到正式环境
  - 将业务侧paas sdk相关的异常接入观测云，后面会将更多的关键日志接入观测云
- 今天
  - 继续cde高优先级的issues
  - 处理删除移动文件相关的问题
- [How to override multiple console function? (console.log, console.info etc) - Stack Overflow](https://stackoverflow.com/questions/73232960/how-to-override-multiple-console-function-console-log-console-info-etc)
  - for-loop 逐个覆盖
  - new Proxy(console, { get(console, key){} })
- [Hijack console.log, console.warn, and console.error without breaking the default browser function.](https://gist.github.com/designbyadrian/2eb329c853516cef618a)
- [How to override the console methods in Javascript | Our Code World](https://ourcodeworld.com/articles/read/104/how-to-override-the-console-methods-in-javascript)

## 0205

- 年前
  - 根据反馈调整端口转发的交互细节
  - 在playground状态inactive时，添加自动重试发送激活消息的逻辑
- 本周
  - 修复年前规划的剩余issues
- 今天
  - 排查文件树在某些场景下未自动更新的问题
# dev-01-forwarded-ports-&-inner-testing-fixes-agentWriteFile-timeout-&-iframe-url-updates-&-cmdk-ux-close-btn

## 0124

- 昨天
  - 和佳路确定探测中端口的交互细节，并上线staging
  - 修复一些影响发版的issues
- 今天
  - 继续修复紧急优先级的issues
  - 设计删除文件的体验和实现方案

## 0123

- [How can I force a `span` to not wrap at the end of a line? - Stack Overflow](https://stackoverflow.com/questions/7015317/how-can-i-force-a-span-to-not-wrap-at-the-end-of-a-line)

```CSS
.span-nowrap {
  display: inline-block;
  width: max-content;
}
```

- 昨天
  - 优化cde的编辑体验，进一步还原cmdk的动效边框，优化了cmdk在ai返回大量内容时的超时问题
- 今天
  - 和佳路确定端口转发中探测中端口的交互细节，并上线
  - 设计删除文件的体验和实现方案
- cmdk卡片是否要自动隐藏，不方便复制粘贴提示词，不方便在异常后保持卡片位置和内容
- cmdk的accept/reject快捷键的样式确认
- cmdk的打字效果在大文件经常超时或卡死，需要讨论解决方案

## 0122

- 昨天
  - 优化cde的编辑体验，解决了点击浮动工具条没有唤起cmdk输入框的问题，还原了cmdk的ai工作动效
- 今天
  - 继续优化cde的编辑体验，还剩余2个紧急问题
  - 设计删除文件的体验和实现方案

## 0121

- 昨天
  - 讨论并梳理年前剩余issue的复杂度和优先级
  - 开始进一步优化cde的编辑器，解决了cmd-z有时会唤起cmdk输入框的问题
- 今天
  - 继续优化cde的编辑体验，集中解决cmdk相关的问题

## 0120

- 上周
  - 集中处理体验测试反馈的问题，主要是add-to-chat背景色挡住文字、webview宽度优化
  - 修复terminal经常不可用的问题
  - 开始实现当用户点击webview内的链接时自动更新上方的url的功能，访问iframe内的对象碰到跨域问题，需要讨论下解决方案
    - 一种思路是用户访问url前向网站注入自定义js脚本逻辑
- 本周
  - 优化webview的体验
  - 实现删除移动文件在live和回放模式的表现
  - 修复年前规划的剩余issues
- 今天
  - 继续优化webview面板的体验
  - 排查文件树在某些场景下未自动更新的问题

## 0119

- [Difference between DOMContentLoaded and load events - Stack Overflow](https://stackoverflow.com/questions/2414750/difference-between-domcontentloaded-and-load-events)
  - `DOMContentLoaded` event is fired when the document has been completely loaded and parsed, without waiting for stylesheets, images, and subframes to finish loading 
  - `load` event will do it when all the images and sub-frames have finished loading.
- [Detect DOMContentLoaded in iframe - Stack Overflow](https://stackoverflow.com/questions/16960829/detect-domcontentloaded-in-iframe)
  - If your page and the iframe are on the same domain, you have to wait for the original page to fire `DOMContentLoaded` first, then attach a `DOMContentLoaded` event listener on the iframe's Window (not Document).
- 周四
  - 协助排查点击action时显示的diff视图与ai实际修改内容不一致的问题
  - 尝试实现当用户点击webview内的链接时，自动更新上方的url，参考了codesandbox的实现，确定了方案
- 今天
  - 继续优化webview面板的体验
  - 排查文件树在某些场景下未自动更新的问题

## 0117

- [WindowProxy and Window objects? - Stack Overflow](https://stackoverflow.com/questions/16092835/windowproxy-and-window-objects)
  - iframe.contentWindow, or window.frames[0], or any other way of attempting to access a window, return a WindowProxy object, not a Window object. That WindowProxy object delegates to whatever the current Window is

## 0116

- 昨天
  - 集中处理体验测试反馈的问题，主要是add-to-chat背景色挡住文字、webview宽度优化
  - 将一些无法复现的问题移入了backlog，再观察一段时间能否复现
- 今天
  - 优化webview面板的操作体验
  - 排查ai写文件超时的问题
  - 修复年前规划的剩余问题

## 0115

- 昨天
  - 修复了terminal经常不可用的问题
  - 修复了文件树搜索的关键词包含特殊字符时导致页面崩溃的问题
- 今天
  - 集中修复体验测试反馈的问题
- 🤔 [innerWidth and outerWidth oddness on desktop - Stack Overflow](https://stackoverflow.com/questions/22468878/innerwidth-and-outerwidth-oddness-on-desktop)
  - One reason `innerWidth` could be larger than `outerWidth` is if your browser is zoomed
- [AWS EFS too slow when i use git & npm install - Stack Overflow](https://stackoverflow.com/questions/63768023/aws-efs-too-slow-when-i-use-git-npm-install)
  - EFS with git, regardless of config is not working very well. However, rsync works much better. 
  - As such a workaround for EFS+git repo that worked for me: Clone to an EBS. Rsync to the EFS

## 0114

- [regex - javascript syntax error: invalid regular expression - Stack Overflow](https://stackoverflow.com/questions/16168484/javascript-syntax-error-invalid-regular-expression)
  - In this case you didn't actually need regular expressions, but if you want to avoid invalid characters in your expression you should escape it:

```JS
RegExp.quote = function(str) {
  return str.replace(/([.?*+^$[\]\\(){}|-])/g, "\\$1");
};
var re = new RegExp(RegExp.quote(filter));
RegExp.quote = function allowSpecialSymbols(str) {
  return str.replace(/([.?*+^$[\]\\(){}|-])/g, '');
};
const regExp = new RegExp(RegExp.quote('some \ string'), 'i');
```

- 昨天
  - 继续排查刷新页面不显示编辑器和文件树的问题，初步结论是没什么思路
  - 尝试修复terminal经常不可用的问题，定位到了原因，修复方法还在尝试
- 今天
  - 继续修复terminal经常不可用的问题
  - 修复体验测试反馈的问题
  - 实现删除移动文件在live和回放模式的表现
[fromMQ] fileChange

```log
[Nest] 44  - 01/14/2025, 10:13:23 AM VERBOSE [RabbitmqService] [mqName:paas-ide-server-dev-6db6599549-c84mm][playgroundId:746966488363220992][rabbitmq.service.ts:129] <=[fromMQ] fileChange[750759531793043456]:{"messageId":"21c50acd-d21d-11ef-a5ca-0242ac110004","timestamp":1736820803,"replyMessageId":"","dockerId":"750759531843375104","fileChanges":[{"path":"venv/include/python3.11","change":1,"type":1},{"path":"venv/lib/python3.11","change":1,"type":1},{"path":"venv/lib/python3.11/site-packages","change":1,"type":1},{"path":"venv/bin","change":1,"type":1},{"path":"venv/include","change":1,"type":1},{"path":"venv/lib","change":1,"type":1},{"path":"venv/pyvenv.cfg","change":1,"type":0},{"path":"venv","change":1,"type":1}]} +9038ms
```

## 0113

```shell
curl -i -X POST -H 'Content-Type: application/json' -d  '{"name": "New1", "email": "yaoo@qq.com","password":"111111"}' http://rest-api.io/items
```

- 上周
  - 修复了重启容器后部分状态未更新的问题
  - 修复布局最大化和收起terminal有时不work的问题
  - 修复了一些紧急issues，如驾驶舱聊天框的光标经常跳到行尾
  - 修复了cde一些其他issue
  - 花了较多时间排查cde激活失败、ai写文件超时、刷新页面不显示编辑器文件树的问题
- 本周
  - 实现删除移动文件在live和回放模式的表现
  - 修复年前规划的剩余issues
- 今天
  - 继续排查刷新页面不显示编辑器文件树的问题
  - 修复一些urgent优先级的bug，特别是佳路反馈的terminal经常不可用的问题

## 0110

- 昨天
  - 继续排查了agentWriteFile超时问题，但staging环境昨天无法复现了，根据日志还是把问题定位在fs.writeFile, 我把排查日志在linear上记录了，这个问题再观察一段时间
  - 修复布局最大化按钮和terminal收起按钮有时不work的问题，已合入staging
  - 修复高优先级bug，在驾驶舱输入框文字中间输入时，光标经常跳到末尾
  - 开始修复昨天反馈的搜索关键词包含正则时，卡住不可用的问题
- 今天
  - 继续修复昨天反馈的搜索体验问题
  - 修复一些urgent优先级的bug，特别是佳路反馈的terminal经常不可用的问题

## 0109

- [node.js - Fs.writeFile callback not called - Stack Overflow](https://stackoverflow.com/questions/52225476/fs-writefile-callback-not-called)
  - I've temporarily fixed the issue by writing a synchronous version with fs.writeFileSync
  - If process is dead before the writing path is done, your callback will not be called because it is an asynchronous.
- 昨天
  - 修复布局最大化和收起terminal有时不work的问题，还剩一点工作
  - 排查佳路反馈的激活失败的问题，暂时没什么解决思路
  - 排查staging环境的agentWriteFile超时问题，已定位到问题出在是node fs.writeFile这一步
- 今天
  - 修复agentWriteFile超时问题
  - 测试和完善布局相关的功能，并合入staging
  - 修复一些urgent优先级的bug，特别是聊天框输入时光标自动跳到行尾

## 0108

```log
tempOTInfo before write file: true, {"revision":0,"locked":false,"currentDoc":""} 
```

- 昨天
  - 修复restart container后，部分playground status未更新的问题
  - 排查布局上的最大化按钮、terminal收起按钮有时不生效的问题，定位到是最近实现布局自动持久化和恢复导致的，与编辑器无关，已经修改了持久化相关的逻辑，还要再测试下
- 今天
  - 测试和完善布局相关的功能，并合入staging
  - 修复一些高优先级的bug，特别是聊天框输入时光标自动跳到行尾
  - 实现删除文件在live和回放模式的表现

## 0107

- 昨天
  - 端口转发增强的功能合入staging，并修复相关问题
  - 梳理了linear上删除移动文件相关的issues，分析了删除移动重命名文件在live和回放模式的主要交互
- 今天
  - 和产品确认删除移动重命名文件的需求和交互细节
  - 实现删除文件在live和回放模式的表现
- 风险
  - terminal上的restart按钮导致容器重启后，有一些ide-server上的数据没有及时清除，如开放的端口，需要讨论解决方案

## 0106

- restartServer后如何更新ports数据
  - S1: ~~在restartServer的逻辑中，加上获取ports的逻辑~~ 后端方案，调整restart成功的时机
  - S2: 在restartServer后， 在前端业务侧手动请求ports数据，缺点是sdk的demo不能正常使用
    - 此方案耦合度最低，易维护
  - ✅ S3: 在周边事件中添加ports数据或playgroundStatus数据，如在active事件后自动发送ports数据
  - S4: 纯前端的场景定制方案, 前端主动将webview设为空白
- 上周
  - 根据业务需求，与杨豪调整了端口转发事件相关的数据结构
  - 端口转发渲染层逻辑重构
  - 进一步优化了ai写字和显示动画的时序
  - 修复cde的一些issue，如action不显示描述，webview面板的自动打开和刷新页面恢复
- 本周
  - 快速完成删除移动文件在live和回放模式的表现
  - cde空间布局体验优化
- 今天
  - 端口转发增强的功能尽快合入staging
  - 快速完成删除移动文件在live和回放模式的表现

## 0103

- 昨天
  - 根据业务需求，与杨豪调整了端口转发事件返回的数据结构
  - 重构webview组件的渲染和更新逻辑，因为要兼容很多现有的状态计算，所以没调整完，internal server error的逻辑还在处理中
  - 修复action不显示描述的问题
- 今天
  - 调整完端口转发的逻辑和体验
  - 快速完成删除移动文件在live和回放模式的表现
- 风险
  - runningStatus的现有实现对于在命令行执行程序的场景几乎没有考虑，影响到了很多组件状态，如iframe的url选择逻辑

## 0102

- 昨天
  - 在ide-server调整了ai写字和显示动画的时序，解决打字动画有时不显示的问题
  - 联调端口转发的事件和逻辑，重构webview组件的渲染和更新逻辑
- 今天
  - 调整完端口转发的逻辑和体验
  - 快速完成删除移动文件在live和回放模式的表现
