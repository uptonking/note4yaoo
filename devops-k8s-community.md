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

- ## 
# discuss
- ## 

- ## 

- ## 

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
