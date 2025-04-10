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

- ## 
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
