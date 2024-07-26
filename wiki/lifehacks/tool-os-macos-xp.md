---
title: tool-os-macos-xp
tags: [macos, usage-xp]
created: 2023-07-23T07:04:54.591Z
modified: 2023-07-23T07:05:19.441Z
---

# tool-os-macos-xp

# guide

# usage

## devtools

```shell

# git/github
brew install gnupg
# passphrase 1123

gpg --armor --export 74CC24A0E78125DD
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEZqNCsxYJKwYBBAHaRw8BAQdAEYetEWDc8OJtwDY5uG2tGxn1DnvEH/uwY4dr
cw+Ul0W0Lmppbnlhb28gKGdtYWlsIGZvciB5YW9vKSA8amlueWFvbzg2QGdtYWls
LmNvbT6IkwQTFgoAOxYhBGp+pD+b7/gpuBnOeXTMJKDngSXdBQJmo0KzAhsDBQsJ
CAcCAiICBhUKCQgLAgQWAgMBAh4HAheAAAoJEHTMJKDngSXdGu8BAMCCBPx/r7qX
NPB7xLzQokw5wk5rBptquuJTjYwlMW0SAPwJJyTInWterPJzwf8S5g+6vvbQ8TLW
kr1/+Es38Nh7Brg4BGajQrMSCisGAQQBl1UBBQEBB0DzgrXG8oNqdDqy2fM068uu
y/23h0rhn+3OXZmHX782dQMBCAeIeAQYFgoAIBYhBGp+pD+b7/gpuBnOeXTMJKDn
gSXdBQJmo0KzAhsMAAoJEHTMJKDngSXdOtoA/1LeTu+cgBnSNT3aL3ES+v2/90Ta
+RPNCVf9f1pdKVNyAP0TmDb1zjuoDnexxtwbMdSCz51iAxLA0N6yWmgpjS2GBQ==
=4gwC
-----END PGP PUBLIC KEY BLOCK-----
```

# blogs-tips

## [Mac使用技巧大整合：基础篇+进阶篇 - 知乎](https://zhuanlan.zhihu.com/p/89987302)

- 按住Command，可以选择并移动顶部菜单栏图标
- 在“聚焦”中搜索文件，按住Command就可以显示文件路径，按住Command打开文件可以打开所在的文件夹
- 在访达界面，按住Command键，可以拖移程序、文件、文件夹到上方工具栏或者是左侧边栏，单击就能快速打开

- 不按Option，移动文件是剪切，按住Option，移动文件变粘贴
- 按住Option，点按小三角，自动展开访达文件夹内的所有子文件夹，所有文件一览无余
# discuss-macos

# discuss-hardware
- ## 

- ## 

- ## 新买了一台新的 Mac 电脑，配置新电脑是非常开心的一个过程，分享几个我认为工程师必装的软件
- https://x.com/vikingmute/status/1800341873179111456
- zed现在支持插件吗？有兼容vscode插件的计划吗
  - 目前没有兼容计划

- HomeBrew、Wezterm、fzf、Neovim...
- DBeaver、TablePlus、Medis，数据库管理
- VMware Fusion，虚拟机
- Microsoft Remote Desktop
- RapidAPI，接口调试

- Replit 桌面客户端，作为各种语言的  Playground； 
- Kap 录制视频和 gif 的轻量工具；
- SwitchKey  自动在各个应用之间切换中英输入法；
- Linear 项目管理的好工具。

- ## 忽然想起来，Apple 主推自己的芯片之后，以后就没有for x86的macOS系统了吧？那么，以后也就没有黑苹果咧？
- https://twitter.com/choicky/status/1682953718004858882
- 对，而且win虚拟机其实也没了，虚拟出的arm的win并没有什么用
- 是的没错以后想要用hackintosh就不能用新硬件只能用老的

- 黑苹果也可以用arm芯片啊，而且成本更低

- ## [macos 如何实现 windows 的双击触摸板进行拖动 - V2EX](https://v2ex.com/t/846111)
- 触控板拖动有三种方式可以设置。
- 设置-辅助功能-指针控制-触控板选项-勾选启动拖移-不使用拖移锁定
  - 使用拖移锁定的意思是，拖移之后放开，重新移动手指还会继续拖移，直到你重新点击一下才会取消这个拖移的状态。
  - 不使用拖移锁定的意思是，单指轻轻双击之后（不用按下去）进行拖移，拖移之后放开一下立即移动还可以拖移，如果这个时间间隔稍长一点就不能在继续拖移了。
  - 三指拖移的意思是只要三个手指在触控板上移动就会触发拖移的状态。
