---
title: thread-domain-file-drive-disk
tags: [cloud-drive, file-manager, thread]
created: 2024-08-03T20:00:08.670Z
modified: 2024-08-03T20:00:33.414Z
---

# thread-domain-file-drive-disk

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-pm
- ## 

- ## 

- ## [File storage server alternative to Nextcloud : r/selfhosted _202403](https://www.reddit.com/r/selfhosted/comments/1bpqfkk/file_storage_server_alternative_to_nextcloud/)
- I ended up with Tailscale to VPN back to my home, Samba to expose my storage on my network and Restic as my backup solution. The Finder app on MAC and Files app on iPhone are decent UI. This may not be fancy enough but get the job done for me.

# discuss-dropbox/google-drive/onedrive-like
- ## 

- ## 

- ## 

- ## 

- ## [Nextcloud Alternative : r/selfhosted _202412](https://www.reddit.com/r/selfhosted/comments/1hdixdv/nextcloud_alternative/)
- Spun up Seafile, and using webdav for Obsidian.me

- Why are you guys moving off of nextcloud? 
  - It gets updated frequently but nothing ever changes, its slow and cumbersome

- ownCloud Infinite Scale (OCIS) has been great for me. It's a rewrite of the original ownCloud in Go, and is much more lightweight. Been using it for a year now.

- Have you tried Filebrowser? It's kind of barebones, but it's perfect for me.
  - It's cool for the first sight, but it has some down sight s like: exposing your filesystem, a lot of little bugs, no 2FA, and GitHub auto closing issues.
- There is no security layer between web browser of application user and filesystem.
  - You specify which folders and subfolder it can use, as well as which user rights it operates during the docker setup.
- 2FA is up to you to setup. Use Authelia or anything else as your proxy auth and pass the header of choice (username, email, ...). Filebrowser will match its value to the user in filebrowser

- ## 🎯 [It's official: Filebrowser is dead, long live FileBrowser Quantum : r/selfhosted _202506](https://www.reddit.com/r/selfhosted/comments/1l92znc/its_official_filebrowser_is_dead_long_live/)
- Been using Quantum for about a month now & it's so much better than the original. Tried other stuff like SFTPGo & others, but settled on filebrowser quantum. The indexing is insanely helpful for finding stuff. I know it's in beta, but it already feels feature complete.
  - Only feature I can think I'd want is a preview for fonts, but that's literally it.

- You can also disable indexing like this, but search won't work for anything you haven't "seen".

- ## [[Request]: Lightweight cloud storage solution that isn't nextcloud? : r/selfhosted _202505](https://www.reddit.com/r/selfhosted/comments/1kgti6z/request_lightweight_cloud_storage_solution_that/)
- If you need only basic file storage and sharing, I would recommend OpenCloud (a fork of ownCloud OCIS)
- Why not using OwnCloud directly? What’s the point of forking something that works
  - Because the core maintainer team also moved to opencloud so I would say that this is the new main tree of this product.

- Does opencloud have a good syncing app for desktop?
  - Released literally today

- Take a look at the german fork OpenCloud, that is easy to install and very lightweight
  - German fork sounds funny because Nextcloud is already a german fork of owncloud which itself started as german. 

- Nextcloud is a hog when you add a lot of addons. Disable all addons you don't need, don't enable needless addons, and it becomes lightweight.
  - But if you only need personal storage and access, https://github.com/sigoden/dufs is pretty good. It comes with webdav and a web interface for remote access.

- ## [Please Share/Vote on your favorite self hosted Cloud File Share (Nextcloud, Owncloud, Seafile, etc) : r/selfhosted _202503](https://www.reddit.com/r/selfhosted/comments/1jab3wt/please_sharevote_on_your_favorite_self_hosted/)
- SMB share + FileBrowser
- What I settled on was simply adding tailscale to my devices, mounting `SMB` shares as a network drive on windows/Linux devices, and pointing `filebrowser` running on docker at the same SMB share to let me access the files through a browser on my android/iOS devices. So far it's been rock solid due to how uncomplicated it is.

- OpenCloud - which has been created and forked by the original owner of OwnCloud who has now left OwnCloud 

- I don't like the proprietary file format of seafile.

- I've been messing with Cryptpad lately, and the standard install has a Cryptdrive

- ## [I am done with Nextcloud & Owncloud hello FileBrowser. : r/selfhosted _202312](https://www.reddit.com/r/selfhosted/comments/18ema7z/i_am_done_with_nextcloud_owncloud_hello/)
- Filebrowser is great. I'm sure Nextcloud is right for some people, but to me it always felt incredibly slow and bloated. My only gripe with Filebrowser is the mobile interface. 

