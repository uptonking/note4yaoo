---
title: devops-deploy-community-vps-paas
tags: [community, deploy, devops, vps]
created: 2024-11-16T16:54:04.677Z
modified: 2026-06-19T06:17:17.268Z
---

# devops-deploy-community-vps-paas

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-paas
- ## 

- ## 

- ## 

- ## 

- ## [茶的服务器公益平台即将开站！ - LINUX DO _202606](https://linux.do/t/topic/2438362)
  - https://github.com/388python/serve-share-platform
- 共享服务器吗？是什么虚拟化呢？lxc还是kvm还是docker呢
  - lxc, kvm可能开

- 但共享的是服务器的话这个用量该怎么计算啊？性能消耗不像是tokens那样能简单量化

- mjj们的闲置/灵车小鸡可以拿来造福了各位吗 

- ## 自部署的话，就别再用宝塔、1panel什么的啦, 我觉得 dokploy 和 coolify 是更好的选择
- https://x.com/javayhuwx/status/1856696509431271863
- dokploy 是不是只能部署在线上的服务器？ 我尝试部署在本地的虚拟机里，但是我没找到方法访问启动的服务
  - 部署在本地？好像没有意义？本地的话就直接run了
- 看了推文，coolify 开局占用 600Mb，dokploy 占用多少，不知道我的 2h2g 能撑住不
  - 2g就不建议折腾这个了
  - 又部署了 dokploy 体验了下，发现它的占用跟 1panel 差不多，使用上挺丝滑的，已经迁移过去了
  - 2g可以跑起来，不过从 Github 拉取编译这部分就吃不动了，得走 github ci 什么的

# discuss-vercel
- ## 

- ## 

- ## [Is it possible to deploy a NodeJs app in Vercel? - Stack Overflow](https://stackoverflow.com/questions/61808973/is-it-possible-to-deploy-a-nodejs-app-in-vercel)
- I just deployed a node.js app(13-09-2022) after hearing that Heroku is no longer offering their free tier.
  - I also got rid of the 404 error after renaming "app.js" => "index.js" (and updating all references to it).

- 🌰 https://github.com/vercel/examples/tree/main/solutions/node-hello-world

