---
title: devops-k8s-blog
tags: [blog, k8s]
created: 2024-06-30T11:14:08.946Z
modified: 2024-06-30T11:15:15.860Z
---

# devops-k8s-blog

# guide

# blogs

## [k8s自动扩缩容方案-HPA-VPA-KPA(18) - 杨梅冲 - 博客园 _202209](https://www.cnblogs.com/yangmeichong/p/16638895.html)

- 在 k8s 中扩缩容分为两种：
1、Node 层面：
对 K8s 物理节点扩容和缩容，根据业务规模实现物理节点自动扩缩容
2、Pod 层面：
我们一般会使用Deployment中的replicas参数，设置多个副本集来保证服务的高可用， 但是这是一个固定的值，比如我们设置 10 个副本，就会启 10 个 pod 同时 running 来 提供服务。如果这个服务平时流量很少的时候，也是 10 个 pod 同时在 running，而流 量突然暴增时，又可能出现 10 个 pod 不够用的情况。针对这种情况怎么办？就需要自动扩容和缩容

- 自动扩缩容对长连接和短连接的影响？
- 如何解决长连接突然断开问题：例如客户端网络闪断、刷新情况
  1. 会话粘性(Session stickiness)：通过启用会话粘性，可以确保同一客户端的请求始终被路由到同一个Pod。Kubernetes中的IngressController(如NGINX Ingress Controller)和Service可以配置会话粘性。
  2. 外部会话储存: 将会话状态存储在外部存储系统中，例如Redis或数据库，这样即使客户端连接到不同的Pod，依然可以通过会话ID从外部存储中获取会话状态。
  3. Graceful Reconnection: 在客户端实现优雅重连逻辑，确保在连接断开后能够快速重新连接并恢复会话状态。例如，通过WebSocket的重连机制，客户端可以在断开后尝试重新连接，并在重新连接时携带会话ID或其他标识信息。

- HPA（Horizontal Pod Autoscaling）：Pod 水平自动伸缩/横向自动收缩
  - 利用监控指标（cpu 使用率、磁盘、自定义的等） 自动的扩容或缩容服务中 Pod 数量，当业务需求增加时，系统将无缝地自动增加适量 pod 容器，提高系统稳定性。
  - HPA controller 已经实现了一套简单的自动扩缩容逻辑，默认情况下，每 30s 检测一次指标，只要检测到了配置 HPA 的目标值，则会计算出预期的工作负载的副本数， 再进行扩缩容操作。同时，为了避免过于频繁的扩缩容，默认在 5min 内没有重新扩缩容的情况下，才会触发扩缩容。
  - HPA 本身的算法相对比较保守，可能并不适用于很多场景。例如，一个快速的流量突发场景，如果正处在 5min 内的 HPA 稳定期，这个时候根据 HPA 的策略，会导致无法扩容.

- VPA（Vertical Pod Autoscaler），垂直 Pod 自动扩缩容，VPA 会基于 Pod 的 资源使用情况自动为集群设置资源占用的限制，从而让集群将 Pod 调度到有足够资源的最佳节点上。
  - VPA 也会保持最初容器定义中资源 request 和 limit 的占比。

- KPA（Knative Pod Autoscaler）：基于请求数对 Pod 自动扩缩容，KPA 的主要限制在于 它不支持基于 CPU 的自动扩缩容。
  1、根据并发请求数实现自动扩缩容
  2、设置扩缩容边界实现自动扩缩容
  - 扩缩容边界指应用程序提供服务的最小和最大 Pod 数量。通过设置应用程序提供服务 的最小和最大 Pod 数量实现自动扩缩容。
  - 相比 HPA，KPA 会考虑更多的场景，其中一个比较重要的是流量突发的时候

- Cluster Autoscaler (CA)是一个独立程序，是用来弹性伸缩 kubernetes 集群的。它可以自动根据部署应用所请求的资源量来动态的伸缩集群。当集群容量不足时，它会自动去 Cloud Provider （支持 GCE、GKE 和 AWS）创建新的 Node，而在 Node 长时间资源 利用率很低时自动将其删除以节省开支。

## [Pod 水平自动扩缩 | Kubernetes](https://kubernetes.io/zh-cn/docs/tasks/run-application/horizontal-pod-autoscale/)

