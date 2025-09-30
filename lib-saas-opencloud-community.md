---
title: lib-saas-opencloud-community
tags: [cloud-drive, community, opencloud]
created: 2025-09-22T12:33:03.218Z
modified: 2025-09-22T12:33:21.753Z
---

# lib-saas-opencloud-community

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-roadmap
- ## 

- ## 

- ## [nats as service registry is redundant · Issue · opencloud-eu/opencloud _202508](https://github.com/opencloud-eu/opencloud/issues/1409)
  - When we started the codebase we adhered to how go micro encapsulated a service registry because we thougth we would need that. 
  - As it turns out, we don't. We can rely on dns to be our service registry
  - We should remove any service registry related code and stick to urls. the grpc client can then handle `unix:// dns:// or kubernetes://` prefixes. for kubernetes we alredy integrate with the kubernetes control plane to pick up new pods when scaling up.
  - We can already prevent nats from being used by using dns:// urls in the endpoints. I tested this and there are a few points where service names have been hardcoded: requests to the settings service and search IIRC. They will need to be made configurable, but IMO it is already a bug that they cannot be configured.
- Using dns as our service registry would significantly reduce the complexity:
  - we can delete the nats-js-kv registry obsolete
  - reva services don't have to manually be registered
  - requests can be made without implementin our own service lookup code with go micro selectors etc
  - drop dozens of env vars
  - less dependency on go micro

# discuss-internals
- ## 

- ## 

- ## 

- ## [wrong user.oc.name xattr in file uploaded to POSIX FS _202506](https://github.com/opencloud-eu/opencloud/issues/1100)
  - I have files on the system that have a wrong user.oc.name attribute and they are not listed in the webUI

- editing existing files is supported, yes. The problem with syncthing seems to be that, when adding files from a remote location, it opens the file with temporary file name, writes the bytes, closes the file and then immediately renames it to the final name. That final rename sometimes isn't handled properly in your case.
  - There either seems to be a race condition in the code which leads to the `rename` event getting lost or the `MOVED_FROM` `inotify` event isn't emitted. Unfortunately I wasn't able to reproduce the issue on my machine, even after sycing tens of thousands of files.
# discuss-auth/permission
- ## 

- ## 

- ## 

- ## 

- ## [Is the Shared User Directory Mode diagram actually correct? · opencloud-eu _202508](https://github.com/orgs/opencloud-eu/discussions/1364)
  - In Shared User Directory Mode, the OpenCloud server gets group memberships from the OIDC token according to the corresponding diagram. 
  - Can anyone confirm whether this is actually correct?
  - In my understanding, the OIDC token does no contain information about group membership.

- Thanks for the hint. That part of the diagram is actually slightly wrong. The "Reads Roles and Group memberships from claims" should actually just be "Reads Roles from claims"

- ## [Issues with Keycloak and User Provisioning in OpenCloud Deployment · opencloud-eu _202506](https://github.com/orgs/opencloud-eu/discussions/1078)
- The combination of external keycloak and internal ldap is not documented / tested and not recommended.
  - Our compose example shows both components as external services.

- If we try with an external LDAP, I assume an "external" LDAP means a standalone LDAP service that is not managed or bundled by OpenCloud. So this could be, a separate OpenLDAP server (or an enterprise LDAP service like Active Directory) that we deploy and manage ourselves (outside the opencloud compose stack). Is that correct?
  - Yes. OpenCloud brings a "built-in" LDAP server which is suitable for small and home lab installations.
  - To get an "enterprise" system, you should replace it with OpenLDAP or something similar.

