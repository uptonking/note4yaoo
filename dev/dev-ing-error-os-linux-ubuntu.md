---
title: dev-ing-error-os-linux-ubuntu
tags: [error, linux, ubuntu]
created: 2022-09-17T09:20:04.911Z
modified: 2022-09-17T09:20:30.236Z
---

# dev-ing-error-os-linux-ubuntu

# guide

# errors
- ## 

- ## 

- ## 

- ## [AppImage: Settings schema 'org.gnome.settings-daemon.plugins.xsettings' does not contain a key named 'antialiasing' · Issue #12776 · Ultimaker/Cura](https://github.com/Ultimaker/Cura/issues/12776)
- FYI: In fedora 36 (wayland, gnome) i also had to set GDK_BACKEND to be able to launch it (i did not edit /etc/gdm/custom.conf)
  - GDK_BACKEND=x11 LD_PRELOAD=/usr/lib64/libstdc++.so.6 ./Ultimaker-Cura-5.1.0-linux. AppImage

- ## Your native host connector do not support following APIs: v6
- https://askubuntu.com/questions/1418937
- This is a known issue. Despite the message, installation of extensions will still work on Ubuntu that currently has Gnome Shell 42.2 , but the website is broken on e.g. Arch systems with Gnome Shell versions containing three components, e.g., 42.3.1.
- So on Ubuntu, ignore the message for now. 
