---
title: thread-devops-deploy-cicd
tags: [cicd, deploy, devops]
created: 2023-10-12T14:06:13.077Z
modified: 2024-04-05T06:34:05.602Z
---

# thread-devops-deploy-cicd

# guide

# discuss-stars
- ## 

- ## CI/CD explained in simple terms.
- https://twitter.com/NikkiSiapno/status/1720810644713455793
  - [CI/CD Demystified — Build, Test, Deploy, Repeat](https://blog.levelupcoding.co/p/luc-26-cicd-demystified-build-test-deploy-repeat)
  - 使用流程图解释

# discuss-github-workflow
- ## 

- ## [How I Prefer to Write GitHub Workflows for zustand _202504](https://newsletter.daishikato.com/p/how-i-prefer-to-write-github-workflows)

- ## [GitHub Actions: A Basic Workflow Syntax _202407](https://medium.com/@leroyleowdev/github-actions-a-basic-workflow-syntax-4f06775790e8)
- 核心: trigger, job, step(action/shell-scripts)
  - Each job runs in a fresh instance of the virtual environment specified by `runs-on` .

```yml
name: Node.js CI

# triggered on every push
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-node@v2
      with:
        node-version: '14'
    - run: npm ci
    - run: npm test
```

- GitHub Actions imposes several limitations on workflows
  - Each workflow run is limited to 35 days. This includes the execution duration and any time spent on waiting or approvals. If a workflow run reaches this limit, it is canceled.
  - Each job in a workflow can run for up to 6 hours of execution time. If a job exceeds this limit, it is terminated and considered failed.
  - You can execute up to 1, 000 requests to the GitHub API in an hour across all actions within a repository. Exceeding this limit can cause additional API calls to fail
  - Free tier: Up to 20 total concurrent jobs, with a maximum of 5 concurrent macOS jobs.

- ## 🧑‍🏫 [Workflow syntax for GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions#concurrency)
- on
  - You can define single or multiple events that can trigger a workflow, or set a time schedule.

- permissions
  - use permissions to modify the default permissions granted to the `GITHUB_TOKEN`, adding or removing access as required
  - If you specify the access for any of these permissions, all of those that are not specified are set to `none`.

- env
  - Variables in the env map cannot be defined in terms of other variables in the map.

- defaults
  - create a map of default settings that will apply to all jobs in the workflow.
  - use `defaults.run` to provide default `shell` and `working-directory` options for all `run` steps in a workflow. 

- concurrency
  - 🔀 The default behavior of GitHub Actions is to allow multiple jobs or workflow runs to run concurrently. 
  - Use concurrency to ensure that only a single job or workflow using the same concurrency group will run at a time.
  - This means that there can be at most one running and one pending job in a concurrency group at any time. Any existing pending job or workflow in the same concurrency group, if it exists, will be canceled and the new queued job or workflow will take its place.

- jobs
  - A workflow run is made up of one or more jobs, which run in parallel by default.
  - To run jobs sequentially, you can define dependencies on other jobs using the `jobs.<job_id>.needs` keyword.
  - Each job runs in a runner environment specified by `runs-on`.

- steps
  - A job contains a sequence of tasks called steps. 
  - Steps can run commands, run setup tasks, or run an action 
  - Not all steps run actions, but all actions run as a step.
  - Each step runs in its own process in the runner environment and has access to the workspace and filesystem. 
  - 💡 Because steps run in their own process, changes to environment variables are not preserved between steps. 
  - GitHub provides built-in steps to set up and complete a job.
- uses 🧩
  - Selects an action to run as part of a step in your job.
  - The location and version of a reusable workflow file to run as a job. 
    - `{owner}/{repo}/.github/workflows/{filename}@{ref(SHA/tag/branch)}` for reusable workflows in public and private repositories.
    - `./.github/workflows/{filename}` for reusable workflows in the same repository.
  - Actions are either JavaScript files or Docker containers. If the action you're using is a Docker container you must run the job in a Linux environment. 
  - We strongly recommend that you include the version of the action you are using by specifying a Git ref, SHA, or Docker tag.
- with
  - Some actions require inputs that you must set using the `with` keyword.
  - When a job is used to call a reusable workflow, you can use with to provide a map of inputs that are passed to the called workflow.
  - use a GitHub App instead of a personal access token in order to ensure your workflow continues to run even if the personal access token owner leaves.
- run 🧩
  - Runs command-line programs that do not exceed 21, 000 characters using the operating system's shell.
  - Commands run using non-login shells by default.
  - Each `run` keyword represents a new process and shell in the runner environment. When you provide multi-line commands, each line runs in the same shell.

- container
  - If you do not set a `container`, all steps will run directly on the host specified by `runs-on` unless a step refers to an action configured to run in a container.
  - Use `jobs.<job_id>.container` to create a container to run any steps in a job that don't already specify a container.
  - If you have steps that use both script and container actions, the container actions will run as sibling containers on the same network with the same volume mounts.

- services
  - Used to host service containers for a job in a workflow. Service containers are useful for creating databases or cache services like Redis. The runner automatically creates a Docker network and manages the life cycle of the service containers.

- Filter pattern
  - *: Matches zero or more characters, but does not match the `/` character.
  - **: Matches zero or more of any character.
# discuss-release-publish-changelog
- ## 

- ## 

- ## 

- ## I prefer keeping CHANGELOG.md in git for my open source projects.
- https://twitter.com/sitnikcode/status/1756657599485735044
  - But Github gives some handy features on top of Releases.
  - @edloidas wrote a script for Github Action to create a release when a new tag appears.

- I use Changesets for this. They have GHA to release packages to npm registry (and you can release packages for different languages too), update changelogs and create a release
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 修了一个有趣的 bug。之前 CI 一直稳过，还以为自己代码写得好呢，今天发现是有问题，挂了ci也认为过了。
- https://x.com/laixintao/status/1810629972715020606
  - 出问题的地方是 ci 脚本开子进程，子进程如果失败，直接用子进程的 return code 来 sys.exit()。 实际上如果code大于255 Python 就用0退出，神奇。

- 在我的 Linux 上，返回的值范围是 0 到 255，实际上的返回值是 result & 0xFF，而不是大于 255 返回 0
- 和python好像没关系，bash也是这样的 bash -c 'exit 257'; echo $?
- 你再测试下 257 和 258， 就会发现是 code & 0xFF

- ## 把静态网站，next.js 网站部署在 Cloudflare 上，和部署在 Vercel 上相比，有什么优势呢？
- https://twitter.com/xqliu/status/1775874477538320521
1. 大体上体验非常接近，包括 GitHub 导入、构建脚本支持、版本预览等等
2. Vercel 好处：
   1. 域名放在哪里都可以；
   2. 集成数据服务（KV，DB，Config）非常方便
   3. 团队管理更好用
3. CF 好处：
   1. 提供很好用的分析工具，包含 Web Vitals
   2. 免费额度更高
   3. 全球最近接入

- CF Workers 也有 KV 和 D1 做存储。
  - 不过 D1 不是基于 Postgresql 而是 Sqlite 的
- 昨天刚宣布了prisma集成，可以连第三方PG了

- 区别就是能在vercel跑起来的next项目在cloudflare有可能失败

- 静态随便，nextjs 的server 用cf的话，想連Postgres或者redis都不行。Vercel 则可以

- 超过免费额度后，Vercel 的费用远高于 Cloudflare。

- ## 优化 golang 项目 CICD 速度的技巧, CD 耗时爆降超过 50%
- https://twitter.com/jarredsumner/status/1712218329413489011
  - pr 的描述写的也非常好, 不仅有 how 还有 why
  - [ci: optimize build](https://github.com/Ehco1996/ehco/pull/242)
- 原来这个不用 push 中间镜像的写法是 Docker 文档建议的, 学到了新的合并镜像（不用 push 中间镜像）的技巧
- 学习了，还有这种操作，本来想法是该动docker，build两种架构的binary，然后分别copy到不同的镜像中，但是那样就没法buildx 了
- webp也分享过, 混合部署 GitHub Actions Runner：Multi Arch 镜像构建速度飙升 10 倍