- [I'm using OIDC with Keycloak. OpenCloud receives the token successfully, but it fails with could not get user by could not get user by claim email with value email@email.com machine error. How can I register or auto-provision users? · opencloud-eu _202507](https://github.com/orgs/opencloud-eu/discussions/1261)

- [In the Keycloak deployment example,  `PROXY_USER_OIDC_CLAIM`  should be `sub` _202504](https://github.com/opencloud-eu/opencloud/issues/682)
  - That really depends on your requirements. 
  - the autoprovisioning example was indeed switch to sub 

- ## [question: external OIDC with internal LDAP server (idm) possible? _202506](https://github.com/orgs/opencloud-eu/discussions/1118)
- The "built-in IDP" is lico (libregraph/lico) which is an OIDC Server. The built-in LDAP Server is based on libregraph/idm which is a different component (internally we call that component "idm" not "idp".

- It is technically possible. We just do not document such a setup currently as we have to focus a bit on which combination for internal/external IDPs and LDAP servers we actually what to actively support otherwise this gets too much of a maintenance burden.

- we do not want this setup to be considered as an option because we cannot maintain so many different approaches. Although you can do that on your own, it should not be documented.

- ## 💡 [Authentik without openldap · opencloud-eu  _202506](https://github.com/orgs/opencloud-eu/discussions/1093)

- OpenCloud always uses LDAP to store its users. The built-in service is called `idm` and is usable for small deployments. 
  - If you want enterprise grade, you always need to substitute that LDAP with an external service (like OpenLDAP or Active Directory or something similar)

- Turns out the authentik LDAP outpost was sending back the `uid`, not the `entryUUID`. Once I switched to `OC_LDAP_USER_SCHEMA_ID: "uid"` and `OC_LDAP_GROUP_SCHEMA_ID: "uid"`, everything worked and I could log in

- [User Role Mapping Fails on Auto-Provisioning with External IDP Enabled  ](https://github.com/opencloud-eu/opencloud/issues/1282)

- ## [OpenCloud not claiming "groups" from OIDC Token _202506](https://github.com/opencloud-eu/opencloud/issues/1116)
- the requested scopes can be configure with the `WEB_OIDC_SCOPE` env var.

- ## [Getting OpenCloud to work with External SSO/OIDC (Authentik) · opencloud-eu _202505](https://github.com/orgs/opencloud-eu/discussions/835)

- https://github.com/patchmonkey/opencloud-authentik-specific-config /202505
  - My personal configuration for integrating authentik with opencloud 2.3.0 for external OIDC.
  - Understanding that I needed autoprovisioning mode (opencloud needs an ldap dir to store users always, and if you haven't provided that explicitly, you need to configure your docker files to spin up the ldap server AND make sure you have the correct parameters set for autoprovisioning

- the problem with Authentik (and seemingly with other IdPs) is that Authentik's endpoints are tied to a single Client/Client ID, and that additional ClientIDs have different URLs.

- [External OIDC (Authentik) Broken with Upgrade form 2.3.0 to 3.0.0 _202506](https://github.com/orgs/opencloud-eu/discussions/1052)
  - 🐛 no role in claim maps to an OpenCloud role
  - Disregard, this was due to a config bug where the radicale container was not running after the containers were updated to the newest version.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## [confused about the install one-liner · opencloud-eu _202505](https://github.com/orgs/opencloud-eu/discussions/924)
- This script is a very quick way to install opencloud backend, frontend and Identity Provider as a single binary with no needed dependencies.
  - That means you have a very bare feature set without external services like collabora or tika.
  - This script is targeting localhost setups for "take aquick look" usecases.
  - Bare metal is also possible but not supported because it creates too many issues.

- ## there is a 'Bare-metal' section in the Gettings started - but.... there is also a disclaimer saying that this is not supported, so what is the official supported way to install OpenCloud if I don't want to use Docker ? _202509
- https://matrix.to/#/!MXIMfhTMMRFPuXSKJZ:matrix.org/$FoxVobZSB60wmgqbpzjvux_k8nh4nVrnnQGDhsYtJM0?via=chat.opencloud.eu&via=matrix.org&via=tchncs.de
- I just tried the install script: curl -L https://opencloud.eu/install | /bin/bash
  - but that did not help much as it want one to connect to https://localhost:9200, which I cannot do on a clean Ubuntu Server installation and the `https://<ip>:9200` just gives an error saying "missing or invalid config"
- 💡 I just changed the `runopencloud.sh` script to have ip instead of localhost, and that seems to work
  - If it’s on a remote machine, localhost can’t work externally
- but u can use nginx reverse proxy tho to make it work with localhost

- You can manually download the binary and then run “opencloud init” before running opencloud! Here some useful envs
  - OC_INSECURE=true
  - OC_URL=https://${host}:9200
  - IDM_CREATE_DEMO_USERS=true
  - OC_LOG_LEVEL=debug

- You can overwrite the `localhost` default with the following env: `OC_HOST` for the install script

- Everything from our compose example can run in any way you like (kubernetes, compose, bare metal)… but you have to know how to setup and organize your infrastructure. I suggest, stick to the compose version or use it as inspiration for your bare metal setup
  - bare metal and docker uses the same env variables

- opencloud stores metadata as files, not in a heavy database, so accessing them over a modern NAS connection introduces almost no latency compared to local storage
  - the real bottleneck is usually the NAS disk I/O or overall network throughput, not whether the metadata is stored locally

- ## [OpenCloud : r/selfhosted _202507](https://www.reddit.com/r/selfhosted/comments/1ls2a83/opencloud/)
- Technology wise OpenCloud is much much superior. It is based on Go, and thus needs way less memory, is much faster and does not need a database. 
  - Also its frontend, while currently lacking some of the bells and whistles of Nextcloud, is much simpler and not the grown mess of PHP and different Vue.js versions seen in Nextcloud.

- I tested OwnCloud client with OpenCloud server and suprise suprise everything works even more features. It even has Virtual File support! I trully dont know how... Its on the roadmap for OpenCloud yet it works.

- ## [Opionion on OpenCloud? : r/selfhosted _202504](https://www.reddit.com/r/selfhosted/comments/1k1augc/opionion_on_opencloud/)
  - I recently tried out OpenCloud and the experience has been... quite smooth. Easy to setup with docker compose, the webui is minimal and blazingly fast. The keycloak sso integration is pretty neat, too.
  - The major downside is lack of mobile and desktop apps (for now) 

- I'm switching from NextCloud as soon as it ships with contacts/calendar support. I can't justify the added complexity of NextCloud for a single-user instance.

- Opencloud is a fork of owncloud the owncloud app should work.
  - It's a fork of ocis(owncloud infinite scale, which i never got working) written in go, not to be confused with the old php stuff. But yeah that might work
  - just tried it and it seems to retrieve the files properly but then states the server version is too low and not supported

- I have a working ocis instance but im not a fan of the blob storage which opencloud is looking to change.
  - Yeah it uses PosixFS by default which retains the file structure.
- Are there any other major differences you noticed between these two? ocis seems a bit more mature
  - I would say not for what i want/need i will be switching to opencloud when it's had a few updates.

- I wanted to make it work with the full feature set (Collabora, etc.), but I have my own Traefik instance, and the partial example is far too complicated to make it work with an existing Traefik infrastructure.
  - I just replaced the content of `docker-compose.yml` with the content of `opencloud.yml` and adapted the labels for Traefik.
  - Finally, remove `${OPENCLOUD:-}` from the last line in `.env` (the `COMPOSE_FILE` variable). Works like a charm.

- [Docker compose with existing traefik · opencloud-eu · Discussion _202503](https://github.com/orgs/opencloud-eu/discussions/533)

- Does OpenCloud support WebDAV? 
  - Yeah it supports WebDav out of the box, haven't tested it myself though. You probably need to generate an access token from the webui if using oidc for authentication.

- Have you tried Seafile? It works well for me, and it has mobile apps, but it only provides file storage. It doesn't have all the other apps provided by Nextcloud and Opencloud.
  - Seafile doesn't provide file locking in its community edition. That makes it unsuitable for two or more users working on the same file. It's a deal breaker for me
- I also heard that seafile uses proprietary format to store all of user files whereas nextcloud keeps all files in plain accessible format.

- ## [What's the Obsidian of file hosting/cloud storage? : r/selfhosted _202506](https://www.reddit.com/r/selfhosted/comments/1ljnsf9/whats_the_obsidian_of_file_hostingcloud_storage/)
- NextCloud, OwnCloud both do this. Otherwise any WebDAV server (Caddy, Apache, KaraDAV etc) with WebDAV client of your choice.
  - OpenCloud (recent fork of OCIS the GoLang rewrite of OwnCloud) is making thier Posix backend the default.
  - It's just about perfect in my opinion, the only downside is it's not the easiest to configure, but has been very stable and lightweight in my experience.
- OpenCloud has only been forked for a month or two. Give it time.

- Opencloud stores everything as normal files on the filesystem, and includes Collabora for editing. I recently switched to it from Seafile and am happy with the change, quick and stable with a better UI.

- ## 🚀 [OpenCloud v1.0 has been released to the public (Owncloud OCIS fork) : r/selfhosted _202502](https://www.reddit.com/r/selfhosted/comments/1iy00zc/opencloud_v10_has_been_released_to_the_public/)
- The thing I dislike about Seafile is the custom format. That makes sense for businesses. But for a homelabber it’s frustrating IMO

- The AIO for Nextcloud is the epitome of overly complicated. It has at least 3 different webservers in it, requires Docker socket access, and it's very, *very* temperamental about the setup environment. There's a reason there's so many "I gave up on the AIO and just ran the underlying Nextcloud Docker manually and it's so much better even though I had to do a ton of manual work" posts.

- It seems that a bunch of Owncloud employees have switched to OpenCloud as well.

- I think Nextcloud isn't so much a "File sharing and storage" platform as it is a "Virtual Office"; it has different departments, like data storage, but also the Talk app, the Notes stuff, hell Nextcloud is even an OAuth provider now
  - Yes, thats exactly the point. It started as a file sharing and storage solution, and lost its focus by wanting to be everything at once, without being particulary good in any dimension.

- OpenCloud was developed from the ground up as a cloud-native solution. The architecture uses microservices and is optimized for container technologies such as Docker and Kubernetes. This enables flexible deployment and rapid adaptation to modern IT requirements. Really? It was developed from the ground up? Give credit where credit is due.
  - The CEO of Kiteworks which bought ownCloud a year ago threatened to sue OpenCloud.
