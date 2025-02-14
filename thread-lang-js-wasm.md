---
title: thread-lang-js-wasm
tags: [js, lang, thread, wasm]
created: 2021-07-07T06:26:49.767Z
modified: 2021-07-07T06:27:10.266Z
---

# thread-lang-js-wasm

# guide

# discuss
- ## 

- ## 

- ## 

- ## 

- ## this is QuickJS running natively vs Porffor compiling to Wasm; 
- https://x.com/CanadaHonk/status/1888572230277222687
  - QuickJS running in Wasm would be even slower
  - this improvement was thanks to tweaking the memory allocator to use smaller pages internally as Wasm pages are pretty huge relatively (Wasm: 64KB, Linux x64: 4KB)

- How does wasm2c perform compared to interpeted version
  - This has some more complex Wasm so it doesn't fully work yet, I'll work on that soon though

- I found out recently wasm can be slower than JS for simple functions. I was comparing rgb to xyz color space conversion (mat3 * vec3 essentially). And it doesn’t seem due to just js-> wasm tax, it seems wasm has overhead itself
- Thats because js engines are super optimised for JIT? How about js interpreter vs wasm?
  - Just having one (JS) function in Wasm generally isn't that useful/helpful; plus JITs have existed for >a decade so I'm not that concerned atm. Node JITless gets ~210 in this same benchmark, and Porffor still has a lot it can do to improve even in just Wasm.

- ## #Google #Chrome 112 Released With WASM Garbage Collection Trial, CSS Nesting_202304
- https://twitter.com/phoronix/status/1643363243031937025

- ## Rust is faster than JS in some cases, but those cases are rarer than we expected, 
- https://twitter.com/dalmaer/status/1520809822530142208
  - and the performance gain is on the order of 2x some of the time, not 10x most of the time.” 
  - WebAssembly is amazing, but it isn’t a silver bullet to make “everything faster”
  - [Zaplib post-mortem](https://zaplib.com/docs/blog_post_mortem.html)
- The rust is faster than js part is silly. WASM is faster than JS is the proper phrasing
- "...but most of Figma’s performance magic is due to their WebGL renderer." Interesting too.
- A few data-points that illustrate this:
  1. Moving from asmjs -> wasm was a 3x speedup for many things in Figma
  2. For the prototype viewer, attempting to switch from Skew (not wasm, but AOT optimization) to TypeScript resulted in a ~10% slowdown
- The asmjs -> wasm switch of course has confounding factors, making the comparison difficult
  - The existence of the prototype viewer, written in Skew rather than C++ but against WebGL also demonstrates that it's possible to write high perf w/o wasm. But AOT opt is still helpful

- I agree getting a 10x perf boost moving from perf-tuned JS -> perf-tuned wasm is unlikely.
  - Getting a 10x boost moving from DOM -> WebGL or Canvas2D -> WebGL is much more plausible because it unlocks totally different execution models.

- You are comparing WASM with JS VM, not Rust vs JS.
  - WASM is, on average, 10 times slower than native (Rust) code.

- ## I was writing some WebAssembly code in C, and it performed quite well. 
- https://twitter.com/dogriffiths/status/1412441672768688130
  - But then discovered if I re-wrote it in JavaScript, it ran 20% faster
  - What does wasmstudio compile with? I used emcc.
  - Now I'm really confused. The performance.now() times running my compiled copy shows JS taking around 30ms to render a frame, and WASM taking in the upper 50s. 
  - But the wasmstudio versions both taking around 30ms.
  - Did I do bad compiler optimization?
- If you are not using any WASM-only features (like SIMD instructions), at the end of the day both codes will get optimized in V8 using the same optimizer, so if you can make your JS as easy to understand for the optimizer as your WASM is they should perform similarly.
  - Maybe your JS code is faster in this example because the optimizer is able to understand it about as well as the WASM code, but executing JS functions from JS is cheaper than executing WASM functions from JS, hence a bit less overhead.
- Wasm can't draw directly to the ImageData buffer since it only has access to its Memory object, so you have to do an additional copy. Maybe that could explain the difference?
- If the compiler is written correctly, C should always be faster than Java because it is at least one layer closer to the hardware. If you’re working with Javascript, which is interpretive, then it should be much slower than C. If this is not the case, try a better C compiler.
