---
title: devops-net-nginx-community
tags: [community, network, nginx, traefik]
created: 2025-07-19T09:47:56.650Z
modified: 2025-07-19T09:48:20.797Z
---

# devops-net-nginx-community

# guide

# discuss-stars
- ## 

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
# discuss-alternatives-caddy
- ## 

- ## 

- ## [Caddy Web server is awesome. stop using apache and use caddy instead. : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1khbhqj/caddy_web_server_is_awesome_stop_using_apache_and/)
- More indepth reason you should give caddy a try.
- pros-caddy
  - Automatic HTTPS with Let's Encrypt
  - Simple Configuration: JSON config is also available for advanced use cases or dynamic configuration.
  - Modern, Secure Defaults: Strong TLS defaults and automatic redirects from HTTP to HTTPS.
  - Built-in Reverse Proxy
  - written in Golong: single binary
  - Extensible via Plugins
  - Great for Local Development and Self-Hosting

- cons-caddy
  - Fewer third-party modules and community scripts compared to more mature servers.
  - Performance Benchmarks Are Good—but Not Always Best

- benefits of caddy:
  - Caddy has automatic https with Let's Encrypt
  - Caddy config is trivial. It takes a 1 liner to serve your website
  - Even advanced features like url rewrites are much easier on caddy than on nginx. Furthermore there are plugins which make this much easier.
- Nginx proxy manager handles 1 and 2 doesn’t require any code to be written

- Caddy does support TLS GREASE

- Been using nginx for 15 years. No reason to switch. Rock solid and easy to configure.

- Swag makes nginx configuration trivial and almost entirely in your docker compose...
  - SWAG, which contains all the templates you’ll ever need.

- The main advantage of Caddy is that it's not a server, it's a "server of servers". It's a framework on which you add "apps" that do stuff. People (especially on this sub) tend to just use the http app to serve files or as a reverse proxy but it can do a lot more. Also, it's fully controllable via API and with JSON configs, which makes it even more interesting.

- I just use NPM and done. The UI is the easiest of em all. Why change to Cuddy?

- from my understaning traefik is best used for kubernetes or similar "docker only" setups. When you are in such a setup, it's nice to configure it through docker tags, but I really didn't enjoy the other ways of configuration.

- I don't think traefik offers a static web server

- [NPM vs Caddy : r/selfhosted _202405](https://www.reddit.com/r/selfhosted/comments/1copfx7/npm_vs_caddy/)

- [Planning to switch from Nginx reverse proxy to Caddy - will i miss or regret anything? : r/linuxadmin _202401](https://www.reddit.com/r/linuxadmin/comments/1aepv6g/planning_to_switch_from_nginx_reverse_proxy_to/)
# discuss-traefik
- ## 

- ## 

- ## 

- ## [Traefik vs NGINX Proxy manager(NPM) : r/selfhosted _202501](https://www.reddit.com/r/selfhosted/comments/1hucr6c/traefik_vs_nginx_proxy_manager/)
- I discovered caddy and it was immediately obvious that I want that simplicity instead of 3 abstraction layers and complicated dynamic setup and labels. Caddy is just the winner for me, the perfect balance between feeling in control and ease of setup.

- Traefik all the way, even though I also use Nginx and HAproxy. I would never see the need to use NPM though, since Nginx is very easy to configure.

- I like NPM, because I can set up access to devices on multiple networks/VLANs, as well as open streams across VLANS for single port access. I have some services on my LAN, that need be there to "see" everything, and it is firewalled that only the NPM instance can access those

- I moved from NPM to Traefik. Took me a while to get my head around the fact that with docker integration, the proxy config is done not in Traefik but within the container itself. The yml config for stuff that's not running in containers is less straight forward. If NPM works for you, stick with it, I don't think function wise, none is superior than the other. They are both proxies, in the end.

- I used NPM for most of last year. It is a slick GUI and I liked adjacent containers like goaccess-for-nginxproxymanager for log monitoring 
  - Caddy already has http/3 which NPM still lacks--if that matters to you. I did recently switch to Caddy full time after I found out goaccess-for-NPM now supports caddy logs
  - Traefik seemed to offer a lot more features, none of which I want beyond a simple reverse proxy with Let's Encrypt, but also a lot more complicated setup, so I've never tried.

- ## [Traefik vs Ngnix Proxy Manager : r/selfhosted _202104](https://www.reddit.com/r/selfhosted/comments/mhv0mx/traefik_vs_ngnix_proxy_manager/)
- I liked Ngnix Proxy Manager over Traefik since it has a GUI and i add and remove domains enough to find that valuable.

- 
- 

- ## [Traefic vs. Nginx : r/kubernetes _202109](https://www.reddit.com/r/kubernetes/comments/pgj5c1/traefic_vs_nginx/)
- I like nginx a lot and have been using it up until I started using K8s. Nginx is very capable, but it fits a bit awkwardly into k8s because it comes from a time when text configuration was adequate, the new normal is API driven config, at least ingresses. For k8s I expect hot reload without any downtime and as far as I can tell Nginx does not provide that. I would opt for a k8s native ingress and Traefik looks good.
  - NGINX does "hot reload". Is it somewhat expensive by spawning new threads to replace old ones? Also yes. If you have medium to low traffic volumes, you probably won't notice it though. We run ingress-nginx in our production environments that reload dozens to hundreds of times per day, this has never been an issue for us.

- Contour is fully opensource without the licensing issues of Traefik. Also it's already supporting Gateway API [1] which will replace Ingresses.

- Nginx works quite well. I needed to proxy not just http but arbitrary tcp ports. Pulled my hair out reading traefik docs. Traefic update also broke http for me and that was it for me. Running nginx in production and works very well.

- ## 🆚 [Traefik vs NGINX: Compare Features and Benefits](https://traefik.io/compare/traefik-vs-nginx)
- Traefik Hub is a cloud-native API gateway and management platform that is built for modern multi-cloud, hybrid, and legacy migration scenarios. 
  - Unlike NGINX, Traefik Hub enables advanced API management, streamlines Day-2 operations, and provides robust observability in a single, extensible solution.

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
# discuss-nginx-k8s
- ## 

- ## 

- ## [K8s体系下，ingress代表的云原生网关和传统的Nginx有哪些不同？会是未来的流量入口么？ - 知乎](https://www.zhihu.com/question/491886832)
- 在Kubernetes（K8s）体系下，Ingress（入口）是一种API对象，用于配置和管理应用程序服务的外部访问。
  - k8s中的ingress是一个标准规范，是定义外部流量进入集群内部的规则描述，
- ingress-nginx是一个具体的K8s ingress控制器提供者之一，通俗说就是一个k8s ingress的具体实现。同时也存在其他很多的实现，例如istio、kong等。

- 
- 
- 

# discuss
- ## 

- ## 

- ## [nginx's prefix is /opt/homebrew/Cellar/nginx/1.25.3 but why does the file search always have html subpath ? _202311](https://github.com/orgs/Homebrew/discussions/4880)
  - I checked nginx's prefix with nginx -V and see it is /opt/homebrew/Cellar/nginx/1.25.3 but why does the location search always start from /opt/homebrew/Cellar/nginx/1.25.3/html.

- The `html` part comes from nginx's default config

- 
- 
