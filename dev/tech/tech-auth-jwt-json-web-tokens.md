---
title: tech-auth-jwt-json-web-tokens
tags: [auth, json-web-tokens]
created: 2021-08-12T14:34:30.861Z
modified: 2021-08-12T14:36:02.148Z
---

# tech-auth-jwt-json-web-tokens

# guide
- jwt
  - 主要逻辑不包括注册，而侧重服务端不保存session的身份验证
  - 适合前后端分离，适合移动端

- tips
  - mock jwt核心功能的示例都依赖于服务端express/koa的支持
    - 因为每次请求都要发送token到服务端进行解码、验证
    - 但完全mock返回值和验证逻辑也可用于测试

- todo
  - jwt的核心功能的示例
  - 切换 fake backend api的例子，不必执着，全局的替换需要考虑的场景太多
# jwt-blogs

## [五分钟带你了解啥是JWT](https://zhuanlan.zhihu.com/p/86937325)

- JSON Web Token (JWT)是一个开放标准(RFC 7519)，
  - 它定义了一种紧凑的、自包含的方式，用于作为JSON对象在各方之间安全地传输信息。
  - 该信息可以被验证和信任，因为它是数字签名的。
- JSON Web Tokens是如何工作的
  - 当用户用他们的凭证成功登录以后，一个JSON Web Token将会被返回。此后，token就是用户凭证了
  - 无论何时用户想要访问受保护的路由或者资源的时候，用户代理（通常是浏览器）都应该带上JWT，典型的，通常放在Authorization header中，用Bearer schema。
  - 服务器上的受保护的路由将会检查Authorization header中的JWT是否有效，如果有效，则用户可以访问受保护的资源。
  - 如果JWT包含足够多的必需的数据，那么就可以减少对某些操作的数据库查询的需要
  - 如果token是在授权头（Authorization header）中发送的，那么跨源资源共享(CORS)将不会成为问题，因为它不使用cookie。

- 以前基于服务器session的身份认证
  - HTTP协议是无状态的，那么下一次请求的时候，服务器不知道我是谁，我们必须再次认证
  - 传统的做法是将已经认证过的用户信息存储在服务器上，比如Session
  - 用户下次请求的时候带着Session ID，然后服务器以此检查用户是否认证过。
  - 随着认证通过的用户越来越多，服务器的在这里的开销就会越来越大
  - 由于Session是在内存中的，这就带来一些扩展性的问题。
  - CORS跨域问题

- JWT是在客户端存储用户信息
  - 用户携带用户名和密码请求访问 - 服务器校验用户凭据 - 服务器提供一个token给客户端 - 客户端存储token，并且在随后的每一次请求中都带着它 - 服务器校验token并返回数据
  - 每一次请求都需要token -Token应该放在请求header中 -我们还需要将服务器设置为接受来自所有域的请求，用Access-Control-Allow-Origin: *
- jwt token无状态
  - 我们的负载均衡器可以将用户传递到任意服务器，因为在任何地方都没有状态或会话信息
  - Token在一段时间以后会过期，这个时候用户需要重新登录。这有助于我们保持安全。

- token过期了，那用户是需要重新登录？
  - 解决方案是过期时间到了，反馈给前端，前端重新申请一个新的token，下次请求就是用新的token就可以了
  - 可以在前端得到响应的时候拦截一下 如果过期重新生成并且重新request。但你的方案开销更小
- token的续期，每次访问都更新token的有效期，把token和后端sessionId一样存储起来，只是为了方便前后端分离
  - 这样子和cookie+session方案就一样了，变得有状态，那么无状态的那些优点将失去，只是重新自定义了一套有状态的会话实现。
- 看你是否引入令牌
  - access_token(访问令牌, 时间通常短，我一般设一小时)
  - refresh_token(刷新令牌，时效我通常设置一个月或更久)，
  - 客户登录后获得这两个令牌
  - 凭借访问令牌获得restful api 各个资源，凭借刷新令牌更新访问令牌（客户端可以设个判时间机制，在访问令牌快过期的时候PUT API一下, 这时旧的访问令牌就失效了）
  - 最主流的还是 凭借刷新令牌更新访问令牌，客户凭借访问令牌访问各种资源，那么客户是否重新登录取决于客户端(前端)是否设计成自动更新访问令牌了，即**在客户每个请求资源之前客户端都能保证访问令牌始终有效**(被更新，时效性延续)，客户就无需重新登录了

- 然后redis炸了jwt还能用。 但session id没了，就没有登录状态了。
  - 到服务端后获取鉴权信息，都是拿id 先读缓存，再读数据库。
- jwt就是一个规范。第三个是防篡改的。放进jwt里的串是明文的。第三段是防篡改。
  - jwt里的那个openId服务端检测到没篡改，权限等等还是会通过读取数据库，读取缓存，来获取权限的
  - 要是把鉴权信息都放jwt里，那jwt串得多大？session id 也是这样，跟jwt里存的 都只是一个用户标识，无论是jwt里的那个用户标识还是session id 都叫他用户标识id。表明这个请求是谁请求的。然后拿上id 获取权限。在根据有的权限 获取资源。 都是这么设计的。
  - 不同的是jwt可以做到用户标识 id，可以做到不存到服务器 也能安全。
  - 因为拿到用户标识id，如果不是由服务器签发的 就是jwt的第三段，服务器是不认的。这就能起到防篡改。jwt的核心思想就是 用户标识，谁发的谁能解，谁就认。
  - 不过都有个共同的问题，谁拿到这个串，不管是传统的session id 还是 jwt。 都是可以在另外一台机器上请求。
