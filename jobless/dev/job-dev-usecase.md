---
title: job-dev-usecase
tags: [job, usecase]
created: 2021-09-24T18:42:57.211Z
modified: 2021-09-24T18:43:09.080Z
---

# job-dev-usecase

# guide

# 扫码登录的实现思路
- 参考淘宝的实现
  - 用户网页每隔3秒发送一次匿名扫码请求登录
  - 服务端首次生成并返回 qrLoginId 设置到cookie，并在网页展示qrLoginRequestId的二维码
  - 服务端在扫码前不再对重复请求生成新的qrLoginId，直接返回listening
  - 用户手机app内扫码，确认发送userInfo+qrLoginId到服务器
  - 服务端对手机登录请求信息验证通过后，就对下一个网页登录请求的qrLoginId返回正常登录成功的响应结果，更新或添加到cookies

- 用户请求登录，服务端根据请求生成一个有有效期的UUID，存储为一个数据库字段key，并以此生成网页二维码，响应给客户端
- 客户端收到后，网页周期性携带UUID向服务端请求，查询字段的value是否完整，判断是否登录
- 用户使用手机扫码确认，将UUID和用户信息（或加密后 token）一并发送至服务端
- 服务端根据UUID，将用户信息存为字段value
- 此时浏览器下次请求时，字段完整，开始在服务端内部使用 value中的密码信息登录，响应登录成功的token 
# 单点登录的实现思路
- 之前谈到的session还有token的方案，在集群环境下，他们都是靠第三方缓存数据库redis来实现数据的共享。

- JWT全称JSON Web Token，实现过程简单的说就是用户登录成功之后，将用户的信息进行加密，然后生成一个token返回给客户端，与传统的session交互没太大区别。
  - 不同点就是：token存放了用户的基本信息，更直观一点就是将原本放入redis中的用户数据，放入到token中去了！

- token: header + payload + signature

- ref
  - [手把手教你，使用JWT实现单点登录](https://zhuanlan.zhihu.com/p/141065758)
# 海量数据哈希

> 海量IP中找出访问量 topK 的IP、使用什么算法、如果建立哈希表时内存不足怎么办

- 哈希映射
  - 总共1000G，内存1G，则通过哈希函数将大文件映射到1000个小文件中，
  - 因为使用了哈希函数，则相同 IP 一定会映射到同一文件，
  - 如果单文件超过了 1G，则使用线性探查思想，向下一个相邻文件写入
- 遍历每个小文件，更新 IP 键值对
# bloom过滤器
