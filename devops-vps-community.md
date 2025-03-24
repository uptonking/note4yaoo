---
title: devops-vps-community
tags: [community, vps]
created: 2024-11-16T10:52:39.113Z
modified: 2024-11-16T10:52:53.263Z
---

# devops-vps-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 对比不同平台 serverless 的结论出来了，有点出乎意料。同样 hono 写后端，开发部署速度、性能、成本最优都是 AWS Lambda。
- https://x.com/zhdsuperman/status/1904070505583563070
  - AWS 的方案是一开始最不愿意用的，结果用 CDK 编排技术栈上线速度超快，控制台都不用打开域名、证书、DNS 解析都自动配完了。
  - 使用 CDK 前提要熟悉 AWS 各种服务。

- lambda 性价比这么高吗？
  - vercel 的函数计算背后就是 aws lambda。

- 也应该是对比AWS GCP Azure. 过来人经验，不要被cdk拴死，直接上terraform

- ## 国内的云服务器快到期了，不打算续了。准备全部搞到海外服务器，但又不想用aws，调研一番，
- https://x.com/wsygc/status/1856623132087558565
  - 似乎digital ocean + dokploy是个不错的选择，兼具了便捷与可定制化。 有实战经验的推友分享下吗？
- 刚实战完，dokploy 非常好用
- 我看dokploy官方视频演示的就是 Hetzner ，算是官推首选了，有点介意的是“德国”产品，会不会延迟比较高

- 然后你的域名还需要转移出去，否则没法用，因为海外没法备案，然后你把域名从国内转移到国外会发现有多麻烦。 而国外域名往国内转就有想收个验证码的事儿
