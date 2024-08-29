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
