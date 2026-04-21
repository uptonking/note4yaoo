---
title: toc-ux-icons
tags: [icon]
created: 2024-05-28T12:38:00.123Z
modified: 2021-05-06T09:58:23.803Z
---

# guide
- popular-icons
  - feather-icons, heroicons-tailwind, tabler
  - iconpark, phosphor

- ✨ icons-pack
  - https://icon-sets.iconify.design/
    - https://github.com/iconify/iconify
    - 100+ open source icon sets
    - collection of SVG icons created by various authors, released under various free licenses.
    - Icon sets are stored in `IconifyJSON` format
  - https://icones.js.org/
    - https://github.com/antfu/icones

- icons
  - https://fonts.google.com/icons?selected=Material+Icons
  - https://primer.style/octicons/

- 搜索矢量图标
  - https://uxwing.com/

- ✨ brand-icons
- apple-store
  - https://www.apple.com/us/search/notion?src=globalnav
- google-play 应用商店可以获取到图标url
  - https://play.google.com/store/apps
  - 商店的图标大小一般都是512x512，但部分图标可能偏高
- https://logos.fandom.com/wiki/Android_Studio
  - 记录了logo变更

- ## “How to make complex icons with only CSS”. Don’t do this.
- https://twitter.com/SaraSoueidan/status/643803332117704704
  - Use #SVG. It was *made* for this kind of stuff.
- If someone wants to show off skills they should try hand-coding SVG path data
- SVG icons are accessible and semantic. CSS icons are FAKE icons. Also, the epic icon fonts vs SVG comparison guide
- use SVG instead of icon fonts whenever possible.
- CSS only icons are awful, iconographers have a job for a reason.
  - Iconography is such a specific art form with considerable effort taken to convey meaning, brand personality and functionality.
- the only advantage I can see is you can mutate glyphs without js—but those mutations are super specific so it's kinda moot

- ## Seriously, Don’t Use Icon Fonts
- https://cloudfour.com/thinks/seriously-dont-use-icon-fonts/
- Screen Readers Actually Read That Stuff
  - Most assistive devices will read aloud text inserted via CSS, and many of the Unicode characters icon fonts depend on are no exception. 
  - Best-case scenario, your “favorite” icon gets read aloud as “black favorite star.” 
  - Worse-case scenario, it’s read as “unpronounceable” or skipped entirely.
- They’re a Nightmare if You’re Dyslexic(诵读困难的)
- They Encroach on Emoji Turf(unicode冲突)
- They Fail Poorly and Often(下载失败时浏览器可能显示乱码)
- They Never Looked Right
  - The way browsers hint fonts to optimize legibility was never a good fit for our custom iconography
  - Multicolor icons are even worse.
  - 还要考虑不同浏览器渲染字体所产生的不一致
- There’s Already a Better Way
  - svg is a vector image format with optional support for CSS
- 不要墨守陈规，盲目模仿
# icons-css-svg
- https://github.com/erikflowers/weather-icons
  - https://erikflowers.github.io/weather-icons/
  - Weather Icons is the only icon font and CSS with 222 weather themed icons

- https://github.com/mono-company/mono-icons
  - https://icons.mono.company/
  - The Mono icon font is a simple, consistent open-source icon set
  - You can download the whole set of SVG icons or selected items

- https://iconpark.oceanengine.com/home
  - IconPark图标库是一个通过技术驱动矢量图标样式的开源图标库
