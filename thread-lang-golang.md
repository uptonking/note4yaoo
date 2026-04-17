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
# discuss
- ## 

- ## 

- ## 

- ## [Indentation in Go: tabs or spaces? - Stack Overflow](https://stackoverflow.com/questions/19094704/indentation-in-go-tabs-or-spaces)
- The official recommendation is formatting your code with `go fmt` ; 
  - or `gofmt -w .` 

- Gofmt formats Go programs. It uses tabs for indentation and blanks for alignment. Alignment assumes that an editor is using a fixed-width font.
