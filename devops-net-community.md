---
title: devops-net-community
tags: [community, devops, network]
created: 2024-11-16T10:58:13.978Z
modified: 2024-11-16T16:58:32.628Z
---

# devops-net-community

# guide

# discuss-stars
- ## 

- ## 🆚 [tx/rx which direction : r/networking](https://www.reddit.com/r/networking/comments/6muphz/txrx_which_direction/)
- Rx is "receive", i.e. stuff coming in and waiting in queue to be processed.
  - Tx is "transmit", i.e. stuff waiting in queue to go out.

- ## 🆚️ What's the difference between load balancers, reverse proxies, and API Gateways?
- https://x.com/Franc0Fernand0/status/1905922643837984991
- 1. Load Balancers  
Their main job is sending client requests to several servers. The goal is to spread the load evenly so there are no bottlenecks and the system works smoothly.  

1. Reverse Proxies  
- They act as an intermediary for client requests, fetching data and communicating with servers on their behalf. They effectively hide the identity of the servers and provide them with increased security.  
- The main benefit of a reverse proxy is that it adds another level of control and abstraction to make sure that network traffic between clients and servers flows smoothly. 
- Reverse proxies reduce the risk of attacks and external threats and can provide additional benefits.   
- For example, they can cache content to reduce server load and compress data to improve transmission speed. 
- They also often handle SSL/TLS termination, which means they manage encrypted connections, offloading this task from the web servers.

1. API Gateways 
- Their main job is to serve as a single access point for all API calls. They send requests to the right microservices and gather the results. 
- The main benefit of an API Gateway is that it makes the client interface for different servers easier to use. 
  - It can also enforce rules, add extra layers of protection, translate between web protocols, and collect data from many services. 
- Their ideal use case is as entry points to microservices systems.

- Nginx, which is a Reverse Proxy can have several "upstreams" and spread the load between them
# discuss-nginx
- ## 

- ## 

- ## 之前在服务器上用 docker 跑服务，需要折腾一下 Nginx 转发到 80 端口再套 Cloudflare 的解析。
- https://x.com/Stv_Lynn/status/1856325914076033419
  - 现在发现根本用不着这么烦，直接用 Cloudflare Tunnel 把端口转发出来就行了，甚至还能保护源站不被 censys 扫到。
  - 延迟会有一点差异。免费，能接受

- 在本机调试也是这样用，非常方便。

- 再来个tailscale，可以一个端口都不开

- 自用服务用tunnel 不错，但是没日志输出，跟nginx不一样

- 多一层还是有好处的，一个宽字符*dns记录多个子域名转到nginx上然自动proxy到多个容器上，如果tunnel负载加上nginx负载

- 然而用这个还是需要有域名，若是要用国内的云服务商，通过域名访问就要ICP备案
# discuss-net-protocols
- ## 

- ## 

- ## 最近几天折腾各种隧道：二层隧道（vxlan，pptp，l2tp，ikev2），三层隧道（openvpn，wireguard），四层隧道（redsocks，tproxy），七层隧道（shadowsocks，trojan），还漏了啥么
- https://x.com/skywind3000/status/1864123514728665559
- 理论上越底层效率越高?
  - 主要是内核支不支持

- pptp ，l2tp 至少是我十年前的玩法了，基本上部署出来直接秒封，流量特征太明显，换 IP 也没用。后面 shadowsockets 也不太行，真正抗的时间久的还是 trojan。
- 经验来看，这些大部分都很容易被封，特别是古老的pptp、l2tp这类。ikev2、vpn这些一旦频率过高也会封。

- l2tp/ipsec 数据层就是走的 gre 封装
# discuss-tcp
- ## 

- ## 

