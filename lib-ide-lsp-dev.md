---
title: lib-ide-lsp-dev
tags: [ide, lsp]
created: 2025-01-05T14:59:47.574Z
modified: 2025-01-05T15:00:07.466Z
---

# lib-ide-lsp-dev

# guide
- pros
  - 标准化的方式，支持多种ide如vscode/jetbrains, 启发技术发展如MCP/backlink
  - 采用c/s的架构，能支持和扩展的能力更强，上限更高，比浏览器纯前端的autocomplete/lint更强

- cons
  - 会将文件内容保存在内存，对大文件不友好 ❓
  - jsonrpc是非主流协议
  - 协议设计目标未考虑并发: The protocol currently assumes that one server serves one tool

- features
  - autocomplete
  - go to definition
  - Go to Implementation
  - find all references
  - format on type
  - rich code navigation

- language-servers list
  - [Language Servers](https://microsoft.github.io/language-server-protocol/implementors/servers/)
  - [Langserver.org by sourcegraph](https://langserver.org/)
# not-yet
- ## 🆚 需求: 切换不同语言的文件时，如何快速连接到对应的 language server
  - 背景: 正在开发LSP hover/definition 相关的功能， 已经在CodeMirror6 编辑实现了LSP client， 然后本地启动单个language-server能使hover/definition正常工作
  - 方案1: 添加language server网关gateway，lsp client 每次发送的事件如textDocument/hover时都添加新字段lspLang，网关服务根据lspLang转发到对应server处理
  - 方案2: 添加language server网关gateway，lsp client 发送的事件不变，网关服务根据didOpen事件自动判断language并缓存，然后将后续请求如textDocument/hover转发到对应的server处理
  - 备注: 需要考虑多人协同编辑不同语言文件的场景。还要确保不同用户的同名文件不会混淆, 如一个关了另一个没关。
- 🤔🤔 上面的方案都是客户端主动发送languageId给gateway，可以改造下，方案1的语言由gateway根据请求参数location的文件后缀自动识别再转发到对应language server，而不用加在消息体中，这种方案需要手动解包再修改再传递？
  - 语言检测兜底逻辑，若客户端未正确发送 languageId（如自定义文件类型），网关可通过文件扩展名或内容启发式判断语言。
  - 🤔 codesandbox/replit/github-codespace 都复用了一条websocket，会定制传递LSP消息的格式

- 方案1
  - 网关逻辑相对简单，主要是一个查找表 (language -> server endpoint)，不需要维护太多状态
  - 要求客户端在 每个请求 中重复发送语言信息，而这些信息在 didOpen 时已经告诉了服务器
  - 无状态设计：网关不缓存文档语言，扩展到更多用户或语言时，网关无需调整，只需识别新字段值并转发
- 方案2
  - 有状态设计：网关需维护每个打开文档的 URI–语言 映射。用户数或文档数增加时，映射表会变大，占用更多内存；需妥善处理文档关闭(clean up)以避免泄漏。
  - 网关需要维护状态（URI 到语言/服务器的映射）。这增加了网关的复杂性，需要考虑缓存的生命周期（基于 didOpen/didClose）、并发访问、内存占用等
  - 这个方案非常适合多人协作。每个用户打开的文件会有独立的 URI。网关的缓存将是 uri -> languageId -> server 的映射
  - 使用 (session_id, file_uri) 作为缓存键，而非仅 file_uri，确保不同用户或会话的隔离性。 session_id 可通过客户端连接标识（如 WebSocket 连接 ID）生成。
# draft

# dev-xp

- 有些language server如java-jdtls在初始化时的 `initialize` 事件只会返回部分支持的 capabilities, 比如其中不包含hoverProvider/definitionProvider但server实际支持此能力
  - 实测将`initialize`事件参数中的 `dynamicRegistration` 设为false或去掉，可以在response中获取到capabilities
  - 另一种思路是，开启dynamicRegistration后lsp server会向lsp client发送 `client/registerCapability` 事件，根据事件结果可以手动更新 client capabilities
  - 另一种思路是首次触发 textDocument/hover 事件后根据结果来判断server到底是否支持此能力

- 基于web worker实现LSP的缺点，对于更新内容和types不友好
  - a language server requires all source code files be available on a local disk
  - The goal of the Language Server Index Format is to augment the LSP protocol to support rich code navigation features without these requirements. 

## LSP-diagnostics/lint

- 纯前端实现lint的缺点
  - 支持js/ts外的语言较困难
  - 跨文件的类型lint在前端难以实现
  - 前端引入lint工具包和规则包会显著增加体积，降低性能

- eslint
  - [Rules Reference](https://eslint.org/docs/latest/rules/)
  - [List of available rules](https://denar90.github.io/eslint.github.io/docs/rules/)
  - No rules are enabled by default. The "extends": "eslint:recommended" have a check mark ✅
  - The --fix option on the command line automatically fixes problems with 🔧

```JS
// response
{
  "jsonrpc": "2.0",
  "method": "textDocument/publishDiagnostics",
  "params": {
    "uri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-projects/go-gin-gorm/main.go",
    "version": 3,
    "diagnostics": [{
        "range": {
          "start": {
            "line": 9,
            "character": 1
          },
          "end": {
            "line": 9,
            "character": 55
          }
        },
        "severity": 1,
        "code": "UnusedImport",
        "codeDescription": {
          "href": "https://pkg.go.dev/golang.org/x/tools/internal/typesinternal#UnusedImport"
        },
        "source": "compiler",
        "message": "\"github.com/examples-hub/realworld-gin-gorm/validator\" imported and not used",
        "tags": [
          1
        ]
      },
      {
        "range": {
          "start": {
            "line": 36,
            "character": 4
          },
          "end": {
            "line": 36,
            "character": 13
          }
        },
        "severity": 1,
        "code": "UnusedVar",
        "codeDescription": {
          "href": "https://pkg.go.dev/golang.org/x/tools/internal/typesinternal#UnusedVar"
        },
        "source": "compiler",
        "message": "declared and not used: unusedVar",
        "tags": [
          1
        ]
      }
    ]
  }
}
```

## LSP-hover

- hover返回的数据格式都是markdown
  - hover浮窗显示在左右侧边栏内容上层
  - hover浮窗内容显示为line-wrapping自动换行，支持竖直滚动，不支持水平滚动

- tests
  - js https://develop.app.clackyai.com/thread/0197e48d-bd3b-7222-a90e-3f14ec8ec31d
  - ts https://develop.app.clackyai.com/thread/0197f28d-04e6-78b4-a6b7-d1dc981b4751
  - go https://develop.app.clackyai.com/thread/0197e8e8-2193-711d-b9f4-90f0c1553e4b
  - python https://develop.app.clackyai.com/thread/0197c3ca-9d82-7e10-8890-18834e521aa0
  - java https://develop.app.clackyai.com/thread/01971696-4771-722b-b644-a95259dcd705
  - ruby https://develop.app.clackyai.com/thread/0196f2bb-a022-7457-beba-ce32439eeb4d

- 👉 tsserver, 数据包含range
  - 结构是 code block, 后能可能接着是 换行
  - .js文件的hover数据和.ts文件数据格式相同
  - { "kind": "markdown", "value": "\n```typescript\n(alias) const hello2: \"world \"\nimport hello2\n```\n" }
  - { "kind": "markdown", "value": "\n```typescript\nfunction Root(): JSX.Element\n```\n" }
  - { "kind": "markdown", "value": "\n```typescript\nfunction useCollabMulti(): {}\n```\n测试hook方法" }
- 👉 gopls, 数据包含range
  - 结构是 code block, 后能可能接着是 ---
  - { "kind": "markdown", "value": "```go\nfunc main()\n```" }
  - 🧐 注意水平分隔线 { "kind": "markdown", "value": "```go\nfunc main()\n```\n\n---\n\n\\* \\* go的启动方法\n" }
- 👉 pylsp, 数据不包含range
  - 结构是 desc-md
  - { "kind": "markdown", "value": "```python\nmain()\n```\n\n\nRun administrative tasks." }
  - { "kind": "markdown", "value": "```python\ninclude(arg: Any, namespace: Optional[str]=...) -> Tuple[List[URLResolver], Optional[str], Optional[str]]\n```\n\n\n```\n\n```\n" }
  - basedpyright
    - 结构是 code block, 后能可能接着是 ---
- 👉 jdtls ☕️, 数据不包含range
  - 内容可能是数组，也可能不是
  - { contents: [ { "language": "java", "value": "org.springframework.web.bind.annotation. RestController" }, "annotated with @Controller and @ResponseBody"  ] }
  - { "contents": { "language": "java", "value": "AuthUtils authUtils" } }
- 👉 ruby, 数据不包含range
  - { "kind": "markdown", "value": "CodeHTML\n\n`=~ CodeHTML`" }
  - { "kind": "markdown", "value": "String\n\n`=~ String`" }
  - { "kind": "markdown", "value": "Post\n\nCalculates the factorial of a number." }

- hover ts/js
  - 对于字面量如字符串/数字/保留字，hover返回的内容是 null
  - 普通变量 "\n```typescript\nconst stateLsp=aa;```"
  - 普通方法 "\n```typescript\nfunction example(): void\n```\n"
  - 系统对象 "\n```typescript\nnamespace console\nvar console```"
  - import namespace "\n```typescript\nimport locales\n```\n"
  - import相对路径 "\n```typescript\nmodule  absolute/path/to/src.js```"
  - import三方库 "\n```typescript\nmodule  absolute/path/to/src.js```"

```JS
{
  "contents": {
    "kind": "markdown",
    "value": "```python\n(method) def format(\n    *args: object,\n    **kwargs: object\n) -> str\n```\n---\nReturn a formatted version of the string, using substitutions from args and kwargs.\nThe substitutions are identified by braces ('{' and '}')."
  },
  "range": {
    "start": {
      "line": 19,
      "character": 44
    },
    "end": {
      "line": 19,
      "character": 50
    }
  }
}

{
  "contents": [{
      "language": "java",
      "value": "java.lang.System"
    },
    "The `System` class contains several useful class fields and methods. It cannot be instantiated. Among the facilities provided by the `System` class are standard input, standard output, and error output streams; access to externally defined properties and environment variables; a means of loading files and libraries; and a utility method for quickly copying a portion of an array.\n\n *  **Since:**\n    \n     *  1.0"
  ]
}

// method: textDocument/hover
// result: Hover | null

/**
 * The result of a hover request.
 */
export interface Hover {
  /**
   * The hover's content
   */
  contents: MarkedString | MarkedString[] | MarkupContent;

  /**
   * An optional range is a range inside a text document
   * that is used to visualize a hover, e.g. by changing the background color.
   */
  range ? : Range;
}

type MarkedString = string | { language: string;value: string };

/**
 * A MarkupContent literal represents a string value which content can be represented in different formats. 
 * - Currently `plaintext` and `markdown` are supported formats
 * - If the format is markdown the content should follow the GitHub Flavored Markdown Specification.
 */
export interface MarkupContent {
  kind: MarkupKind;
  /**
   * The content itself
   */
  value: string;
}

export type MarkupKind = 'plaintext' | 'markdown';
```

## LSP-definition/语法跳转

- ux
- vscode/idea 在按住cmd+click时，会跳转到目标位置并高亮，并将光标设在高亮范围的开头，高亮很快消失
  - zed会将光标设在高亮范围的末尾
  - 💡 将光标设在开头更合理和一致，因为cmd+click点击 import的路径 会跳转到整个文件
  - vscode/zed按住cmd就会显示下划线，idea需要按住且轻微移动鼠标才会显示下划线样式
  - vscode/zed cmd+click跳转会自动居中定义所在行，若在变量仅在1处使用，则会跳转到使用处
- 对于有多个定义项的场景
  - vscode会显示一个占满编辑器宽度的popover来展示，左边是编辑器、右边是定义列表， 其实不是popover而是嵌入式卡片
    - 默认定位在当前文件的定义处,编辑器显示最新内容(split-view)
  - zed会在新标签页(defintions for variable)来展示，占满编辑器宽度的定义列表
    - 默认定位在当前文件的定义处

- 下划线的实现
  - 思路1: 利用LSP的hover事件，有内容的一般都可以跳转就显示hover; 要测试其他语言
  - 思路2: 利用codemirror的syntaxTree

- 
- 
- 
- 

- 定义跳转相关props
  - originSelectionRange: 鼠标位置下的变量或方法名
  - targetRange: 定义所在行或方法的范围
  - targetSelectionRange: 定义所在位置的变量或方法名，一般会高亮这里

- 实测点击 保留字如for 或 字面量如数字/字符串 时，返回的定义为空数组

```JS
{
  result: []
}
```

- 系统内置对象如console/window/window.setTimeout都支持definition事件
  - 可能包含多个结果
  - targetUri:"file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/node_modules/typescript/lib/lib.dom.d.ts"

### 文件内跳转的数据结构

- 对于定义自身如`let hello11 = 'Hello';`， 点击hello11会高亮自身

```JS
// textDocument/definition
{
  // 鼠标位置下的变量或方法名
  "originSelectionRange": {
    "start": {
      "line": 26,
      "character": 2
    },
    "end": {
      "line": 26,
      "character": 7
    }
  },
  // 定义所在行或方法的范围
  "targetRange": {
    "start": {
      "line": 23,
      "character": 0
    },
    "end": {
      "line": 23,
      "character": 37
    }
  },
  "targetUri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-project/jslang.ts",
  // 定义所在位置的变量或方法名，一般会高亮这里
  "targetSelectionRange": {
    "start": {
      "line": 23,
      "character": 4
    },
    "end": {
      "line": 23,
      "character": 9
    }
  }
}
```

### 相对路径跳转的数据结构

```JS
// textDocument/definition

{
  // targetUri 的路径是定义所在文件的路径
  "targetUri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-project/redux.ts",
}

// 直接点击 import { stores } from './redux';  的 ./redux，返回的定义范围是文件开头
{
  "originSelectionRange": {
    "start": {
      "line": 5,
      "character": 35
    },
    "end": {
      "line": 5,
      "character": 44
    }
  },
  "targetRange": {
    "start": {
      "line": 0,
      "character": 0
    },
    "end": {
      "line": 0,
      "character": 0
    }
  },
  "targetUri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-project/redux.ts",
  "targetSelectionRange": {
    "start": {
      "line": 0,
      "character": 0
    },
    "end": {
      "line": 0,
      "character": 0
    }
  }
}
```

### node_modules 跳转的数据结构

- 实测 default import 和 namespace import 在点击ctrl+click时，返回的定义范围相同

```JS
// textDocument/definition

{
  // targetUri 的路径是定义所在文件的路径
  "targetUri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-project/node_modules/%40types/react/index.d.ts",

}

// 直接点击 import { format } from 'date-fns'; 的date-fns，返回的定义范围是整个文件
{
  "originSelectionRange": {
    "start": {
      "line": 2,
      "character": 44
    },
    "end": {
      "line": 2,
      "character": 57
    }
  },
  "targetRange": {
    "start": {
      "line": 0,
      "character": 0
    },
    "end": {
      "line": 397,
      "character": 0
    }
  },
  "targetUri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-project/node_modules/date-fns/fp.d.ts",
  "targetSelectionRange": {
    "start": {
      "line": 0,
      "character": 0
    },
    "end": {
      "line": 397,
      "character": 0
    }
  }
}
```

- 
- 
- 

- codesandbox devbox的语法跳转
  - 在浏览器内支持跳转到symbol，跳转到相对路径，跳转到自定义路径，跳转到node_modules下的文件(不会自动定位到文件树文件)
  - 在vscode通过ssh打开时，也能跳转到相对路径/自定义路径，跳转到node_modules下的文件(不会自动定位到文件树文件)

- 💻 stackblitz纯前端方案实现的ide不支持在vscode/cursor打开
  - codesandbox的纯前端版sandbox也不支持在vscode打开

- replit的ssh/在本地vscode打开是付费功能
  - replit的定义跳转未直接使用LSP，使用自定义river协议来传输二进制数据
  - codesandbox的定义跳转也未直接使用LSP，用的是自定义二进制协议

### 根目录外的跳转

```JS
[{
  "range": {
    "end": {
      "character": 13,
      "line": 47
    },
    "start": {
      "character": 6,
      "line": 47
    }
  },
  "uri": "file:///home/runner/.pyenv/versions/3.12.8/lib/python3.12/site-packages/fastapi/applications.py"
}]
```

## LSP-codeAction

```JS
[{
    "title": "Browse gopls feature documentation",
    "kind": "gopls.doc.features",
    "command": {
      "title": "Browse gopls feature documentation",
      "command": "gopls.client_open_url",
      "arguments": [
        "https://github.com/golang/tools/blob/master/gopls/doc/features/README.md"
      ]
    }
  },
  {
    "title": "Add test for main",
    "kind": "source.addTest",
    "command": {
      "title": "Add test for main",
      "command": "gopls.add_test",
      "arguments": [{
        "uri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-projects/go-gin-gorm/main.go",
        "range": {
          "start": {
            "line": 20,
            "character": 11
          },
          "end": {
            "line": 20,
            "character": 30
          }
        }
      }]
    }
  },
  {
    "title": "Browse amd64 assembly for main",
    "kind": "source.assembly",
    "command": {
      "title": "Browse amd64 assembly for main",
      "command": "gopls.assembly",
      "arguments": [
        "1",
        "github.com/examples-hub/realworld-gin-gorm",
        "main.main"
      ]
    }
  },
  {
    "title": "Browse free symbols",
    "kind": "source.freesymbols",
    "command": {
      "title": "Browse free symbols",
      "command": "gopls.free_symbols",
      "arguments": [
        "1",
        {
          "uri": "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-projects/go-gin-gorm/main.go",
          "range": {
            "start": {
              "line": 20,
              "character": 11
            },
            "end": {
              "line": 20,
              "character": 30
            }
          }
        }
      ]
    }
  },
  {
    "title": "Show compiler optimization details for \"go-gin-gorm\"",
    "kind": "source.toggleCompilerOptDetails",
    "command": {
      "title": "Show compiler optimization details for \"go-gin-gorm\"",
      "command": "gopls.gc_details",
      "arguments": [
        "file:///Users/yaoo/Documents/repos/com2024-showmebug/yaoo/codemirror6-lsp-typescript-language-server/example-projects/go-gin-gorm/main.go"
      ]
    }
  }
]
```

# more
