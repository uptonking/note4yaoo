---
title: lib-utils-codesandbox-community
tags: [codesandbox, community]
created: 2024-01-25T13:28:03.358Z
modified: 2024-01-25T13:33:23.267Z
---

# lib-utils-codesandbox-community

# guide

# codesandbox-news
- 在预览界面集成了react-devtools和chrome-devtools，支持在不打开浏览器控制台的条件下inspect预览界面的元素并高亮定位到源码位置
  - 原理是远程调试
  - https://codesandbox.io/p/chrome-devtool/app/index.html
  - https://github.com/browserless/browserless
  - https://github.com/ChromeDevTools/devtools-frontend
# discuss-stars
- ## 

- ## [Incredibly slow performance · Issue · codesandbox/codesandbox-client _201810](https://github.com/codesandbox/codesandbox-client/issues/1220)
- import * as am4charts from "@amcharts/amcharts4/charts"; 
  - The first two imports are what makes the execution quite slow.
  - We then transpile these files (because we see export/import statements which aren't supported in the browser) and download/transpile all the files that are referenced by those. This takes a long while and takes the main amount of time.

- Normally we do some optimizations for this:
  - We prepackage any files we can find for a dependency on a server and cache that.
  - We don't transpile files if we detect that it's not needed.
  - We cache transpilation results on our server and in the browser.

- ## 🤔 if you want to eval some untrusted js in the browser, try quickjs-emscripten. 
- https://x.com/jitl/status/1832520899766915354
  - if you want to eval some untrusted js in your untrusted js, try quickjs-for-quickjs.
- why not add wasn support to quickjs-emscripten instead
- what do you mean; like an API that the host can expose to the guest to allow the guest to instantiate wasm modules using the host's wasm runtime? or compile a wasm runtime to wasm? or compile/implement a wasm runtime in js?
  - I think I meant the first one. maybe my second best approach would probably be some wasm-to-wasm translation if you want to do things like prevent infinite loops
- The host can implement that in user-space already, no need for it to be first party. Another building-to-js advantage is you can now use quickjs in hosts that don't support wasm at all. Eg for iOS Safari Lockdown Mode, fall back to the js variant
  - binaryen wasm2js mite b cool tho! then you can have the memory limit & cpu interrupt API of quickjs to govern a wasm.
  - or possibly this madlad, same name, independent pure-js impl

- ## The fastest way to restore an environment is to take a memory snapshot and restore it. 
- https://twitter.com/Vjeux/status/1777721284345930088
  - It’s pretty wild that CodeSandbox made it happen at scale!

- ## 🐛 If I could remove one thing from JavaScript it would be `eval()` .
- https://twitter.com/awesomekling/status/1758775888647188567
  1. Calling eval() may change the set of bindings in the existing environment. This prevents a lot of optimizations based on static knowledge of environment layout (although engines can still optimize anyway in scopes where eval is not called.
  2. It forces us to plumb the “completion” value around in a million finicky ways so that eval() can return it. (This is what’s bugging me today
  3. Running arbitrary strings as code at runtime in the first place is a pretty goofy API!
- how do you feel about new Function()? #3 applies but iirc 1 and 2 should be much less
  - Yeah, it’s a lesser evil and much less annoying to support than eval() 

- #3. is still important for me. I compile HTML templates (a PHP lookalike, containing <? js() ?>) using `new Function()` at runtime. Doing my best to avoid that pesky build step

- ## 🐘🏘️ Most sandboxes in CodeSandbox are stored in a Postgres database. _202306
- https://twitter.com/CompuIves/status/1667148424389566465
  - 40M+ sandboxes and 400M+ files stored in Postgres, and we still have performant load times.
  - When going with Postgres, I thought "this is the first thing we'll have to replace". Still didn't happen after 6 years
- Generally, the three technologies that exceeded my expectations in scale and performance:
  - Postgres
  - Elixir
  - Rust
- Now we're seeing that the database is growing very big (leading to long & big backups), so we started archiving sandboxes to GCP to save space. We're considering moving our DB from k8s to a managed instance. But still, Postgres has exceeded all my expectations.
- Curious, which components are written in Rust vs Elixir? Did you find that Elixir was better suited for some tasks than Rust?
  - Yah, Elixir is doing everything with the API (including websocket message handling).
  - Rust is doing computationally expensive things, or things that require a lot of string manipulation.
  - For example, we use Elixir to handle WS OT messages, but we use Rust then to apply the OT operations on the string. We first did this with Elixir, but (partly because of my implementation) it started to eat a lot of memory as every mutation created a new string.
  - Elixir + Rust interop is fantastic, so it's nice if you can pull out Rust for these kind of things while maintaining the concurrency/robustness of Elixir for the server.
- Erlang/Elixir under load is just amazing. Incredibly resilient. One of the many reasons I became a fanboy of CouchDB. Still love Postgres but there is something beautiful about storing everything in a giant B-tree

- 🤔 How is the Postgres DB structured.  Is it single node or shareded across multiple nodes?  And do you store files in Postgres as blobs?
  - 💡 Single DB (with a R/O replica). Files are stored as text, binary files are uploaded to GCP and we store a link in the db.

- Wow, just single DB for such huge workload! Must be a huge machine.
  - It's not huge! 4 cores and 24GiB RAM (actually I believe 16GiB would be fine too). Plus we also store sandbox pageviews (hourly, daily, weekly, monthly)/users/teams etc...
- Incredible! I am using a little bigger machine for a much lesser scale application.  Likely I am doing something wrong.
# discuss-sandbox-agent 👾
- ## 

- ## 

- ## 

- ## 

- ## Cloudflare 发布了一个 AI 沙箱工具 Dynamic Worker Loader，用 V8 isolate 替代容器：
- https://x.com/xiaohu/status/2036616677115441307
  - 无并发上限，百万级请求随便扛 
  - 同机同线程执行，零网络延迟
  - 配套三个库也一起发了：代码执行（codemode）、自动打包（worker-bundler）、虚拟文件系统（shell）。

- 不支持 python、cli 安装和存储记忆，到头来还得是 e2b

- 这类‘同机同线程 + isolate’路线确实很适合 agent 跑短任务。对我来说更关键的是 TS 接口直接定义 API 这点，既省 token，又让工具调用和实现约束天然对齐。

- ## zeroboot — 用 Firecracker 快照 + CoW fork 做亚毫秒级 AI agent VM 沙箱
- https://x.com/QingQ77/status/2034580389742944576
  - 它是直接把 Firecracker 快照当母体，再用 CoW fork 出新的 KVM VM，目标就一个，让 agent 跑代码的时候，既别太慢，也别太像在裸奔。
- https://github.com/zerobootdev/zeroboot /apache2/202603/rust
  - Sub-millisecond VM sandboxes for AI agents via copy-on-write forking

- ## Browsers have spent decades solving a similar problem of executing untrusted code safely, and porting those architectural learnings to backend infrastructure feels like a natural evolution
- https://x.com/auchenberg/status/2027949839581945871
  - [Let's discuss sandbox isolation _202602](https://www.shayon.dev/post/2026/52/lets-discuss-sandbox-isolation/)
- v8's isolates were literally designed to sandbox js execution, and now we're seeing that pattern everywhere - from cloudflare workers to lambda to deno
  - the multi-tenant security story is already solved, just needs adapting

- ## sandbox-as-a-service is becoming the default agent infrastructure layer. 
- https://x.com/ivanburazin/status/2027879361177850177
  - E2B, Daytona, Modal, now Alibaba — everyone's converging on 'give the agent its own ephemeral compute.'
  - the interesting question is who wins on cold start time. agents need sub-second sandbox spin-up for interactive workflows, and that's where the MicroVM vs container tradeoff gets real. Firecracker can do ~125ms but most hosted offerings are still 2-5 seconds.
- the bottleneck isn't building the sandbox. it's deciding what belongs inside it. most people sandbox everything or nothing. reality is you need granular permissions per tool, per context, per risk level. treat agents like unix processes, not all-or-nothing executables.

- ## going to benchmark sandboxes
- https://x.com/ryanvogel/status/2024266375825363207
  - cloudflare
  - vercel
  - daytona
  - e2b.dev
  - exe.dev
  - sprites

- https://github.com/computesdk/benchmarks /ts
  - Compare startup time-to-interactive for top sandbox providers.

- [A thousand ways to sandbox an agent](https://michaellivs.com/blog/sandbox-comparison-2026)

- You forgot the best part Firecracker

- Add the user’s browser to the mix. Python running inside Chrome/WASM. It’s not the full capability of Python but it can get you pretty far depending on your use case.

- try @modal ! we've also got GPU sandboxes, nice for developing CUDA kernels, training ML models, or doing ray tracing.

- What’re you measuring? IME startup time is pretty similar across most of those. What I’ve found more important for coding agents is developer ergonomics (Modal), scale without a custom plan (Modal), persistence (Sprites), and s3fs (CF, Modal).

- Daytona and runpod for gpu sandbox

- ## 我想了想…大规模用 Python 或者 node 做 appengine 类似的 sandbox ，隔离靠 vm，存储 fuse 接口直接挂进去…没错，今年一定是 2013 年
- https://x.com/CMGS1988/status/2022592355975729516
- 十年前给人做cloud，十年后给agent做cloud。非常合理

- gae那时候有容器隔离吧，你说的是dae或sae？
  - 嗯 DAE…GAE 有的，GAE 毕竟是 public 服务

- k8s 表示等你成熟了，接入调度吧。

- ## this is how i currently visualize the best way to do sandboxing with @opencode
- https://x.com/ryanvogel/status/2022694821929136144
  - each sandbox is running an opencode server instance, and the clients have full range to switch between which server they are on 
- https://github.com/R44VC0RP/serverbox /202602/ts
  - On-demand, sandboxed OpenCode server instances powered by Daytona.
  - ServerBox manages infrastructure and lifecycle only. You get back a URL and credentials, then use @opencode-ai/sdk directly against it.

- this is all suboptimal we're doing work to make this a lot more seamless

- What about a local sandbox?
  - It would still be handled the same, replace the sandbox provider with a docker instance
- Any exploration on using apple containers on macOS instead of docker? One less dependency to manage

- ## 🆚🏘️🧩 Agent 与 Sandbox 的两种集成架构模式
- https://x.com/shao__meng/status/2021488624446079160
  - 来自 @LangChain 创始人 @hwchase17 的分享，他提出了两种集成架构：Agent 运行在 Sandbox 内部，或外部。
- 🧩 模式一：Agent 运行在沙箱内部（Agent IN Sandbox）
  - 架构特征： 将 Agent 框架打包进 Docker 镜像或 VM，在沙箱内启动，外部通过 HTTP/WebSocket 与之通信。
- 优势：
  - 与本地开发体验一致——本地怎么跑，沙箱里就怎么跑，降低了部署的心智负担。
  - Agent 与执行环境紧耦合——Agent 可以直接操作文件系统、维护复杂的环境状态，适合需要持续与特定库交互的场景。
- 代价：
文章列举了五个明确的 trade-off：
1. 通信基础设施成本——需要自行搭建跨沙箱边界的网络通信层（除非 SDK 提供商已封装好）。
2. API 密钥暴露风险——Agent 需要在沙箱内调用推理 API，密钥必须存在于沙箱中。一旦沙箱被攻破（无论是隔离技术漏洞还是 prompt injection 导致的凭证外泄），密钥即面临风险。
3. 迭代速度慢——每次更新 Agent 逻辑都需要重建镜像、重新部署。
4. 冷启动问题——沙箱需要先恢复（resume）才能让 Agent 活跃，需要额外的编排逻辑。
5. 知识产权风险——Agent 的全部代码和 prompt 都运行在沙箱内，容易被整体提取。

- 特别值得注意的是 Nuno Campos 补充的一个深层安全洞察：在此模式下，Agent 的任何组件都不能拥有比 bash 工具更高的权限。举例来说，如果 Agent 同时拥有 bash 工具和 web fetch 工具，那么 LLM 生成的代码就能无限制地执行网络请求——这是一个重大的安全隐患。安全边界围绕的是整个 Agent，而非单个工具。

- 🧩 模式二：沙箱作为工具（Sandbox as Tool）
  - 🤔 是否更适合并行任务、多任务
- 架构特征： Agent 运行在本地或你的服务器上，需要执行代码时通过 API 远程调用沙箱服务（E2B、Modal、Daytona、Runloop 等）。
- 优势：
· 快速迭代——改 Agent 逻辑不需要重建镜像，开发效率高。
· 密钥安全——API 密钥留在 Agent 侧，沙箱内只有执行，不持有敏感信息。
· 关注点分离更清晰——Agent 状态（对话历史、推理链、记忆）与沙箱解耦。沙箱崩溃不会丢失 Agent 状态，切换沙箱后端也不影响核心逻辑。
· 并行执行——可以同时在多个远程沙箱中并行执行任务。
- 按需付费——只在执行代码时才产生沙箱费用，而非为整个 Agent 进程持续付费。
- Zo Computer 的 Ben Guo 还补充了一个前瞻性观点：未来 Agent 推理可能需要运行在 GPU 机器上，而沙箱环境的需求完全不同，两者的基础设施要求会进一步分化，提前解耦是明智的。
- 代价：
  - 主要是网络延迟。每次执行调用都要跨网络边界，对于大量小粒度执行操作的工作负载，延迟会累积。不过文章也指出，有状态会话可以缓解这个问题——变量、文件、已安装的包在同一会话内持久化，减少往返次数。

- 两种架构模式的选择建议
- 选择模式一（Agent IN Sandbox）
  - Agent 与执行环境紧耦合
  - 希望生产环境与本地开发一致
  - SDK 提供商已处理好通信层
- 选择模式二（Sandbox as Tool）
  - 需要快速迭代 Agent 逻辑
  - 需要保护 API 密钥安全
  - 偏好 Agent 状态与执行环境分离

- 理想状态下沙箱中的agent是不需要快速迭代的，是完全和业务解耦的一个通用agent，业务相关的部分完全交给cli和skill来实现动态更新。 安全问题随着模型能力的提高，对于prompt injection的防范会相对轻松

- 开发爽一时，安全风险高。将 Key 置于沙箱内部确实极大增加了 Prompt Injection 的攻击面。但若完全剥离，跨边界通信的延迟与复杂度又是另一项沉重的工程税收。

- ### The two patterns by which agents connect sandboxes
- https://x.com/hwchase17/status/2021261552222158955
  - More and more agents need a workspace: a computer where they can run code, install packages, and access files. Sandboxes provide this.
  - There are two architecture patterns for integrating agents with sandboxes:
  - Pattern 1 (Agent IN Sandbox): Agent runs inside the sandbox, you communicate with it over the network. Benefits: mirrors local development, tight coupling between agent and environment.
  - Pattern 2 (Sandbox as Tool): Agent runs locally/on your server, calls sandbox remotely for execution. Benefits: easy to update agent logic, API keys stay outside sandbox, cleaner separation of concerns.
  - `deepagents` supports both patterns with simple configuration

- ### I hold this truth to be self-evident: Putting the agent in a different container than the environment makes a lot more architectural sense.
- https://x.com/bernhardsson/status/2021527682534760709
- yep - learned this the hard way with container networking latency. putting agent + env in the same pod cuts p50 latency by ~40ms and eliminates a bunch of failure modes around container orchestration race conditions

- Separation wins at scale. Single container = tight coupling. When your agent crashes, it shouldn't take the env with it. Latency matters less than fault isolation when you're running 1000+ concurrent sessions. Ask me how I know.
  - State management becomes the entire game. File-based task state forces deterministic retries, audit trails, and canary deploys. Every concurrency problem becomes debuggable. That's where the moat lives.

- ### Default to #2. Sandbox as tool → clean separation, faster updates, better secret isolation.
- https://x.com/AstasiaMyers/status/2021389843318919230
- API keys must live inside the sandbox to allow the agent to make inference calls.
  - That's false; the understood pattern today is that you proxy inference calls and inject secrets outside the sandbox

- In #2, your server now has access to all of the same API keys. if one of the N agents you’re running on that server get compromised, your exposure is much larger. Agent in sandbox allows you to scope and inject scoped credentials, limiting exposure and better manage resources.
  - there is no difference when all agents use same API keys, that's the most common case.
- you can do this with terraform I think.

- yes. agent-sandbox decoupling also lets you run functional tests against the sandbox API separately. learned this after our first sandbox had a subtle race condition that only showed up when agent ran multiple commands in parallel
# discuss-iframe
- ## 

- ## 

- ## 🛍️ [Apps Marketplace · Issue · webstudio-is/webstudio _202311](https://github.com/webstudio-is/webstudio/issues/2648)
  - This marketplace will facilitate the enhancement of websites with additional functionalities and features, ranging anywhere from email tools through to new ecommerce integrations. 

- Similar thing to figma apps, they are effectively standalone web apps loaded via iframe, hosted by the 3rd-party provider but with access to project data and api to change it

- iframes are a terrible solution, since they do not get resized based on their content the way a div does.
  - Webflow is doing the same thing, and it works fine for them. When implementing an app you choose the window size, small, medium, large. I believe you can even change between sizes from within the app (if I remember correctly).
  - IFrames are the safest way to integrate 3rd party application into a web-app. Importing 3rd party scripts into the main-window would be a security nightmare.

- plugins could be used to extend the range of available elements/components in the Webstudio Editor — i.e., elements that use custom calculation logic (eg., custom calculators, countdowns, counters), elements pre-programmed to interface with specific APIs (eg., 'Mailchimp newsletter subscription element', 'Google Reviews widget', 'Instagram Feed Gallery', etc.), and more.

- Apps is more about custom UI in the builder rather than custom components. Both a planned though.

- ## is there some js library that makes main<>iframe page communication more maintainable? 
- https://x.com/aidenybai/status/1921645175757041912
- I had exactly this problem. I ended up building "Webmesh" exactly for this use case to facilitate the communication for the @livestoredev devtools (particularly for the browser extension).

- https://github.com/psd-coder/typed-channel
  - Evil Martians just released a new open source tool for TypeScript to add types to postMessage for communication via Web Workers, BroadcastChannel, etc.

- If the iframe is on the same origin, they can just access each other's global contexts (via frame.contentWindow).

- I created a simple RPC using postMessage. RPC returns a promise to the caller, and sends a unique ID with postMessage to the iframe, the result is sent back from the iframe to the parent window with the same ID and then the promise is resolved.

- ## [Does the iframe have any effect on page load time? Why not? - Stack Overflow](https://stackoverflow.com/questions/2323374/does-the-iframe-have-any-effect-on-page-load-time-why-not)
- The biggest drawback is that they block the window `onload` event until complete, which can make the users perceive that the page they requested is slow.

- ## [How to make iframe load faster - Ionic Framework / ionic-v3 - Ionic Forum _201805](https://forum.ionicframework.com/t/how-to-make-iframe-load-faster/130056)
- If your App is a PWA you can use a Service Worker to cache URLs 

- ## [Embed iFrame loading times very slow and not appearing at times | Figma Forum _202309](https://forum.figma.com/ask-the-community-7/embed-iframe-loading-times-very-slow-and-not-appearing-at-times-11724)
- it would be really awesome if your embedded view API allowed to show some kind of a message while the view is loading
  - I’d just write something like “It may take a while to load…”, to just let the users know that this is an expected behaviour

- ## [Lazy load an iframe by IntersectionObserver - DEV Community](https://dev.to/phuocng/lazy-load-an-iframe-4jp1)
- Setting up lazy loading for an iframe is similar to lazy loading images. 
  - Instead of setting the `src` attribute directly, we'll use a custom data attribute like `data-src` . This way, the iframe won't load immediately when the page loads.
  - we'll set up an `IntersectionObserver` to watch the iframe and detect when it comes into view. Once the iframe becomes visible, we'll grab the URL from the `data-src` attribute and use it to set the `src` attribute, which will start loading the iframe.

- ## [Adding javascript to an iframe - Anvil Q&A - Anvil Community Forum](https://anvil.works/forum/t/adding-javascript-to-an-iframe/17599/2)
- Do you control the source of the iframe? If so, include the Javascript in it originally.
  - If you’re trying to inject the Javascript into the iframe dynamically, you’ll run up against cross domain security issues. Imagine a hacker creating an iframe that goes to Paypal and injecting their own Javascript into it.

- ## [How can I manually append three.js code into an iframe - Stack Overflow](https://stackoverflow.com/questions/72862663/how-can-i-manually-append-three-js-code-into-an-iframe)
- `iframeDocument.write(generatedCode)` ; 
  - Your generatedCode will produce error Unterminated template literal you need to escape/replace `</script>` in variable with `<\/script>` 

- ## [Is it safe to have sandbox="allow-scripts allow-popups allow-same-origin" on <iframe />? - Stack Overflow](https://stackoverflow.com/questions/35208161/is-it-safe-to-have-sandbox-allow-scripts-allow-popups-allow-same-origin-on-if)
- allow-scripts This allows JavaScript code within the IFrame to run
  - Without allow-scripts being set, all this does on its own is allow your outer IFrame to manipulate and read objects, 
  - however, with allow-scripts this can allow the IFrame to manipulate and read objects in the parent, i.e. your page, which is not safe.

- allow-same-origin is not safe. That will give the iframe the possibility to access parent data (also local storage for example)
  - Also allow-same-origin will allow the iframe to make ajax requests to the parent's apis which can also be harmful.

- ## [Running Javascript in an iframe from a different domain - Stack Overflow](https://stackoverflow.com/questions/28780057/running-javascript-in-an-iframe-from-a-different-domain/28780131)
- There are two ways you could tell the document in the iframe to do stuff, and neither can be done unilaterally.
  - the easiest way (for structural things like tabs) would be to use the URL with a hash; the app on the other domain just needs to support them.
  - The other, more flexible way would be to use Cross-document messaging. For that to work, the developers of the app on the other domain must write a message handler on their side.

- ## [inject script inside iframe of different domain - Stack Overflow](https://stackoverflow.com/questions/15041820/inject-script-inside-iframe-of-different-domain)
- Nope. Same Origin Policy dates back to Netscape 2.0.
  - Unless you can hack/XSS the other site's files to inject the JS, you will have a hard time.
  - Now if you legitimately need to communicate with the other page, and you either have control of the other page or can setup it to communicate with your server, you can use window.postMessage, JSONP or even Ajax with CORS

- ## [Injecting javascript into an iframe - Stack Overflow](https://stackoverflow.com/questions/68161803/injecting-javascript-into-an-iframe)
  - I actually ended up taking a different approach with this. Rather than injecting the script into the the iFrame, realised that I could reference the parent.function() from the iFrame. This resolved the issues with not having access to the variables and the scope to call the function.

```JS
var iframe = document.getElementById('my_iframe');
var iframeDocument = iframe.contentDocument || iframe.contentWindow.document;

var scriptSource =`

    window.addEventListener('DOMContentLoaded', function() {
        var form = document.getElementById('form'); // change to the actual form selector
        var input = document.getElementById('transaction_amount');
        input.value = 100;

        form.addEventListener('submit', function (ev) {
            if (Number(input.value) > 100) {
                alert('No chance');
                ev.preventDefault();
            }
        });
    });
`;
var script = iframeDocument.createElement("script");
var source = iframeDocument.createTextNode(scriptSource);
script.appendChild(source);
iframeDocument.body.appendChild(script);

// in your specific case you could do something like:
frames[0].window.eval(foo.toString());

// another way
const iframeDoc = iframe.contentDocument || iframeWin.document;
var script = iframeDoc.createElement("script");
script.append(`
    window.onload = function() {
     document.getElementById("fire").addEventListener('click', function() {
        const text = document.getElementById('title').innerText;
        alert(text);
     })
  }
`);
iframeDoc.documentElement.appendChild(script);

// another way
window.document.getElementById("baidu-container").onload = function() {
  var s = document.createElement("script");
  s.type = "text/javascript";
  s.src = "my.js";
  window.document.head.append(s);
}
```

- 
- 

- ## I found the dumbest way to preload an iframe ahead of time: `<iframe src="..." sandbox="allow-same-origin">` ; 
- https://x.com/iamakulov/status/1863609927568429456
  - Downloads the iframe + its CSS/JS/etc
  - Puts these resources into the cache, so they’re there when you need them later
  - Critically, doesn’t execute any JS at all
  - All at the cost of a single annoying console error
- “Why not just `<link rel="preload">` ?” That will load the HTML – but not its CSS/JS/etc. Also, Chrome doesn’t support preloading HTML
  - “Why can’t you just cache CSS/JS/etc with a service worker, or with some custom JS?” Because these files will get cached in the wrong place – and won’t actually speed up anything. This is for privacy reasons
  - “Why would you do this at all, you madman?” Well, sometimes you do need to show an iframe ASAP! E.g. at Framer, we use cross-origin iframes to render plugins. When you hover over a plugin in the picker, we preload the plugin’s iframe. This makes it pop up 0.5-1s sooner

- ## [Alternative to iFrames with HTML5 - Stack Overflow](https://stackoverflow.com/questions/8702704/alternative-to-iframes-with-html5)
- You can use object and embed
  - Keep in mind that most modern browsers have deprecated and removed support for browser plug-ins, so relying upon `<embed>` is generally not wise if you want your site to be operable on the average user's browser.
- There is one alternative to `<iframe>` and that's the `<object>` tag. It can display content from different sources as well. The pro is it being conform to the **xhtml-standards** and encouraged to use but there's not such a broad / usable support in older browsers (you have to mess with it to get it right in IE).

- As others have mentioned you can also use the embed tag and the object tag but that's not necessarily more advanced or newer than the iframe.
  - HTML5 has gone more in the direction of adopting web APIs to get information from cross domains. **Usually web APIs just return data though and not HTML** .

- ## [How to show google.com in an iframe? - Stack Overflow](https://stackoverflow.com/questions/8700636/how-to-show-google-com-in-an-iframe)
  - Why does google.com not load in an iFrame 

- The reason for this is, that Google is sending an `X-Frame-Options: SAMEORIGIN` response header. 
  - This option prevents the browser from displaying iFrames that are not hosted on the same domain as the parent page.

- Because it has `X-Frame-Options` Header policy and browsers tend to respect those policies.
  - The "X-Frame-Options" allows a secure web page from host B to declare that its content (for example a button, links, text, etc.) must not be displayed in a frame of another page (e.g. from host A). 
  - In principle this is done by a policy declared in the HTTP header and obeyed by conform browser implementations.

- You can use this URL in an iframe
  - `https://www.google.com/webhp?igu=1` this url works
  - it's Google itself leaves the hole. I don't say it's a Loophole, just maybe Google think it's necessary under some circumstances.

- If you want to embed Google into an iframe you can do what sudopeople suggested in a comment above and use a Google custom search link like the following. 
  - `<iframe id="if1" width="100%" height="254" style="visibility:visible" src="http://www.google.com/custom?q=&btnG=Search"></iframe>`

- ## [how to resolve iframe cross domain issue - Stack Overflow](https://stackoverflow.com/questions/40866219/how-to-resolve-iframe-cross-domain-issue)
  - I'm making web page that has to show another domain's web page.
  - `<iframe src="http://stackoverflow.com"></iframe>` usecase
  - My web page can't show stackoverflow.com. Because, stackoverflow denies this

- You need control over the domain you want to embed to remove/amend its CORS policy.
  - If the domain has explicitly blocked Cross-Origin requests, there's nothing you can do about it.
  - This is used to avoid anyone hijacking any site you want (you could have a full screen Google in an iframe running with your ads on top on bettergoogle.com, things like that).

- CORS does not apply when attempting to programmatically access content from a cross-origin iframe. 
  - If you want to access content from an iframe on a different domain, you will need to make use of the Web Messaging API (window.postMessage & the onmessage event) to communicate between your page and the iframe.

- It's also possible to access an iframe's content from another domain using Window.postMessage().
  - yes, but not here : because its iframe will not answer to the message. The question was "can they access the content of the iframe without my permission", and the answer is no.

- ## [iframe有什么好处，有什么坏处？](https://www.zhihu.com/question/20653055)
- 浏览器兼容性特别好
- iframe原本的用法在现在看来是不合时宜的，问题太多了但是它的其他功能却是不错的黑魔法，这里列举一些
  - 用来实现长连接，在websocket不可用的时候作为一种替代，最开始由google发明。Comet：基于 HTTP 长连接的“服务器推”技术
  - 跨域通信。JavaScript跨域总结与解决办法 ，类似的还有浏览器多页面通信，比如音乐播放器，用户如果打开了多个tab页，应该只有一个在播放
  - 历史记录管理，解决ajax化网站响应浏览器前进后退按钮的方案，在html5的history api不可用时作为一种替代。
- 纯前端的utf8和gbk编码互转。
  - 比如在utf8页面需要生成一个gbk的encodeURIComponent字符串，可以通过页面加载一个gbk的iframe，
  - 然后主页面与子页面通信的方式实现转换，这样就不用在页面上插入一个非常巨大的编码映射表文件了

- 用iframe实现无刷新文件上传，在FormData不可用时作为替代方案
- 在移动端用于从网页调起客户端应用
- 创建一个全新的独立的宿主环境。

- iframe还可以用于创建新的宿主环境，用于隔离或者访问原始接口及对象，
- 比如有些前端安全的防范会覆盖一些原生的方法防止恶意调用，那我们就能通过创建一个iframe，然后从iframe中取回原始对象和方法来破解这种防范。

- 可以用于单页面项目强制更新title
- 可以做委托提交，使页面不刷新、不跳转

- ## [为什么前端尽量少用iframe？](https://www.zhihu.com/question/23683645/answers/updated)
- 因为iframe等于打开一个新的网页，所有的JS/CSS全部加载一遍，内存会*2，无法释放，典型的内存泄露
- 最近一个vue项目，一个组件用到了iframe，每次切换路由，会销毁这个组件，再重新加载，
  - 在火狐浏览器下，切换几十次内存占用暴增，最后浏览器崩溃，但是在谷歌浏览器下一切正常，
  - 通过各种方法最终定位到是iframe导致的内存泄漏，就是因为每次组件销毁但是iframe的内存在火狐下不会被释放，谷歌没有这种问题。
  - 解决方法是：把iframe提取到上一层组件，只加载一次，切换路由不会重新加载iframe，就一切正常了。

- 移动端对iframe不友好
  - 最近有个项目在移动端使用iframe，解决了安卓IOS又出问题，解决完ios安卓又出问题
- iframe是(几乎)不能访问外部数据的，js的作用域也会很奇怪
- iframe会阻塞主页面的Onload事件；
  - 动态创建iframe利用src来进行异步加载就可以避免上面的问题了
- iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
- 当时是基于iframe实现布局方便考虑的，没成想这是一个巨大的坑，
  - 内容区域iframe高度自适应可把我们坑苦了，然后布局上出现各种怪异的问题

- ## [Why Not Iframe](https://www.yuque.com/kuitos/gky7yw/gesexv)
- 为什么不用 iframe，这几乎是所有微前端方案第一个会被 challenge 的问题
- iframe 最大的特性就是提供了浏览器原生的硬隔离方案，不论是样式隔离、js 隔离这类问题统统都能被完美解决。但他的最大问题也在于他的隔离性无法被突破，导致应用间上下文无法被共享，随之带来的开发体验、产品体验的问题。
1. url 不同步。浏览器刷新 iframe url 状态丢失、后退前进按钮无法使用。
2. UI 不同步，DOM 结构不共享。想象一下屏幕右下角 1/4 的 iframe 里来一个带遮罩层的弹框，同时我们要求这个弹框要浏览器居中显示，还要浏览器 resize 时自动居中..
3. 全局上下文完全隔离，内存变量不共享。iframe 内外系统的通信、数据同步等需求，主应用的 cookie 要透传到根域名都不同的子应用中实现免登效果。
4. 慢。每次子应用进入都是一次浏览器上下文重建、资源重新加载的过程。
- 其中有的问题比较好解决(问题1)，有的问题我们可以睁一只眼闭一只眼(问题4)，但有的问题我们则很难解决(问题3)甚至无法解决(问题2)，而这些无法解决的问题恰恰又会给产品带来非常严重的体验问题， 最终导致我们舍弃了 iframe 方案。

- 慢的问题：慢的问题可以使用单例的iframe，不销毁，而且可以预加载
- 路由问题：主应用和iframe的路由做个映射关系，这样iframe就可以实时响应url变化了
- 弹框遮罩、通讯问题：可以在创建iframe的时候把topwindow的对象挂在到子应用的window上，这样子应用就能直接调用topwindow的方法了，比如使用topwindow的弹框，而且这种方式主应用可以往iframe中注入脚本和样式等，通讯也可以通过管理“事件中心实现” （这个方案还在探索中）

- 另外某些情况下，比如网页截屏，iframe 就不被支持
- 事件处理也是个问题，比如实现顶层菜单展开时，需要点击空白处收起，如果点到iframe则无法触发

- iframe 还有一个问题就是不能改变其在 DOM 树中的位置，否则也会导致重新加载 iframe。而在以 VDOM + Router 的场景中  iframe 都会被重新加载
# discuss-csb-editor ✏️
- ## 

- ## [Feature request: Monaco Editor integration option? · codesandbox/sandpack _202201](https://github.com/codesandbox/sandpack/issues/305)
  - Codesandbox website uses Monaco, so it would be nice to have a similar experience when cross over between the sandpack version and the codesanbox website
- I'm curious, are there any pros & con's that come to mind when it comes to choosing codemirror vs monaco-editor? Was also curious about why you chose codemirror over vscode for prisma/text-editors 
  - Just to add a little bit of context, the current difficulties we had facing is a little bit out of scope, the main trouble we had is the setup of typescript's language server.
  - The Monaco editor is able to generate autocomplete based on the provided and customized d.ts files relatively easy but not for .tsx | .ts files, 
  - so for those packages written in `.tsx` by default, I cannot find an easy way to auto generate d.ts files and bundle them for the Monaco editor.
  - In term of UI/UX, as long as we are able to setup the environment and get the hint from the typescript server stably, it's just a matter of time to improve them gradually.
  - In fact, using CodeMirror in this case leave a lot of flexibilities to users to craft their own hint UI

- 🌹 Although I wasn't here when this decision of CodeMirror over Monaco was made, I think I can understand some of the reasons and highlight them here:
  - Mobile support: Monaco doesn't have great mobile support, and this is crucial for Sandpack to deliver a uniform experience throughout all types of devices; 
  - Final bundle size: CodeMirror provides an easy way to load only the modules/extensions we want to, which gives us the possibility to lazy-loading and code-splitting the CodeEditor component. Meanwhile, Monaco is a heavy package, and that's why CodeSandbox.io/CodeSandbox Embeds also defaults to CodeMirror in the mobile version (due to the previous reason too
  - Extensibility: TBH, I haven't had many experiences with Monaco before, but I can tell what I've heard, and Monaco makes it hard to customize and extend some configuration - and Monaco provides a great API to extensions, which pretty much solved many of our problems; 
  - Plus, Sandpack is designed to be extensible and provide a basic (but powerful) development experience, so the initial goal was never to support any language server by default but to provide ways (API, documentation, support) for the application consumer (you) implement it by yourself.
  - In fact, you can easily switch from CodeMirror to Monaco at your end, as Sandpack exposes all the APIs needed to implement it. 

- I think Danilo nailed the reasons I also considered when I picked CodeMirror over Monaco. For me personally, the biggest one was extensibility, because we had very specific interactions in mind, and I wasn't very confident that Monaco would let me build some of them. This is more of a matter of taste, but I also preferred CodeMirror's API over Monaco's (plus CodeMirror's source code seemed a lot more approachable), so I went with it for prisma/text-editors.
# discuss-sandpack
- ## 

- ## [How to securely install sandpack on a website? · codesandbox/sandpack _202401](https://github.com/codesandbox/sandpack/discussions/1061)
  - The bundler evaluates and transpiles all files in an iframe under a different subdomain. This is important, because it prevents attackers from tampering with cookies of the host domain when evaluating code.

- When using Sandpack, CodeSandbox never stores the sandbox content in its server - everything runs in the user's browser.
  - By using Sandpack, you will only get static files from codesandbox.io, and these files will be responsible for evaluating and bundling the sandbox content you create.

- ## I'm trying to implement Sandpack in Svelte, using sandpack-client. _202210
- https://discord.com/channels/333980639973867521/913053362738573312/1031251046930067507
  - So far i'm getting it working, but I'm trying to understand the concept with multiple files. 
- I don't think Sandpack can help on this specific case. 
  - Sandpack simply evaluates the code and runs it on another thread, and it doesn't capture any output execution (except the logs). 
  - But I think you can be inspired by Sandpack and use some concepts, like running the code in an iframe or a worker (due to security and performance issues), and using codemirror to provide a pretty neat coding experience

- Currently, Sandpack only supports JavaScript frameworks and those that don't have server dependencies. We're considering supporting server script in the future, but it's currently on research, and I can't make any promise when we'll have it running.

- ## 🆚️ Why choose CodeMirror? I think Monaco seems better? _202202
- https://discord.com/channels/333980639973867521/938366408889352223/938469861749825568
- We did consider Monaco, but that's a huge project for the purpose of sandpack (integrate small code snippets/sandboxes that can in the browser). 
  - Also, Monaco is not so easy to integrate in a simple react component library. 
- On the other side, it is quite easy to add Monaco on top of sandpack, if you want to customize the experience. We have an example right here: https://codesandbox.io/s/sandpack-monaco-integration-citxd?file=/src/App.tsx

- ## Do the code execute in the Browser like Stackblitz Webcontainers, or do they have to proxy to a server to process code and return a response? _202202
- https://discord.com/channels/333980639973867521/938366408889352223/938474311495340102
- Sandpack runs entirely in the browser, transpiling code in webworkers and executing everything inside an iframe. 
  - The only servers sandpack uses are CDNs for fetching the `node_modules` .

- ## 🚀 [Codesandbox open sources their execution environment: Sandpack | Hacker News _202112](https://news.ycombinator.com/item?id=29417937)
- Does it download the dependencies on the client side, and compile the JS on the client side as well?
  - Yep, it downloads and compiles dependencies on the client side. However, it does this on a different domain for security reasons.
  - Also, while it uses the CodeSandbox bundler, you can self host it so it's not dependent on our servers
- Is there an API to get the compiled and bundled sources into one output/result?
  - Yes, after every compilation we send the full bundler state. This is saved on the context so you can use that to analyze the output. In one of the examples in the blog post we show the transpiled code for example.
  - A hidden "feature" is that we automatically run tests defined (e.g. index.test.js) using jest, and dispatch the test results. So you can listen to that as well.

- I'd like to see storybook with support for this.
# discuss-author
- ## 

- ## [devpod: Codespaces but open-source, client-only, and unopinionated | Hacker News _202306](https://news.ycombinator.com/item?id=36407477)
- At CodeSandbox we're also working on this! Main focus of us is that we're running the environment in Firecracker microVMs, which allows us to snapshot and clone environments very quickly. 
  - This enables us to create a VM for every branch, which comes with the added advantage that every branch automatically has a snapshotted preview environment that can resume in ~2 seconds.

- ## ✏️🆚️ [Codemirror 6 and Typescript LSP - v6 - discuss. CodeMirror _202107](https://discuss.codemirror.net/t/codemirror-6-and-typescript-lsp/3398)

- Did https://codesandbox.io/ switch away from CodeMirror to Monaco for it’s TypeScript/LSP editor? If so, is there a discussion somewhere of why? _202212
  - 💡 Actually, CodeSandbox has always used Monaco as the default editor, except for a specific mobile version where we defaulted it to CodeMirror.

- ## [Vscode.dev: Local Development with Cloud Tools | Hacker News _202307](https://news.ycombinator.com/item?id=36855517)
- The editor on CodeSandbox runs web VSCode, and in that version we emulate Node.js in the browser to run local extensions.
- I'm curious about the technical details. Could you elaborate on how CodeSandbox runs Node.js in the browser? Does it use a Linux VM like Alpine compiled to WASM?
  - Nodebox is a runtime for executing Node.js modules in the browser

- Something else I find very confusing is that vscode.dev & github.dev are both free and run the editor fully locally in your browser. 
  - Github Codespaces on the other hand provisions a VM behind the scenes so you can run containers, build tooling and whatever else alongside the editor. That one charges by the hour.
- You do get something like 60 hours free a month with Codespaces (with lowest CPU/memory), which is fairly generous.

- Why use this - a stripped down unusable version of vscode when you can host a full instance of vscode on your linux server
  - You can use vscode.dev to achieve something very similar
  - Run a vscode-server on your server
  - - Connect (tunnel) to that code-server from vscode.dev using the Remote Development extension

- If you want a similar in-cloud VSCode experience, but tied more tightly to your SDLC (e.g. CI/CD, branch previews, deployments) for each project and requiring less configuration to get a dev server running alongside it (this just lets you edit code, not run it) we offer “Workspaces” at withcoherence.com.
# discuss-news-csb
- ## 

- ## 

- ## 

- ## 🤖 [Introducing AI Code Autocomplete Powered by Codeium - CodeSandbox _202311](https://codesandbox.io/blog/introducing-ai-code-autocomplete-powered-by-codeium)
- Today, AI takes a huge leap forward in CodeSandbox with code autocomplete powered by Codeium.
  - This is the result of a months-long collaboration with the fantastic team behind Codeium
  - Plus, we are making this available for free for everyone coding in our Devboxes 

- ## 🤖 [Meet Boxy, Your New AI Coding Assistant - CodeSandbox _202305](https://codesandbox.io/blog/meet-boxy-ai-coding-assistant?via=topaitools)
- I am Boxy, your new AI coding companion
  - I've been designed to thrive within the CodeSandbox environment, and that gives me a unique advantage. By having access to your entire codebase, I can understand your app's context like no other.

- Intuitive code refactoring
- Contextual code generation
- Automatic, meaningful commit messages
- Making learning more accessible

- ## We've hit the point that more than 150 thousand new MicroVMs get created on a monthly basis! _20240510
- https://twitter.com/CompuIves/status/1788888447119225192
  - The cost stays low thanks to VM cloning & snapshot/resume. 
  - I'm writing a new post about how our memory (de)compression works, might as well become a series now

- ## Over the past months we've received a lot of feedback about our pricing, and today we're updating the pricing of CodeSandbox to make public sandboxes free again! _20240509
- https://twitter.com/CompuIves/status/1788596561032937720
- From today, our free plans will include:
  - Unlimited public sandboxes
  - 5 private sandboxes
  - Private npm support
  - Our most important goal is to make coding more accessible, so we decided to remove that friction.

- ## We’re thrilled to announce our Storybook add-on: making every story come to life _20240508
- https://twitter.com/codesandbox/status/1788205375189025090
  - Open any story as a Sandbox with a click

- ## Our Web VSCode editor now has the GitHub Pull Request extension pre-installed _20240420
- https://twitter.com/CompuIves/status/1780960480649257444
  - Every PR will now have a development preview that resumes within 2s, which you can use to review and test code from VSCode directly.
  - The repo needs to have the github app of CodeSandbox installed, then it should work!

- ## People have asked me about the difference between CodeSandbox and other cloud/remote development environments.  _20240409
- https://twitter.com/CompuIves/status/1777719678384910582
  - Soo, I've written a post about the unique features we've implemented and how that creates a new powerful workflow.
- [What's Unique about CodeSandbox CDEs - CodeSandbox](https://codesandbox.io/blog/whats-unique-about-codesandbox-cde)

- ## ✏️ We have just deployed the VSCode Web editor for CodeSandbox! _20240408
- https://twitter.com/CompuIves/status/1777321064311496732
  - Now you can install VSCode extensions and use VSCode to build on CodeSandbox. All our templates will have their language extensions pre-installed.
  - You can turn it on in Settings under "Experiments".
  - The editor with our own UI is already powered by a headless VSCode so to say (we don't use its UI, but we use its state and editor). So I can see that the settings of Web VSCode stick around when disabling it.
- this using the gitpod or coder vscode-server or something else?
  - Using pieces from https://github.com/CodinGame/monaco-vscode-api, and it's connected to VSCodium server
  - The cool thing is that we can still render custom React UI within the VSCode UI.
- Can you setup extensions by default into some projects? Like once you fork the OCaml template it installs the ocaml lsp, for example?
  - Yes! You can do that in the devcontainer config
  - It should automatically install the extensions from the config. Though I did notice a race condition that I intend to fix by tomorrow!

- ## I finally got VSCode Web working together well with CodeSandbox. This way we can enable the VSCode extension marketplace! 
- https://twitter.com/CompuIves/status/1771151980607799738
  - It's been challenging making our existing UI/UX work well with VSCode, but I think we're finally striking a balance where we're getting best of both worlds.
  - We're using the open vsix marketplace 
  - We have Codeium integrated by default in the editor, so it's already enabled even now
- which extensions are you most excited about?
  - For me it'd be GitLens, Error Lens and GitHub PR integration. Also it would ensure that all language extensions (TS, Rust, Elixir) don't need a custom implementation anymore.

- ## We use Dev Containers to make the environment setup fast and reusable, so you can get up and running in minutes, powered by our VMs _20240221
- https://twitter.com/codesandbox/status/1759984324361760918
  - Have you tried running your Postgres project in CodeSandbox?

- ## Introducing CodeSandbox CDE: instant cloud development environments _20240131
- https://twitter.com/codesandbox/status/1752368702878527776
  - Run every branch in a powerful VM
  - Resume & fork in 2 seconds
  - Collaborative 24/7
  - Available now with usage-based billing
  - DevContainer support
  - VS Code, AI code auto-complete, automated git flow & more
  - [Introducing CodeSandbox CDE - CodeSandbox _202401](https://codesandbox.io/blog/introducing-codesandbox-cde)
- I think you guys are changing the game with this one, it is a step towards remote programming and who knows maybe sooner than later your service will play a huge role in the big playing field.

- ## 💰 I don't really understand this upcoming @codesandbox pricing/plans updates _20240116
- https://twitter.com/tomlienard/status/1747267455767150641
  - Sandboxes runs in the browser, they're not using any cloud RAM/CPU resources (these are Devboxes), why limit them to 20?

- I want to like CodeSandbox because I know how hard they’re working and innovating. But this change might require me to move away from them, and I’m not happy about that

- ## I'm very excited to announce that the CodeSandbox editor is now powered by VSCode _202311
- https://x.com/CompuIves/status/1727745935814349125
  - This makes CodeSandbox both faster & more familiar, where you can use your own keybindings, settings & themes from VSCode.

- Wasn't it the case in the original version of CodeSandbox (with Monaco)?
  - Yeah we've had quite a journey, from codemirror to monaco to a forked vscode to monaco and now finally the real vscode

- ## [Dev Container Support in CodeSandbox | Hacker News _202310](https://news.ycombinator.com/item?id=37950384)

- ## ✨🐍 [Python Support Now Available for CodeSandbox | Hacker News _202302](https://news.ycombinator.com/item?id=34870667)

- ## ✨🦀 [Introducing Rust Support in CodeSandbox, start a Rust VM in one click | Hacker News _202301](https://news.ycombinator.com/item?id=34444129)
- I'm one of the co-founders of CodeSandbox and a big fan of Rust. Rust support is something that we've been working on for a while, but the recent addition of Docker support in CodeSandbox really enabled it. 

- How many developers are there who are happy using some web based IDE versus their own tools?
  - I'm using a web based IDE for my dev, but I'm biased in that sense. The main advantage for me is that I can easily switch branches, as every branch has its own VM. + I can easily share in-progress work. I do use the VSCode integration, because I'm very used to VSCode.
  - That said, I've also spoken with people who use a Web IDE next to their local environment. E.g. they use a Web IDE for reviewing PRs or making smaller changes, and they use their local editor for feature development.
  - the main advantage I have here is that the dev server also stays running when I go to another branch (since it's a different VM). So I can work on one thing, share it with the team and in the meantime continue on another branch. They can see the devserver / running code, while I am working on something else.
  - It's especially useful for things like migrations or dependency management. In one branch I could work on something that has some database migrations, and then I can still switch to other branches without having to roll back the migrations.

- 🆚️ Is your biggest competitor Repl.it? What advantages do you have compared to them?
  - I'd say that CodeSandbox has a strong focus on extending the existing workflow for developers. That's why we have a VSCode integration, a GitHub integration with a GitHub App that creates a running dev env for every branch/PR, and we make sure that generally all editor features you expect (autocomplete, go to definition, hover info, etc) are available for the languages that we support.

- 🤔 Are you basically reselling hosted https://github.com/coder/code-server?
  - No, we've built our own web editor & iOS code editor. In our v1 editor we did run VSCode in the browser, but that was before code-server was released (in 2018). 
  - Even if we wanted to run code-server, that would be impossible as we allow for multiple users to open the same sandbox/branch, which wouldn't fit the model of VSCode server (which is single user per server).

- I'm not really a fan of in-browser IDEs. To me, it seems like a good way to constrain tooling environments. What I would love to see is an extension that runs all of my tests and debugger in a type 1 hypervisor that can simply send a set of instructions to setup the VM, a snapshot of the changeset, and allows a developer to run that exact environment on their machine. Combine that with LiveShare and you have something that closely mimicks the experience of handing a keyboard and mouse back and forth during pairing.

- I'm hoping Codesandbox would provide for CI/CD to directly deploy to production somehow. Basically, it's a "code in cloud" dream.
  - it is something on our radar, being able to press a button for deploy from CodeSandbox would be valuable for many people!

- ## 🐳 [Docker Support in Codesandbox | Hacker News _202301](https://news.ycombinator.com/item?id=34341818)
- Github Spaces, Gitpod, Codeserver (Coder), AWS Cloud9 (and AWS CodeCatalyst)... many bet on a workspace in the cloud. Wonder who will get the most attraction. 
  - So far my best UX was with Codesandbox for UI (react), Gitpod for a general (=Docker) single repo, and Codeserver on a VM for multi repo setup.
- We're now working a lot on making CodeSandbox a great experience for development, and we're now at the point that we're doing all our development of CodeSandbox on CodeSandbox as well. It's a quite opinionated experience, because every branch will have a URL that you can share, but it works really well when working together with a team. More info on that is here: https://projects.codesandbox.io/

- As a long time user, it’s been a pleasure following CodeSandbox’s progress recently. It works really well on an iPad, making it a great learning tool.

- ## Suuuper happy to finally share what we've been working on for the last year! We're introducing a new version of CodeSandbox, built with CodeSandbox itself. _20220317
- https://twitter.com/CompuIves/status/1504479650612871170
  - We've also grown our team from 12 to 29 people in that time, it's really really been a crazy year.

# discuss-csb
- ## 

- ## 

- ## 

- ## [CodeSandbox | Hacker News _201808](https://news.ycombinator.com/item?id=17814006)
- Ives van Hoorne (of CodeSandbox) got Visual Studio code to run in the browser
  - Very cool. We (Sourcegraph) could never get VS Code fast enough to be the right fit for code browsing and search, which is what we're targeting. So we built our own components

- ## [Show HN: CodeSandbox – A React editor built for easy sharing and reusability | Hacker News _201704](https://news.ycombinator.com/item?id=14022860)
- For now a quick summary of what we use now:
  1. Phoenix/Elixir for the API
  2. Node for bundling NPM packages
  3. Postgres for SQL
  4. Redis for caching NPM package metadata
- The editor itself is written in React (hah!) and uses styled-components, redux, redux-thunk and react-router@4.0.0 as most used libraries. I code split every optional preference a user may have (like autocomplete, vim or prettify) using webpack 2.

# discuss-collab
- ## 

- ## 

- ## [[Feature Request] Multi-user support _202203](https://github.com/codesandbox/sandpack/issues/405)
- I was able to get it working with firepad. It gives live text updates, and cursor positions, and I am able to see the changes in the iframe as well.

# discuss
- ## 

- ## [Lazy, lightweight sandbox for embedding on sites _201712](https://github.com/codesandbox/codesandbox-client/issues/381)
  - The problem is that the sandbox is still too heavy weight for this. We already initialize it only when user scrolls down to it, but eventually we should go even further and only render full sandbox when user clicks on it.
  - So the idea would be to render something very lightweight first, so we can have many sandboxes on the same landing and only load the rest when user actually wants to edit.

- The embed version is a separate application, made to be lightweight. With that url it only loads the preview, and loads the editor when the user changes view to editor. I also made the editor codemirror to lower payload size.
- ✨ 201805: We got runonclick now, which defers execution of the sandbox on click. We're also working on Sandpack, which allows you to kind of embed CodeSandbox as a component. I'm closing this one now, but we can always reopen it if there are new suggestions.

- A generated iframe shouldn't be much of a problem as long as you don't load all the js into it, because that would make a lot of js evaluations given many playgrounds on one page.

- ## Is there a good client-side-only React playground/sandbox? 
- https://x.com/adamwathan/status/1896581693538291840
  - Something that's lightweight and basically instant without all of the complexity of running VMs in the browser like all the other tools seem to be doing these days.

- Basically I’ve found the answer is no. We did our best to do something like this on the http://FormKit.com website, the current version is Vue only but there originally was also a react one. Still it always leaves out huge amounts of ecosystem ability unless you boot all of Vite in the browser (ala stackblitz) but those solutions are so slow they aren’t appropriate for docs sites imo.
  - On tempo’s site (http://tempo.formkit.com) I did something similar for the docs (also live playgrounds) but just ran the code raw in a web worker with a light handwritten code mod first.

- I use react-live for a few years now. Works for simple use cases, no support for external packages, and code executes in the same context, so keep an eye on security.

- ## I like it when products append `-${id}` to the slugified post titles.
- https://twitter.com/CompuIves/status/1757726648491798600
  - This makes links robust to renaming, without having to permanently tombstone the previous slug.
  - Medium and Notion do this.
- CodeSandbox does this too! No regrets.
- StackOverflow too. And as of last week, Maven as well

- My feedback. For a news site, it's important to include the current slug in canonical, when the title changes, the slug changes, it's a major update, it will be automatically detected by the crawlers and placed in the latest news.

- ## 🧊 wrote about @ValDotTown 's runtime, which we've rewritten three times in the last year because sandboxing untrusted code is a hard problem
- https://twitter.com/tmcw/status/1755616125474504960
  - [The first four Val Town runtimes _202402](https://blog.val.town/blog/first-four-val-town-runtimes/)
  - Val Town is a social website to write and deploy TypeScript. Build APIs and schedule functions from your browser.
- Nice overview! For https://skybear.net (runs user-provided Hurl/cUrl scripts) I ended up using AWS Lambda without IAM permissions given to it. Isolation from my application servers, no credentials issue and they can break whatever they want there.

- ## my course platform has a custom sandbox (built using Sandpack) that automatically persists any edits to my database, and restores them when the lesson is revisited.
- https://twitter.com/JoshWComeau/status/1749075678379626683
  - I just saw that the DB contains 285, 000 saved snippets, over 1GB of code!
  - originally, saved edits were stored in localStorage. Migrated to this solution maybe a year ago, since people noticed that their work wasn't following them from device to device.

- ## 👣 Are there any good sandboxes for Rails apps that let you also run docker containers?
- https://twitter.com/RogersKonnor/status/1747415376768487822
  - Why docker containers (more specifically docker-compose)? Because I use it to start a MinIO container to be able to simulate direct uploads locally.
- You could accomplish that with Codespaces for sure. Everyone gets a free amount of Codespaces usage every month, so this would be available to everyone with a GitHub account.
- gitpod can handle docker/rails pretty easily
