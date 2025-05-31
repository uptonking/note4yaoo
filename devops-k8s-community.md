---
title: devops-k8s-community
tags: [community, docker, k8s]
created: 2024-06-30T11:14:40.088Z
modified: 2024-06-30T11:15:28.002Z
---

# devops-k8s-community

# guide

# discuss-stars
- ## 

- ## 

- ## 🤔 is "service mesh" just a kubernetes marketing term for 25-year-old boring technologies like proxies and load balancers and tunnels?
- https://x.com/jer_s/status/1852770230680129700
- No. Among other notable differences, the main one is the central control plane to distribute configurations, apply global policies and provide e2e observability. Letting alone sidecar-less meshes that didn't exist
  - Istio, Cillium and others all call themselves service mesh. Sidecar has a clear meaning in K8s, so makes sense. But the same pattern (called as such or not) can be employed outside of K8s (by bundling Envoy/whatever in the VM).

- pretty much, each “service” has a proxy sharing its loopback as side car and only the proxies talking to each other. Each proxy is exposed as both forward proxy (for client requests from the service) and reverse proxy (for incoming requests to the service)

- Basically, yes!! Imagine you have a big playground with lots of kids playing different games. Proxies and load balancers are like teachers who help pass messages between the kids so they can play nicely. A service mesh is like giving each kid a walkie-talkie and a rulebook they can communicate directly, share secrets safely, and know the best ways to work together. So, while it uses some old ideas, a service mesh is a new and smarter way to help all the kids in the playground play together smoothly.

- I think it's a bit of both - new ideas built on top of old concepts. Service mesh does bring some much-needed advancements like traffic management and observability, but I agree the underlying tech isn't exactly new.

- May I use a MQ to replace those proxy mesh? Much simpler

- I remember the days we called this the “ambassador model”.
# discuss-scaling
- ## 

- ## [How do you guys move nodejs applications to k8s with cluster module? : r/node](https://www.reddit.com/r/node/comments/15qwkrg/how_do_you_guys_move_nodejs_applications_to_k8s/)
- I would say its not recommended because you don't get the granularity in scaling. We ran some sidecars in k8 for the message queue.. and that was about all the dependent scaling I have ever done with cloud.
  - I think the clusters would lead to over scaling. If one cluster is busy while the others are idle could lead to 3x the resources being consumed unnecessarily replicate this 3/4 times and you definitely over scaled.

- Clustering in containers is a bad idea. You are layering virtualization. While programmatically it's fine, it's also inefficient as all hell. Better to remove the clustering and scale up your container count by 4.

- 
- 

- ## [How to prepare my app to scale horizontally? : r/node _202208](https://www.reddit.com/r/node/comments/x0i7rp/how_to_prepare_my_app_to_scale_horizontally/)
- Just to add, other than about server architecture, your app itself have to be aware of horizontal scaling. It has to be stateless or make it shared across instances. E.g. configure cache in Redis instead of in memory only, No local file, commit all data into db.
  - If you do care about lengthy processing or background processing, it's better to be done in queue.
  - If you have websocket connection, you have to link those instances so listener connected at instance B can be notified from changes made on instance A.

- the key thing is: measure. Don't assume you need to scale big, but measure what your system can do, how you can increase it with simple measures and identify the pain points. (Often the real scaling problem is in your backend database or whatever you are using)
# discuss
- ## 

- ## 

- ## Why Kubernetes remains so popular:
- https://x.com/GergelyOrosz/status/1923869661713793342
  1. It avoids cloud vendor lock-in. Using cloud vendor autoscaling doesn’t!
  2. Kubernetes supports autosclaing well
  3. Its declarative. Predictable!
  4. It supports containers - while most cloud autosclaing supports more heavyweight VMs

- Doesn’t make much sense, sorry. Two more likely reasons are:
  - Bigger companies choosing Kubernetes because it’s the best tech to build an internal platform on.
  - Smaller companies following the pack without really understanding when not to use the technology.

- It’s a framework most devs know these days. Easy to onboard new hires/devs from other teams. Much harder to do so with obscure cloud-dependent infra.

- ## I understand that k8s and containers is impossible to avoid these days, but when shit goes wrong, the layers of the onion you have to unravel are wild. 
- https://x.com/mitsuhiko/status/1843307524700934176
  - Gone are the days you quickly create a coredump or attach gdb/strace etc. Now debugging takes ages and sometimes is not helpful.