- 多台服务器负载均衡，你存的session是不是挨个服务器都放一份还是怎么做到session的统一？
  - session共享的方法，是不是要占用大量带宽或者服务器的大量存储空间。存到数据库，是不是也不方便？

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
  - Header 部分是一个JSON对象，描述JWT的元数据
    - 将上面的JSON对象使用Base64URL算法转成字符串
  - Payload部分也是一个JSON对象，用来存放实际需要传递的数据。
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

- 客户端收到服务器返回的JWT，可以储存在 Cookie 里面，也可以储存在 localStorage。
  - 此后，客户端每次与服务器通信，都要带上这个JWT。你可以把它放在 Cookie 里面自动发送，但是这样不能跨域，
  - 所以更好的做法是放在HTTP请求的头信息Authorization字段里面。

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
  - 只实现了登录，未实现注册，后续/get/users发送了jwt token
  - 抽象出services触发api请求

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
# discuss
- ## 

- ## 🤼🏻 Please stop using middleware to protect your routes
- https://twitter.com/pilcrowonpaper/status/1774251864743449019
  - I see middleware and wrappers as different things. One's a library level abstraction while one's an application/dev level

- Any reason why wrappers instead of local middleware (middleware only for a specific route)?
  1. Everything is local - you don't have to deal with your auth logic scattered across your project
  2. It leads to nested middleware
  3. I'd rather have one way of handling authorization and not mix middleware and route-level approach

- I like the wrapper function approach. Basically, high order functions. Authorization belongs in the logic anyway, because it depends on the route and sometimes user data etc. But what's wrong with using middleware for authentication?
  - "Protecting routes" == authorization ?

- I personally don't see any logical benefit in the proposed approach
  - Doing authentication checks in every controller is unnecessary. It'll be the same logic in every single app controller. Even with a wrapper you'll end up just wrapping every single app route anyway

- I don't quite use middleware in the same way you showed but I still think it has some value: preventing accidental mistakes. i.e. I forget to check for auth in one of the 10s of handlers I have

- ## 👨🏻‍🏫💡 What’s the difference between Session-based authentication and JWTs?
- https://twitter.com/ProgressiveCod2/status/1747885840544755981
- Session-Based Authentication
  - In this approach, you store the session information in a database or session store and give a session ID to the user.
  - For the user, it’s similar to just getting the Ticket ID of their flight. All other details are stored in the airline’s database.
  - The user makes a login request and the frontend app sends the request to the backend server
  - The backend creates a session using a secret key and stores the data in session storage
  - Then, the server sends a cookie back to the client with the unique session ID
  - The user makes a new request to view another page and the browser sends the session id along with it.
  - The server verifies the user using this ID.

- JWT-based Authentication
  - In the JWT-based approach, you don’t store the session information in the session store.
  - The entire information is available within the token. It’s like getting the flight ticket along with all the details available on the ticket but encrypted.
  - The user makes a login request and it goes to the backend server
  - The backend server verifies the credentials and issues a JWT. The JWT is signed using a private key. No session storage is involved.
  - The JWT is passed to the browser using a cookie. For every subsequent request, the browser sends the cookie with the JWT
  - The server verifies the JWT using the secret private key and extracts the user info.

- What’s the better approach -  Session or JWTs?
- jwt-pros
  - No separate storage
  - Easier to scale the client and server
- jwt-cons
  - Invalidating a JWT is not easy. With session, you can simply delete them from the session store.
  - The data in the JWT can become stale
  - The JWTs aren’t exactly small when it comes to size

- JWT can also help in avoiding Single point of failure(SPF) as the verification code can be an sdk Integrated in clients rather than multiple clients depending on a central storage.

- Not to forget that JWT tokens expire after a set expiry time 
  - So an additional overhead to issue a new JWT token 
  - From the client side it creates an overhead to refresh token after that expiry period. Generally it’s around 1 hour. So client will make 1 additional call every hour to get refreshed tokens

- In my perspective, JWTs are good for complex applications where scalability is a prime factor. Maintaining a separate storage for session ids is a headache there. But for simpler applications, JWT adds more payload for every request.

