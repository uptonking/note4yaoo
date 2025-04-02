---
title: tool-os-linux-ubuntu-issues
tags: [issues, ubuntu]
created: 2022-08-30T22:46:40.640Z
modified: 2022-08-30T22:47:08.515Z
---

# tool-os-linux-ubuntu-issues

# guide

# not-yet
- [fractional scaling blurry](https://www.reddit.com/r/gnome/search/?q=fractional%20scaling%20blurry&restrict_sr=1&sort=new)

## 

## 

## [Temp of nvme-pci-0300 too high? : r/homelab _202202](https://www.reddit.com/r/homelab/comments/svgbhn/temp_of_nvmepci0300_too_high/)

- I wouldn't be concerned with these temperatures. Generally speaking SSD temperature is only something to worry about when the temperature of the controller gets so high that it starts thermal throttling and reduces the performance. It depends on the exact SSD, but that generally starts in the high 80 degree C range, and when it does kick in it doesn't do any damage to the SSD; it just causes the controller to reduce the power draw (and therefore performance) until it gets back below the throttling point.
- There's also another issue to consider, which is that the NAND on SSDs actually works best when it's relatively warm/hot (as long as it's within spec, of course). That's part of the reason why many high performance modern SSDs come with a thermal label on them, rather than a thermal pad and heatsink. The thermal label spreads heat from the controller to the NAND packages, which helps with both of the above problems (i.e. it keeps the controller below the throttling point and it keeps the NAND warmer, where it works best).

## [What is the state of fractional scaling on GNOME? : gnome](https://www.reddit.com/r/gnome/comments/11ekj8o/what_is_the_state_of_fractional_scaling_on_gnome/)

- Tl:dr No, and it won't for a very long time (many years from now), because GTK4 doesn't support it.
- KDE has the best fractional scaling. It is currently better on the Xorg version but 5.27 officially supports wayland frac scaling protocol and once everything is built on qt6 (later this year) the wayland session should be good if not better than windows.
- For now I would try a live usb with a distro that has kde 5.27 and check out fractional scaling under both xorg and wayland and see if it works well for you

- KDE Plasma is shipping fractional scaling as an officially supported Wayland feature, and the implementation is more advanced that Gnome's, at least in the testing I have done.

- Note: GTK does not and has no plans to support DPI scaling on all elements except fonts. Therefore, fractional scaling on gnome uses oversampling, which means rendering at a higher resolution, then scaling down with integer scaling, and is true for both wayland and xorg sessions. This brings higher GPU and CPU (since GTK is not fully hardware accelerated) usage, more power consumption, and in some cases significantly slower responsiveness, particularly noticeable in xorg. If it's necessary to avoid these problems, consider switching to a Qt based desktop environment.
- 

## [Will gnome 45 include any improvements to fractional scaling on wayland? : gnome](https://www.reddit.com/r/gnome/comments/16bb2zt/will_gnome_45_include_any_improvements_to/)

- TL; DR GNOME 45 has no actual improvements for fractional scaling.
  - You've kinda answered your own question. 
  - GTK 4 does not support fractional scaling and never will because trying to implement it would break things, therefore necessitating its implementation to be done in GTK 5- so GNOME 45 won't improve fractional scaling in any meaningful way. 
  - Now, you may have heard that Mutter got support for the `fractional_scale_v1` protocol, but that can't do anything when apps don't support it.

- Until wine supports wayland + fractional_scale_v1 (protocol), these issues will remain, sadly. I have to play at 1536x864 because of 125% scaling on a 1080p laptop ha.
# issues

## 

## [python - ModuleNotFoundError: No module named 'distutils.util' - Ask Ubuntu](https://askubuntu.com/questions/1239829/modulenotfounderror-no-module-named-distutils-util)

- `distutils` package is removed in Python version 3.12
  - It was deprecated in Python 3.10 by PEP 632 “Deprecate distutils module”. 
  - For projects still using `distutils` and cannot be updated to something else, the `setuptools` project can be installed: it still provides distutils.
  - if it doesn't work, you may need stay on Python < 3.12 until the package is supported.

## [Touchpad stopped working 20.04 - Ask Ubuntu](https://askubuntu.com/questions/1235067/touchpad-stopped-working-20-04)

- Well, all I did was to get to the “settings” and enabled the touchpad which surprisingly was disabled. 
  - This touchpad issue happened on my ASUS N550JK and I think after I did “dist-upgrade” and my Linux distribution was upgraded.

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
# kde
- ## 

- ## 

- ## [Three-finger gesture for equivalent of alt-tabbing : kde](https://www.reddit.com/r/kde/comments/10kvw6f/threefinger_gesture_for_equivalent_of_alttabbing/)
- There isn't something like this that currently exists, and three-finger swipes in KDE (only on Wayland) are set to switching workspaces (you cannot change this unfortunately). However, if you use https://github.com/JoseExposito/touchegg with the https://github.com/JoseExposito/touche GUI, you can customise a gesture to press Alt-Tab.
- It's worth noting that **Touchegg does not support Wayland**, but I'm sure there are alternatives that do.

- ## [Overview 3 finger gesture : kde](https://www.reddit.com/r/kde/comments/yep337/overview_3_finger_gesture/)
- Unfortunately it is not possible to use 3 finger gestures to use Overview. The devs said they will bring it to 5.26 but they could not. They focused on stability on this release I guess. My laptop does not support 4 finger gestures either. 5.27 will be the last plasma 5 version and it will be an LTS release, so I hope they will add an option to customise gestures when it releases.

- Just install touchegg and Touché (GUI for touchegg) and you'll be fine.
