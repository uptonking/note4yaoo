---
title: job-fe-web-dev
tags: [frontend, job, web]
created: 2021-09-23T08:18:44.835Z
modified: 2021-10-10T09:19:13.926Z
---

# job-fe-web-dev

# guide
- not-yet
  - 利用http range实现请求github pages上托管的sqlite的部分数据
# web性能优化
- 资源压缩
- 异步加载
- 浏览器缓存
- cdn
- 懒加载
- 服务端推送
# http协议
- 用户和服务器之间的信息传递依赖http request和http response
  - 报文一般包括了：通用头部、请求/响应头部、请求/响应体

## https

- https 就是安全版本的 http
  - https 在请求前会在客户端与服务器建立 ssl 链接，确保接下来的通信都是加密的
  - 要将网站升级成 https，需要后端支持，申请 ssl 证书等
  - 因为需要建立安全链接以及加密，https 的开销比 http 要大，所以一般来说 http2.0 配合 https 的体验更佳
- 主要关注的就是 SSL/TLS 的握手流程，共5步

## http 1.0/1.1/2.0

- 1.0 to 1.1
  - HTTP1.1 默认支持长连接
  - HTTP1.1支持只发送 header 信息，节约带宽
  - HTTP1.1 的请求消息和响应消息都支持指定 Host 域，1.0请求消息中的 URL 并没有传递主机名（hostname）
  - 1.0 中主要使用 header 里的 Expires 来做为缓存判断的标准
    - 1.1 则引入了更多的缓存控制策略，例如 Cache Control、Entity tag、 If-Match 等更多可供选择的缓存头来控制缓存策略

- 1.1 to 2.0
  - HTTP/2 采用二进制格式传输数据，而非 HTTP/1.x 的文本格式。二进制格式在协议的解析和优化扩展上带来更多的优势和可能
  - HTTP/2 对消息头采用 HPACK 压缩传输，能够节省消息头占用的网络的流量。而 HTTP/1.x 每次请求，都会携带大量冗余头信息，浪费了很多带宽资源。
  - 多路复用，直白的说就是所有的请求都是通过一个TCP 连接并发完成。HTTP/1.x 虽然通过 pipeline 也能并发请求，但是多个请求之间的响应会被阻塞的，所以 pipeline 至今也没有被普及应用，而 HTTP/2 做到了真正的并发请求。同时，流还支持优先级和流量控制
  - Server Push：服务端能够更快的把资源推送给客户端。例如服务端可以主动把 JS 和 CSS 文件推送给客户端，而不需要客户端解析 HTML 再发送这些请求。当客户端需要的时候，它已经在客户端了
# 跨域解决方法
- cors
  - 在服务器设置 header 的 Access-Control-Allow-Origin 为请求端域名（设置为 * 时不安全）
- jsonp
  - 点击 button 时，触发动态添加 `<script>`，且令 src 为目标域，目标域最后应该携带一个回调函数名称，该回调函数需要在请求端实现
  - 服务器截取请求中的 callback 字段，拼接要发送的数据，构成 callback({... : "..."}) 的 JS 代码形式作为响应体，请求端收到响应体后，会直接执行回调
- location.hash + iframe
# 错误处理
- 常见的两种方案：try catch 与 window.onerror
  - try catch：没有办法捕获全局错误，没有办法处理代码块外的错误
  - window.onerror：前端js错误监控主要是利用了 window.onerror 函数来实现，onerror 回调会在页面发生 js 错误时被调用

```JS
window.onerror = function(message, url, line, column, error) {
  console.log('log---onerror::::', message, url, line, column, error);
}
```

# jwt的使用体验
- 安全性
  - 无法主动注销，对于已经签发的token，在其未过期之前都会处于有效状态，
  - 如果token被截获，就可能被攻击者利用
- 性能
  - 无法续签，同一个payload、同一个secret生成得到得 token 都会不同，且过期后同一 token 无法续签（expires 时间不同，token 不同），导致如果要维护验证状态，就需要定期重新在服务端生成token并替换本地已过期 token
- 实用性
  - jwt本身过长，在 payload 较大的情况下，生成的 token 本身会非常长，而 cookie 的上限为 4kB