- ## Explaining JSON Web Token (JWT) with simple terms.
- https://twitter.com/alexxubyte/status/1732077250626179578
  - [Why is JWT popular? - YouTube](https://www.youtube.com/watch?v=P2CPd9ynFLg)

- ## 原来JWT还可以使用私钥签名+公钥验证的方式发放，那其实可以用在第三方和serverless场景上了
- https://twitter.com/Hooopo/status/1241664133201719296
- 其实okta之类的IDaaS都是用的 OIDC + JWT公私钥方案
- 合法的 JWT 并不代表他有效，所以去找签发方验证永远少不了，都要去找签发方验证了，那比普通随机字符串的 Access Token 还有多少好处呢？
- 失效时间短+refresh token是推荐的策略，其实还有一个blacklist策略
- Blacklist 是当你知道 JWT 被废弃后要做的事，但问题是失效时间短但仍然会出现在 JWT 标称过期前被 revoke 的情况（而第三方无法感知），有时间差可以利用就一定有可能产生可被利用的安全漏洞，这对外部服务来说是致命的。而请求签发服务验证 Token 有效性天然不存在这些问题

- ## JWT 合法不代表有效，有效只有去签发方的服务验证才可以，JWT 没有解决 Revoke 问题
- https://twitter.com/jasl9187/status/1241719669829947393
- JWT没解决，又不代表不能解决
- 不用去签发方，比如 auth0签发一个token，你有公钥你自己验，验证的是合法性，不能revoke只是因为jwt是stateless的，你自己在服务端记录一下就可以revoke了，并不需要签发方参与。

- ## The JWT is stored on browser, so on logout you remove the token by deleting the cookie at client side but how does one invalidate the token from server side?
- https://twitter.com/kioko_benedict/status/1374784256380129291
- I think you typically have two tokens, one is a long lived refresh token than can generates new short lived jwt tokens.
  - Then you have a table in which you can block specific refresh tokens that you check before generating a new jwt
  - You could also store all refresh tokens as a sort of user session which I’ve also seen
- how do you invalidate the token from server side before its expiration time?
  - I do have refresTokens and a table where they're stored. On logout I have a way to revoke them meaning they can't be used to generate new tokens.
  - But the jwt might still be active (few minutes)before it expires, how do ensure that it can be used to make requests (server side)?
- I mean you could have blocklist for the jwt.
  - Though origin of jwt is you didn’t have to do a lookup for user info first before your actual queries.
  - Eg I cryptographically validate that my server signed this jwt and and trust the user is/email is valid

- ## One of the main questions I repeatedly get whenever I talk about JWTs is "can I revoke a JWT?"
- https://twitter.com/bpontarelli/status/1091017706411683840
- [Revoking JWTs & JWT Expiration](https://fusionauth.io/learn/expert-advice/tokens/revoking-jwts/)
- you’ll find that the most common answers are:
  - Set the duration of the JWT to a short period
  - Implement complicated blacklisting techniques
  - Store every JWT so you can validate them
- The most common solution is to reduce the duration of the JWT and revoke the refresh token so that the user can’t generate a new JWT. 
  - With this setup, the JWT’s expiration duration is set to something short (5-10 minutes) and the refresh token is set to something long (2 weeks or 2 months). 
  - At any time, an administrator can revoke the refresh token which means that the user must re-authenticate to get a new JWT. 

- ## I still don't get JWTs.what's with the refresh token? Doesn't that just make a JWT's expiry infinite? And how do you revoke a JWT?
- https://twitter.com/JessTelford/status/1427884068989898756
- If you store the state of a JWT somewhere, then... you've just invented session-based auth, but more complicated.
- in micro-service architecture, it make most sense. 
  - suppose you have distributed system and a service needs to know who is user and is it authenticated (is token valid), the token itself tells everything, you don't have to dig up any db to check that
  - As so if you have to logout a user, generally you can't. its expiry which dictates that. you can however place something when refreshing so further it won't be refreshed.
- Here's my simplistic take on it.
  - JWT with LONG expiry. No way for admin to block this approved JWT. Has access when it shouldnt.
  - JWT with SHORT expiry. Has to refresh a lot. In the middle of one of these 'refresh' attempts, admin denies this user. Now the next JWT is denied.
- JWTs are impractical for app auth. (e.g. web apps) The session (aka random is stored on the server. Server stores the state to understand who's behind this string.
  - But JWTs are useful in microservices (and other APIs talking to each other). 
  - Because JWT contains info (aka state) of who is behind the JWT. Not only who, but also what permissions this token has, aka ACL.
  - Main here - the server does not need to store any state. JWT is the state.
- They are fabulous when you need to cache the content for scale but restrict access. They also work on all devices, cookies are limited 
  - Come check out token auth signed URLs. Useful if you need to revoke and work with multiple CDNs
  - Agreed; cookies have their place, but both JWTs and session IDs can be sent via multiple avenues (cookies, headers, request bodies, URLs, etc)
- If you're building a normal frontend, you're often much better off using traditional sessions with the session cookie being httpOnly so JavaScript does not even have access to it.

# ref
- [Next.js 11 - JWT Authentication Tutorial with Example App](https://jasonwatmore.com/post/2021/08/04/next-js-11-jwt-authentication-tutorial-with-example-app)
- [Next.js - Basic HTTP Authentication Tutorial with Example App](https://jasonwatmore.com/post/2021/08/29/next-js-basic-http-authentication-tutorial-with-example-app)

- the access and refresh token are shared across tabs! fortunately, you can implement a cross-tab lock since localstorage is shared and single ops are atomic.
  - https://twitter.com/_paulshen/status/1478441122993086464
