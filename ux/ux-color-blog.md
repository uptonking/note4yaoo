---
title: ux-color-blog
tags: [blog, color, css]
created: 2022-11-30T16:33:12.320Z
modified: 2022-11-30T16:33:25.382Z
---

# ux-color-blog

# guide

# [Color Formats in CSS - hex, rgb, hsl, lab](https://www.joshwcomeau.com/css/color-formats/)
- CSS has a whole slew(+of 大量) of different color formats: hex codes, rgb(), hsl(), lch(), the list goes on!

## Named colors

- HTML comes with 140 named colors. 
- this isn't really a color format, but it's a good place to start!
- Named colors are great when you need a placeholder color.
- Developer Anthony Lieuallen created this neat demo, showing all 140 named web colors in a circle
- the 140 named web colors are sourced from different places, including the HTML4 spec, the X11 Unix windowing system, and a heartbreaking memorial. 
- It's a hodgepodge of different palettes, and so it isn't always super consistent.

## RGB

- The neat thing about RGB color is that it's based on the physics of light.
- CSS Colors level 4, which introduces a standardized notation used across newer color formats. rgba() isn't explicitly deprecated
  - rgb(255 0 0 / 0.5)    👍🏻
  - rgba(255, 0, 0, 0.5)  👎🏻

## HEX Codes

- This is probably the most commonly-used color format on the web
- Fundamentally, hex codes are the same as RGB values. 
  - a 6-digit hex code contains three 2-digit values, one for each channel (red / green / blue). 
- 8-digit hex codes are widely implemented in modern browsers, with 96% global support. Sadly, they aren't supported in IE.

## HSL

- This tends to be a really intuitive way to think about color. 
- Frustratingly, most graphic design software uses a closely-related color format called HSB. 
  - Hue-Saturation-Brightness instead of Hue-Saturation-Lightness.
  - In HSL, “lightness” is a scale between black and white. 0% lightness is always black, 100% lightness is always white. 
  - In HSB, things are a bit more complicated. "Brightness" is still a measure of lightness, and 0% will still produce black, but 100% no longer always produces white. It depends on the saturation: at full brightness, 0% saturation is white, and 100% saturation is our bright, vivid color.
- HSB is not an option in CSS. 

## Display P3

- All of the true color formats we've seen so far — rgb(), hex codes, and hsl() — are all bound by the “standard RGB color space”, commonly abbreviated as sRGB.
- A color space is a collection of available colors, the palettes we have to pick from. 
- P3 extends the standard sRGB color space, giving us access to brighter and more vibrant colors.
- color(display-p3 1 0 0); 

## LCH (Lightness Chroma Hue)

- LCH stands for “Lightness Chroma Hue”. 
  - “Chroma” is more-or-less a synonym of “saturation”. 
- It's conceptually very similar to HSL, but with two big differences
  - it prioritizes human perception, so that two colors that share the same “lightness” value will feel equally light.
  - It isn't bound to any particular color space.
- The HSL color format is modeled after math/physics. It doesn't take human perception into account. 
- LCH is a color format that aims to be perceptually uniform to humans. 
  - Two colors with an equivalent “lightness” value should feel equally light!

- In HSL, saturation ranges from 0% (no saturation) to 100% (fully saturated).
  - But LCH isn't linked to a particular color space, and so we don't know where the upper saturation limit is.
- LCH is currently only supported in Safari (though they're working on it in Chrome!)

## Picking the right color format

- Personally, I recommend using HSL. At least until LCH gains widespread browser support.
  - The wonderful thing about HSL is that it's intuitive.