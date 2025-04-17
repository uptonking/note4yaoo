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

- cons
  - jsonrpc
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
# draft

# dev-xp
- 基于web worker实现LSP的缺点，对于更新types不友好
  - a language server requires all source code files be available on a local disk
  - The goal of the Language Server Index Format is to augment the LSP protocol to support rich code navigation features without these requirements. 

## LSP hover事件

- hover返回的内容都是markdown

- hover ts/js
  - 对于字面量如字符串/数字/保留字，hover返回的内容是 null
  - 普通变量 "\n```typescript\nconst stateLsp=aa;```"
  - 普通方法 "\n```typescript\nfunction example(): void\n```\n"
  - 系统对象 "\n```typescript\nnamespace console\nvar console```"
  - import namespace "\n```typescript\nimport locales\n```\n"
  - import相对路径 "\n```typescript\nmodule  absolute/path/to/src.js```"
  - import三方库 "\n```typescript\nmodule  absolute/path/to/src.js```"

## LSP语法跳转

- ux
  - vscode/idea 在按住cmd+click时，会跳转到目标位置并高亮，并将光标设在高亮范围的开头，高亮很快消失
    - zed会将光标设在高亮范围的末尾
  - vscode/zed按住cmd就会显示下划线，idea需要按住且轻微移动鼠标才会显示下划线样式

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
# more