- ## Why Kubernetes uses Pods instead of Containers
- https://x.com/iximiuz/status/1816522606834786540
  - A container is an isolated and restricted "box" to run (a single instance of) your app. 
  - But what if this single instance consists of multiple processes - the main one and some helpers? Pods to the rescue
  - You can indeed run multiple processes in one container. Nginx and Postgres, for instance, are multi-process apps, and they run perfectly in containers. But all these processes constitute a single app - they start and exit together and produce only one stream of logs. 
  - However, there are cases when you need to have two sets of processes in one "deployment unit" - for instance, the main app and its reverse proxy. And while technically it's possible to have such a setup inside a container, it's rarely practical. That's where Pods come to the rescue.

- ## [Show HN: Simplenetes – I replaced Kubernetes with 17k lines of shell script | Hacker News _202104](https://news.ycombinator.com/item?id=26661223)
- k3s (https://k3s.io), which is Rancher's awesome and lightweight Kubernetes distribution.
  - I use k3s in production, and it is great. But as far as daily use, it is not any simpler than kuberenetes. Initial setup and clustering is a breeze with k3s. But after that, you are mostly just working with the same k3s api as a full kuberenetes setup.

- 

- ## [Isn't a load balancer a single point of failure - Stack Overflow](https://stackoverflow.com/questions/21981514/isnt-a-load-balancer-a-single-point-of-failure)
- The point in avoiding a load balancer as a single point of failure is the load balancer(s) will run in a high availability cluster with hardware backup.
- I believe the answer to this question is redundancy. The load balancer, instead of being a single computer/service/module/whatever, should be several instances of that computer/service/whatever.l

- ## [Kubernetes HA and single point of failure - General Discussions - Discuss Kubernetes](https://discuss.kubernetes.io/t/kubernetes-ha-and-single-point-of-failure/8434)
  - By reading HA configuration doc, I’m a little confused as although multiple control plane nodes provides HA for cluster orchestratio, if the load balancer fails, the worker nodes can no longer communicate with control plane nodes. Isn’t the SPOF just shifted from control plane to the load balancer?
  - Does this mean I need to make load balancer redundant as well?

- Yes. The way we’ve done this in our own deployment was to run an LB on each of the control plane nodes and use keepalived 28/VRRP 15 for failover for a shared Virtual IP.

- ## [Kubernetes single point of failure and load balancing - Stack Overflow](https://stackoverflow.com/questions/37929770/kubernetes-single-point-of-failure-and-load-balancing)
- If Kubernetes service is a single point of failure or because it is supported by multiple pods on which kube-proxy is configured and services is just a virtual layer, it cannot be considered as single point of failure?
  - It will be single point of failure if Load balancer (LB) is mapped to single node IP as failure of that VM / Physical server will bring down the entire application. Hence point LB to at least 2 different node IPs.

- There is a guide on how to set up the k8s cluster in HA mode

- ## K8s的kubelet默认的maxPods是110个，不知道这样设计的缘由是什么
- https://twitter.com/stephenzhang233/status/1773648671940149460
- 早期版本 kubelet 有个本地的 kube API burst 和 qps 5 还是10的限制，这也会导致节点pod 太多，同步状态都会卡住。这也是为了减小apiserver压力， 一个节点qps5，kube qps 1000只能支撑 200个节点。而最初kube设计可能是几百个节点，～10000pod的数量级。才会有这些限制。
- 不希望集群太大了，规模太大了的话会各种组件都要魔改

- ## Google 当时的Borg 是没做网络虚拟化的，服务启动后前分配随机端口，启动后注册端口。这些都是在SDK里实现的。
- https://twitter.com/9hills/status/1730829030239117766
  - 这套方案社区根本接受不了。上下游全都要对接服务发现，否则你端口号都拿不到！至于负载均衡直接在SDK中实现。
  - 不是说Google藏着内部基建不愿意开源，而是内部基建别人根本就用不起来。
  - 所以说当年K8s 竟然能仅依靠现有的条件糊出一层虚拟网络加LB，大家都觉得真厉害。 当然现在都有各种方案了，以VxLAN 为主。

- ## k8s的黑点不在于那套实现 实现都能改，无非多花几个人月。
- https://twitter.com/ayanamist/status/1729942162249543996
  - 在于那套API，不管用go用java，甚至从零用C艹把apiserver重写一遍，你为了保证其它人用起来像个k8s，就得保留那套渣到爆炸的API
  - 没有精细的权限控制，workload+pod的设计导致防御面放在pod维度就要接受workload controller的ddos，而放workload维度就要穷举各种workload，哪天有人新弄了个workload就又要爆炸。
