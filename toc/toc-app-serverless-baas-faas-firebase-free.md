---
title: toc-app-serverless-baas-faas-firebase-free
tags: [baas, faas, firebase, free, serverless]
created: 2022-02-26T15:46:39.316Z
modified: 2022-02-26T19:26:04.762Z
---

# toc-app-serverless-baas-faas-firebase-free

# guide
- 选择的产品方向
  - 存储、图片
    - 七牛云oss：每个月有免费的10G流量
    - 腾讯云oss
    - 将对象存储作为类关系型数据库使用的缺点
  - 数据库
    - [飞书，一个免费的在线数据库，提供了云文档api、多维表格api](https://zhuanlan.zhihu.com/p/234834695)
      - 后端存储基于飞书文档，中台提供一个serverless服务 + API网关，前端使用飞书的小程序，界面采用类似AirTable的形式。 这样就可以类似AirTable那样搭建各种各样的应用了
  - serverless/faas
    - 腾讯云Serverless、CloudBase
    - 阿里云Serverless

- 国内可用免费托管
  - gitee pages 需要等待人工审核
# popular

## 免费cdn

### css/js 的免费cdn

- popular
  - https://www.bootcdn.cn/all/
- more-cdn
  - http://jscdn.upai.com/
  - https://www.staticfile.org/

## 免费图床

- guide
  - 很多需要绑定备案过的域名
  - 注意支持https是否需要付费
- 体验
  - 建议直接建站，打包发布图片，维护更容易

- [为什么国内没有像样的图床?](https://www.zhihu.com/question/19758488/answers/updated)
  - 最主要就是成本问题。作图床吃力不讨好，没有稳定的能长期付费的消费群体
  - 其次政策以及监管问题。
  - 用户上传的图片无法得到长期的保存。不知什么时候就会倒闭跑路。就算是微博图床这类大图床，也会有这类问题，前段时间微博开启了防盗链
  - 对于图床有比较大的需求的用户，还是建议使用自建图床

- Github+jsDelivr搭建免费快速的个人图床
  - https://cdn.jsdelivr.net/gh/你的用户名/你的仓库名@发布的版本号/文件路径

## 腾讯云 免费额度

- [CloudBase 免费额度](https://cloud.tencent.com/document/product/876/47816)
- 免费资源是以环境维度赠送，不区分计费模式；
  - 例如在腾讯云云开发已创建一个包年包月免费版环境，此时再创建按量计费环境时不会有免费资源赠送。
- 云存储
  - 容量	5GB
  - 下载操作次数	2000/月
  - 上传操作次数	1000/月
  - CDN 回源流量	1GB/月
- 云函数
  - 资源使用量 GBs	1000/月
  - 外网出流量	1GB/月
  - 函数数量限制	150个
  - 固定外网 IP	✓
- 数据库
  - 容量	2GB
  - 同时连接数	5个
  - 读操作数	500/天
  - 写操作数	300/天
  - 集合限制	15个

- 静态网站托管、云托管、短信
  - 1个月的免费体验

- 包年包月免费版套餐
  - 每个月都会清空上月未用完的免费额度，生成当月新的免费额度。
  - 包年包月环境使用免费版套餐，超出用量上限当前环境会被隔离停服（不影响其他环境），如需恢复请升级套餐或等待下月自动恢复。

- [云开发 Webify：专为 Web 开发者打造的应用托管平台，极速开发、部署、上线](https://webify.cloudbase.net/)
  - Web 应用托管采用按量计费模式，自身能力免费，应用按照其使用的 TCB 底层环境的各项资源独立计费，如静态托管等。
  - Webify 为每个应用分配一个专属的免费默认域名，天然支持 HTTPS，您也可以将自己的域名绑定至 Web 应用托管。
  - Webify 集成了各类框架，从基于 React/Vue 的前端应用，再到 Next.js/Nuxt.js 等一体化框架
  - Webify 内置 CI/CD 能力，您只需要将变更推送至 Git 仓库，便可触发应用的构建和重新部署。

- [Serverless 应用中心 购买指南](https://cloud.tencent.com/document/product/1154/38792)
- 云函数 SCF
  - 每月可享受 40万GBs 的免费资源使用量及100万次调用次数
- 对象存储 COS
  - 新开通对象存储 COS 服务的个人用户将享受6个月 50GB 标准存储容量的免费额度

- 云函数
  - 调用次数	5万次（事件函数和Web函数各5万次）
  - 资源使用量	2万GBs
  - 外网出流量	0.5 GB

- 使用中国内地（大陆）的 Serverless 服务开办网站并绑定域名服务时必须先办理网站备案，备案成功并获取通信管理局下发的 ICP 备案号后才能开通域名访问。

## 阿里云 免费额度

- [函数计算 计费概述](https://help.aliyun.com/document_detail/54301.html)
- 免费额度：函数计算每月为您提供价值约46元的免费额度，注意 免费额度只能在弹性实例的按量付费模式下使用。
  - 调用次数：每月前100万次函数调用免费。
  - 函数实例资源使用量：每月前400, 000 GB-秒函数实例资源使用量免费。

- 如果您在浏览器中直接打开请求地址，将会以附件的方式下载响应。
  - 这是因为 Http 触发器会自动在响应头中添加 Content-Disposition: attachment 字段。您可以使用自定义域名避免该问题。

- 对象存储OSS
  - 新用户免费试用

## aws 免费额度

- 永久免费
  - Amazon DynamoDB 25G 
    - 快速灵活的 NoSQL 数据库，具有无缝可扩展性。
  - AWS Lambda
    - 每月的免费请求数 100w
  - Amazon SNS

## 七牛云

- [七牛云 CDN 免费额度](https://www.qiniu.com/prices/qcdn)
  - 开通七牛云 CDN 并完成实名认证的用户可分别享有国内和海外 10 GB HTTP 下载流量以及 5 万次动态加速请求数免费额度。
  - 每月计费时，会先抵扣免费额度，超出部分再按照价格详情付费结算
- 静态 HTTP 下载流量/动态加速 HTTP 流量
  - 10G 免费（仅限静态 HTTP 下载流量）
- 静态 HTTPS 下载流量/动态加速 HTTPS 流量
  - 0.28 元/GB

- [七牛云开发者 免费额度](https://developer.qiniu.com/af/kb/1574/free-credit-information)
- 对象存储
  - 标准存储免费空间	0-10 GB
  - 标准存储数据读取	无上限
  - 标准存储 GET 请求	第 0 次至 100 万次
  - 标准存储 Put / Delete 请求	0-10 万次
  - 标准存储 CDN 回源流出流量	0GB - 10GB
  - 上传流量	无上限
- CDN
  - 国内、国外	HTTP 下载流量	第 0 GB 至 10 GB
  - 注：中国大陆和其他区域独立享有 10G HTTP 免费额度，共 20 G。
- 部分图片处理服务
  - 每月共享 20TB 免费额度

## 免费云数据库、对象存储

- https://db4free.net/
  - db4free.net is a service for testing, not for hosting. 
  - Databases that store more than 200 MB data will be cleared at irregular intervals without notification

- [目前国内有哪些免费的云数据库？](https://www.zhihu.com/question/23221581/answers/updated)

- [Using Amazon S3 as a limited-database](https://stackoverflow.com/questions/59623145)
  - 将对象存储作为类关系型数据库使用的缺点
  - using s3 for database or data storage will make you code more complex. 
  - since you need to retrieve file from s3 every time and have to iterate thorough the file every time. 
  - I think your code will be more efficient if you use dynamodb with all its feature. 
  - And in case of dynamodb you can easily query and filter the data which is required. 
  - At the end s3 is a file storage and dynamodb is a database.
# ref
- [如何看待心动网络收购 leancloud ？](https://www.zhihu.com/question/453253024)
  - 因为阿里，腾讯都在大力推 serverless ，本质上会完全取代 leancloud。

- [CODING 网站托管服务倒闭](https://www.v2ex.com/t/822876)
  - 因 CODING 产品战略调整，决定将于 2021 年 12 月 30 日起不再提供网站托管服务的使用入口，请您直接前往腾讯云 Serverless 控制台使用，并对站点进行管理与维护
  - 国内连有统一后台的博客都没几个办得下去的，何况是这种不方便统一审核的；我从来不信国内这类平台可以不收费而长期稳定运营
