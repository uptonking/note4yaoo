---
title: docs-web-mozilla
tags: [docs, web]
favorited: true
created: '2020-07-18T12:22:41.248Z'
modified: '2020-07-18T12:23:25.933Z'
---

# docs-web-mozilla

## Replaced elements

- In CSS, a replaced element is an element whose representation is outside the scope of CSS; they're external objects whose representation is independent of the CSS formatting model.
- Put in simpler terms, they're elements whose contents are not affected by the current document's styles. 
  - The position of the replaced element can be affected using CSS, but not the contents of the replaced element itself. 
  - Some replaced elements, such as `<iframe>` elements, may have stylesheets of their own, but they don't inherit the styles of the parent document.
- The only other impact CSS can have on a replaced element is that there are properties which support controlling the positioning of the element's content within its box
- Typical replaced elements are:
  - `<iframe>`
  - `<video>`
  - `<embed>`
  - `<img>`
- Some elements are treated as replaced elements only in specific cases:
  - `<option>`
  - `<audio>`
  - `<canvas>`
  - `<object>`
  - `<applet>`
- HTML spec also says that an `<input>` element can be replaced, because `<input>` elements of the `image` type are replaced elements similar to `<img>` . 
  - However, other form controls, including other types of `<input>` elements, are explicitly listed as non-replaced elements (the spec describes their default platform-specific rendering with the term "Widgets").
- Objects inserted using the CSS `content` property are anonymous(匿名的) replaced elements. They are "anonymous" because they don't exist in the HTML markup.
- CSS handles replaced elements specifically in some cases, like when calculating margins and some `auto` values.
  - Note that some replaced elements, but not all, have intrinsic(自身的) dimensions or a defined baseline, which is used by some CSS properties, such as vertical-align. 
  - Only replaced elements can ever have intrinsic dimensions.

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
  - If used on the `font-size` property itself, it represents the inherited `font-size` of the element.
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

## `<number>` css data type 

- represents a number, being either an integer or a number with a fractional component.
- The syntax of `<number>` extends the syntax of `<integer>` . 
  - A fractional value is represented by a `.` followed by one or more decimal digits, and may be appended to an integer. 
  - There is no unit associated with numbers.
- When animated, values of the `<number>` CSS data type are interpolated as real, floating-point numbers. 
- The speed of the interpolation is determined by the timing function associated with the animation.
