---
title: pm-saas-xp-web-browser
tags: [browser, saas, xp]
created: 2021-08-02T15:19:56.259Z
modified: 2021-08-02T15:20:28.360Z
---

# pm-saas-xp-web-browser

# guide
- tips
  - 第三方书签/收藏夹同步服务
  - 类似 History Trends Unlimited 这类离线分析服务

# extensions

- edge直接支持从chrome的webstore中安装extensions

# sync

- chrome的同步需要代理

- edge的同步系统设计得非常缓慢，一次只上传20个bookmarks
  - 上传数量过多时就开始出现一次比一次长的`SERVER_RETURN_THROTTLED`强制等待时间
- edge导入本地bookmarks.html时，经常出现无响应并且什么都没导入的问题

- firefox的国际版和国内版数据不能同步
  - firefox官方提供的安装包默认只能登录firefox.com.cn国内版账号；
  - 国际版需要到ftp目录去下载，然后在设置同步的地方选择切换到全球同步服务，否则仍然是使用国内版同步服务

