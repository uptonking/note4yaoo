---
title: thread-lang-js-wasm
tags: [js, lang, thread, wasm]
created: '2021-07-07T06:26:49.767Z'
modified: '2021-07-07T06:27:10.266Z'
---

# thread-lang-js-wasm

# discuss

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

- ## 

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
