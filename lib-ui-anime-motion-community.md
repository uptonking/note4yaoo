---
title: lib-ui-anime-motion-community
tags: [animation, community, motion-one]
created: 2024-11-16T10:34:57.687Z
modified: 2024-11-16T10:35:13.534Z
---

# lib-ui-anime-motion-community

# guide

# discuss-stars
- ## 

- ## 

- ## 
# discuss-news/author
- ## 

- ## 

- ## 

- ## 🌰 Introducing Motion view animations, the View Transition API for the rest of us.
- https://x.com/mattgperry/status/1876621824752296253
  - view() is the easiest way to create view animations. Play, pause, scrub, scroll, and spring

- ## 🚀 Today, we’re spinning Framer Motion out into its own independent open-source project, to better serve the whole community. _202411
- https://x.com/mattgperry/status/1856347846796005472
  - [Framer Motion is now independent, introducing Motion - Motion Blog _202411](https://motion.dev/blog/framer-motion-is-now-independent-introducing-motion)
  - All React and vanilla for now. But certainly a Vue integration guide, literally a draft in progress

- Sorry I'm a bit confused. So there was motion which was for vanilla js. Now Framer Motion is also motion? What happens to the previous motion? For context, i never used Framer Motion but I like motion and use it with svelte.
  - There is now one library, Motion. This replaces both Motion One, which you were using, and Framer Motion. There's an upgrade guide for Motion One users

- Any plan also to sopport inline animation any element like aos library, e.g  data-aos="...". That would be very handy for animations when working with simple html pages
  - Any plan also to sopport inline animation any element like aos library, e.g  data-aos="...". That would be very handy for animations when working with simple html pages

- 🛝 It would be awesome if there was a visual way of making animation if Motion (just as it's currently implemented in Framer) and the ability to export the code. A separate product from Framer itself
  - Wouldn't it just

- Are we going to have react native implementation soon??
  - Honestly speaking I think React Native is the least likely thing to happen. Never say never but I think the effort/payoff ratio is out of whack.

- Any plans for layout in vanilla?
  - Layout in vanilla is sadly a little ways off. Not because I don't want to do it. There's actually a bit of a vanilla API already. Its just not nice to use. The scale correction requires precise integration with the DOM tree and that would need rewriting

- Congrats Matt! Popmotion is still one of the best animation APIs I’ve ever used. Excited to see where you take Motion now
  - Thanks Travis, and thanks for being literally my first notable user. I was honestly thinking about packing Popmotion in until I saw a tweet from your kind self.

- Does this mean I can remove Framer Motion 12 alpha and use Motion instead? Is there any changes for React API?
  - No you stay on the Framer Motion 12 alpha. You're not missing anything by doing so, there's no API changes yet. I will spin up a Motion 12 alpha soonish though.
# discuss-examples
- ## 

- ## 

- ## 🚀 Introducing Blendy – a framework-agnostic tool that smoothly transitions any element into any other element with just a few lines of code. _202412
- https://x.com/tahazsh/status/1869046551500456418
  - https://blendy.tahazsh.com
  - 卡片从小变大的动画示例

# discuss
- ## 

- ## 

- ## 

- ## 

- ## Did you know that Motion interpolates RGB colors differently to browsers?
- https://x.com/mattgperry/status/1892939449303994791
  - Because of the way RGB colors are stored, straight interpolation will lead to dips in brightness. Motion instead mixes the square of the color, which avoids this dip.
  - I once explored achieving hardware accelerated background-color animations with this blending by generating a ton of keyframes, but encountered this unresolved bug in Chrome where that can be 100x slower than a standard two keyframe animation

- ## For years, Figma has been using Motion to drive delightful animations throughout their site, core product, and now FigJam too.
- https://x.com/mattgperry/status/1869761398223634733
- Don't get bought by Figma!
  - 100% aboard the independent train, no worries
