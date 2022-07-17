---
title: wiki-format-binary-hex
tags: [format]
created: 2020-07-28T07:13:15.690Z
modified: 2020-10-22T14:03:07.408Z
---

# wiki-format-binary-hex

- RGB colors model can be expressed through both hexadecimal (prefixed with `#` ) and functional ( `rgb()` , `rgba()` ) notations.
- Hexadecimal notation: `#RRGGBB[AA]`
  - R (red), G (green), B (blue), and A (alpha) are hexadecimal characters (0–9, A–F). A is optional. 
  - For example, `#ff0000` is equivalent to `#ff0000ff` .
- 这里涉及到十六进制AA到百分比的映射
  - `100% — FF`
  - 95% — F2
  - 90% — E6
  - 85% — D9
  - `80% — CC`
  - 75% — BF
  - 70% — B3
  - 65% — A6
  - 60% — 99
  - 55% — 8C
  - `**50% — 80**`
  - 45% — 73
  - 40% — 66
  - 35% — 59
  - 30% — 4D
  - `25% — 40`
  - 20% — 33
  - 15% — 26
  - 10% — 1A
  - 5% — 0D
  - `0% — 00`
