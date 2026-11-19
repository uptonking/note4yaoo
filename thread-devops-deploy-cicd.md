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

- ## 

- ## 

- ## [How do you prefer to deploy services? : r/selfhosted _202601](https://www.reddit.com/r/selfhosted/comments/1qlw8ln/how_do_you_prefer_to_deploy_services/)
  - docker >> k8s > apt/yum

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
# discuss-domain-name
- ## 

- ## 

- ## [国内注册商的可备案域名续费好贵，有没有便宜推荐 - LINUX DO _202605](https://linux.do/t/topic/2104137)
  - 之前一直用的国外注册商的数字.xyz域名，几块钱一年，自用老香了
  - 这次买了阿里ecs99一年，打算配个域名，发现国内注册商的域名，续费一年上百！
- 国内服务器好像只能绑备案域名，不然80和443会被拦截

- 国内别想了，cnnic 神人操作一堆，而且不备案锁你 HTTP/HTTPS 端口。

- 国内没辙，都是第一年便宜，续费贵死，之前国际平台是6~8位纯数字的xyz后缀十年大概五十块，现在的话，大概60多块

- 国内对于每种网站都有极其细致的备案要求，个人博客还分有可评论和不可评论两种，更别提论坛还要给管局提供超管账号。

- 个性域名都这样，首年便宜，续费贵死，而且容易 serverHold，我的 .top 就被封过一次。

- .top 的阿里云首年 1 元，续费十几块。
- top域名早期很多诈骗网站使用，所以三大运营商都或多或少的对top后缀有所针对

- 好像新用户才便宜，再到618 1111这种还有打折打包的，你也可以让亲戚朋友给你买然后再迁到自己名下
- 可以用另一个手机号再用另一个实名，然后过户！

- 可以试试阿里云，挺划算的。或者在国外买，多续费几年，再转移国内

- ## [xyz域名转移到哪里续费便宜啊？ - LINUX DO _202603](https://linux.do/t/topic/1773602)
  - 宝塔0.01买了一年.xyz的域名（是英文不是数字），宝塔续费要91一年，有没有转移过去以后续费会更便宜的厂家啊？
  - 看了一圈都不太便宜，续费比.com还贵了，老实当年抛域名算了

- spaceship 四块几毛钱（不过是六个数字.xyz）

- https://tld-list.com 这里可以对比价格
# discuss-cicd-github
- ## 

- ## 

- ## 

- ## 

- ## 

- ## Installing Playwright browsers can take minutes on GitHub Actions.
- https://x.com/jiahan_c/status/2082299710577201216
  - GitHub-hosted runners already include several browsers. If a compatible one meets your E2E needs, use it directly to skip the install and speed up CI.
  - Keep in mind that runner-provided browsers may change independently of Playwright. This can introduce differences, but the CI time savings often make it worthwhile.

# discuss-cicd-local
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## Problem: Your CI server is slow, but your dev machines are fast. 
- https://x.com/housecor/status/2070608867268911340
  - Solution: Use your dev machine to run checks quickly instead of waiting on slow CI.

- "tests pass on my machine"
  - Yep genuine risk - env vars are primary risk to me

- I’ve started doing the same. I’ve got a lot of respect for GH, but as an industry we’ve backed ourselves up in a stupid corner with the centralised ci. Local running isn’t for every project, but it is for most.

- Yes. Tart has been quite useful on macOS for Linux/macOS and QEMU for Windows. 
# discuss-cicd-mac
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 运行 Snapshots 测试，本地始终通过，CI（Mac mini）始终失败，百思不得其解…
- https://x.com/tualatrix/status/2050940460903071828
  - 后来让 AI 来看这个问题，抽丝剥茧，终于找到了问题：Mac mini 由于没有接显示器，默认按  1x backing scale 来生成 snapshot 截图，而测试集是本地机器按 2x 生成的，自然就失败了。
  - 测试集也是在 CI 机器上生成的
- https://github.com/iamsyc/VoidDisplay  创建一个虚拟显示器开启 hidpi 的

