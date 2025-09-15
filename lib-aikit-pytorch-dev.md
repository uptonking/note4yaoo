---
title: lib-aikit-pytorch-dev
tags: [ai, large-language-model, machine-learning, pytorch]
created: 2025-09-15T09:30:19.813Z
modified: 2025-09-15T09:30:50.277Z
---

# lib-aikit-pytorch-dev

# guide

# draft

# dev-xp

- setup pytorch with uv on macos
  - [Accelerated PyTorch training on Mac - Metal - Apple Developer](https://developer.apple.com/metal/pytorch/)
  - [Accelerated PyTorch training on Mac - Metal - Apple Developer](https://developer.apple.com/metal/pytorch/)

```sh
conda install pytorch torchvision torchaudio -c pytorch-nightly

pip3 install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu

uv pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu

uv pip install torch --torch-backend=auto

```

# devlog

# more
