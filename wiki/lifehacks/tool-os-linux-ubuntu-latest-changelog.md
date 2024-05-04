---
title: tool-os-linux-ubuntu-latest-changelog
tags: [changelog, linux, ubuntu]
created: 2024-05-04T08:42:02.666Z
modified: 2024-05-04T08:42:22.821Z
---

# tool-os-linux-ubuntu-latest-changelog

# guide

# roadmap

# changelog

## 24.04

- ### [Canonical releases Ubuntu 24.04 LTS Noble Numbat | Ubuntu _20240425](https://ubuntu.com/blog/canonical-releases-ubuntu-24-04-noble-numbat)
- 24.04 LTS delivers the latest Linux 6.8 kernel with improved syscall performance, nested KVM support on ppc64el, and access to the newly landed bcachefs filesystem.
- 24.04 LTS also enables frame pointers by default on all 64-bit architectures so that performance engineers have ready access to accurate and complete flame graphs as they profile their systems for troubleshooting and optimisation.
- 24.04 LTS includes Python 3.12, Ruby 3.2, PHP 8.3 and Go 1.22 with additional focus dedicated to the developer experience for . NET, Java and Rust.
  - . NET 8 will be fully supported on Ubuntu 24.04 LTS and 22.04 LTS for the entire lifecycle of both releases
- For the first time in an LTS, Ubuntu Desktop now uses the same installer technology as Ubuntu Server. 

- ### [Ubuntu Desktop 24.04 LTS: Noble Numbat deep dive | Ubuntu _20240425](https://ubuntu.com/blog/ubuntu-desktop-24-04-noble-numbat-deep-dive)
- New core apps
- The new App Center (also flutter-based) is another notable highlight, bringing a modern, more performant new look to app discovery 
  - While the App Center defaults to a snap-centric view by default to enable us to deliver these usability features, you can still use it to find and install deb packages via the search toggles.
- GNOME v46
  - 24.04 LTS continues our commitment to shipping the latest and greatest GNOME with version 46
- Consistent networking across desktop and server with Netplan 1.0
  - In Ubuntu 23.10 we included Netplan as the default tool to configure networking on desktop, unifying the stack across server and cloud where Netplan has been the default since 2016. 
  - It is important to note that Netplan does not replace NetworkManager and will not impact workflows that prefer the previous configuration methods. 
  - NetworkManager has bidirectional integration with Netplan, meaning changes made in either configuration are updated and reflected in both.
- Comprehensive GPO support with Active Directory
# more
