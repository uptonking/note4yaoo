---
title: lib-aikit-claude-code-community
tags: [claude-code, community]
created: 2025-12-18T12:25:39.540Z
modified: 2025-12-18T12:26:08.445Z
---

# lib-aikit-claude-code-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## [Claude Code真假鉴别工具 _202601](https://linux.do/t/topic/1471272)
  - 做了个claude code测试真假的小工具，目前测试aws, crs框架的max号池皆可满分通过，kiro, cursor等逆向得分较低
  - [Claude Code 真伪鉴别](https://cctest.blueshirtmap.com/)
- 老哥你这个要粘贴APIKEY, 我怕你把我的apikey拿走了… 不敢用呀. 如果是本地部署的会好点.
  - key用完就可以删了，这个倒是没什么问题

- 虽然不知道是不是真的有用，但是我希望看到各大富可敌国的用户放出你们的评分截图

- 应该还有一个路子可以测试，kiro 是不能完全支持所有 tools 的，比如 json，read_page 这些，我之前kiro转的调这些工具都会报错但也能模仿出来
# discuss-roadmap
- ## 

- ## 

- ## [Petition: Claude Code should support AGENTS.md : r/ClaudeCode _202601](https://www.reddit.com/r/ClaudeCode/comments/1q3q8x6/petition_claude_code_should_support_agentsmd/)
  - [Feature Request: Support AGENTS.md _202508](https://github.com/anthropics/claude-code/issues/6235)
- Add a CLAUDE.md file with only one line "@AGENTS.md". works perfectly.
- I just symlink a Claude.md to the agents.md. Easy.

# discuss-news
- ## 

- ## 

- ## 
# discuss-tips/xp
- ## 

- ## 

- ## 

- ## [提升Claude Code 读 GitHub 和文档的速度 _202601](https://linux.do/t/topic/1487840)
  - 吐槽一下 Claude Code 读 GitHub 和文档的龟速体验, 实在受不了，摸索出了个新路子：
  - 直接把常用的开源项目 Clone 到本地！
  - 让它直接读本地源码，响应速度比联网查快了不止一点半点。强烈建议大家把这个流程封装成一个 Skill，用起来简直不要太爽。

- 下到本地看，看起来舒服多了，Github有时候挺卡的

- ## 💡 [今天偶然发现，Claude Code 是可以同时使用多个中转站的 ](https://linux.do/t/topic/1421764)
  - 核心思路是： 每次启动 Claude Code 时，会固定读取当前的中转站配置。
  - 使用 cc-switch 选择 中转站 A， 打开一个 Claude Code 实例（不要关闭）， 再次使用 cc-switch 切换到 中转站 B， 再打开一个新的 Claude Code 实例
  - 两个实例互不影响，可以同时使用
- 新版本不是这样了，如果打开a没关闭，然后cc切换api2，那打开的a也是用api2了
  - 是的，现在切换了之后即使不用重启都会到切换之后的中转地址了～

- claude code 本身也支持。 例如使用 claude --settings settings.xxx.json 来使用不同配置启动 Claude code

- 其实可以用 ANTHROPIC_BASE_URL=xxx ANTHROPIC_API_KEY=xxx claude 新版也可以用

- 我不缺工具 我缺中转

- 为什么不自己搭建一个负载均衡的中转
  - 搭负载均衡中转会有缓存问题吧

- ## 🤔 can i open multiple terminals and use multiple claude code to do different tasks at the same time? will the ai get confused? please check if it's possible . if it's possible to do it, what should i take care?
- Separate sessions = separate context. If each terminal/process uses its own conversation/session ID (or sends its own system prompt), the model won’t mix tasks.

- Each terminal maintains separate context - what you tell one doesn't affect the others
  - Claude handles conflicts automatically and is very reliable when multiple terminals touch the same file

- ## [Is Claude Code better on the Terminal? : r/ClaudeCode _202601](https://www.reddit.com/r/ClaudeCode/comments/1q3dp6c/is_claude_code_better_on_the_terminal/)
  - I been using Claude Code extension through VSCode Insider for a while now but I am not actually sure if it is better to use the CLI version or if there's any hidden advantages that I am missing.

- Much better especially if you are using Skills, a Spec and a couple of plugins

- I used it in cursor for a while, but honestly, it’s just easier to work in terminal. Way better information density and way fewer distractions.

- Yes. Terminal is the new IDE!!
  - Terminal is the old ide lmao

- I honestly don't know why they haven't enhanced the vs code extension to have the exact same features as the terminal by now. Can't they just use Claude code to ask it to add slash commands and make it equivalent to the CLI? 

- ## [《我是如何使用 Claude Code 每一项功能的》 译文 _202511](https://linux.do/t/topic/1145488)
  - 对我来说，把任务交出去，设定上下文，然后让它自己工作，只根据最后的PR成品来评估，而不是纠结过程
  - 从基础的 CLAUDE.md 文件和自定义斜杠命令，到 Subagents、Hooks、GitHub Actions等强大能力。这篇文章篇幅较长，我更建议把它当作参考手册，而不是一次性读完。

- [Claude Code中文教程：100%免费，从入门到精通 ](https://linux.do/t/topic/1403054)

- ## Claude Code has been a game-changer for me. But where I've felt the real magic is how it enables multitasking.
- https://x.com/omarsar0/status/2005337800284188879
- Are you seeing more benefits of multitasking on the same repo/project or different repos?
  - It’s across repos. Actually, that is what inspired the initial post. 
  - We need better interfaces and operating tools with these agents but you can still get a nice decent setup to the point where you don’t feel too many bottlenecks. Still experimenting with better setups so I feel like it can only get better from here.

- For a better interface for Claude Code, would you take a look at Nimbalyst, https://nimbalyst.com.  Its a free, local UI for Claude Code, session manager, tied to WYSIWYG markdown editor

- Multitasking works because the model is carrying state, not just generating code. The real unlock isn’t speed …it’s context persistence, task boundaries, and knowing when to hand control back to humans. That’s where productivity turns into reliability.

- ## [ClaudeCode固定在150K~160K压缩怎么办  ](https://linux.do/t/topic/1358788)
  - CC中转站、GLM都是稳定150K~160K期间压缩
  - 设置了不知道哪看到的 “CLAUDE_AUTOCOMPACT_PCT_OVERRIDE”: “90”, 也是稳定150K~160K压缩，想让他180K再压缩，有的时候刚好那20K就完成的了

- 不如关掉自动压缩. 总感觉自动压缩丢上下文太厉害, 还不如让它总结后 echo 到 一个md, clear后再读取.

- 我一般在150左右就换到 sonnet 1m，或者让它总结一下开新对话

- ## [用了几天claude code 发现提示词非常重要，看了论坛很多大佬的提示词，结合了一下分享一下我的提示词  ](https://linux.do/t/topic/1358954)
  - 代码调研优先（强制）修改代码前必须完成调研
  - 红线原则（绝不妥协）
  - 复杂问题深度思考（强制）
  - 知识获取（强制）遇到不熟悉的知识，必须联网搜索，严禁猜测
  - 修改前三问

    - “这是真问题还是臆想？” - 拒绝过度设计
    - “有现成代码可复用吗？” - 优先复用
    - “会破坏什么调用关系？” - 保护依赖链

- ## [分享一下我是如何使用Claude Code的，适用于简单日常任务(包含插件选择，提示词生成) _202512](https://linux.do/t/topic/1358868)
  - 前段时间发了一个使用CC为开题报告修改参考文献的内容, 发现大家对于这种使用CC来代替网页端的深度研究模式的方法还蛮感兴趣的，并且使用公益站成本也降了很多，所以就有了今天的分享
  - VSCode插件选择，我选用的是Chat for Claude Code插件
  - 最后附上编写好的一些Prompt，方便佬友们随取随用，在项目目录中创建CLAUDE.md，cc会自行遵守规则。
  - 具体的使用方法：先别急着让AI完成你的任务，先让他读取指定的文件，例如你的PDF，明确你的需求让他制定方案，然后按方案执行，这样完成任务的质量会好很多

```prompt
科研专家（用于改模型代码想点子）
论文分析（用于读论文和总结论文）
加强版AI助手（用于多种日常任务，写论文查资料都可以）
自适应专家代理（AutoGPT风格）
英语长难句翻译（适合改写成Web端使用）
系统建模分析师（UML建模设计，配合绘图专家和NanoBanana生图，我觉得会有奇效）
科研绘图专家（适合转为Web端，生成）
```

- 你们这些Prompt，CLAUDE.md都是怎么想出来的？我也想和我的Gemini 用一下。
  - 交给ai写的，把你要设计的角色说清楚然后慢慢改进，最好是先喂一个专门的设计Prompt的角色

- ## [佬们，问下在使用ai coding或vibe coding的时候如何防止工具执行危险命令 ](https://linux.do/t/topic/1354672)
- 本来便利性和安全性就是一组平衡，似乎既要又要比较困难。现在大多是白名单或者黑名单机制。

- 在.claude.config.json中设置deny常用的风险命令，然后别开dangerously skip permissions。我宁可次次审批也不要它误删。读写文件还好（rewind），命令执行了就麻烦，不可逆转。特别管好系统关键目录的权限（744，755），禁用sudo。

- ## [claude code如何禁用haiku-4这个模型 _202511](https://linux.do/t/topic/1132983)
- 这个是快速模型 一般小任务读文件之类的才会用到的。可以用环境变量指定模型，或者中转的时时候重定向模型

```sh
export ANTHROPIC_MODEL="claude-sonnet-4-5-20250929"
export ANTHROPIC_SMALL_FAST_MODEL="claude-sonnet-4-5-20250929"
```

- ## [Claude Code as a Sysadmin - Surprisingly good! : r/ClaudeCode _202510](https://www.reddit.com/r/ClaudeCode/comments/1oil25z/claude_code_as_a_sysadmin_surprisingly_good/)
- Here's my experience with using it as my sysadmin that i'd like to share:
- The task: Take a bare Ubuntu 22.04 VPS and turn it into a fully provisioned, multi-domain web and email hosting server.
- I made an account that can sudo, and without using it for production I've asked Claude Code to make three scripts:
- init_system.sh: that sets up the core stuff, my components were: nodejs, mariadb, PM2 and Nginx
  - it made me that script, it had everything, checked if it runs as root first etc...
  - Surprise: I ran it and everything was set up!!
- the next challenge: How do I add a domain, i want it in Nginx, and a web-root directory for it. plus a port where nodejs runs on, for PM2. So i asked Claude Code to make me another script:
  - that makes the config changes for Nginx and PM2 and creates a web root directory
- Once i had them. I made a fresh install, put the scripts there, and now this works perfectly.
- I even got it to make a security assessment of my server, where it has found a few issues, which i applied and iteratively patched the initial scripts that it had made.

- I used to spend days pulling my hair out about issues that are beyond my expertise (as most are regarding sysadmin), often having to hire somebody on Upwork to fix it, where now just copy pasting errors and logs fixes it within an hour.

- Claude Code is very helpful for troubleshooting and writing scripts for daily sysadmin / SRE tasks. For example, I haven't worked with Windows at all (100% Unix — Linux and FreeBSD), but created a couple of pretty complex scripts in Powershell.

- You're absolutely right! I shouldn't have run `rm -rf /`
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [TIL that Claude Code has OpenTelemetry Metrics : r/ClaudeCode](https://www.reddit.com/r/ClaudeCode/comments/1pjon1r/til_that_claude_code_has_opentelemetry_metrics/)
  - I just now learned that the lines of code metric is a delta and so it wasn't tracking the actual number of lines of code correctly. My actual lines of code accepted (not necessarily generated, just accepted) is 27, 925. In 7.5 hours. And I've eaten food, taken a long walk, chatted with my kids, and done other stuff during that time, so it wasn't 7.5 hours of straight claude coding. It's just been 7.5 hours since I enabled the metrics.

- I have been trying to learn more about these telemetry platforms. Can you make / point me to a tutorial about this?
  - Grafana is the viz tool. If your app logs to stdout you can use a scraper like promtail or alloy to scrape it to prometheus/loki for grafana to viz. This is commonly known as grafana stack or lgtm
  - This is a common observability setup. Do note it's relatively resource intensive

- ## [How do you use Claude Code? One big session for an entire project, or one session per task. : r/ClaudeAI _202507](https://www.reddit.com/r/ClaudeAI/comments/1m763t5/how_do_you_use_claude_code_one_big_session_for_an/)
  - One big session for an entire project, or one session per task, or do you use one session until something gets messed up, then create another session?
- One session per task but I manage them in Crystal https://github.com/stravu/crystal

- Usually large chunks

- One session for a piece of work: read handover document (created previous session), plan next steps etc etc using the many approaches detail here already eg think carefully, don’t assume - verify first, ask me any questions…go towards work. At 10% context remaining I will stop work, ask for a detailed handover plan, rinse and repeat. Still encounter problems though! Claims things are done but not, so I’ve introduced a new step, verify and confirm handover document
  - Interesting approach. What is the difference between this approach and auto compacting? Did you get better results with that compared to /compact?
- You don’t know what Claude has compacted eg it could have carried over irrelevant or aged info. I just want it to focus on the task at hand with the latest context. It seems to work better for me, especially using the handover > review and confirm approach as the new session catches out BS.

- Claude is going to do a bunch of searching and crap that fills up the context anyway. So I do one session per task and /clear after a summary of what was just done is updated.
  - However I use sub-agents that get fed instructions from the main session, so my main session lasts a pretty long time. 

- If I'm building something complex, with many features, I use Context Engineering with https://github.com/marcelsud/spec-driven-agentic-development
  - In a clean session I use the spec commands to help me plan the features, requirements, technical design and the tasks to be implemented.
  - I start a fresh session and start the implementstion by loading the feature context engineered with spec driven development and iterate with it. Then I go with it until the end, compacting the context before it reaches 3% left.
  - I use a clean session to help me double check the features completion, to prevent cobtext bias (the model saying it is correct because it thinks it built it corretcly)

- One session per task. If small enough, one session per feature to keep the flow and context, but if I'm close to needing to compact, then I will split on microservice boundaries like we do tasks.
  - I have a shared documentation repo. So, the end of each session is to maintain the documentation, which makes it easy for new sessions to pick up on architecture from previous tasks.

- It depends on the size of the task, IMO the sweet spot is using a context until it's about 50% full. So if there are a series of small related tasks then I might use the same session to do a bunch of them. Large tasks get a fresh session.

- Claude Code does not reread Claude.md after compaction or /clear command. For this reason I put the content of Claude.md into a slash command like /dev. When done with a bigger task I use /clear followed by /dev and have a proper context for the next big thing (I’m too lazy to restart CC).
