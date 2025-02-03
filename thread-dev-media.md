---
title: thread-dev-media
tags: [image, media, thread, video]
created: 2023-04-12T08:40:29.327Z
modified: 2023-04-12T08:40:44.109Z
---

# thread-dev-media

# guide

# plex/stremio
- comparison
  - [Compare Media Servers · Protektor-Desura/Archon Wiki](https://github.com/Protektor-Desura/Archon/wiki/Compare-Media-Servers)
  - [Universal Media Server | Comparison of Media Servers](https://www.universalmediaserver.com/comparison/)
  - [Top 13 Awesome Video Players for Linux [2023]](https://itsfoss.com/video-players-linux/)

- [Is plex or stremio better to use : RealDebrid_202307](https://www.reddit.com/r/RealDebrid/comments/14s6phb/is_plex_or_stremio_better_to_use/)
  - Most modern smart TVs have access to plex (some preloaded)
# discuss-image
- ## 

- ## 

- ## 

- ## Fully client-side OCR and Content Search + Autocomplete for Mirador 3.
- https://twitter.com/jbaiter_/status/1686452012009799690
  - Shoutout to the WASM builds of #SQLite (https://github.com/sql-js/sql.js) and #Tesseract (https://github.com/naptha/tesseract.js) that make this possible *and* quite performant.

# discuss
- ## 

- ## [我们一群独立开发者，甚至还有大厂兼职人员，大家在卷infuse，突然出来一个网易，这领域有这么大市场吗？](https://twitter.com/okasupportgroup/status/1786774180291371430)
  - 惊呆了，今天，完全看不懂，这领域一年收入能养活两个大厂员工吗？
- 网易还有个 1KPlayer，感觉现在这个是一个分支
  - 刚去看了1kplayer，似乎是刚收进网易的，不知道网易爸爸还能不能收了vidhub，求收购。
- 先用着infuse，毕竟现在这个还是最强大的！而且我是apple tv

- 这玩哟居然只在果区上架，还只有iOS端可用
  - 官网有安卓
  - 最重要的tvOS居然没有上

- 腾讯已经彻底下架了qq影音
  - 所以我对大厂搞这种项目不抱希望。迟早项目组完蛋就下架了。
- 这些大厂就是先占领，做不做得好那又是一回事
  - 战略意义
- 谁做的好用谁的，这样竞争，才有好产品
- 大厂不都这样，小众产品打磨的差不多他们都省的调研直接开发竞争，要钱有钱要资源有资源先把坑占了反正耗得起
  - 然后如果收益不高可能就直接就扔了
- 大厂的操行就是一个只要不快速盈利，过不了多久就直接取消项目了

- 特意体验了一下，暂时只能导入阿里云盘和百度网盘的资源

- 对于既有Apple TV又有Android TV的用户，强烈建议有双平台的产品。网易filmly目前貌似不支持NAS..

- ## [视频制作软件 Wondershare Filmora | Kdenlive | Capcut 选择 - V2EX_202310](https://fast.v2ex.com/t/986902)
- [DaVinci Resolve vs. Filmora vs. Kdenlive vs. Lightworks Comparison](https://sourceforge.net/software/compare/DaVinci-Resolve-vs-Filmora-vs-Kdenlive-vs-Lightworks/)
  - 原来已经有人做了大概对比，看起来选择达芬奇和 kdenlive 应该更好点，不知道这 2 个软件内置的一些特效是否丰富。

- DaVinci Resolve 18 基础版永久免费，这格局 比 Adobe 高了不知道多少量级，Adobe 是完全不考虑用户的使用频率问题，通通收费；
  - 而且达芬奇收费的也只是 Studio 版，因为那是给工作室、专业团队、接商业订单的用户使用的，普通人多数用不到那些 studio 版本的额外功能，唯一问题是 达芬奇偶尔会出现 剪辑轨道里的视频文件不出声，这个问题由来已久

- 短视频，就用剪映。
- AE 是行业标准，起家早，但贵，而且按年续费；
- Final Cut Pro：苹果出的，功能与 AE 相当，主打“一次购买，终身使用”，也有很多专业人士使用。
- DaVinci：从视频调色起家，调色是它的长项且不能替代。近几年才加入的视频编辑功能。

- Filmore | Kdenlive 国外比较流行， 其中 Kenlive 免费并且支持 2 路 video 和 2 路 audio 同时处理，感觉一般应用都足够了，我一直挺喜欢这个的。

- ## There are several ways to upload files, like
- https://twitter.com/ReactAdmin/status/1737770310496075923
  - Sending files as Base64 string
  - Using multipart/form-data
  - Sending files to a third party service e.g. CDN, etc.
- [React-admin - Data Fetching](https://marmelab.com/react-admin/DataProviders.html#handling-file-uploads)
  - The Handling File Uploads section of our doc has example code for all 3.

- ## It's such a shame that WebRTC didn't get wider adoption in fields other than audio/video conferencing.
- https://twitter.com/Horusiath/status/1712091176487293222
  - But tbh. it's its own fault - it's overcomplicated on many fronts and basically designed to drive you into a corner and repent at some point.

- ## [纯JS实现多个音频的拼接或者合并 « 张鑫旭](https://www.zhangxinxu.com/wordpress/2023/10/js-audio-audiobuffer-concat-merge/)

- ## I got a 100MB mp4 file in an S3 bucket. What‘s the easiest way to turn it into a stream? 
- https://twitter.com/_mql/status/1645711914482421760
  - (Maybe a CDN sort of thing that sits in front of the mp4 file?)
- Video stream ngx_http_mp4_module | Nginx