- [How to deploy Node.js server on Vercel properly? - Stack Overflow](https://stackoverflow.com/questions/78929927/how-to-deploy-node-js-server-on-vercel-properly)
# discuss-cloudflare-devops
- ## 

- ## 

- ## 

- ## 

- ## Cloudflare 新版 wrangler 的 Local Explorer 真好用，总算有个 web 界面可以看本地的 CF 资源了，
- https://x.com/vikingmute/status/2048404675960139788
  - 升级到最新版，运行 wrangler dev 命令以后，在 console 中再按 e，就会弹出一个 localhost:8787/cdn-cgi/explorer 这样的界面，就可以看本地所有的 CF 资源了，比原来方便好多。
- 之前用着另一个 `npx localflare` 也非常好用, 基本和这个界面一样

- 很不错了，不过还差个关键的 queue

- With Cloudflare CLI, Wrangler CLI, and Cloudflare Skill, I no longer need to use the UI. 
# discuss-multiple-vps
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Client-Software for managing multiple SSH-Connections? : r/selfhosted _202401](https://www.reddit.com/r/selfhosted/comments/18zd8pt/clientsoftware_for_managing_multiple/)
- `~/.ssh/config` You can sync it between multiple devices using any cloud service, self-hosted tool or git.

- Termius, the sftp tool helps a lot

- MobaXterm
  - ditto but it's only on windows 

- ## [How do you monitor multiple VPS instances across multiple providers : r/VPS _202501](https://www.reddit.com/r/VPS/comments/1huxv6u/how_do_you_monitor_multiple_vps_instances_across/)
  - So I have many VPS instances that host multiple personal projects, I bought them from different providers (Hetzner, Vultr racknerd...) and I'm looking into a centralized way to monitor all of them. I'm only interested in basic monitoring, CPU/RAM/Disk Usage/Uptime etc Preferably something with an alert system

- Netdata. Its very simple to install and works great

- Prometheus with Grafana for more detailed and control, netdata for quick and easy installation.

- Prometheus + node_exporter + Alertmanager + Grafana is a second option. But I should go with netdata too

- Beszel for a much simpler, light-weight option.

- ## [How do you manage multiple VPS servers in your workflow? What tools do you use? : r/VPS _202603](https://www.reddit.com/r/VPS/comments/1rq0ssm/how_do_you_manage_multiple_vps_servers_in_your/)
- I'm curious how people here manage multiple VPS servers in their daily workflow.

For example when you need to:

• connect via SSH
• transfer files
• deploy updates
• check logs
• run quick commands

Do you mostly rely on things like:

• SSH config / aliases
• tmux sessions
• tools like Termius or MobaXterm
• custom scripts
• something else?

- Mostly a mix of SSH config + tmux.

• SSH config for host aliases

• rsync or scp for quick file transfers

• tmux for persistent sessions

• small bash scripts for repetitive tasks across servers

Once the SSH config is set up, managing multiple VPS boxes becomes much faster.

- I use free Termius with keys on each server, numbered in groups based on platform (Enhance 1 2 … X, same for Plesk, FlyWP, xCloud, CloudPanel, NPM, and then ded servers. I went from running a bunch of VPS, to a bunch of ded bare metal running ProxMox running my own spec VPSs. Unattended upgrades in place, Beszel for monitoring server resources, email and Discord webhook notifications.
  - Separate VPS is nice and easy… ProxMox is great once you get past the networking and vmbr config learning curve, oh and buying costly subnets.
- We are big fans of Termius where we utilise it as our primary connection method. We also use Remote Desktop Manager too as its great for a mix of connection protocols

- I use XPipe, It has many features, I only use it for ssh connections management and file transfer
  - Do you still end up using other tools for things like deployments, logs, or running commands across servers?
- for small projects and development environments, I use CapRover, I set it up to auto deploy from git repositories once I make a new push, using Dockerfile, it keeps the most recent runtime logs for each Docker instance, if I need more logs I ssh into the server to get them. 
  - Coolify seems to be better the CapRover but I haven't had time to expirement with it yet.
- XPipe shows list of Docker containers inside a server if Docker is setup on it, so I can quickly ssh into the docker container with one click, then check the logs inside it. I rarely need to check logs via ssh, usually CapRover is sufficient.

- https://github.com/Termix-SSH/Termix Termix blows Termius out of the water and it's free to boot.
  - I'm mostly docker so also https://dockhand.pro
  - Recently I've been considering looking at https://wolfstack.org/ which looks really good, but it's still early and undergoing heavy development. Literally big changes daily.
  - Beszel for stats tracking, Gatus for uptime.
  - If you're willing to spend some money and are mostly dealing with basic website action, FlashPanel and ServerAvatar are both neat options.
- Do you find switching between all those tools manageable, or does it ever get fragmented when debugging or deploying?
  - Not really. Vast majority of the work I actually need to do is DockHand and Termix, and 100% of it could be done in termix if I wanted to.
  - The other services are just nice to have. If you use one of the last two paid options I mentioned you don't really need anything other than the one option.

- ## [For those of you that have multiple servers/VMs, how do you decide what goes where? : r/selfhosted _202205](https://www.reddit.com/r/selfhosted/comments/ukv7cp/for_those_of_you_that_have_multiple_serversvms/)
- I structure my networks as follows:

Logging and monitoring

Public

External

Internal

Private

- My setup, running on a Proxmox host:

file server, incl. services for media streaming, downloading etc

web server, LAMP stack for all my web projects. Also contains Gitea.

monitoring server, basically Zabbix server, and some ELK experiments

mail server, based on iRedMail

vpn server based on OPNSense

- I went a little different from you as i wanted to isolate some services for security reasons:

1 VPS for my email (alias) service as it attracts most crawlers/port scanners/attacks

1 VPS for my cloud instance (in a jurisdiction with strong privacy laws)

1 VPS for VPN (to chose my IP geo-loc)

1 VPS for all my tools (Gitea, Notes, Pastebin, Web bookmark...)

- My main parameter for services assignment to VMs are security and priority.

security: Different VMs operate in different VLANs (IOT, Private LAN, Management LAN, Service LAN) - depending on whether I, all, or only the family use services, they get assigned to the respective VM

priority: For important services, I have dedicated VMs, e.g. Gitlab has its own, Nextcloud has its own - other less important services are combined in a LXC-Docker nesting "catch-all", e.g. music/audio/photo/feedreaders etc.

# discuss
- ## 

- ## 

- ## 

- ## 

- ## 
