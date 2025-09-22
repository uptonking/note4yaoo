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

- ## 

- ## 
# discuss-internals
- ## 

- ## 

- ## 

- ## [wrong user.oc.name xattr in file uploaded to POSIX FS _202506](https://github.com/opencloud-eu/opencloud/issues/1100)
  - I have files on the system that have a wrong user.oc.name attribute and they are not listed in the webUI

- editing existing files is supported, yes. The problem with syncthing seems to be that, when adding files from a remote location, it opens the file with temporary file name, writes the bytes, closes the file and then immediately renames it to the final name. That final rename sometimes isn't handled properly in your case.
  - There either seems to be a race condition in the code which leads to the `rename` event getting lost or the `MOVED_FROM` `inotify` event isn't emitted. Unfortunately I wasn't able to reproduce the issue on my machine, even after sycing tens of thousands of files.
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

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
