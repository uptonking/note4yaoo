---
title: tech-auth-jwt-json-web-tokens
tags: [auth, json-web-tokens]
created: '2021-08-12T14:34:30.861Z'
modified: '2021-08-12T14:36:02.148Z'
---

# tech-auth-jwt-json-web-tokens

# guide
- jwt
  - 主要逻辑不包括注册，而是服务端不保存session的登录验证
  - 适合前后端分离，适合移动端

- tips
  - mock jwt核心功能的示例都依赖于服务端express/koa的支持，因为每次请求都要发送token到服务端进行解码、验证
- todo
  - jwt的核心功能的示例
  - 切换 fake backend api的例子，不必执着，全局的替换需要考虑的场景太多
# jwt-blogs

## [JSON Web Token 入门教程](https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)

- 典型的用户认证流程一般是
  1、用户向服务器发送用户名和密码。
  2、服务器验证通过后，在当前对话（session）里面保存相关数据，比如用户角色、登录时间等等。
  3、服务器向用户返回一个 session_id，写入用户的 Cookie。
  4、**用户随后的每一次请求，都会通过Cookie，将 session_id 传回服务器**。
  5、服务器收到 session_id，找到前期保存的数据，由此得知用户的身份。
- 这种模式的问题在于，伸缩性（scaling）不好。
  - 单机当然没有问题，如果是服务器集群，或者是跨域的服务导向架构，就要求 session 数据共享，每台服务器都能够读取 session。
- 一种解决方案是session数据持久化，写入数据库或别的持久层。各种服务收到请求后，都向持久层请求数据。
  - 这种方案的优点是架构清晰，
  - 缺点是工程量比较大。
  - 另外，持久层万一挂了，就会单点失败。
- 另一种方案是服务器索性不保存session数据了，所有数据都保存在客户端，每次请求都发回服务器。
  - JWT就是这种方案的一个代表。

- JWT的原理
  - 服务器认证以后，生成一个 JSON 对象，发回给用户
  - 用户与服务端通信的时候，都要发回这个 JSON 对象。服务器完全只靠这个对象认定用户身份。
  - 为了防止用户篡改数据，服务器在生成这个对象的时候，会加上签名

- JWT的数据结构
  - Header. Payload. Signature
  - Header 部分是一个 JSON 对象，描述 JWT 的元数据
    - 将上面的 JSON 对象使用 Base64URL 算法转成字符串
  - Payload 部分也是一个 JSON 对象，用来存放实际需要传递的数据。
    - 除了官方字段，你还可以在这个部分定义私有字段
    - 注意，JWT 默认是不加密的，任何人都可以读到，所以不要把秘密信息放在这个部分。
    - 这个JSON对象也要使用 Base64URL 算法转成字符串。
  - Signature 部分是对前两部分的签名，防止数据篡改。
    - 首先，需要指定一个密钥（secret）。这个密钥只有服务器才知道，不能泄露给用户。
    - 然后，使用 Header 里面指定的签名算法（默认是 HMAC SHA256），按照下面的公式产生签名。
    - 算出签名以后，把 Header、Payload、Signature 三个部分拼成一个字符串，每个部分之间用"点"（.）分隔，就可以返回给用户。

