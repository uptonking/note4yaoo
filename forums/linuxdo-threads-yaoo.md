---
title: linuxdo-threads-yaoo
tags: [forum, linuxdo, yaoo]
created: 2026-02-12T12:11:42.166Z
modified: 2026-02-12T12:25:24.608Z
---

# linuxdo-threads-yaoo

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# 整理下免费提供 GLM 5 大模型token的 API (非公益站) 和 Coding 工具  __20260212

> 多次触发审核，但同样的信息其他人发短内容就没问题
> 已放弃， 可能是markdown格式的列表和emoji 被判断为agi内容
> 帖子语言风格也像 agi

~~GLM 5 已经在2月11号发布，佬友们都蹬上了嘛，~~
下面整理下免费提供 GLM 5 的渠道，失效了就评论下提醒我更新。

## 免费 API

- Modal平台免费提供API到4月30号 [Try GLM-5 on Modal](https://modal.com/blog/try-glm-5)
  - 在官网 [Modal](https://modal.com/) ~~通过 google/github 注册后~~， 访问 https://modal.com/glm-5-endpoint 创建api token, 就可以像公益站的api一样使用了
  - token **免费不限量**, 但请求并发数是 1: Usage is limited to a single concurrent request.
  - 实测速度大概是 32 token/s

- 阿里魔搭 [GLM-5](https://modelscope.cn/models/ZhipuAI/GLM-5)
  - 魔搭平台的热门模型请求限制会动态调整，大概一天200次左右 

- ~~S级推荐:~~ 阿里iflow-cli命令行已经免费提供不限量的glm-5, 需要手动通过类似 [CliProxyAPI](https://github.com/router-for-me/CLIProxyAPI) 的工具 2api 后才能在其他工具使用api
  - 暂时只能在 iflow-cli 免费使用， 资源紧张，速度不快
  - **用CliProxyAPI工具2api导出 glm-5 暂时未实现**，需要等开发者修复，修复后我会更新

- Ollama cloud [glm-5](https://ollama.com/library/glm-5)
  - 注意免费用量有 每5h限制， 每3天限制

- [AIHubMix](https://aihubmix.com/model/coding-glm-5-free): 每天免费 1M token
  - 没有渠道时，可以凑合用用
 

## 免费 工具

- Kilo Code/CLI 限时免费: [GLM-5 is free on Kilo Code/CLI](https://blog.kilo.ai/p/glm-5-free-limited-time)
  - 在官网 [Kilo Code](https://app.kilo.ai/get-started) 去下载 vscode扩展或cli工具，~~登录kilo账号~~就能免费用了

- 字节 [TRAE IDE ](https://www.trae.cn/)
  - 需要更新到最新版才能看到免费的 glm 5, 快来个懂哥试试要不要排队(以前经常排队)

> 敲碗等 Coding 工具开始推广 ...

## 其他

其他非公益站的大模型API可以看我以前的帖子，因为时间太久已经无法编辑了，但大多渠道都还能用

https://linux.do/t/topic/1349579