- [自动扩缩工作负载 | Kubernetes](https://kubernetes.io/zh-cn/docs/concepts/workloads/autoscaling/)
- When you scale a workload, you can either increase or decrease the number of replicas managed by the workload, or adjust the resources available to the replicas in-place.
  - The first approach is referred to as horizontal scaling, while the second is referred to as vertical scaling.
- Kubernetes supports manual scaling of workloads. 
  - Horizontal scaling can be done using the kubectl CLI. 
  - For vertical scaling, you need to patch the resource definition of your workload.
- The concept of Autoscaling in Kubernetes refers to the ability to automatically update an object that manages a set of Pods (for example a Deployment).
- In Kubernetes, you can automatically scale a workload horizontally using a HorizontalPodAutoscaler (HPA).
  - It is implemented as a Kubernetes API resource and a controller and periodically adjusts the number of replicas in a workload to match observed resource utilization such as CPU or memory usage.
  - You will need to have the Metrics Server installed to your cluster for the HPA to work.

- You can automatically scale a workload vertically using a VerticalPodAutoscaler (VPA). Unlike the HPA, the VPA doesn't come with Kubernetes by default, but is a separate project that can be found on GitHub.

- Resizing a workload in-place without restarting the Pods or its Containers requires Kubernetes version 1.27 or later.

- It is also possible to scale workloads based on events, for example using the Kubernetes Event Driven Autoscaler (KEDA)

- 
- 
- 

- 水平扩缩意味着对增加的负载的响应是部署更多的 Pod。 
  - 这与“垂直（Vertical）”扩缩不同，对于 Kubernetes， 垂直扩缩意味着将更多资源（例如：内存或 CPU）分配给已经为工作负载运行的 Pod。
- 如果负载减少，并且 Pod 的数量高于配置的最小值， HorizontalPodAutoscaler 会指示工作负载资源（Deployment、StatefulSet 或其他类似资源）缩减。
  - 水平 Pod 自动扩缩不适用于无法扩缩的对象（例如：DaemonSet。）
- 在 Kubernetes 控制平面内运行的水平 Pod 自动扩缩控制器会定期调整其目标（例如：Deployment）的所需规模，以匹配观察到的指标， 例如，平均 CPU 利用率、平均内存利用率或你指定的任何其他自定义指标

- Kubernetes 将水平 Pod 自动扩缩实现为一个间歇运行的控制回路（它不是一个连续的过程）。间隔由 kube-controller-manager 的 --horizontal-pod-autoscaler-sync-period 参数设置（默认间隔为 15 秒）。

- 期望副本数 = ceil[当前副本数 * (当前指标 / 期望指标)]

- 
- 
- 
- 
- 

# blogs-concepts
- [什么是 Kubernetes 集群？— K8s 集群详解 — AWS](https://aws.amazon.com/cn/what-is/kubernetes-cluster/)
  - Kubernetes 将容器放入容器组中并在节点上运行。Kubernetes 集群具有至少一个运行容器组的主节点和一个管理集群的控制面板。
  - 容器组（pod）是 Kubernetes 下的标准可部署单元。Pod 包含一个或多个容器，在 Pod 内，容器共享相同的系统资源，例如存储和网络。每个 Pod 都有一个唯一的 IP 地址。 
  - Pod 中的容器不是隔离的。可以将 Pod 视为类似于虚拟机，其容器类似于在 VM 上运行的应用程序。可以通过为容器组（pod）和容器组（pod）群组附加属性标签来对其进行组织
  - 节点是运行 Pod 的机器。节点可以是物理服务器或虚拟服务器，例如 Amazon EC2 实例
  - Pod 是一个独立的构件，当其节点出现故障时，它不会自动重启。如果将一个或多个 Pod 分组到一个副本集中，则在 Kubernetes 中，您可以指定始终跨节点运行的副本集。

- [通俗易懂 | k8s 集群是什么？Kubernetes cluster 解读](https://www.redhat.com/zh/topics/containers/what-is-a-kubernetes-cluster)
  - Kubernetes 集群是一组用于运行容器化应用的节点计算机。如果您正在运行 Kubernetes，那么您运行的其实就是集群
  - 集群至少包含一个控制平面，以及一个或多个计算机器或节点。控制平面负责维护集群的预期状态，例如运行哪个应用以及使用哪个容器镜像。节点则负责应用和工作负载的实际运行。
  - 集群会有预期状态，它定义了应运行哪些应用或其他工作负载、应使用哪些镜像、应提供哪些资源，以及其他诸如此类的配置详情
  - Kubernetes 会自动管理您的集群，以匹配预期状态。举一个简单的例子，假设您部署一个预期状态为“3”的应用，这意味着要运行该应用的 3 个副本。如果这些容器中有 1 个发生崩溃，Kubernetes 就会看到只有 2 个副本在运行，那么它会再增加 1 个副本以满足预期状态。
  - 红帽® OpenShift® 是一个企业级 Kubernetes 版本。

- [Kubernetes 架构入门指南：一文带你看懂 K8s 架构](https://www.redhat.com/zh/topics/containers/kubernetes-architecture)
# more