- ## 这个网站很有意思，致力于简化TCP分析，让TCP分析变得跟看聊天记录一样简单。
- https://x.com/austinit/status/1863763735602725345
  - [ChatTCP：上传PCAP文件在线进行TCP分析](https://online.chattcp.com/zh)

# discuss-tunnel/gateway
- ## 

- ## 

- ## 你目前在用哪种方式翻墙呢？ 🆚️
- https://x.com/__Inty__/status/1905650995750649966
- 这图挺误导人的，而且已经有些过时了
- v2RAY 很流行，软件多，节点多，提供商作坊多，trojan，提供的作坊比较少。支持的软件比较少
- 最安全的是 ssh 隧道，不过一般人搞不来。

- ## 一款内网穿透工具 Frp 的跨平台桌面客户端：Frpc-Desktop。
- https://x.com/GitHub_Daily/status/1893616798718685446
  - 开箱即用，提供简洁可视化配置界面，支持所有 Frp 版本，轻松实现内网穿透。
  - 还支持开机启动、快速分享 frps、所有配置的导入导出、批量端口等功能。
  - 兼容 Windows、macOS 和 Linux 系统安装使用。

- ## 内网穿透方案之tailscale+cloudflare tunnel
- https://x.com/Stv_Lynn/status/1878316656998649969
  - 很多homelab玩家拿到机器遇到的第一个问题就是怎么把服务部署到公网。
  - 有的人会选择frp，但考虑到国内服务器带宽和价格的情况下frp效果实在太差。
  - 也有人使用tailscale这种p2p方案，但这种并没有把服务暴露到公网。这里分享一个我的解决方案。
  - 首先你需要在本地机器和一台海外vps上都部署tailscale并且完成登录。关于vps的选择，推荐使用新加坡的vps（可以做到一机多用，能够正常代理ChatGPT，大多直连效果也不错），不推荐使用国内的vps，因为后面还要连接cloudflare。

- ## 有人用过 tailscale 的开源实现 headscale 吗？感觉也不错…想折腾一下。 
- https://x.com/tualatrix/status/1879877738733130087
- 都用，这类工具的核心是要打洞成功率。我一直都是  tailscale 和 zerotier 一起用，在我场景下，zerotier 的成功率明显高于 tailscale

- 没啥区别，到最后只要能打洞就行。headscale好就好在可以自建derp和无限机器。无限机器我们用不到，tailscale的就够用能直接打洞就不用自建，所以不如都有IPV6好

- 不好用，我就是用过那个之后才换到 tailscale 的。 另外， zeronet 也没有 tailscale 好用

- headscale只是tailscale的后端而已，用它可以不依赖tailscale的官方后台自由度高一点，客户端仍然还是用tailscale

- 个人感觉 headscale 完全没有必要，直接用 tailscale + 自建 derp 就行。

- 用过了，因为自建所以稳定性比不上官方，功能缺失挺多不好用，不如官方服务。

- ## 🆚️ Proxy Vs reverse proxy
- https://x.com/bytebytego/status/1885934707944345892
  - 正向代理侧重客户端限制，反向代理侧重服务端
- A forward proxy is a server that sits between user devices and the internet. A forward proxy is commonly used for: 
  - Protect clients
  - Block access to certain content
  - Avoid browsing restrictions
- A reverse proxy is a server that accepts a request from the client, forwards the request to web servers, and returns the results to the client as if the proxy server had processed the request. A reverse proxy is good for:
  - Protect servers
  - Load balancing
  - Cache static contents
  - Encrypt and decrypt SSL communications

# discuss-ssh
- ## 

- ## 

- ## 服务器 ssh 被扫了 16w 次，就离谱。
- https://x.com/hubingkang/status/1900362862767595638
  - `sudo lastb | wc -l`

- 紧查了查，我的几台国外服务器，20多万次。国内的反而少一点，不到两万次。但是我内网穿透的家里主机，竟然也有将近2万次，家里的电脑密码很简单，也不知被攻破了没
  - 家里内网得注意，一被破解了不是盗取资料就是要勒索了。

- 慌什么，用密钥登录他又无法攻破
  - 有些用密钥，有些用的密码

- 用fail2ban拦截
  - 还可以自动报 http://blocklist.de，顺便做个 crontab 每天拉那个网站的 ip 黑名单
# discuss
- ## 

- ## 

- ## 

- ## 发现一个Tailscale服务端的开源替代品，Headscale，可以用它自建Tailscale服务，客户端还是Tailscale，但是可以完全掌控在自己手里，不限制用户数和设备数
- https://x.com/ShouChen_/status/1868228852449005735
