---
title: lang-golang-toolchain-devtools
tags: [devtools, golang, toolchain]
created: 2025-04-09T02:58:15.644Z
modified: 2025-04-09T02:58:41.258Z
---

# lang-golang-toolchain-devtools

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-golang-js-wasm
- ## 

- ## 

- ## 

- ## 

- ## 在 js 中可以写 golang 了？这是我今天看到的很创意的玩意
- https://x.com/vikingmute/status/1983153718754456049
  - https://github.com/yarlson/vite-plugin-use-golang
  - 在文件前面写个 'use golang' 的 directive（又是 directive）就可以愉快的写 go 代码了。
  - 原理： * 提取 use golang 其后跟随的 Go 代码 * 将其写入 .vite-golang/ 目录下作为一个临时 .go 文件
  - 运行 `tinygo build -target wasm` 进行编译
  - 返回一个 JavaScript 模块，加载 WASM 并使函数可用
  - WASM 文件会被打包进你的应用中。你通过 http://js.Global(). Set() 暴露的函数将出现在 window 对象上。

- 直接import go文件多舒服，用个loader 处理下

- 从 Go 1.11 开始，Go 提供了对 WebAssembly 的实验性支持，并且在后续版本中不断改进。 WebAssembly 并非静态语言专属。 虽然很多静态语言都可以编译成 WebAssembly，但动态语言 (例如 Python, JavaScript) 也可以通过一些方式在 WebAssembly 上运行。

- go 支持 wasm，wasm 3 已经正式发布， 原生支持 gc， 这样像 go 这样有垃圾回收机制的，编译成 wasm，体积更小

- tinygo是go的子集，没有go的运行时，可以编译到wasm
# discuss-pkg/gvm
- ## 

- ## 

- ## 🆚 [Difference between go mod download and go mod tidy - Stack Overflow](https://stackoverflow.com/questions/71495619/difference-between-go-mod-download-and-go-mod-tidy)
  - When I run `go mod tidy` , if the import is not found it also downloads it.
- The `go mod download` command is useful mainly for pre-filling the local cache or to compute the answers for a Go module proxy.
- `go mod tidy` .
  - It adds any missing modules necessary to build the current module's packages and dependencies, and it removes unused modules that don't provide any relevant packages. 
  - It also adds any missing entries to go.sum and removes any unnecessary ones.

# discuss-compiler
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 