```JS
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

- 客户端收到服务器返回的 JWT，可以储存在 Cookie 里面，也可以储存在 localStorage。
  - 此后，客户端每次与服务器通信，都要带上这个 JWT。你可以把它放在 Cookie 里面自动发送，但是这样不能跨域，
  - 所以更好的做法是放在 HTTP 请求的头信息Authorization字段里面。

- JWT的特点
  （1）JWT 默认是不加密，但也是可以加密的。生成原始 Token 以后，可以用密钥再加密一次。
  （2）JWT 不加密的情况下，不能将秘密数据写入 JWT。
  （3）JWT 不仅可以用于认证，也可以用于交换信息。有效使用 JWT，可以降低服务器查询数据库的次数。
  （4）JWT 的最大缺点是，由于服务器不保存 session 状态，因此无法在使用过程中废止某个token，或者更改 token 的权限。也就是说，一旦 JWT 签发了，在到期之前就会始终有效，除非服务器部署额外的逻辑。
  （5）JWT本身包含了认证信息，一旦泄露，任何人都可以获得该令牌的所有权限。为了减少盗用，JWT 的有效期应该设置得比较短。对于一些比较重要的权限，使用时应该再次对用户进行认证。
  （6）为了减少盗用，JWT 不应该使用HTTP协议明码传输，要使用HTTPS协议传输。

- discussion

- 无状态的东西好在方便扩展，例如map reduce。
  - 不过通常服务器还是需要对session或者token有比较高的掌控权。
  - JWT还是用在一些不那么需要保证安全的地方会好一些例如确认退订邮件等。

- 无法在使用过程中废止某个 token，或者更改 token 的权限。
  - 也就是说一个用户在手机A中登录了，然后又在手机B中登录，在过期之前手机A和B都可以登录，无法做到B登录后让A过期，如果要做到这点，就必须让服务器维护一个清单（记录该账号是否已经签发token），这样又回到session的老路了
  - 以上就是我们公司后端拒绝使用jwt的理由，我该怎么驳倒他？
- JWT最大特点不就是状态存储在客户端么，可以实现多点登录，服务端不用做很多的额外工作
- JWT解决的最大问题是跨域，如果你们的业务不涉及跨域完全没有必要用JWT， session 就够用了，
  - 如果有跨域需要，那么改造Session实现跨域访问，要比改造JWT实现单用户登陆复杂的多
- 不引入数据库支持的话这个的确没法实现。最好的方案是维护一张基于 jti (JWT ID) 的表，将jti和user_id关联起来，生成新的jwt时将该user_id旧的jwt标记为失效就好，具体场景还得看你们的具体业务逻辑。
- 签名可以加时间戳或这其他随机参与加密，一旦登录就更新签名，之前的签名失效，不会出现多个在线啦
- 你可以让他对比维护是否签发token的清单和维护session列表哪个更容易一些，如果在这方面JWT没有优势，也就没有重新发明的必要额。
- 使用jwt的场景是前后端彻底分离，无法通过session来认证的。默认的确是可以多次登录，发了多个token，也能改成只发一个啊，让前面的失效，这和session是2回事情。
- 原文第四条的意思应该是jwt颁发后，一般扩展包没提供让其失效方法。但是要让jwt失效依然很简单，因为jwt一般会放在redis或者mysql表，只要逻辑上去找到uid对应的jwt，删了就可以了。

- 使用JWT用户数据由客户端传入，每个请求都会带着这些信息，也就不需要后端生成Session了，在每次请求的时候验证登陆状态及登陆用户
- 跨域这块，前端也是要处理的，两种情况：
  1. token 存储在 cookie 里，按传统的跨域方案，共享/传递 cookie 里的 token
  2. token 存储在 localStorage 里，则需要 localStorage 的跨域方案，以便 共享/传递 cookie 里的 token，localStorage 的跨域方案可以搜搜，有开源类库

- jwt主要还是用在移动端
  - 还可以用于前后端分离，对后端来说，没有移动端不移动端的概念，反正你们都是调用接口，我管你是pc，h5 or app
- 如果是移动端的话，可以考虑签发的时候加入手机的设备编号作为验证。

- 可以去参考CAS的方案。或者我简单说一下ucenter的方案，a系统登录后，拿到了jwt，访问一下b系统的一个链接，由b系统的此链接将jwt存入localStorage

- 后端用redis或数据库记录一个用户id到token的对应表，token不用有任何意义，也不需要加密解密，随机字符串即可。
  - 客户端发送token的方法跟JWT一样，可以选择用cookie、header或url参数，服务器校验根据 seesion -> 用户id 的公共存储判断。这样可以很简单地在后台根据用户最后访问时间更新token有效时间和自动删除过期token ，还能通过这个表查看在线用户，这些都是JWT不具备的功能。
  - 所以我看不出JWT相比这个方案有什么好处，除了能节约服务器上 token 到 用户ID 表的这一次查询，还有其他好处吗？ 而且一般业务请求，除了拿到用户ID，还有更多需要服务器调用的服务，比如拿到用户完整对象、用户权限、用户业务操作对象等等，这些不比 查询 token 到用户ID表的开销大得多吗？
# examples-jwt-react
- https://github.com/cornflourblue/react-jwt-authentication-example
  - [React (without Redux) - JWT Authentication Tutorial & Example](https://jasonwatmore.com/post/2019/04/06/react-jwt-authentication-tutorial-example)

- react + rxjs
  - configureFakeBackend会拦截window.fetch
  - 通过rxjs. BehaviorSubject共享数据，包括用户信息和jwt token
  - 只实现了登录，后续/get/users发送了jwt token

- 还提供了express后端示例
  - https://github.com/cornflourblue/node-jwt-authentication-api
    - [NodeJS - JWT Authentication Tutorial with Example API](https://jasonwatmore.com/post/2018/08/06/nodejs-jwt-authentication-tutorial-with-example-api)
  - https://github.com/cornflourblue/react-redux-jwt-authentication-example
  - https://github.com/cornflourblue/next-js-11-jwt-authentication-example
  - https://github.com/cornflourblue/node-mongo-jwt-refresh-tokens-api
  - https://github.com/cornflourblue/node-jwt-authentication-api
- https://github.com/JulienMora/react-jwt-authentication-sample
  - 结构和上面jwt例子相同，依赖rxjs
- https://github.com/cornflourblue/react-role-based-authorization-example
  - 请求api时用到了 rxjs BehaviorSubject

- https://github.com/bespalowlad/react_base_auth
  - Base login and registration user with fake backend
  - 标准的注册登录app
  - 依赖redux-thunk, formik, material-ui.v4
  - 不依赖后端，在header的Authorization字段存放了jwt token
  - 注册登录点击提交按钮后都没有跳转route；
  - Register和Login组件都只是Form，思路清晰
  - 没有提供手动logout的菜单，但实现了action-reducer
  - fakeBackend采用拦截window.fetch并匹配url的方式模拟数据；初始用户数据读取自localStorage，新注册用户数据就保存在内存



- https://github.com/zafar-saleem/react-login
  - Before using this project please make sure you get the [server side](https://github.com/zafar-saleem/NodeScalableArchitecture) running 
# examples-jwt
- https://github.com/alex-c/mock-auth-backend
  - A mock backend to test authentication and authorization with JSON Web Tokens (JWT). 
  - By default, this backend exposes an /auth route, which lets you perform a login with a user identifier and password and returns a JWT, 
  - and a /protected route, which requires a valid JWT in the request header. 
  - Additional routes can be configured (see below), to authorize routes depending on roles in the JWT. 
  - By default, an /admin route is exposed, which requires the admin role.

- https://github.com/thiagoluiznunes/mock-user-auth
  - a mock user authentication API developed in Nodejs and Express using JWT as an authenticator

- https://github.com/techiediaries/fake-api-jwt-json-server
  - 依赖json-server, jsonwebtoken, body-parser
  - A Fake REST API using json-server with JWT authentication. 
  - Implemented End-points: login, register
  - [Building a Fake and JWT Protected REST API with json-server](https://www.techiediaries.com/fake-api-jwt-json-server/)
- https://github.com/abdelrahman-haridy01/full-mocks-api
  - 依赖json-server
  - Make a Full fake REST API, MakePOST, PUT, PATCH or DELETE requests, Fake Register and login based on role Api with jwt.
