---
title: devops-docker-community-vm
tags: [docker, virtual-machine, vm]
created: 2025-11-06T09:09:18.057Z
modified: 2025-11-06T09:09:36.570Z
---

# devops-docker-community-vm

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-Proxmox
- ## 

- ## 

- ## 

- ## 

- ## [Proxmox vs OpenStack : r/virtualization _202412](https://www.reddit.com/r/virtualization/comments/1hbusou/proxmox_vs_openstack/)
- Openstack is better used for Cloud environments. Proxmox is more suitable for virtualization.
  - You can even install Proxmox to create Openstack VM for learning purposes, and then if you decide, install Openstack baremetal. I did basically this, but i use KVM instead of Proxmox to virtualize the Openstack servers.

- If you want to run some vm's and containers use proxmox.
  - If you wsnt to mimic an aws region or 2 with multiple separate tenants that admin their own stuff: use openstack.

- Aren’t you just looking for a hypervisor? Both proxmox and openstack are orchestrators (of different scales) which just use KVM for the actual virtualization.
  - Correct, which is why I'm using QEMU with KVM right now. Under the hood KVM is all I really need, but of course there are many ways to get there.

- [Proxmox vs OpenStack : r/Proxmox _202102](https://www.reddit.com/r/Proxmox/comments/lca6cv/proxmox_vs_openstack/)
- Openstack is more of a cloud resource orchestration platform. It contains some VM and container elements, but focuses not so much on the minutia of running virtualized services, but also on storage, auth, api, resource scaling etc.
  - If you are serious about creating cloud-based services, open stack is a better choice. 
  - Proxmox is a virtualization back end that can handle some storage management, but orchestration and scaling are beyond its scope of offering.

- OpenStack is not just complex. It's complex. Maintenance takes a lot of time even if you go with defaults. If you don't, it requires pretty much a team effort to keep it up at a level where a proper business can depend on it.
- Openstack is near parity in services compared to public cloud providers like AWS. This means you can design cloud n Native applications and orchestrate across numerous services to deploy like you would in AWS. Like the cloud, it is designed for multi-tenancy and can leverage private, and public provider networks. 

- Bear in mind proxmox can use lxc lxd containers out of box and you can do provisioning by command line. So you can write automation for provisioning and configuration by ansible/chef or just bash

- ## [Debian + docker feels way better than Proxmox for self hosting : r/selfhosted _202511](https://www.reddit.com/r/selfhosted/comments/1opjeb8/debian_docker_feels_way_better_than_proxmox_for/)
  - My initial impressions was that Proxmox is obviously a super power OS for virtualization and I can definitely see its value for enterprises who have on prem infrastructure.
  - However for a home server use case it feels like peak over engineering unless you really need VMs. But otherwise a minimal Debian + docker setup IMO is the most optimal starting point.

- Except Proxmox has very little overhead and does things Docker can’t like system snapshots, live migration, ZFS integration, proper isolation, LXC, etc etc. What do you think is “hype”?

- Jokes on you I run Debian + docker for my services inside of a VM on proxmox.
- Sames - feels easier to backup, and having web access is nice. I also run most services behind traefik, but wanted to have some LXCs and VMs that are not in thay environment, and full separation is better imo.
  - It’s so much easier to backup this way. I recently moved my whole Proxmox setup from one machine to another. Absolutely seamless.
- Jokes on you, i run my dockers in proxmox unprivileged lxc, with intel gpu acceleration...(and can share igpu with another lxc)
  - Any "a-ha" moment or trick? I was never able to run docker properly in an unpriviledged LXC container, always some issues I got too tired to solve.

- I only have two VMs on my proxmox instance one for Debian/Docker and one for Roon. I get why someone may think running Debian bare metal is easier but the flexibility of running them inside containers on proxmox is so so nice. And it lets me spin up a new one whenever I want to fart around with something new before I decide if it becomes a full part of the system.

- Depends on what your goals are. If you want the simplest system possible, sure. Or if the hardware is right on the edge of what is needed to run the workload.
  - But in most other cases I'd value the flexibility that a hypervisor provides more.
  - For example: I run most of my services in docker inside a VM. This VM gets assigned most of the resources. But for some software there may be benefits for running them inside specialized images. Home assistant comes to mind. I'm also in the process of migrating services from the aforementioned docker VM a new one running k3s. With a hypervisor is easy to have both running at the same time and I don't have to migrate everything at once.
  - Also snapshots and easy backups.

- Same for me: Debian + KVM + Docker runs great

- Proxmox 9 is Debian 13 Trixie at the core. I see what you mean though without all the extra overhead.
- Technically proxmox is also Debian + containers, so I agree 

- Why not both, spin a Debian/Docker VM on Proxmox, that way you get backup and restore when shit hits the fan, and can spin up additional VMs on demand
# discuss
- ## 

- ## 

- ## 
