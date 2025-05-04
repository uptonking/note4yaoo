---
title: tool-os-macos-xp
tags: [macos, usage-xp]
created: 2023-07-23T07:04:54.591Z
modified: 2023-07-23T07:05:19.441Z
---

# tool-os-macos-xp

# guide

# usage

## macbook

- mac-apps-loved
  - pkg-manager: homebrew, cork
  - apps: localsend

### 全局快捷键

- cmd + tab 切换程序时，松开tab然后按Q(cmd+q)，可退出程序
  - 此时可恢复隐藏窗口的app
- Command-H：隐藏最前方 App 的窗口。
  - 要查看最前方的 App 但隐藏所有其他 App，请按 Option-Command-H。
- Command-M：将最前方的窗口最小化至程序坞。
  - 要最小化最前方 App 的所有窗口，请按 Option-Command-M。
  - 此时 cmd+tab 无法恢复
- 最大化当前窗口没有快捷键
  - fn+f 可全屏当前窗口
  - Control-Command-F 全屏
  - [macos - Keyboard Shortcut to maximize a window? - Ask Different](https://apple.stackexchange.com/questions/421443/keyboard-shortcut-to-maximize-a-window)
  - [How do you maximize windows in MacOS? : r/MacOS](https://www.reddit.com/r/MacOS/comments/15t7gdc/how_do_you_maximize_windows_in_macos/)

- 截屏 cmd + shift + 3/4
  - 📷 截指定窗口 cmd +shift + 4 + space
- Option-Command-Esc：强制退出 App。

- 回到桌面 四指抓拢手势
  - cmd + f3
  - fn + f11

- Command-W：关闭最前方的窗口。 
  - 要关闭App 的所有窗口，请按下Option-Command-W

- 类似win的delete键向后删，fn + backspace

- 按住Command，可以选择并移动顶部菜单栏图标

- [Mac新手使用技巧——设置Finder(访达)快捷键](https://blog.51cto.com/u_15127651/4081089)
  - 系统偏好设置，点击键盘，快捷键选项卡，在左侧找到聚焦，看到右侧的显示访达

- [Mac 键盘快捷键 - 官方 Apple 支持 (中国)](https://support.apple.com/zh-cn/102650)
- [Use Multi-Touch gestures on your Mac - Apple Support](https://support.apple.com/en-us/102482)

- a11y
  - 在zoom可打开按住 Control+向上scroll， 向下scroll可恢复

### 文件管理器

- 显示Finder/访达: cmd+option+space
  - Command-N：打开finder新窗口
  - Command-Shift-N：在“访达”中创建一个新文件夹
  - cmd+[/]是后退或前进上一个文件夹

- 唤起finder cmd + opt + space
  - 进入Download, cmd + opt  + L
  - 进入Documents, cmd + shift  + O
  - 进入Home, cmd + shift  + H
- 打开finder，输入路径 cmd + shift + g
  - 输入~，可直接打开 /Users/yaoo
- 打开文件夹 cmd + N
- 进入文件夹 cmd + arrow-down
- 返回上级文件夹 cmd + arrow-up
- 切换到列表视图 cmd + 2
- 重命名 回车
- 删除文件 cmd + delete
- 文件路径查看 cmd + i
- 文件路径复制 cmd + opt + c
- 移动文件 cmd + opt + v

- 在finder显示文件路径
  - defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

### 浏览器

- command+L/option(alt)+command+F/fn＋control+F5：定位地址栏/聚焦搜索栏
- command+点按：新标签页后台打开链接
- shift+command+点按：新标签页前台打开链接
- control+tab/shift+command+]/shift+command+→：显示下一个标签页，其中箭头对空tab无效。
- 前后切换标签页导航
  - ctrl+shift+tab
  - shift+cmd+[
  - shift+cmd+←：显示上一个标签页，其中箭头对空tab无效。

### vscode

- 跳转到定义
  - cmd + 点击
  - cmd + f12 + fn
- 返回上一个位置
  - Windows: Alt + ← ; 或者 鼠标侧键
  - Linux: Ctrl + Alt + - ; 
  - Mac: Ctrl + -
- 左右括号之间跳转： ctrl/cmd + shift + \

## devtools

- terminal
  - fn + shift + ArrowLeft/Right 让光标跳到行首/行尾

- gpg
  - [Generating a new GPG key - GitHub Docs](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
  - [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
  - [生成新的 SSH 密钥并将其添加到 ssh-agent - GitHub 文档](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```shell

# git/github
brew install gnupg
# passphrase 1123

```

# mac-apps
- appstore
  - [MacKed - 专注于Mac破解资源的分享与下载](https://macked.app/)
    - 很多站点会转发macked的工具包
  - [MacWk.com.cn - 精品mac软件下载](https://macwk.com.cn/)
  - [MacWk.cn - 精品mac软件下载](https://macwk.cn/)
  - [XMac.App - Download crack app for mac with full speed just one step](https://xmac.app/)
  - 还可在 twitter/zhihu 搜索 mac 软件


- tips
  - 很多热门软件会在固定几个站点间相互转发，碰到失效时可以多尝试几个站点
  - 某一软件难免费，可以尝试寻找其他热门软件 或 开源替代
    - 还可以在站点交流群里面寻求帮助

- git
  - [UGit - 让每个人都可以轻松使用Git](https://ugit.qq.com/zh/) 从这个带/zh的url进去才能下载
    - 内置LFS模版，腾讯众多大型项目LFS管理经验沉淀，尤其是游戏项目
    - UGit的快速提交，可以实现只要用户提交的文件其他人没修改，可以在不更新情况下直接完成提交
    - 工蜂锁是针对游戏项目中存在大量二进制文件协作场景而设计的锁方案，解决了Git LFS Lock的稳定性和性能问题
    - 支持检出子目录
    - OAuth，支持工蜂、Github、Coding.net平台的OAuth认证
    - Gitflow，可视化的交互集成业界经典的Gitflow工作流实践
    - 加速服务，支持Git LFS缓存加速、UE4 DDC、Unity Cache
    - 多仓库管理，Git Submodule的替代方案，通过可视化操作，旨在解决大型项目多仓库依赖管理问题，支持批量克隆，一键更新、拉分支、切分支等等
    - 支持Excel Diff&Merge，支持单元格内容、公式，暂不支持表格样式
  - [Sourcetree | Free Git GUI for Mac and Windows](https://www.sourcetreeapp.com/)

- 
- 
- 

- https://github.com/mulaRahul/keyviz /GPL/cpp/dart/支持win/mac/linux
  - https://github.com/zetaloop/keyviz /汉化版
  - 一款免费开源的按键可视化软件，可以实时显示您的按键和鼠标操作
  - 在录屏、演讲还是团队协作中，您都能让观众一目了然地看到操作过程。

# arm-mac

# intel-mac

- [If you need to install Rosetta on Mac - Apple Support](https://support.apple.com/en-us/102527)
  - Open any app that needs Rosetta. If the app opens, Rosetta is already installed and working.
  - If Rosetta is not installed, you're automatically asked to install it.
  - Rosetta is not an app that you open or interact with. Rosetta works automatically in the background whenever you use an app that was built only for Mac computers with an Intel processor. It translates the app for use with Apple silicon.
# blogs-tips

## [Mac使用技巧大整合：基础篇+进阶篇 - 知乎](https://zhuanlan.zhihu.com/p/89987302)

- 按住Command，可以选择并移动顶部菜单栏图标
- 在“聚焦”中搜索文件，按住Command就可以显示文件路径，按住Command打开文件可以打开所在的文件夹
- 在访达界面，按住Command键，可以拖移程序、文件、文件夹到上方工具栏或者是左侧边栏，单击就能快速打开

- 不按Option，移动文件是剪切，按住Option，移动文件变粘贴
- 按住Option，点按小三角，自动展开访达文件夹内的所有子文件夹，所有文件一览无余
# discuss-macos

# discuss-not-yet
- ## 

- ## 

- ## [Is it possible to change the menu bar's height? - Ask Different](https://apple.stackexchange.com/questions/429853/is-it-possible-to-change-the-menu-bars-height)
- No, it is not possible to change the menubar's height using any Apple-provided settings or configuration tools.

- the Top Notch app does a decent job hiding the bar by adding a black bar around it

- [Make notch bar height configurable - Feature Requests - BetterTouchTool Community](https://community.folivora.ai/t/make-notch-bar-height-configurable/25889/1)
  - unfortunately this height is set by Apple and can not be changed as far as I know (but if I ever find a way I’ll make it configurable)

- ## [node.js - Create directory "/dotenv" on MacOs, Read-only file system - Stack Overflow](https://stackoverflow.com/questions/60469031/create-directory-dotenv-on-macos-read-only-file-system)
- If you really want to, you can disable the read-only file system in Catalina 

# discuss-macos
- ## 

- ## ScreenBrush: 录课的时候有非常多的同学都问我是什么软件，尤其是它的 Ghost Mode。
- https://x.com/vikingmute/status/1844275556797513785
  - 如果你做一些视频教程或者展示类的功能，这个软件非常好用，就一个功能，但是做的很丝滑。

- 这类软件如果再加上个快捷键显示就完美了

- 付费版 [Presentify - Screen Annotation and Cursor Highlight for Mac](https://presentifyapp.com/)

- ## [为什么会有MacWK这么良心的网站？ - 知乎](https://www.zhihu.com/question/531886608)
- 其实都是 http://mac-torrent-download.net 的搬运工（mac-torrent-download 已于2022年被FBI查封）

- 站长收了一波会员费之后，从今年初开始，就再也没回过消息。群友说站长把网站交给别人了。实际上你懂的，就是割韭菜跑路，换个网站继续

- ## [为什么macOS软件生态不敌Windows? - 知乎](https://www.zhihu.com/question/630055595)
- MacOSX: 每次升级都有老程序跑不了了
  - Windows: 每天都有人写程序，几十年前的程序还能继续跑。

- 其中一个原因是因为贵。macmini降价是最近几年的事情，十年以前往前数，苹果电脑是很贵的。

- ## 新购一台 Mac Pro M4（10+10C/32G/2T）作为办公机器，分享一下我第一时间安装的软件
- https://x.com/idoubicc/status/1899285222597984315
  - 办公必备
  - 开发工具
  - 沟通交流
  - 效率工具
  - 终端软件
  - 浏览器插件

- 推荐 Mihomo-party 替代 ClashX Pro，开源且在维护
  - mihomo内核仓库有个clash mate项目，好用
  - 不如clash verge
  - Clash Nyanpasu这个也类似

- 小火箭，其实是iPad版，但M芯片MacBook也可以安装，复制链接到剪贴板就可以添加节点。

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
# discuss-hardware
- ## 

- ## 

- ## 

- ## 

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
