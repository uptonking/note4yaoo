---
title: lib-notb-jupyter-community-stars
tags: [community, jupyter, notebook]
created: 2024-06-30T03:28:01.973Z
modified: 2024-06-30T03:28:19.638Z
---

# lib-notb-jupyter-community-stars

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-cluster
- ## 

- ## 

- ## 

- ## [Multiple hub server,Server not running · Issue #3053 · jupyterhub/zero-to-jupyterhub-k8s _202303](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/3053)
  - when I tried to use Multiple hub server, the server is not running ,it works well when i use only 1 replicas. how can i add hub service from 1 to 2 or more ?
- This isn't currently supported

- ## [JupyterHub Multi-Node setup - JupyterHub - Jupyter Community Forum _202107](https://discourse.jupyter.org/t/jupyterhub-multi-node-setup/10120)
  - Just wanted to check if it is possible to have multi-node setup where end user will have single entry point and notebooks will be served on one of the hub nodes based on the request.

- There’s a Helm chart for running JupyterHub on Kubernetes
  - There are other options though, for instance if you have a high performance cluster (HPC) have a look at GitHub - jupyterhub/batchspawner

- Kubernetes is the best way to run JupyterHub across multiple nodes.
  - If that’s not suitable you can search for other JupyterHub spawners which support remote launches, for example

- ## [Jupyterhub multi instance/node - JupyterHub - Jupyter Community Forum _202111](https://discourse.jupyter.org/t/jupyterhub-multi-instance-node/11831/1)
  - for multi instance/node i mean just HUB component, each user’s singleuser-server running on worker node of cluster hadoop through Yarn Spawner.
  - Reading the documentation it seems that jupyterhub can only be installed on one node/VM, for example HUB component can it be handled on 2 vm?

- That’s right, a given JupyterHub deployment can have only one Hub instance

- The biggest task is changing the lifecycle of our ORM objects to no longer be persistent for the process, instead always creating a new session for each request. We have to lose lots of performance optimizations to do this, so it’s tricky long-term work.

- ## [Support HA (High Availability) · jupyterhub/jupyterhub _201805](https://github.com/jupyterhub/jupyterhub/issues/1932)
- There are two main obstacles to HA:
  - The proxy is a single-point-of failure. EDIT 2020: Using jupyterhub-traefik-proxy eliminates the proxy as SPOF. Only Hub state remains.
  - The Hub itself is a single-point-of-failure and must own the database it talks to. Other Hub instances may not be running and talking to the same database, or there will be errors and inconsistent state. So you cannot easily have two Hub replicas and failover between them.
- The way services have achieved this today is to run multiple wholly independent JupyterHub instances (including a proxy for each), and maintaining sessions such that users are always routed to the same Hub (so that the Hub databases are independent), and failing over to new Hubs when the Hub a user is associated with has gone.
- If, however, your interpretation of HA allows brief downtime when a node disappears, using a technology like Kubernetes allows the Hub (and other processes) to automatically be relocated to a new node when the previous node goes away. This isn't HA per se in that there is nonzero downtime, but the downtime is on the scale of the time it takes for the node loss to be noticed and for the new Hub pod to start (typically < 1-2 minutes), and no human intervention is required.

- The end-goal is that a given user, once assigned to a Hub, is always routed to that Hub. Typically, this is accomplished by setting an affinity cookie that is checked in the edge proxy (not the hub's proxy, but a layer before that) before routing. 

- What would be involved in making the Hub DB shared so that we could have many hub instances running at once?
  - it isnt enough :/ if the state of the db change by another hub instance, and one hub instance isnt aware, it acts with the wrong assumptions still. Whats needed is to remove all assumptions throughout in jupyterhub.

- 202210: Thanks for your sketch! I think I've outlined everything above that needs to be solved in the Hub to allow more than one Hub pod to talk to the same database without conflict. The proxy part is already fully solved if you use traefik (long-since the default in littlest jupyterhub, hit some snags that stopped a migration in z2jh). CHP can also be fully HA if you use CHP's redis backend.

- 
- 
- 

# discuss-extensions
- ## 

- ## [JupyterHub as a frontend for multiple apps/services · Issue  jupyterhub/jupyterhub](https://github.com/jupyterhub/jupyterhub/issues/1880)
- 
- 
- 

- ## [JupyterHub Extension Mechanism · Issue · jupyterhub/jupyterhub](https://github.com/jupyterhub/jupyterhub/issues/3416)

# discuss
- ## 

- ## 

- ## 

- ## 