- it's a file browser so you can share the same folder to Windows or MacOS with SMB.

- I love that it doesn't encrypt your files - I just want the ability to throw files onto my home server at any time and in any place.

- Seafile here.
  - The biggest limitation is the non-standard file storage format, that makes backup (e.g. via BorgBackup / Kopia) and interplay with other apps (e.g. PhotoPrism / Paperless / Immich) a real pain.

- Im now switching to it, but only missing feature for me would be user stroage quotas

- ## [Selfhosted alternatives for Dropbox : r/selfhosted _202307](https://www.reddit.com/r/selfhosted/comments/151clya/selfhosted_alternatives_for_dropbox/)
- I've been using Seafile on docker for years, ~75gb in sync across 7 libraries. Only issue I've ever had was a "too many files to sync" error that was fixed with a config line to increase the default and it synced right back up. Still stupid fast compared to NC/OC's sync over WebDAV.

- I'll just give my two cents on filebrowser: 
  - I've been using it for the past few months as a solution to my gf's and I's holiday pictures. 
  - It's incredibly lightweight and simple, however, I find the UI difficult to manage. 
  - Browsing long lists of files, it won't remember where you were and it doesn't keep sort and view preferences per folder. 
  - Uploading multiple files and large files is really buggy over WiFi: as in, they will upload, but the UI won't actually respond so you don't know where you are in your upload progress, then you get back to the folder and your view preferences have reset. It's incredibly frustrating.

- ## [Looking for a self-hosted alternative to OneDrive/Google Drive/Dropbox : r/selfhosted _202408](https://www.reddit.com/r/selfhosted/comments/1ezuu39/looking_for_a_selfhosted_alternative_to/)
- Google drive alternative is Seafile. Install docker instance on home server. Just like Google drive, it has clients for Android, iPhone and PC. All sync & files are available anywhere you go.
  - Another option is Next cloud but it's slow.
  - Third option is OIDC, own cloud based file storage/sync.
  - For photos, look at immich (similar to google photos but self hosted)
- Been using Seafile for so many years. Phone (auto-sync photos), Linux, Windows, Mac. Great piece of self-hosted software

- 🐛 Seafile has (had?) a proprietary file organization, if it breaks you wont able to repair it or export your data, as said in othet comments. Try filebrowser or filerun or nextcloud. I wrote proprietary filesystem, is has a proprietary file organization in a db or something like it. By the way it could be problem I dont want to face.
  - Yeah, this is why I usually recommend OwnCloud or NextCloud. I am not comfortable with an abstracted file system that relies on a database to make sense. If something goes wrong with my OwnCloud install, I can just copy files out of the individual user folders, and recreate it. I can also back it up and get files out of the backup without restoring the entire SeaFile instance.

- Worth noting that "Nextcloud being slow" is solved by used Nextcloud AIO (a setup that uses docker containers). This is my current setup and I've been loving it.
# discuss
- ## 

- ## 

- ## 

- ## 不理解为何一定要套个 https，下载这种东西流量很大，使用 http 可以有效降低服务器负载和碳排放，
- https://x.com/skywind3000/status/1819754568022106389
  - 下载完了通过可信渠道校验下 md5 就完了，比如通过 https 获取更新配置时带上 md5 和对应 http 的下载地址就足够了，根本不怕被截获，为何非要套个娃呢？
- Linux 的软件仓库，一般可以自选 http/https，反正后面会验 hash 以及 pgp 签名。http 或许会被截获以及篡改，进而暴露你在做一个重要的安全更新，然后被阻止接着第一时间被攻击。而 https 则更稳定，且没有暴露更新细节的风险。这里的碳排能省，但人们或许懒得去省
- http可以被改
  - 改了你会校验 md5 的啊，md5 从 https 获取即可
- 安全团队建议甚至强制https是因为很多业务团队压根不会检验数据。。
  - 没毛病，但凡事别教条主义
- https成本已经很低了
  - 不低，有云厂商甚至卖 https 转 http 服务，因为应用提供分的服务器压力大，自己解码 https 撑不住，所以只提供 http 接口，前面套个云厂商的转换加速服务
- 会不会就是考虑https要正确的客户端时间，这会让很多不常开机的电脑，或时间没有自动同步的用户无法更新。比如中国时间同步的服务器可能访问有限制。
- https连缓存都做不了，这种数据最适合缓存了
- 用 HTTP 的意義在於可以被各級輕易的緩存來節省流量
