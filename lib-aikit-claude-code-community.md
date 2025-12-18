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

- ## 
# discuss-roadmap
- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 
# discuss-tips/xp
- ## 

- ## 

- ## 

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
