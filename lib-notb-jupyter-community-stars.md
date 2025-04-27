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
# discuss-server
- ## 

- ## 

- ## 

- ## 

- ## 

- ## [Make jupyterlab_server optional _202109](https://github.com/jupyterlab/jupyterlab/issues/11101)
- JupyterLab currently depends on jupyterlab server. For alternative servers to the JupyterLab frontend, such as jupyverse, this dependency is really not necessary, and makes the installation more problematic.

- 
- 
- 

# discuss-cluster
- ## 

- ## 

- ## [Jupyter hub pod autoscaler (HPA) · Issue · jupyterhub/zero-to-jupyterhub-k8s _201811](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/1019)
- 202010: The original issue was about using a horizontal pod autoscaler, which is about creating more and more pods as they get busier. This is not plausible for any pod in our Helm chart currently though because we cannot support High Availability

- ## [moving state out of BaseHandler · jupyterhub/jupyterhub _202112](https://github.com/jupyterhub/jupyterhub/issues/3699)
- Right now, the architecture of JupyterHub is such that a large fraction of functionality is implemented in BaseHandler. This ties us rather tightly to tornado, but also impacts testing because most of our logic cannot be easily instantiated without making an HTTP request.
  - This is related to the need to move the database connection lifecycle to per-request instead of a global, as we take baby steps towards HA 

- ## [High availability story? · Issue · dask/dask-gateway _201910](https://github.com/dask/dask-gateway/issues/148)
  - I'm curious how the various components (dask-gateway-server, scheduler-proxy & web-proxy) work in a Highly Available configuration? 
- They don't really work in a HA configuration. A lot of the internal design is blatantly copied from JupyterHub, so we inherit JupyterHub's problems as well.
  - When enabled, the gateway server can be killed and restarted without losing any work - the proxies stay up and the gateway server reloads its state from the database. While the gateway server is down all existing clusters still work - users can connect to clusters and view their dashboards. They won't be able to add/remove workers or start/stop clusters until the gateway server is back up.
- If it's like JupyterHub, the HA story is tough because there's quite a bit of in-memory state that's reconstructible from the database, but takes a nontrivial amount of time to do so 
  - The HA design discussed in JupyterHub is to make it more of a stateless server - each request gets a new db connection, makes queries, etc. The challenge here for JupyterHub is the fairly complex 'pending' state locks that prevent certain duplicate / conflicting actions in a way that's easy to reason about with coroutines 
- I'll add that tools like BinderHub deployed on top of the JupyterHub are able to themselves be HA by tolerating the downtime of a Hub restart. 
  - Making API requests as easily retry-able as possible makes it easier for client applications to behave as if JupyterHub is HA by resubmitting requests on failure. 
  - This works for BinderHub because the JupyterHub Hub service doesn't serve any human-facing pages, which would see real downtime during a restart—it only uses the API behind the scenes. 
- So while JupyterHub can't be HA yet, BinderHub can, because:
  - nothing but direct requests to the Hub fail while the Hub is down
  - Hub transactions can be retried if connection is lost
  - proxy can be HA after switch to traefik (or redis store for CHP)
  - the user-facing BinderHub application has no meaningful state

- [Rearchitecture · Issue · dask/dask-gateway _202002](https://github.com/dask/dask-gateway/issues/186)

- ## [Support more than 1 proxy or hub replicas · jupyterhub/zero-to-jupyterhub-k8s _201711](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/254)
- jupyterhub/kubespawner#64 should allow switching to a setup with HA proxies, so proxy pod going down wouldn't cause problems.
  - Unfortunately the hub also stores state in memory, so using psql doesn't let you have HA hubs yet. Right now when the hub process dies, only new logins / spawns are unavailable - users already logged in continue to be able to access. While this isn't good enough super long term, it sortof works ok right now... We have a long running ~3000 user Hub at UC Berkeley that we have continuous deployment for, and it works ok.

- ## [alternate way of setup ha with master-slave mode · jupyterhub/jupyterhub _201808](https://github.com/jupyterhub/jupyterhub/issues/2068)
- JupyterHub cannot run in a hot-swappable 'failover' mode. JupyterHub has in-memory state, so two running JupyterHubs pointed to the same database will diverge in their understanding of what's running. It only reconstructs its state from the database on startup. A new JupyterHub instance can take over from a previous one that died, but only if it starts after the previous one stopped.

- ## [Multiple hub server, Server not running · Issue #3053 · jupyterhub/zero-to-jupyterhub-k8s _202303](https://github.com/jupyterhub/zero-to-jupyterhub-k8s/issues/3053)
  - when I tried to use Multiple hub server, the server is not running , it works well when i use only 1 replicas. how can i add hub service from 1 to 2 or more ?
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

- 202504: It's a big project and requires substantial resources and time. There is not currently available time or funding to develop this
  - HA and scaling were both explicitly out of scope during JupyterHub development, but folks want what they want
  - JupyterHub was designed such that availability of the Hub wouldn't be critical (i.e. everything involved in users running code is not disrupted while the Hub is restarting/migrating, only new user spawns and admin UI are affected). So if you have your own UI for launching servers via the JupyterHub REST API that is fault tolerant (as e.g. BinderHub does), you should be able to get pretty close to an HA deployment. That's part of what makes this a lower priority.
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