# icons
- tabler-icons
  - https://github.com/tabler/tabler-icons
  - https://tabler.io/icons 
  - A set of 5200 free MIT-licensed high-quality SVG icons
  - Each icon is designed on a 24x24 grid and a 2px stroke.
  - 粗细默认2px，网站可调整粗细
  - 样式风格有点圆润，图标数量多
  - 在github提供下载多种格式svg/png/pdf
  - 🆚 [Compare to FontAwesome _202211](https://github.com/tabler/tabler-icons/discussions/370)
    - Tabler Icons are made by stroke width (like variable font), not by outline, so you can change it in any time. 

- feather /MIT/16kStar/201908/样式好/图标少
  - https://github.com/feathericons/feather
  - https://github.com/feathericons/react-feather
  - https://feathericons.com/
  - At its core, Feather is a collection of SVG files. Each icon is designed on a 24x24 grid with an emphasis on simplicity
  - 粗细默认2px，网站可调整粗细
  - 图标数量不多，文件相关图标少
  - https://github.com/zaydek/feathericons.dev
    - https://feathericons.dev/
    - Remake of the classic Feather by @colebemis. 
    - Brand and payment icons by @thewolfkit (Twitter)
- https://github.com/lucide-icons/lucide
  - https://lucide.dev/
  - fork of Feather Icons, hundreds of icons more than Feather 
- https://github.com/pqoqubbw/icons /MIT/202512/ts
  - https://lucide-animated.com/
  - collection of smooth animated icons

- iconpark
  - https://github.com/bytedance/iconpark
  - https://iconpark.oceanengine.com/official
  - Transform an SVG icon into multiple themes, and generate React icons，Vue icons，svg icons
  - more than 2000 high-quality icons
  - 默认提供分好类的图标文件夹，部分有色
  - 在网站支持批量下载svg，图标名包含中文，下载时可配置风格、拐点、端点

- phosphor-icons /212Star/MIT/202112/易用性高
  - https://github.com/phosphor-icons/web
  - https://github.com/phosphor-icons/react
  - https://phosphoricons.com/
  - 提供6套图标6x1248个，包括不同粗细和风格，thin/light/regular/fill/bold/duotone
    - If you'd like to use the raw assets directly to modify them, click the toggle in the toolbar to change from Flat to Raw. 
    - 实测Flat的体积会小一点
  - 可下载svg/png/iconfonts
  - 文件操作相关icon不多
  - available for web, React, Vue, Flutter, Elm
  - providing icons as several webfonts that uses Unicode's Private Use Area character codes to map normally non-rendering characters to icons.
  - [Release v2.0.0](https://github.com/phosphor-icons/homepage/releases/tag/v2.0.0)
    - All icons use currentColor for instead of #000000 for fills and strokes to ease styling of icons
  - providing icons as a webfont that uses Unicode's Private Use Area character codes to map normally non-rendering characters to icons. 
  - Since the icons are just text under the hood, they can be colored and styled with CSS

- https://github.com/tailwindlabs/heroicons /MIT/202403/js
  - https://heroicons.com/
  - Beautiful hand-crafted SVG icons, by the makers of Tailwind CSS.
  - Available as basic SVG icons and via first-party React and Vue libraries.
  - 样式风格有点圆润
  - github下载的图标数量少

- simple-icons /CC0-1.0/svg/主流产品的logo图标
  - https://github.com/simple-icons/simple-icons
  - https://simpleicons.org/
  - SVG icons for popular brands
  - Creative Commons Zero v1.0 Universal 无著作权，可商用
    - 500+ icons

- font-awesome  /MIT/60kStar/201610
  - https://github.com/FortAwesome/Font-Awesome/tree/v4.7.0
  - https://fontawesome.com/v4.7.0/
  - 675 pictographic icons
- fork-awesome  /MIT/619Star/201907/inactive
  - https://github.com/ForkAwesome/Fork-Awesome
  - https://forkaweso.me/Fork-Awesome/icons/
  - 744 icons 
  - `src/icons/svg/` 提供了svg图标
- material-design-icons  /Apache2/6kStar/201908
  - https://github.com/Templarian/MaterialDesign
  - https://materialdesignicons.com/
  - converted icons from Google's official icon set
  - available via Webfont/SCSS, JavaScript/TypeScript, SVG/Meta.json, react

- react-icons  /9.9kStar/MIT/202306
  - https://github.com/react-icons/react-icons
  - https://react-icons.github.io/react-icons/
  - svg react icons of popular icon packs, including fa, md 

- ionicons   /MIT/13kStar/201908
  - https://github.com/ionic-team/ionicons
  - https://ionicons.com/
  -  icon font for Ionic Framework and web apps everywhere
- https://github.com/CoreyGinnivan/system-uicons
  - https://systemuicons.com/
  - /384Star/Unlicense/202008
  - System UIcons is a collection of icons designed for products and systems in mind. 
  - Each icon is on a 21x21 grid.
  - Use the icons how you want, for free, and without any attribution.
# font icons
- catalog
  - https://getbootstrap.com/docs/4.0/extend/icons/
  - http://iconfont.cn/ 
      - iconfont的版权说明包括：官方图标库若无书面授权不得用于商业
- free
  - Fork Awesome
      - A fork of the Font-Awesome 4.7
      - https://forkawesome.github.io/Fork-Awesome/
          - https://github.com/ForkAwesome/Fork-Awesome
      - MIT
      - 733 icons
  - feather icons
      - beautiful open source icons. Each icon is designed on a 24x24 grid with an emphasis on simplicity, consistency and readability.
      - https://feathericons.com
          - https://github.com/feathericons/feather
          - https://github.com/carmelopullara/react-feather
      - MIT
      - 271 icons
  - font awesome 4.7
      - gives you scalable vector icons that can instantly be customized — size, color, drop shadow, and anything that can be done with the power of CSS.
      - https://fontawesome.com/v4.7.0/
          - https://github.com/FortAwesome/Font-Awesome/tree/v4.7.0
          - https://github.com/AndreLZGava/font-awesome-extension
      - CC BY 4.0
      - 675 icons
  - ionicons
      - open-source icon set with 700+ icons crafted for web, iOS, Android, and desktop apps. Ionicons was built for Ionic Framework
      - https://ionicons.com/
          - https://github.com/ionic-team/ionicons
      - MIT
      - 700+ icons
      - 图标数量较少
  - icono
      - One tag One icon, no font or svg, Pure CSS
      - https://saeedalipoor.github.io/icono/
      - https://github.com/saeedalipoor/icono
      - MIT
      - 130+ icons
      - 纯css实现的icon set，自己制作和添加图标不方便，css在不同浏览器渲染效果可能不同
          - https://github.com/wentin/cssicon
              - Creative Commons Zero v1.0 Universal
              - 512+ icons
  - line awesome
      - Replace Font Awesome with modern line icons
      - https://icons8.com/line-awesome
      - https://github.com/icons8/line-awesome
      - MIT/GBL GOOD BOY LICENSE
      - 674 icons
      - more icons
          - https://github.com/icons8/flat-color-icons
          - https://github.com/icons8/webicon
          - https://icons8.com/
          - animated: https://github.com/icons8/titanic
  - jam icons
      - icons shipped in JavaScript, font & SVG versions
      - https://jam-icons.com/
      - https://github.com/michaelampr/jam
      - MIT
      - 896 icons
  - open-iconic
      - the open source sibling of Iconic. It is a hyper-legible collection of 223 icons with a tiny footprint—ready to use with Bootstrap and Foundation
      - https://useiconic.com/open/
          - https://github.com/iconic/open-iconic
      - MIT
      - 223 icons 
      - dead project
  - google material design icons
      - Each symbol is available in five themes and a range of downloadable sizes and densities.
      - https://material.io/tools/icons/?style=outline
          - https://github.com/google/material-design-icons
      - Apache 2.0
      - 1k+ icons
  - bytesize icons
      - Tiny style-controlled SVG iconset
      - https://danklammer.com/bytesize-icons/
          - https://github.com/danklammer/bytesize-icons
      - MIT
      - 94 icons, 10kb
  - octicons
      - Octicons are a set of SVG icons built by GitHub for GitHub.
      - https://octicons.github.com/
        - https://github.com/primer/octicons/
      - MIT
      - 150+ icons
  - glyph
      - a semantic and versatile SVG icon set designed for customization.Glyph is 16x16, but because it's SVG, it can be any size you want.
      - http://glyph.smarticons.co/
          - https://github.com/frexy/glyph-iconset/
      - Attribution-ShareAlike 4.0 International (CC BY-SA 4.0) 署名-相同方式共享
      - 800+ icons
  - IKONS
      - Hand crafted, scalable vector icons，with 300 custom icons in SVG, AI, ESP, PSD, CSH and PNG format.
      - http://ikons.piotrkwiatkowski.co.uk/index.html
      - free to use these icons for personal and commercial work without obligation of payment or attribution.You may not redistribute or sell these icons
      - 300+ icons
  - dripicons
      - free vector line iconset by Amit Jakhu.
      - http://demo.amitjakhu.com/gg/
          - https://github.com/amitjakhu/dripicons
      - Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)
      - 150+ icons
  - nerd fonts
      - Nerd Fonts is a project that patches developer targeted fonts with a high number of glyphs (icons). 
      - https://nerdfonts.com/
          - https://github.com/ryanoasis/nerd-fonts#tldr
      - MIT
  -  Seti-UI
- paid
  - font awesome 5
      - Version 5 has been re-written and re-designed completely from scratch. 
      - https://fontawesome.com/how-to-use/on-the-web/setup/upgrading-from-version-4
      - https://github.com/FortAwesome/Font-Awesome
      - CC BY 4.0.  
          - free: solid, brands
          - paid: regular, light
      - 414 brand icons: weixin, qq, alipay, zhihu
- icons for industry
  - https://konpa.github.io/devicon/
      - icons representing programming languages, designing & development tools
      - v2: https://github.com/konpa/devicon
      - v1: https://github.com/vorillaz/devicons/
      - 78 icons and 200+ versions
  - http://labs.mapbox.com/maki-icons/
      - poi icon set made for cartographers
      - https://github.com/mapbox/maki
  - https://erikflowers.github.io/weather-icons/
      - weather themed icons
      - https://github.com/erikflowers/weather-icons
- other font icons
  - https://github.com/snwh/paper-icon-theme
  - https://github.com/stark/siji
  - https://materialdesignicons.com/
  - font-family: Wingdings
- tools for icons
  - https://icomoon.io
  - http://fontastic.me
  - Typefont
      - The first open-source library that detects the font of a text in a image.
      - https://github.com/Vasile-Peste/Typefont
- tips
  - Moving Away From Font Icons
      - https://blog.ionicframework.com/announcing-ionicons-v4/
      - When we originally released Ionicons, we went the route of making an icon font. At the time, this made a lot of sense: 
          - Icon fonts are vector-based, 
          - scalable to any physical size without pixelation, 
          - able to be styled with CSS,  
          - come from a single resource (which means fewer HTTP requests).
      - they also have a cost that can flip their advantage into a disadvantage: all of the icons are bundled in one file. And in previous versions of Ionicons, we were packing nearly 700 icons into one large file!
          - Large font files have a negative impact on a webpage or app’s Time to First Paint, which makes for a subpar user experience and has been known to lower PWA Lighthouse scores. 
          - On top of that, adding any custom icons to a font icon is far from easy.
      - All of the benefits of font icons (vector-based and styling with CSS) can be achieved just as easily with SVGs, but without all the baggage.
# icons-utils
- https://github.com/aykutkardas/react-icomoon
  - It makes it very simple to use SVG icons in your React and React-Native projects.
  - You can use svgps.app to access over 40, 000 free icons and convert your own icons into selection.json.
  - https://github.com/aykutkardas/svgps
    - https://svgps.app/
    - SVGPS removes the burden of working with a cluster of SVG files by converting your icons into a single JSON file. You can easily use this file in your frontend or mobile projects.
# icons-engineering
- https://github.com/svg-jar/plugin /MIT/202604/ts
  - An unplugin for importing SVGs as components. 
  - Supports sprite sheets, inline SVGs, and raw file exports across Vite and Rollup.
  - Sprite mode (default): SVGs are collected into a sprite sheet and rendered via `<use href>`. The sprite file is emitted with a content-hashed filename for cache busting.
  - Inline mode: Embed the full SVG markup directly in the component. No sprite sheet, no external request.
  - Inline SVGs are embedded in your JavaScript bundle, increasing parse time and preventing separate caching. Sprite mode (the default) is more efficient for most use cases. 
  - https://x.com/evo1/status/2046511527172170205
    - SVG Jar goes multi-framework and multi-bundler. The best way to work with SVGs in your web apps. 
# icons-tooling
- [Iconbuddy — 200K+ open source free svg icons](https://iconbuddy.app/)
  - Download, Customize, Edit and Personalize. Over 200k+ open source icons.

- https://github.com/dicebear/dicebear /7.6kStar/MIT/202508/ts/经典图层组合
  - https://dicebear.com/
  - https://www.dicebear.com/playground/
  - With DiceBear you can create awesome avatars for your project in no time.
  - In addition to purely random avatars, you can also create deterministic avatars for user identities. With the built-in PRNG you create the same avatar over and over again based on a seed.
  - The avatars are created in SVG format. This allows to generate avatars dynamically without much computing power.
    - In most cases, various SVG elements such as hair, eyes, ears etc. are selected from a set and combined to create a character / avatar.
    - XorShift32 is used as the algorithm for the PRNG. It is important to note that the PNGR does not attempt to be cryptographically secure
  - [Host the HTTP API yourself | DiceBear](https://www.dicebear.com/guides/host-the-http-api-yourself/)
  - [Licenses | DiceBear](https://www.dicebear.com/licenses/)
    - While our code is MIT licensed, the avatar styles are licensed under different licenses that the artists can choose themselves
    - 友好的风格: Avataaars, Bottts, Bootstrap Icons
  - https://github.com/dicebear/api /118Star/MIT/202507/ts
    - source code for the DiceBear API. It's built on Fastify

- https://github.com/cossistantcom/cossistant/tree/main/packages/facehash /MIT/NoDeps
  - https://www.facehash.dev/
  - Deterministic avatar faces from any string. Zero dependencies, works with React 18/19 and Next.js 15/16.
  - https://x.com/anthonyriera/status/2020784989919498545
    - Nobody talks about how ugly your app looks when users do not upload avatars.
    - So I fixed that with FaceHashes
    - This was originally in http://cossistant.com, a AI / human  customer support widget you add with a simple `<Support />` component to your React app.

- https://github.com/boringdesigners/boring-avatars /6.2kStar/MIT/202509/ts/inactive
  - 头像填充渐变色、小方块、表情形状；可选方形、圆形
  - https://boringavatars.com/
  - Boring avatars is a tiny JavaScript React library that generates custom, SVG-based, round avatars from any username and color palette.

- https://github.com/jaywcjlove/icongo /MIT/202405/ts
  - https://icongo.github.io/
  - Search SVG Icons. Easily include popular icons in your React projects and provide an easy tool to convert SVG into React components

- https://github.com/vemetric/favicon-api /MIT/202511/ts
  - https://vemetric.com/favicon-api
  - Free and open-source API to fetch favicons from any website.
  - [I built an open source Favicon API : r/selfhosted _202510](https://www.reddit.com/r/selfhosted/comments/1oj4uzr/i_built_an_open_source_favicon_api/)
    - Is this different to the one DuckDuckGo offers? For example, the Reddit icon is: https://icons.duckduckgo.com/ip3/www.reddit.com.ico
    - main difference is that my API lets you control the returned size and convert the image into different formats (png, jpg, webp)
    - it also lets you define a custom fallback image and always tries to find the image in the best quality possible
    - in the end I just wanted to create a (more flexible) alternative to the available APIs
  - 💡 By the way, there’s a neat trick to use emojis as favicons via (inline) SVG. I like using that for small (internal) sites to quickly have a nice looking favicon.
  - https://css-tricks.com/emoji-as-a-favicon/
  

# icons-anime
- https://icons.pqoqubbw.dev/
  - animated icons i’ve been working on lately are now open source

- [Vector Motion Kit](https://vectormotionkit.web.app/)
  - https://x.com/romankhrupa/status/2046142681445798127
  - We’re trying to build the biggest animated icon library for Android devs
# logos-generator
- https://github.com/Nutlope/logocreator /202411/ts
  - https://www.logo-creator.io/
  - A free + OSS logo generator powered by Flux on Together AI
  - Flux Pro 1.1 on Together AI for logo generation
  - nextjs + shadcn + redis + clerk + plausible
  - Create a .env file and add your Together AI API key: TOGETHER_API_KEY=
# logos-resources
- [FreeLogo.me – Free SVG Logo Templates](https://freelogo.me/)
  - SVG Logo placeholders you can download and use with no restrictions for free.

- [Logo Design & Brand Identity for Entrepreneurs | Looka](https://looka.com/)
  - AI-powered platform to design a logo and brand you love
  - 生成超多选择性的 logo 图标 , 然后下载是要收费的，你可以去直接扒 dom 里的 svg，去绕过这个问题
# brand-icons
- https://github.com/pheralb/svgl /5.6kStar/MIT/202603/ts/svelte
  - https://svgl.vercel.app/
  - https://svgl.app/
  - most popular SaaS logos in SVG format, with lightning-fast search
  - Built with @sveltejs & @tailwindcss
  - All svgs provides the link to the product or company that owns it, please contact them if you are going to use their logo. If you are the owner of an svg and do not want it to appear here, please create an issue on Github.

- https://github.com/xandemon/developer-icons /MIT/202603/ts
  - https://xandemon.github.io/developer-icons/
  - https://xandemon.github.io/developer-icons/icons/All/
  - A collection of well-optimized SVG tech logos for developers and designers—customizable, scalable, and free.
  - https://x.com/heygurisingh/status/2041073938114191492
    - It's a fully-typed React component library with customizable, perfectly scalable SVGs for every major framework, language, and tool you actually use.
    - Every icon ships as a typed React component (HtmlIcon, JavascriptIcon, ReactIcon, etc.)
    - Customize size, color, stroke width, and style with standard SVG props
    - Optimized with SVGO so file sizes stay microscopic without losing quality
    - Light mode, dark mode, and wordmark variants built in for every brand
    - Works in React, Next.js, Astro, or download raw SVGs for Figma

- https://github.com/preetsuthar17/loftlyy /MIT/202603/ts
  - https://loftlyy.com/
  - A brand identity reference site — discover and explore brand colors, typography, logos, and design systems. Like Mobbin, but for branding.
  - Next.js 16, shadcn/ui
  - https://x.com/preetsuthar17/status/2035251357855502604
    - Loftlyy is now open-source
# qrcode/barcode
- https://github.com/productdevbook/etiket /MIT/202603/ts/NoDeps
  - Zero-dependency barcode & QR code SVG generator. 
  - 40+ formats, styled QR codes, tree-shakeable. Pure TypeScript.
  - https://x.com/productdevbook/status/2036082175024496801
    - French word again. Ty for that. I love it
# more
- https://github.com/fontello/fontello
  - This tool lets you combine icon webfonts
  - shrink glyph collections, minimizing font size
  - merge symbols from several fonts into a single file

- https://twitter.com/search?q=pure%20css%20icon&src=typed_query
