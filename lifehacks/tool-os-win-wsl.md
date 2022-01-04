---
title: tool-os-win-wsl
tags: [windows, windows-subsystem-linux, wsl]
created: '2020-11-25T11:03:58.894Z'
modified: '2020-12-22T12:41:57.687Z'
---

# tool-os-win-wsl

# guide

- 是否有必要从ubuntu切换到wsl
  - 是自己笔记本电脑的问题
    - 不管是在win下还是ubuntu下，都会出现找不到硬盘的情况
    - 都会无法开机

- wsl优点
  - 同时使用优秀的win工具和linux工具，如office excel、shell

- wsl缺点
  - 暂时不完善，特别是对GPU的支持
  - 跨系统访问文件和文件夹效率不高，文件路径不简单
  - 被 docker 的网络和 wsl2 的网络问题搞了一上午。还没解决。
  - webpack热加载不支持
  - 在windows删除linux安装的node_modules超级慢

- 使用Linux开发并不一定需要自己装一个Linux，
  - 一般思路是远程登陆到服务器上，用ssh登陆到服务器上进行开发。也是不错的选择。
# pieces

- wsl体验
  - react开发可以无缝切换
  - wsl自身内存占用很高

# 在windows中访问wsl

- 在wsl中启动create-react-app npm start后，在win上 http://localhost:3000 可直接访问
  - 注意win主机ip为 192.168.x.x，但访问wsl时localhost对应的ip为  http://172.28.200.181:3000


# 在wsl中访问windows

- curl yaoohpwin10.local
  - 不能用 curl yaoohpwin10
  - 不能用 curl yaoohpwin10.localdomain

# wsl install

- wsl 默认安装路径
  - C:\Users\jinya\AppData\Local\Packages\CanonicalGroupLimited. Ubuntu16.04onWindows_79rhkp1fndgsc\LocalState

- [服务器Ubuntu安装nvm踩坑篇](https://blog.csdn.net/handsomezhanghui/article/details/111872159)
  - failed to connect raw.githubusercontent.com port 443
  - 解决方法 修改 hosts 文件

# ref

- [nvm 安装失败の解决方案!](https://segmentfault.com/a/1190000040303862)
- [Ubuntu 必备配置 && 开发环境配置](https://juejin.cn/post/6844903935279366152)
  - /etc/sudoers
    - 将 %sudo ALL=(ALL:ALL)ALL 修改为  %sudo ALL=(ALL:ALL)NOPASSWD:ALL
- [在win10的WSL中设置前端开发环境](https://juejin.cn/post/6844903892564574222)
