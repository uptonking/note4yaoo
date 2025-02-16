---
title: lib-ide-vscode-community-dev-log
tags: [community, dev-log, vscode]
created: 2024-12-01T12:01:13.080Z
modified: 2024-12-01T12:01:26.714Z
---

# lib-ide-vscode-community-dev-log

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss
- ## 

- ## [Obsidian AppImage - The SUID sandbox helper binary was found, but is not configured correctly - Ask Ubuntu](https://askubuntu.com/questions/1512287/obsidian-appimage-the-suid-sandbox-helper-binary-was-found-but-is-not-configu)
- You could run your appimage with the --no-sandbox-option:

```sh
./Obsidian-1.4.13.AppImage --no-sandbox
./Obsidian-1.4.13.AppImage --disable-setuid-sandbox
```

- ## [Building electron linux distro : The SUID sandbox helper binary was found, but is not configured correctly - Stack Overflow](https://stackoverflow.com/questions/63780918/building-electron-linux-distro-the-suid-sandbox-helper-binary-was-found-but-i)

```shell
sudo chown root chrome-sandbox
chmod 4755 chrome-sandbox
# dev-xp
sudo chown root .build/electron/chrome-sandbox
sudo chmod 4755 .build/electron/chrome-sandbox

sudo chown root node_modules/electron/dist/chrome-sandbox
sudo chmod 4755 node_modules/electron/dist/chrome-sandbox

```
