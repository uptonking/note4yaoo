---
title: tool-os-linux-ubuntu-issues
tags: [issues, ubuntu]
created: 2022-08-30T22:46:40.640Z
modified: 2022-08-30T22:47:08.515Z
---

# tool-os-linux-ubuntu-issues

# guide

# issues

## 

## 

## 

## [The following packages have been kept back](https://askubuntu.com/questions/1399734)

- 方法是通过第三方包管理器强制安装

```shell
sudo apt install -y aptitude 
sudo aptitude safe-upgrade
```

# common

## [What's difference of apt-get and aptitude?](https://askubuntu.com/questions/347898)

- apt-get and aptitude are both front ends to dpkg
  - Use one or the other but be consistent. 
  - aptitude is newer and is suppose to be easier to use. It also unifies some of the apt-* functions. 

- aptitude is more user-friendly because it adds a layer of abstraction away from apt-get, apt-cache etc..; 
- apt-get is more user-friendly than dpkg for the same reason.
- aptitude and apt-get use the same repositories. 
  - Let it be clear that aptitude does not itself run apt-get apt-cache etc..
