---
title: lib-notb-jupyter-community-collab
tags: [collaboration, community, jupyter]
created: 2024-06-30T03:27:39.301Z
modified: 2024-06-30T03:27:54.711Z
---

# lib-notb-jupyter-community-collab

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-jupyterhub
- ## 

- ## [Need info on jupyterhub pod working with replicas set to 2 · Issue · jupyterhub/zero-to-jupyterhub-k8s](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/1536)
- these are guesses of the issue:
  - JupyterHub assume no one else is updating the state of the database, so if another hub pod would do that there could be faulty logic and potentially inconsistencies could arise.
  - JupyterHub may have state in memory, and if another hub instance would get the next request, it wouldnt be in memory.
- Hmm i have not digged down into this, but it is a matter of the jupyterhub/jupyterhub repo to support multiple instances running side by side

- ## [Document the chart's non-HA status · Issue · jupyterhub/zero-to-jupyterhub-k8s](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/1951)
- About HA for JupyterHub itself
- About HA for autohttps
  - We run traefik, which support HA, but, not for automatic TLS cert acquisition. They support that in their enterprise version, but we can't use that.
- About HA for the proxy pod
  - The proxy pod runs jupyterhub/configurablehttpproxy (CHP) - a NodeJS server, which is configured dynamically by JupyterHub's proxy_class in Python of the same name. The problem is that JupyterHub sends one REST API request configuring one CHP server chosen at random behind the k8s Service exposing it, not all. So, if we have multiple replicas, JupyterHub configuring CHP will only configure one with how to route traffic.
  - #1673 is open to support using KubeIngressProxy - a standalone Python class that defined in the jupyterhub/kubespawner project. It creates k8s Ingress resources that describe how to route traffic to pods, which in turn an external ingress controller could use to know how to route traffic. That way the limitation of the CHP based setup is resolved

- ## [[WIP] use traefik for the proxy by minrk · Pull Request #1162 · jupyterhub/zero-to-jupyterhub-k8s _201902](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/pull/1162)
- I still think we should try to get traefik going, but it's so weird and frustrating that the two biggest selling points for us - native ACME support and multiple replicas, seem to be mutually exclusive!

- ## [Why CHP replicas is 1 and non configurable? · jupyterhub/zero-to-jupyterhub-k8s _202104](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/2155)
- CHP is being remotely configured by JupyterHub, unless we have a system for JupyterHub to configure multiple replicas through the REST API requests, we can't support multiple CHP replicas.
  - If this should be supported, I think we would need a new class to represent multiple replicas of CHP and to ensure that we can communicate with specific replicas and not just any replica chosen at random by communicating with the k8s Service exposing any one replica running.
  - There are several discussions about this

- ## [Document websocket connectivity configuration for nginx ingress · jupyterhub/zero-to-jupyterhub-k8s](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/2786)
- I absolutely agree that the chart should be updated to include theses annotation for thoses using a ClusterIP service instead of loadbalancer.

- ## [JupyterHub 1.0 | Hacker News _201905](https://news.ycombinator.com/item?id=19826169)
- How would JupyterHub compare with something like AWS SageMaker or EMR notebooks?
  - First of all, AWS SageMaker is really a ML system that happens to include Jupyter notebooks as a component. But if you are talking about just the Jupyter notebook part, then I would say - you could use JupyterHub to build your own implementation of SageMaker (you would want to use kubespawner and some deployment of kubernetes if you wanted to scale to multiple nodes). 
  - JupyterHub is more flexible - for example, you could deploy JupyterHub to one beefy server and have Jupyter deployed for many users, which could all read data from a shared filesystem. that kind of thing is not easy to do with SageMaker since everything runs on a separate ec2 instance.

- 
- 

# discuss
- ## 

- ## 

- ## 

- ## 
