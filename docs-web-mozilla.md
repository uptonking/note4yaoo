---
title: docs-web-mozilla
tags: [web, docs]
favorited: true
created: '2020-07-18T12:22:41.248Z'
modified: '2020-07-18T12:23:25.933Z'
---

# docs-web-mozilla

## `<length>` css data type

- represents a distance value. 
- Lengths can be used in numerous CSS properties, such as width, height, margin, padding, border-width, font-size, and text-shadow.
- The `<length>` data type consists of a `<number>` followed by one of the units listed below. 
- As with all CSS dimensions, there is no space between the unit literal and the number. The length unit is optional after the number 0.
- Absolute lengths can cause accessibility problems, since they are fixed and do not scale according to user settings. 
- For this reason, prefer relative lengths (such as em or rem) when setting font-size.

- **Relative length units**
  - Font-relative lengths
  - Viewport-percentage lengths
- em
  - Represents the calculated `font-size` of the element. 
  - If used on the `font-size` property itself, it represents the inherited font-size of the element.
- rem
  - Represents the `font-size` of the root element (typically `<html>` ). 
  - When used within the root element `font-size` , it represents its initial value (**a common browser default is 16px**, but user-defined preferences may modify this).
- cap
  - Represents the "cap height" (nominal height of capital letters) of the element’s font 
- lh
  - Equal to the computed value of the line-height property of the element on which it is used, converted to an absolute length
- vh/vw
  - Equal to 1% of the height/width of the viewport's initial containing block.

- **Absolute length units**
- Absolute length units represent a physical measurement when the physical properties of the output medium are known, such as for print layout.   
  - This is done by anchoring one of the units to a physical unit, and then defining the others relative to it. 
  - The anchor is done differently for low-resolution devices, such as screens, versus high-resolution devices, such as printers.
- For **low-dpi** devices, the unit `px` represents the physical reference pixel; other units are defined relative to it. 
  - Thus, **1in is defined as 96px, which equals 72pt**. 
  - The consequence of this definition is that on such devices, dimensions described in inches (in), centimeters (cm), or millimeters (mm) don't necessary match the size of the physical unit with the same name.
- For **high-dpi** devices, inches (in), centimeters (cm), and millimeters (mm) are the same as their physical counterparts. 
  - Therefore, **the px unit is defined relative to them (1/96 of 1 inch)**.
- px
  - For screen displays, it traditionally represents one device pixel (dot). 
  - However, for printers and high-resolution screens, one CSS pixel implies multiple device pixels. 1px = 1/96th of 1in.
- cm
  - One centimeter. 1cm = 96px/2.54.
- in
  - One inch. 1in = 2.54cm = 96px.
- pt
  - One point. 1pt = 1/72nd of 1in.
- pc
  - One pica. 1pc = 12pt = 1/6th of 1in.

- When animated, values of the `<length>` data type are interpolated as real, floating-point numbers. 
  - The interpolation happens on the calculated value. 
  - The speed of the interpolation is determined by the timing function associated with the animation.

- ref
  - [length CSS data type](https://developer.mozilla.org/en-US/docs/Web/CSS/length)
  - [CSS像素、物理像素、逻辑像素、设备像素比、PPI、Viewport](https://zhuanlan.zhihu.com/p/91636704)
