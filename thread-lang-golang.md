---
title: thread-lang-golang
tags: [golang, thread]
created: 2025-04-18T03:56:43.336Z
modified: 2025-04-18T03:57:00.075Z
---

# thread-lang-golang

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 
# discuss-news
- ## 

- ## 

- ## 

- ## 
# discuss-web-fwk
- ## 

- ## 

- ## 

- ## 
# discuss-golang-usecase 🌰
- ## 

- ## 

- ## 

- ## 

- ## Our @golang load balancer at @render handles more than 150 billion HTTP requests a month across millions of services.
- https://x.com/anuraggoel/status/2044833617889694051
  - The number of times we've wanted to rewrite it in Rust: zero.
  - Go is the most underrated language in infrastructure. "Boring" is the ultimate feature.

- Big fan of Go here too. But scale matters - Render's 150B/month ≈ 58K req/s. @Cloudflare rewrote their proxy in Rust (Pingora) when they hit ~58M req/s, roughly 100x that.
  - How do these numbers makes sense without context like how many hosts are in the fleet serving these requests? Both for 150B/month and 58M req/s. I am assuming these numbers are not from single host.

- This isn't the flex you think it is. Honestly, you need to at least share peak numbers, because 150 billion HTTP requests/month seems like a large number, but it really isn't. From all my tests, Go is a slow language. Like, really slow. The word "half" comes to mind.
# discuss-dev-xp-golang
- ## 

- ## 

- ## 

- ## 

- ## I've heard Java devs call Go "Simpler Java" & I agree after I used it.
- https://x.com/avrldotdev/status/2048278700446359645
  - std-lib is lean but strong, provides OS to HTTP & much more.
  - natively concurrent with goroutines & channels
  - simpler runtime & small GC pauses
  - faster builds & fewer abstractions
  - easier to learn too

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Go has 18 built-in functions (since Go 1.21; there were 15 before that).
- https://x.com/ohmypy/status/2079542805060366467
  - Personally, I use make, append and len/cap all the time. I never use complex/real/imag or print/println. Everything else falls in between.

- its wild that go's built-ins print() and println() are not meant to be used to print and println

- I used len, make and append all the time. Never used cap. Why would you need to use cap?
  - maybe I don't. I paired len with cap out of habit of teaching them together.

- often: make, new, append, delete, len, panic
occasionally: cap, clear, close, copy, min, max
never: complex, real, imag, recover, print, println
- Note: I use `panic` only for impossible-by-contract errors that would indicate a developer bug, so the failure is loud, observable, and never leaked into caller-facing error handling.

- ## I don't like the functional options pattern in Go, and I'm pretty disappointed that it ended up in the standard library with the new json/v2 package.
- https://x.com/ohmypy/status/2076642867104080206
  - An honest, plain Options struct is much better.

- As long as fields of an option struct can be zero value they are not bad at all. The Rob Pike version of self referential functions where you return a closure to the previous state is really cool, though.

- I think it is case by case basis. When you have options struct, and some fields have defaults if not applied, is zero value real zero or is it desired by user. If zero value is valid value, you end up using ptr which is in my opinion worse. Options are quite nice. You can add them nicely while keeping the ability to redesign internal fields how you see fit

- ## [Indentation in Go: tabs or spaces? - Stack Overflow](https://stackoverflow.com/questions/19094704/indentation-in-go-tabs-or-spaces)
- The official recommendation is formatting your code with `go fmt` ; 
  - or `gofmt -w .` 

- Gofmt formats Go programs. It uses tabs for indentation and blanks for alignment. Alignment assumes that an editor is using a fixed-width font.
