---
title: lang-rust-toolchain-devtools
tags: [devtools, rust, toolchain]
created: 2023-05-07T18:08:15.286Z
modified: 2025-04-09T02:49:51.857Z
---

# lang-rust-toolchain-devtools

# guide

# discuss-stars
- ## 

- ## 

- ## macOS 上 Rust 构建速度慢的原因：
- https://x.com/vikingmute/status/2004471362841403485
  - 当编译产生的可执行文件被运行时，MacOS 内部的 XProtectService 守护进程会对其进行恶意软件扫描，这个扫描是单线程的，导致在构建过程中产生大量临时二进制文件时，延迟会累积。
  - 作者推荐的修复方法是将你常用的终端应用添加到 系统设置 > 隐私与安全性 > 开发者工具 中，标记为 开发者工具。这样就可以跳过 XProtect 扫描了。
  - 作者测试Rust 编译器自身的 tests/ui/ 测试套件（涉及近 4000 个小型测试二进制文件），运行时间从 9 分 42 秒缩短至 3 分 33 秒，加速约 63%。
  - 理论上来说所有可编译语言都可以用这个方式加速，不仅仅限于 Rust。
- [Faster Rust builds on Mac _202509](https://nnethercote.github.io/2025/09/04/faster-rust-builds-on-mac.html)
  - You can avoid these scans by adding Terminal (or any alternative terminal app you are using, such as iTerm) as a “developer tool” in System Settings.

# discuss-pkg/cargo
- ## 

- ## 

- ## 
# discuss-compiler/rustc
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## [Error: "could not amend shell profile" when HOME is unwritable · Issue #2040 · rust-lang/rustup _202112](https://github.com/rust-lang/rustup/issues/2040)
- 

```sh
sudo chown $(whoami) ~/.bashrc
sudo chmod 777 ~/.bash_profile

// OR

curl--proto '=https'--tlsv1 .2 - sSf https: //sh.rustup.rs | bash -s -- -y --no-modify-path
```

- ## rustc --version显示的是旧版本
- 卸载通过apt安装的rustc，使用rustup安装的
- [Setting "rustup default nightly" and back to stable ends up using older leftover version](https://github.com/rust-lang/rustup/issues/451)
