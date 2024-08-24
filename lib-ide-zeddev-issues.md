---
title: lib-ide-zeddev-issues
tags: [issues, zeddev]
created: 2024-08-24T16:13:54.508Z
modified: 2024-08-24T16:14:04.119Z
---

# lib-ide-zeddev-issues

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 🐛 [Allow to pin tab _202301](https://github.com/zed-industries/zed/issues/5046)
  - Wanna have ability to pin tab like vs code it does

# discuss-sync-settings/ext_with_settings
- ## 

- ## 

- ## [Settings Sync: Built-in synchronization support _202302](https://github.com/zed-industries/zed/issues/5010)
- Current problems concerning such features are as follows:
  - VS code's settings.json has only editor-related settings, not package-based ones.
  - Atom's sync-settings gives you direct access to the editor features as packages but it doesn't report problems related to packages' dependencies which are system based.

- ## 🔁 [Settings Sync · zed-industries/zed _202302](https://github.com/zed-industries/zed/discussions/6569)
  - While this is not currently on our roadmap, and it will likely not be added anytime soon

- I liked my settings being stored in a location I had control over. That might be a bit biased since I came from Atom prior and having to sync my settings with a GitHub Gist.
  - Maybe you can refer to sublime_text's sync strategy, it has a third-party package can sync the all settings to a private github gist

- What I'd like to see: 
  - Sync Settings has four commands: backup to remote, restore from remote, create profile, and switch profile. 
  - They all look at a git repository in any code host (github/gitlab/bitbucket, etc)

- I really like the "settings repository" plugin for CLion. I point it to a git repo and it does the rest.
  - I appreciate the simplicity of the VScode sync, but it's also a bit shady(靠不住的; 不正当的) isn't it. (Yes, I'm aware of the JetBrains sync plugin that works similarly to VSCode as well).
  - The reason I prefer settings sync that's sort of built-in vs a third party is two parts, the first part is trust, the second part is support.
    - By trust I mean, I'm perhaps a paying customer of Zed and I can trust that the feature is implemented by the company and I'm trusting a single entity in this situation (I don't have to worry about a rogue update to the extension that starts to siphon off secrets from my computer).
    - By support I mean, since it's a tier 1 product feature and so will support sync'ing all relevant settings, extensions, and themes. I don't have to worry about it getting abandoned (like I worry about most of the Sublime ecosystem).

- I would be happy even to be able to change the location of the settings json file to a shared folder (dropbox or google drive or apple cloud or whatever) to be able to keep the settings in sync between my two machines.

- is there any reason why settings sync couldn't happen via source control, like other dotfiles?
  - It's not perfect, as it doesn't sync removal, but the auto_install_extensions setting helps with this.
- I sync my dotfiles, no need for settings sync.

- Can we at least get anything that is not a static configuration removed from ~/.config/zed? It would make syncing the folder much easier.

- 
- 
- 

- ### [Built-in settings/keymaps sync feature _202207](https://github.com/zed-industries/zed/issues/5566)
  - It already has a backing server powering the collaboration feature, and so the stitching to GitHub also already done.
  - So for sure first class settings sync, would be sick!
  - I use 2 machines, work and personal laptop, would be sick to have the setting synced, and possibly also a "workspace" specific settings too? 
# discuss
- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## [run zed error on Ubuntu 24.04 : blade_graphics::hal::init Surface formats are incompatible _202405](https://github.com/zed-industries/zed/issues/11716)
- Update: this error is on WayLand Mode, switch to X11 , zed works!
- I can run zed in x11 mode in wayland using `WAYLAND_DISPLAY='' zed` ; 
  - zed在ubuntu本地的安装地址在 `/home/yaoo/.local/zed.app/bin/zed`

- [[linux] Vulkan ERROR_INITIALIZATION_FAILED _202402](https://github.com/zed-industries/zed/issues/8168)
