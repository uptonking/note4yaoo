---
title: thread-dev-tech-stack
tags: [dev, tech-stack, thread]
created: 2022-12-03T15:30:28.915Z
modified: 2022-12-03T15:30:59.732Z
---

# thread-dev-tech-stack

# guide

# discuss
- ## 

- ## 

- ## 

- ## Stack Overflow bucks(反抗, 抵制) the microservices trend, _202311
- https://twitter.com/sahnlam/status/1719568996297740759
  - handling 1.3 billion monthly pageviews across its 200 sites using a remarkably efficient monolithic architecture with minimal infrastructure.
  - [Performance - Stack Exchange](https://stackexchange.com/performance)
- Web Servers:
  - Uses only 9 on-prem IIS web servers
  - Each server has 64GB RAM and runs highly optimized . NET code
  - Handles 450 peak requests/second per server with just 12% CPU usage
  - Code minimizes memory allocations to limit garbage collection
- SQL Servers:
  - Organized into 2 failover clusters of 2 servers each
  - First cluster: 1.5TB RAM per server
  - Second cluster: 768GB RAM per server
  - About a third of the Q&A dataset resides in memory
  - Each cluster handles over 10, 000 peak queries/second at ~15% CPU
- Redis:
  - A single 256GB main server with a replica
  - Handles 60000 peak ops/sec at 2% CPU

- ## 记录一下简单简历(http://easycv.cn) 用到的所有优质的免费服务
- https://twitter.com/vikingmute/status/1597417185470992384
- 免费的HTTPS服务，这个已经多次推荐过了，
  - 还是放在这里：https://github.com/acmesh-official/acme.sh 或者是 https://certbot.eff.org 
  - 他们提供的脚本生成 let's encrypt 或者 ZeroSSL 的证书，如果国外用户可以直接选择 Cloudflare 的服务
- 免费的企业邮箱，因为应用在国内，所以用了网易的免费邮箱，https://ym.163.com 容量 3G, 速度挺快，反正能用就行。欢迎大家推荐其他的企业邮箱。
  - 免费企业邮箱，https://zoho.com.cn/mail/ 基本满足需求，我看了一下，比 163 的更好，网易的免费版本会是不是有广告，让人不舒服。

- 免费域名：http://freenom.com
  - 很有意思，可以免费提供 tk, ml, ga, cf, gq 后缀名的域名，一下可以同时注册多个后缀，虽然是不太常见的后缀，但是用来做个项目冷启动时很不错的，可以配合 cloudflare pages 做静态网站。
  - 注册很快，我五分钟就搞好了n个，比如这个：http://easycv.ml
- 免费的 CDN 服务，国外的朋友当然可以还是使用 Cloudflare https://cloudflare.com/zh-cn/cdn/ 如果只是 JS 第三方库，可以选取：https://jsdelivr.com
  - 国内的服务比较杂，我尝试的还没有完全免费的服务，比较便宜的有百度云加速，七牛云等，还没有找到最好的方案，欢迎大家补充。
- 免费静态网站托管，这里推荐的两个都是更针对国外用户，国内没有好用的类似服务，
  - https://pages.cloudflare.com 非常棒，免费版完全都满足需求，无限的请求和带宽，自带 CDN 以及 HTTPS。
  - 另外一个大名鼎鼎的 https://vercel.com ，带宽有 1G 限制，不过也完全够了。

- 免费的 landing page 搭建，
  - 很多后端同学不是很会前端，需要快速搭建一些页面，可以使用 https://landing.ant.design/index-cn 基于 ant design，特别丰富的组件和编辑器，直接下载源代码。
  - 喜欢 tailwind.css 可以使用 https://tailblocks.cc 一些常用的模块都有，支持多种颜色，非常实用。
- 免费的图标素材，使用 https://fontawesome.com 可以满足大部分的需求，如果实在没有，可以在 https://iconfinder.com 筛选 free 的图标。
- 免费音乐素材，因为有时候要拍各种视频，需要添加背景音乐，我选择了 https://uppbeat.io 的音乐，完全免费，可以随便使用，使用的时候需要在简介中注明版权信息就好了，非常好用，强烈推荐一下。
- 免费的插画，landing page 不放几张插画是说不过的，我相信这两个网站无数人推荐过了，还是放在这里：https://undraw.co/illustrations
  - 免费的插画网站，很丰富，而且多个参数可以调整，同样可以收藏一下：https://storyset.com
- 免费 PS：https://photopea.com 大名鼎鼎的产品，做产品免不了要修改图啥的，下个PS 太痛苦了，photopea 拯救了我，还是非常实用的。我还写过它一个免费产品怎样一年赚 50 万美元的故事

- 文档型数据库，基于Key Value存储。
  - 首推AWS的DynamoDB，免费档有25G的存储1G的数据传输量，配合缓存基本上可以满足大部分应用需求。
  - Azure的CosmosDB也不错，免费档也是25G存储，比起DynamoDB的API更丰富，甚至可以兼容MongoDB和Postgresql。
  - 但这两都需要应用程序支持
- RDS关系型数据库，大部人都比较熟悉，绝大部分开源系统都是RDS的数据。
  - 但是免费选择不多，AWS和Azure上的RDS都很贵。
  - 目前发现最好的免费方案是PlanetScale https://planetscale.com ，免费档有5G存储。普通应用足够用了。
- 实时数据库，做聊天、实时交互的应用不错。
  - 代表性的是Firebase，早已被Google收购，免费档有1G存储，10G流量，API简单方便。
  - 还有Supabase也不错，完全就是仿照Firebase设计的，但是免费档只有500MB存储和2G流量。