- 一直有这个问题（或者叫特性）。没接显示器的mini在使用在线会议共享屏幕时，对方看到的是白屏。接一次显示器比如hdmi输出，然后再拔掉就一切正常了。
# discuss-vps-configure
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Do I need both Terraform and Ansible? : r/devops _202306](https://www.reddit.com/r/devops/comments/13zzd62/do_i_need_both_terraform_and_ansible/)
- > "Provision with Terraform. Configure with Ansible."  I see this everywhere.
  - at the end of the day, terraform is using the Go SDK in the form of terraform providers while ansible is using the Python SDK in the form of the ansible collections. the approaches are not very different. i would still say the “idempotent” approach of ansible is theoretically cleaner than terraform state. but i use cloudformation for infra. and i dont do any remote configuration management with ansible, chef, puppet, saltstack, anything. just AMIs and userdata.

- Currently using both in our environment. Terraform for infrastructure and ansible for configuration. Ansible can stand up infrastructure, but it doesn’t do it well. For our environment, we are an AWS shop. You’ll need to know what to build first before the next (yaml file is read top down in Ansible). With terraform, the logic is already there and I don’t need to worry about having things in the correct order. For ssh enable, user creation, etc. you just write playbooks and run those after you stand up the infrastructure. Anything that you would do manually after terraform would be done using ansible.

- I would advise the use of Terraform for resources orchestration and Ansible for configuration management. But if you really want to use only one to the the work of both then choose Ansible.

I have witness the use of Ansible for diverse use cases from orchestration of cloud resources, execution of standalone scripts(python, shell), creation of resources in kubernetes, interaction with a ton of services mostly APIs, etc. and to be honest Ansible did it really well.

Ansible is really good for configuration management I seriously doubt Terraform can come close to it in CM.

- Terraform spins up your infrastructure. Ansible configures it.
When integrating with your CI/CD pipelines you need to figure out a pattern and use it across all projects I like having my pipeline invoke both the terraform and the ansible

- Provision: Terraform or Cloud Specific tool(Some give you indications of drift)

Configure: Ansible or Agentless Saltstack(Just learned of it recently...)

What I care most is idempotence(running repeatably without differences in outcomes of is being applied from initial run) and reporting what has changed, been applied etc

- Both. Though Terraform is mainly purposed for a seemless multi-cloud hybrid environment. Ansible will have all of the module you need for reaching out to your VMs and doing health/state checks.

- This also depends on what your tech stack looks like. If you are in the cloud, or running things in managed k8s clusters than you probably don't need traditional configuration management.
If you are managing vms and the software on them then you do.

- I don't see how to use terraform for configuration management, it is mostly a provisioning tool. For configuration management in servers you will use configuration management tools like puppet, ansible and chef. 
  - Think about terraform as a tool working in a higher abstraction layer, provisioning the infrastructure like VMs and some of its higher level configuration like size, network interface, storage, etc. 
  - If you need to go at the lower level of installing software, configuring files in the server, managing users, applications, etc, then you need a configuration management tool.

- I prefer terraform for the infrastructure and Ansible for configuration. We also however keep zero data locally, so it’s easy to just terminate and replace

- Cloudinit can take care oft some oft these task (especialy SSH and key setup)
  - This, and can be combined with Ansible and Chef
# discuss-vps-cicd 👾
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [How do you manage more than 5 VPS from one place? : r/SelfHosting _202610](https://www.reddit.com/r/SelfHosting/comments/1xa6qkv/how_do_you_manage_more_than_5_vps_from_one_place/)
- I would suggest ansible. It's quite a popular self-hosted solution. It is "agentless, " meaning you don't need to install any software on the destination servers; it works entirely over standard SSH. You write simple automated scripts (Playbooks) in YAML to manage everything at once.
  - Claude and Codex make using Ansible a no brainer imho. All I do is create a dedicated Ansible user with an SSH key and password-less sudo. You can use cloud-init at most big VPS providers to automate those steps too. I even deploy Docker images with Ansible.

- I'd probably try and consolidate them into a single or fewer VPS into docker containers and use Caddy or traefik to reverse proxy them.
In terms of mgt, there's several options life Ansible you can look into.

- Ansible for internal os, I run everything in kubernetes so use gitops for deployment of apps. And if possible opentofu for building the vps if there is a provider

- Kubernetes, you don't dealing with machines any more, you dealing with single cluster.

- tailscale. ssh to all from one place

- If you use docker for your projects then dockhand has a free edge client you can install on the VPS and manage from one dashboard.
Otherwise good old SSH using keys only and no password

- ## [How do you set up automatic deployment from GitHub to a Hetzner server? : r/hetzner _202512](https://www.reddit.com/r/hetzner/comments/1ps0itc/how_do_you_set_up_automatic_deployment_from/)
- Build image on GitHub actions, rsync into the server, run docker command

No registry

No frills

Straight forward

- Self hosted GitHub action runner on the server, and GitHub action in target branch. Inspired by fastapi docs

https://github.com/fastapi/full-stack-fastapi-template/blob/master/deployment.md

- I'm using https://github.com/adnanh/webhook with custom bash scripts to receive webhooks from github in case i push something, merge something, etc. Based on this i run the custom script to checkout, build and run my code.

- Just set up a self hosted runner in the server, set up dockerfile and docker-compose file, create a workflow file in .github/workflows to make runner pick them up. Than just push to the repos, ci/cd.

Edit: dokploy is good afaik.

- Caddy + Docker compose is good enough. You can automate your build with GitHub actions. For your static stuff just host on firebase or GitHub pages

- ## [Methods to automatically deploy docker image to a VPS after CI build. : r/devops _202603](https://www.reddit.com/r/devops/comments/1rmj21i/methods_to_automatically_deploy_docker_image_to_a/)
- Things I have considered
  - running ansible from ci. Ansible in another repo still doable by calling another GitHub action for the build GitHub action. But storing ssh keys with sudo access level in GitHub secrets doesn’t sound that safe to me.
  - also similar with running command to docker to update from the ci to server.
  - creating a bash script to may be check images and update containers and run it via cron or systemd service regualar interval of may be 5 min or so. It is a pull base so more secure but a tricky to deploy specific versions.

- The pull-based approach you described (server checks a repo for version changes) is the right instinct. It avoids storing SSH keys in CI and gives you an audit trail of what's deployed via git history.
  - What I've done: a lightweight agent on the VPS that polls a config endpoint or watches a git repo. When the desired image tag changes, it pulls and restarts the container. Basically a stripped-down ArgoCD for single-server Docker. The agent authenticates with a pre-shared key derived from something stable on the server, so no SSH keys in CI at all.
  - For something off-the-shelf, Watchtower can watch for new image tags and auto-update, but it lacks the "deploy a specific version" control you'd want. The cron/systemd script checking a deployment repo is honestly the simplest reliable option for a single VPS.

- I’d probably go pull-based, not “CI SSHes into prod.” The closest thing to ArgoCD-on-a-VPS is usually: keep a small deploy repo with your compose.yaml, pin the app image to an immutable tag or digest, then have the server poll that repo with a systemd timer and run docker compose pull && docker compose up -d when it changes; Docker’s own docs support that workflow cleanly. watchtower exists and can auto-update containers when a new image is pushed, but it tracks the exact tag a container is already using, so it’s great for “always follow this tag, ” less great if you want an auditable “promote version X to prod” flow.
  - For your case, I’d treat CI as “build + push image + update deploy repo, ” and treat the VPS as “reconcile desired state.” That gives you version control, rollback history, and avoids keeping a prod SSH key with sudo in GitHub secrets.
- Super easy with a simple cronjob git pull ; compose up. You can run this every minute. There. You got yourself continous deployment

- If it's a single VPS, don't overthink it: run a systemd timer on the box that docker pulls :latest (or better, a pinned tag) and docker compose up -d. CI just pushes the image. No SSH keys with sudo in GitHub, no remote exec roulette. Bonus: deploy still works when GitHub Actions is having a day.

- I setup github webhooks on push event and just pull the repo onto my vps and rebuild on pull on vps

- 
- 
- 

- ## [Best method for continuous deployment of a Docker Compose stack from GitHub? : r/selfhosted _202506](https://www.reddit.com/r/selfhosted/comments/1lely9q/best_method_for_continuous_deployment_of_a_docker/)
- What I've Considered
  - Portainer and Watchtower — I don't need Portainer and would prefer not to run a heavy container like Portainer or Watchtower to handle this.
  - GitHub Actions SSH to server — I'm not comfortable opening up SSH access.
  - Recurring cron job — This could be a backup option but I'd prefer a real-time solution that deploys immediately after a merge to main.
  - GitHub Actions Self-Hosted Runner — This seems like the 'best' option but I haven't tested it out yet as the setup seems daunting.
  - SSH over Tailscale from GitHub Actions — Another option. I would need to set up Tailscale on my homelab machine.

- What I do is just store an ssh key in Secrets, then ssh into the vm in the action, and do compose up -f ..

- Forgejo (fork of Gitea) + Woodpecker (fork of Drone), both selfhosted.

- Komodo is your answer. Has a great integration with Git repos like GitHub, supports webhooks to trigger actions from GitHub into your Komodo instance, etc.
# discuss-cicd
- ## 

- ## 

- ## 

- ## 
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
