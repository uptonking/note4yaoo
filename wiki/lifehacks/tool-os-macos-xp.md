---
title: tool-os-macos-xp
tags: [macos, usage-xp]
created: 2023-07-23T07:04:54.591Z
modified: 2023-07-23T07:05:19.441Z
---

# tool-os-macos-xp

# guide

# usage
- clean-mac
  - 清理空间很有用的工具 onyx, 在没怎么清理 `~/Library/Caches` 文件夹的情况下都能释放大约6GB空间

## macbook

- mac-apps-loved
  - pkg-manager: homebrew, cork
  - apps: localsend

### hotkeys

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

- open settings
  - alt + any-fn-keys

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

- [How to set a keyboard app shortcut on macOS (along with submenus)](https://woorkup.com/keyboard-app-shortcut/)
  - Edit->Paste From->Rich Text
  - You have to add `->` without any spaces in-between the menu title fields.

### finder/files-explorer

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

- tags
  - spotlight中设置排除文件夹fo11可能导致fo11下文件的tags都失效
  - [Mac点击Finder左边的「标签」，右侧无对应文件；关闭Spotlight聚焦之后的小麻烦。 - 知乎](https://zhuanlan.zhihu.com/p/138489878)

- 在finder显示文件路径
  - 在view中设置显示 path bar 比文本路径更友好
  - defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES

- disable cmd+shift+I 默认会打开邮件
  - settings > Keyboard Shortcuts > messaging/text > New Email With Selection
  - To disable it: Simply uncheck the box next to "New Email With Selection".

- [Navigate a zip without extract it : r/MacOS](https://www.reddit.com/r/MacOS/comments/rhy7xr/navigate_a_zip_without_extract_it/)
  - I see many recommend BetterZip and it is an amazing fully featured app. But for me it is very expensive and I don't use any of the features. 
  - The dev is awesome though and has made the QuickLook part of it free for all: https://macitbetter.com/BetterZip-Quick-Look-Generator/

### safari

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
  - fn + ArrowLeft/Right 让光标跳到terminal的头部/尾部
  - cmd+D 会竖向显示2个terminal， cmd+shift+D可还原

- gpg
  - [Generating a new GPG key - GitHub Docs](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
  - [Generating a new SSH key and adding it to the ssh-agent - GitHub Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
  - [生成新的 SSH 密钥并将其添加到 ssh-agent - GitHub 文档](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```shell
# GNU versions of head, ls, cat, and many others
brew install coreutils
gbase64 -w 0 /dev/urandom | ghead -c 2M > textfile.txt

# git/github
brew install gnupg
# passphrase 1123

redis-server /opt/homebrew/etc/redis.conf
redis-cli shutdown

```

- little snitch 查看network monitor面板的快捷键显示在设置界面

- 查看开放端口: 
  - 可查看进程名: (sudo) lsof -i -P | grep LISTEN
  - 无进程名: netstat -an | grep LISTEN
  - [Open Ports for macOS](https://openports.app/)
    - lsof -P -iTCP -sTCP:LISTEN +c0
    - kill -15 {PID}
# mac-apps
- appstore
  - [MacKed - 专注于Mac破解资源的分享与下载](https://macked.app/)
    - 很多站点会转发macked的工具包
  - [MacWk.com.cn - 精品mac软件下载](https://macwk.com.cn/)
  - [MacWk.cn - 精品mac软件下载](https://macwk.cn/)
  - [XMac. App - Download crack app for mac with full speed just one step](https://xmac.app/)
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

- monitor
  - network: sniffnet
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
# discuss-macos-tricks
- ## 

- ## 

- ## [Change DNS Server From Terminal (or script) on Mac OS X - Super User](https://superuser.com/questions/86184/change-dns-server-from-terminal-or-script-on-mac-os-x)

```sh
sudo bash
mkdir /etc/resolver
cd /etc/resolver
echo "nameserver 119.29.29.29" > domain.tld
echo "nameserver 223.5.5.5" >> domain.tld
```

- ## [Difference between CleanMyMac and CleanMyMacX ? : r/MacOS _202501](https://www.reddit.com/r/MacOS/comments/1i5kqr4/difference_between_cleanmymac_and_cleanmymacx/)
- They are both overpriced garbage apps.

- Why would you use clean my Mac where there is another tool which is free and open like onyx. 
  - Also this tool do nothing to Mac, clearing cache you can do on the command line easily and no risk to expose your data to shady companies.

- ## [macos - Is it safe to delete `~/Library/Caches` ? - Ask Different](https://apple.stackexchange.com/questions/118941/is-it-safe-to-delete-library-caches)
- It's generally safe, though a little dangerous depending, to do it but often not worth the effort.
  - The caches in `/System/Library/Caches` are generally small and useful, the ones in `/Library/Caches` are less system caches and much more readily cleared.

- Have no fear, delete caches but I prefer to do it either via Single-User mode or I use https://www.titanium-software.fr/en/onyx.html Check Onyx out as it does some good maintenance scripts as well.

- [macbook pro - Is it ok to delete all the folders inside the library caches folder on macOS? - Ask Different](https://apple.stackexchange.com/questions/479156/is-it-ok-to-delete-all-the-folders-inside-the-library-caches-folder-on-macos)
  - I contacted Apple direct and they told me to : 
    - Drag the entire content of the Caches folder into trash
    - Restart the machine
    - Delete the trash

- ## 🛢️ [How to do I clear system data on Mac OS? : r/MacOS _202307](https://www.reddit.com/r/MacOS/comments/154rp99/how_to_do_i_clear_system_data_on_mac_os/)
- there are several ways to clear system data on Mac OS.
  - 1: Clear system cache: Go to Finder > Go > Go to Folder, then type in `~/Library/Caches` and hit enter. Select all the folders inside the Caches folder and delete them.
  - 2: Clear system logs: Go to Finder > Go > Go to Folder, then type in `/var/log` and hit enter. Select all the files inside the Log folder and delete them.
  - 3: Remove unused language files: Go to Finder > Go > Go to Folder, then type in `/Library/Languages` and hit enter. Delete all the language folders you don't need.
  - 4: Uninstall unused apps: Go to the Applications folder and delete the apps you don't use.
  - 5: Clean up system files: Use a system cleaning tool like CleanMyMac X to scan and remove unnecessary system files.

- I cleared 190Gb of my system data by having a look at :
  ~/Library/Caches
  ~/Library/Logs
  ~/.cache
  ~/.gradle/caches
  XCode Derived Data
  XCode Simulators
  Docker containers (docker system prune -a)

- here's what my problem was: A 400GB Spotlight search index.
  - sudo du -hs /System/Volumes/Data/. Spotlight-V100/

- ## [Please help me stop mediaanalysisd process because I'm losing my sanity : r/MacOS _202505](https://www.reddit.com/r/MacOS/comments/u17hsa/please_help_me_stop_mediaanalysisd_process/)
- Try: killall -STOP mediaanalysisd mediaanalysisd-access
  - This is the only one that worked for me, without disabling SIP. Huge thanks!

- I recently had the same problem. Seems like it was fixed when I turned off siri.

- ## [system data taking up all my storage, how do i fix this? : r/mac _202211](https://www.reddit.com/r/mac/comments/ynv4d0/system_data_taking_up_all_my_storage_how_do_i_fix/)

```sh
# `du` (disk usage) and `df` (disk free) to work out dirs space consumption
df -h | grep Gi

# `/dev/disk3s5 - /System/Volumes/Data` is consuming large space
du -h /System/Volumes/Data | grep "G\t" | sort -rh
# Then you can manage sub directories similarly and remove files you no longer need.

```

- I followed this thread, and it worked great. Also can recommend using CleanAppsNow app to uninstall software without leftovers. Especially important for programs that like to cache a lot of stuff.

- [Using Terminal to Find Large Files and Folders](https://macmost.com/using-terminal-to-find-large-files-and-folders.html)
  - find . -size +20M -exec du -hs {} \; | sort -hr | head -n 10
# discuss-not-yet
- ## 

- ## 

- ## 

- ## [How to use keyboard shortcuts to navigate the OS X Finder sidebar? - Super User](https://superuser.com/questions/90378/how-to-use-keyboard-shortcuts-to-navigate-the-os-x-finder-sidebar)
- cmd+shift+G Then just fill in the filepath: ~/Desktop | /Backups | and so on.

- ## [Is it possible to change the menu bar's height? - Ask Different](https://apple.stackexchange.com/questions/429853/is-it-possible-to-change-the-menu-bars-height)
- No, it is not possible to change the menubar's height using any Apple-provided settings or configuration tools.

- the Top Notch app does a decent job hiding the bar by adding a black bar around it

- [Make notch bar height configurable - Feature Requests - BetterTouchTool Community](https://community.folivora.ai/t/make-notch-bar-height-configurable/25889/1)
  - unfortunately this height is set by Apple and can not be changed as far as I know (but if I ever find a way I’ll make it configurable)

- ## [node.js - Create directory "/dotenv" on MacOs, Read-only file system - Stack Overflow](https://stackoverflow.com/questions/60469031/create-directory-dotenv-on-macos-read-only-file-system)
- If you really want to, you can disable the read-only file system in Catalina 

# discuss-macos-devtools
- ## 

- ## [MinIO Object Storage for MacOS](https://min.io/docs/minio/macos/index.html)

```sh
brew install minio/stable/minio
brew install minio/stable/mc

minio server --console-address :9001 ./path

# append an ampersand (&) to your command to run it in the background.
MINIO_ROOT_USER=admin MINIO_ROOT_PASSWORD=password minio server ./data --console-address :9001 &

nohup minio server ./data --console-address :9001 &

```

- ## [Install Redis on macOS | Docs](https://redis.io/docs/latest/operate/oss_and_stack/install/archive/install-redis/install-redis-on-mac-os/)

```sh
brew install redis

brew services start redis

brew services info redis
```

- ## [How to Install MySQL on Mac _202305](https://medium.com/@rodolfovmartins/how-to-install-mysql-on-mac-959df86a5319)
- brew install mysql
- 

- ## [[PostgreSQL] Installing PostgreSQL through Homebrew on MacOS - DEV Community _202304](https://dev.to/uponthesky/postgresql-installing-postgresql-through-homebrew-on-macos-388h)
  - [How to Enable Remote Access to PostgreSQL 15 on macOS (Homebrew) _202501](https://medium.com/@jaatcodes/how-to-enable-remote-access-to-postgresql-15-on-macos-homebrew-95923e62166e)

- [PostgreSQL14安装并初始配置外部连接指南。 - 星小梦 - 博客园](https://www.cnblogs.com/XingXiaoMeng/p/18722581)
  - [PostgreSQL 初始化配置设置 - Amd794 - 博客园](https://www.cnblogs.com/Amd794/p/18634417)

- [Setting Up PostgreSQL for macOS Users: Step-by-Step Instructions _202410](https://dev.to/techprane/setting-up-postgresql-for-macos-users-step-by-step-instructions-2e30)

```sh
# 👇 需要手动加上版本号，发行版默认可能是旧版
brew install postgresql@15

brew services start postgresql@15

# -s, --superuser role will be superuser, to fix role postgres not exist
createuser -s postgres
psql -h localhost -U postgres

psql -h localhost -U testuser12 -d testdb12;

# /opt/homebrew/var/postgresql@17/postgresql.conf
listen_addresses = '*'

# /opt/homebrew/var/postgresql@17/pg_hba.conf
host    all             all             0.0.0.0/0               md5

```

```sql
-- set pass
CREATE USER postgres WITH PASSWORD '11111111';
ALTER USER postgres WITH PASSWORD '11111111';
ALTER USER some_user PASSWORD NULL;

CREATE ROLE username WITH LOGIN SUPERUSER CREATEDB CREATEROLE PASSWORD 'password';
GRANT ALL PRIVILEGES ON DATABASE products_db TO your_username;

ALTER USER myuser WITH SUPERUSER;

-- createdb testdb, createdb is a command line utility
CREATE DATABASE mydatabase;

```

# discuss-macos
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [“kextload” in Login Items? What is it? Leads to “sbin” : r/MacOS](https://www.reddit.com/r/MacOS/comments/1ceieyy/kextload_in_login_items_what_is_it_leads_to_sbin/)
- It’s a Kernel Extension loader likely used for NTFS for Mac.

- ## [Finding/ getting rid of the source of a background task in the "Allow in the Background" list? : r/MacOS](https://www.reddit.com/r/MacOS/comments/1jz5qs8/finding_getting_rid_of_the_source_of_a_background/)
- Open Terminal and run `sfltool dumpbtm` . 
  - You can Cmd-F for "He X1a0" and it should show you its filepath.

- ## [Desktop wallpaper keeps changing back - Apple Community](https://discussions.apple.com/thread/254934033?sortBy=rank)
  - OnlySwitch存在相同的问题

- Any one who have installed an app called TopNotion, you may need to uninstall or disable the dynamic wallpaper option, this application changes the wallpaper automatically.

- [Sonoma Wallpaper resets to default??? : r/MacOS](https://www.reddit.com/r/MacOS/comments/16t3vcc/sonoma_wallpaper_resets_to_default/)
  - TopNotch is the issue. You can turn it off, set the wallpapers, and turn it back on.
  - I am currently using for the past 6 months the Bartender app. it has a feature where you can change the menu bar style. it has been flawless 

- ## [Option + Command + Spacebar opens Searching this mac window instead of Finder - Ask Different](https://apple.stackexchange.com/questions/360114/option-command-spacebar-opens-searching-this-mac-window-instead-of-finder)
- Command + Option + T makes the sidebar appear again 

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

- ## [小米67w充电器（非氮化镓）可以用来给macbook air m1充电吗？拿来长期使用的话可以吗？ - 知乎](https://www.zhihu.com/question/609382105)
- 可以，其实只要充电头有20vPD挡位，不管是30w、65w、120w都能冲，无非是跑不满充电速度慢而已。但不建议长期使用，因为手机充电头散热不行，满功率输出对充电头的寿命影响很大。

- 只有12V甚至9V档位也能充，就是慢而已

- 可以用, 没什么大问题。我的m1pro16寸这么用很久了, 更多的时候用的显示器的65w或90w反向充电。

- 没有任何问题，充电器会量力而行的，笔记本电池只怕过放过冲（放电到20%以下，非常伤电池）和高温

- ## [2分钟看懂MacBook Air 13 M4充电 - 小红书](https://www.xiaohongshu.com/explore/67fa37d2000000001c032013?xsec_token=ABufSAS9QghohUw1fzyX0iVCtCVyatOV4oAVyqAGiEEzQ=&xsec_source=pc_search&source=web_search_result_notes)
  - 这款MacBook Air 13 M4在充电方面变化依然不大，可以兼容常见的C口充电器快充，最高功率可以到71W，实测26分钟可以充到50%，1小时58分钟完全充满，充电期间几乎感觉不到发热
- 结论是三方充电器也正常可以用哈

- [MacBook 新发现 - 小红书](https://www.xiaohongshu.com/explore/6814360b0000000022029d14?xsec_token=ABxl5JKVzVRtrdRLAFg3NctkZfBWcgYO1O8rrAd2AbM5Y=&xsec_source=pc_search&source=web_search_result_notes)
  - 我买的时候店员说c口可以，但是充电头要30w以上
- 一直是C口充，好几年了
- m1max c口充了4年 电池一点问题都没有 

- 充电宝建议用支持30瓦以上功率的，如果充电宝功率太低，不仅充不上电，还会掉电，甚至给充电宝反向充电

- 我的建议是，把那破原装头子扔了，自己买个大功率的氮化镓PD头，体积小，还能同时给多个设备充电

- 一直都这么用，家里的磁吸，外出就配一个安钛克的电源一根c口线，手机电脑都能用。

- 自从发现小米13充电器能给苹果67w快充后，就再也没用过苹果自带35w磁吸

- 如果是Air，本来充电器的功率就是三十瓦，所以充电宝充也没事，Win本一般都是65瓦，普通充电宝带不动

- 我都是这么干。小米65w 1A1C省事不累赘，冲啥都够用。

- 那么安卓的手机充电器也可以给mac充电喽？
  - 和什么机型没关系 只要不是特殊协议的手机充电线都可以通用 关键要看数据线（一般叫充电线）的规格 充电器是包含电源适配器和数据线 两个都相互牵制和影响 笔记本如果支持小功率充电的话 usb3.0 的数据线就能充 快慢的区别

- ## [Macbook M1 充电头不见了 但是原装好贵 其他的充电头能用吗？ 会影响电脑电池吗？#macbook配件 - 小红书](https://www.xiaohongshu.com/explore/6721c776000000001d03b23d?xsec_token=ABFkQO1Gl1-pWnjjLTpAWVDyLPOz9T9XFtoQloixAZNB8=&xsec_source=pc_search&source=web_search_result_notes)
- 买个65W的PD充电头就可以了，还能给手机充电

- 随便买个pd45w就行，原装那个才30w就是一个垃圾，我到手就扔了

- ## [求助用小米充电线充苹果15会坏吗？今天没带充电器，抱着试试看心态试了一下用小米可以充 - 小红书](https://www.xiaohongshu.com/explore/669dd5ea000000002701e02a?xsec_token=ABNHgVtAj61rOEMKna5VW9dgOseLpizS3wNz4tG_ctWks=&xsec_source=pc_search&source=web_search_result_notes)
- 不会坏 我天天用小米的

- 我的头坏了，为了省钱天天用的红米充电器，而且充电嘎嘎快

- 小米的通用性比较高，支持pd协议，可以冲苹果。华为的不能充苹果

- 别慌，我还特地买的小米头、线、充电宝来冲

- ## [用type C给macbook充电，应了个急～ - 小红书](https://www.xiaohongshu.com/explore/67b033390000000018011760?xsec_token=AB37FEjnwyYBwILr2RQtHgsUPJG_R7tHXshaF6wgKnQHo=&xsec_source=pc_search&source=web_search_result_notes)
- typec充电的非常慢
  - 那是你电源适配器功率太低，和c口半毛钱关系都没有，甚至magsafe接口之前还被砍掉了，只能插c口充，后面可能觉得还是蛮好用的又给加回来了

- 随便用，我16寸MBP常年用20瓦usbc供电...magsafe基本不用

- 以前去掉 MagSafe 的几年不都是用 usbc 充电的

- ## [好消息！小米不愧是苹果配件厂！ - 小红书](https://www.xiaohongshu.com/explore/6512bd92000000002101c2d5?xsec_token=AB7S78mwEXZaZh0gSyTUVw_q3ouqUlGKUpD3TeOZWbOmo=&xsec_source=pc_search&source=web_search_result_notes)
- 附上直营店店员原话
  - 任何c口线都可以插手机
  - 两端都是c口的线需要配有PD协议的充电头
  - macbook和iPhone的充电器和充电线可以互相用，是上下兼容的，不会出现功率不足或者过大的问题

- 苹果全系列都是PD协议，只要充电头是PD协议就行。功率的话按照水桶效应看，取决于设备/充电头/线各自支持的最大功率的最小值。
  - 比如你拿120W的头充手机，那就会自动协商到手机支持的最高功率，也就是20W。 给电脑的话建议查查电脑是否支持PD充电，以及支持的功率。上古时代小新不一定支持PD，就算支持PD也很可能是65W，没法满足电脑满功率运行的需求。
- 买的原装，不过现在用小米好像也没坏

- [Macbook 充电器好大 - 小红书](https://www.xiaohongshu.com/explore/666951e1000000000e0307c8?xsec_token=ABXyox8CPEs6q5AuOLEfiN3b4dYGZMf2o469B0lqMOBrU=&xsec_source=pc_search&source=web_search_result_notes)
  - 我的m3 pro从开盒之后就没用过原装充电器，被我送给同事了，一直在用小米65w、120w、努比亚80w充电头，还有办公桌上的5w USB充电头，和你们对比起来我是不是对它太坏了

- ## [小米手机充电器能给mac充电吗 - 小红书](https://www.xiaohongshu.com/explore/66d58a37000000001f016b32?xsec_token=AB36raZON7rhJOGKgOTp2CP19lw-O7OQ2_SZBPEkbc7rg=&xsec_source=pc_search&source=web_search_result_notes)
- 可以，小米这个充电器支持65w PD协议，兼容Mac

- [求问：苹果笔记本可以用90w的小米充电器吗 #不懂就问有问必答 #万能的小红书 出门不想带那么多充电器 - 小红书](https://www.xiaohongshu.com/explore/67a02f7c000000001800fdbe?xsec_token=ABe2aRwCPTUNI2eh71Dom8V9RUIjYcjLXJFQaYmjJD3kk=&xsec_source=pc_search&source=web_search_result_notes)
  - 我经常用65w氮化镓充。一点事都没有

- [小米充电器充Macbookpro - 小红书](https://www.xiaohongshu.com/explore/668107e4000000001d016265?xsec_token=ABnKza9r9cWVkWBcrFnQEixWaDHr-AD6HPAwyXjyghnnY=&xsec_source=pc_search&source=web_search_result_notes)
  - 用Mac充电器充手机，发现充的也挺快，而且没发现异常
  - 今天想试试手机充电器能不能充电脑，充了一会，电量有增加，系统信息显示27w

- MacBook对PD协议支持很全的，上至20V，下至9V，都可以充电，不像很多国产笔记本，只支持20V档位
- 我小米 14 的充电器拿来充 mac 还很快

- ## [自己总结手机和笔电充电器互充的注意事项 - 小红书](https://www.xiaohongshu.com/explore/67d2cb090000000006029e0b?xsec_token=ABG6d6mee-BXD05kT1s72Bc2B5lIldBwmav5XAb7e1JeA=&xsec_source=pc_search&source=web_search_result_notes)
- 移动设备充电器协议常见的有两种，一种普通dc充电器（无协议）；第二种是带协议的充电器，主要有qc、pd(pps)、ufcs等，还有各家手机商私有协议挺杂的，不妨统称pd充电器。

- ## [忘带💻电源结果发现手机充电线也能充… - 小红书](https://www.xiaohongshu.com/explore/6821ea190000000021019b91?xsec_token=AB7IcqjUbnYI73r3Laq2wuGuhtKqzA2XGPVKpwkd9DXB0=&xsec_source=pc_search&source=web_search_result_notes)
- 线不重要 头尽量用原装的

- 只要支持PD 充电就都能充啊
  - 苹果都是pd充电，是公版协议，除了华为的某些充电器，几乎所有手机品牌的充电器都可以充，不过功率多高就说不准了。不过苹果设备的充电，是可以长时间跑满功率的，你20w充电器充电脑，充电器要累瘫了

- 不能总用这种瓦数低的充电器充电脑 轻则损伤电池 严重的话就会跟我上一台电脑一样直接主板给烧了
  - 太扯犊子了这个发言，我的Air支持140w，原生充电线时候30w，就是说我一直这样用会把主板烧了？你这个怎么看怎么不对劲，真的服了在这里误导人
- Air苹果自己宣称140w，他的包装里面一直放的就是30w充电器，按照你的意思不就是不能用低瓦数的充电头，这不就是无解，或者Air包装盒里面的充电头给iPhone用？
  - 宣称140w是它最高支持140w的功率 原配的30w是它功率的最低标准 低于这个标准充电会造成损伤（转自Genius Bar工作人员）我所谓的低瓦数充电器是低于它自带的原装充电器瓦数
- 我去Genius Bar修电脑的时候工作人员跟我说的是主板烧了 因为我经常用小功率充电器边充电边使用 所有我就这么发出来 你杠就是你对喽

- ## [如果你有Mac那么你就不需要再买充电头了 - 小红书](https://www.xiaohongshu.com/explore/671b485e000000001b02e470?xsec_token=ABbW1fXGj4wn9zVrDpQ9rElRJTRkI14EqnX07TkY8QUls=&xsec_source=pc_search&source=web_search_result_notes)
- 其实Apple官方也说过Macbook 61W到140W的充电头可以为iphone充电。

- 我就用macbook充电器给ipad 和iphone充电。懒得买头头了

- 我是MacBook air ，手机电脑充了半年了通用

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
