---
title: lib-ai-app-community-gen-image-prompts
tags: [community, image, prompt]
created: 2025-12-16T06:34:20.509Z
modified: 2025-12-16T06:34:43.005Z
---

# lib-ai-app-community-gen-image-prompts

# guide

# discuss-stars
- ## 

- ## 

- ## 

- ## 

- ## 🖼️ 一键生成任何影视剧或者小说的场景海报提示词
- https://x.com/Ali_TongyiLab/status/1998608853903036436
  - We just used this prompt to generate classical scenes from the Four Great Classical Novels at Z-Image-Turbo, and the results are stunning.
  - It’s actually capturing the vibe of ancient Chinese literature—Journey to the West, Dream of the Red Chamber, all of it. The cultural understanding is deep here.

```prompt
请为影视剧/小说《需要添加的名称》设计一张高品质的3D海报，需要先检索影视剧/小说信息和著名的片段场景。
首先，请利用你的知识库检索这个影视剧/小说的内容，找出一个最具代表性的名场面或核心地点。在画面中央，将这个场景构建为一个精致的轴侧视角3D微缩模型。风格要采用梦工厂动画那种细腻、柔和的渲染风格。你需要还原当时的建筑细节、人物动态以及环境氛围，无论是暴风雨还是宁静的午后，都要自然地融合在模型的光影里。
关于背景，不要使用简单的纯白底。请在模型周围营造一种带有淡淡水墨晕染和流动光雾的虚空环境，色调雅致，让画面看起来有呼吸感和纵深感，衬托出中央模型的珍贵。
最后是底部的排版，请生成中文文字。居中写上小说名称，字体要有与原著风格匹配的设计感。在书名下方，自动检索并排版一句原著中关于该场景的经典描写或台词，字体使用优雅的衬线体。整体布局要像一个高级的博物馆藏品铭牌那样精致平衡。
```

- 我在此基础扩展了一下范围，效果依旧很不错：题材可以是电影、剧集、动画、游戏、小说等

```prompt
请为作品《在此输入作品名称》（可以是电影、剧集、动画、游戏、小说等）设计一张高品质 3D 海报，需要先检索该作品的信息和著名的片段场景。
首先，请利用你的知识库检索这个作品的内容和世界观，找出一个最具代表性的名场面或核心地点（可以是关键战斗、转折剧情、标志性城市/建筑、初始村落、迷宫秘境等）。在画面中央，将这个场景构建为一个精致的轴侧视角 3D 微缩模型。风格采用梦工厂动画那种细腻、柔和的渲染质感。你需要还原当时的建筑细节、人物或角色动态，以及环境氛围：无论是暴风雨、末日黄昏，还是宁静午后、赛博夜景，都要自然地融合在模型的光影之中。
背景部分，不要使用简单的纯白底。请在模型周围营造一种带有淡淡水墨晕染和流动光雾的虚空环境，色调雅致、层次柔和，让画面看起来有呼吸感和纵深感，像是漂浮在时间长河中的一件珍贵藏品，用来衬托中央微缩模型的独特与重要。
底部排版请生成中文文字。居中写上作品名称，字体风格需与原作的类型和气质相匹配（例如奇幻、科幻、武侠、都市、悬疑、童话等），具有一定的设计感和辨识度。在标题下方，请自动检索并排版一句与该场景高度相关的经典台词、文本描写或官方设定语，字体使用优雅的衬线体或略带书卷气的印刷体。整体布局要像高级博物馆藏品铭牌一样精致、克制且平衡。
```

- 继续打磨了一下，提示词本身和效果几乎没变，只是调整了一下范围，也还是原来的风格和效果，只能说提示词写到最后面，考验的是语文功底和想象力跟审美。书籍、游戏、电影、甚至产品都能适用

```prompt
请为作品《在此输入作品名称》设计一张高品质的3D海报，需要先检索其背景信息和著名的经典场景。
首先，请利用你的知识库检索这个作品的内容，找出一个最具代表性的名场面或核心地点。在画面中央，将这个场景构建为一个精致的轴侧视角3D微缩模型。风格要采用梦工厂动画那种细腻、柔和的渲染风格。你需要还原当时的建筑细节、人物动态以及环境氛围，无论是暴风雨还是宁静的午后，都要自然地融合在模型的光影里。
关于背景，不要使用简单的纯白底。请在模型周围营造一种带有淡淡水墨晕染和流动光雾的虚空环境，色调雅致，让画面看起来有呼吸感和纵深感，衬托出中央模型的珍贵。
最后是底部的排版，请生成中文文字。居中写上作品名称，字体要有与原著/原作风格匹配的设计感。在书名下方，自动检索并排版一句原著/原作中关于该场景的经典描写或台词，字体使用优雅的衬线体。整体布局要像一个高级的博物馆藏品铭牌那样精致平衡。
```

- 可以省一笔设计封面的费用了
- 有一半以上都是原图抄袭的字体，还没办法自己设计
- https://x.com/aarai666/status/1998732651851583896
# discuss-video-prompts
- ## 

- ## 

- ## 

- ## [This is how I generate AI videos locally using ComfyUI : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1pp8s9s/this_is_how_i_generate_ai_videos_locally_using/)
  - I start by generating a base image using Z-Image Turbo, usually at around 1024 × 1536.
  - I use Wan 2.2 FLF for the animation step at 816 × 1088 resolution.
  - Running the video model at a lower resolution helps keep things stable on 16 GB VRAM.
  - 动画小鹿

# discuss-image-prompts
- ## 

- ## 

- ## 

- ## 

- ## 推荐一个专门收集 Prompt 的网站： [Share and Discover anything to do with AI | Snack Prompt](https://snackprompt.com/)
- https://x.com/Penny777_eth/status/1997916272030527936
  - 里面不只是设计、艺术类别的。也有很多功能性质的 Prompt，比如健身教练，或是日程安排之类的。部分接受定制化，可以改成适合自己的关键词！

- ## 历史长河
- https://x.com/Ali_TongyiLab/status/2000812431535399354

```
Hyper - realistic 3 D isometric masterpiece, set against a magnificent, endless traditional ink - wash historical scroll painting unfurling across the background.The scene visualizes the historical lineage and cultural heritage of [在此处填入地点或主题], featuring its most iconic ancient architecture and landmarks rising dynamically from the scroll.
•Composition: The scroll flows through the space like a river of time.The landscape creates a panoramic timeline.
•Visual Effect: 2 D black ink brushstrokes on the paper surface morph seamlessly into high - fidelity 3 D solid structures, realistic materials, and vibrant colors.
•Details: Faded ancient parchment texture, floating historical calligraphy characters, red seal stamps, atmospheric clouds and fog wrapping around the monuments.
•Lighting: Epic golden hour cinematic lighting illuminating the 3 D structures, contrasting with the monochrome ink background.
•Specs: 8 K resolution, depth of field, Unreal Engine 5 render, grand scale.--ar 16: 9--stylize 350--no flat, simple, cartoon, borders, frame, table, modern buildings [在此处填入地点或主题] = 杭州西湖
备注：
地方不会显示现代建筑， 只是展示历史建筑
```

- ## 别再发平庸的产品图了！试试这个“巨物化”提示词
- https://x.com/rionaifantasy/status/2000814642701148518
  - 这个 AI 商业摄影元提示词，能让你的产品瞬间变身为一个宏大的工程奇迹

```prompt
Using the provided product photo as reference, generate a highly realistic creative product showcase image.
Core concept:
Transform the product into a massive central structure, as if it were a building or precious engineered object.
Numerous miniature workers are actively constructing, polishing, cleaning, and assembling the product around it.
Product requirements:
- The product must closely match the reference image in shape, color, proportions, and material
- The product is oversized, dominating the scene
- Surface details are extremely sharp and realistic
Miniature workers:
- 10–30 tiny human figures
- Roles include construction workers, engineers, technicians, cleaners
- Actions include:
  - Building scaffolding
  - Climbing ladders
  - Polishing, painting, cleaning
  - Measuring and inspecting
  - Lifting parts with cranes
Environment:
- The product sits in a believable but slightly surreal setting
  (tabletop, workshop, platform, plate, display surface)
- Tools, equipment, and materials scattered naturally
Visual style:
- Macro photography / tilt-shift effect
- Shallow depth of field
- Cinematic lighting
- Ultra-realistic textures
- Premium commercial photography quality
Overall mood:
Precision, craftsmanship, scale contrast, industrial elegance
Avoid:
- Cartoon or illustration styles
- Text overlays
- Exaggerated fantasy elements
Final result:
A visually striking product image that feels like a miniature world built around the product.
```

- https://x.com/langzihan/status/2000775067836572096
  - 除了首次加载，下面这个配置，基本是2秒出图, 使用ComfyUI默认模板，修改一下自己需要的图片大小即可。

- https://x.com/servasyy_ai/status/2000516485870178397
  - 2，3层双层是同一个人物+景色切割, 中间裸眼3D人物

```prompt
创建一个3x3网格布局海报，包含9个不同的部分，并在上方叠加一个站立的裸感3D女性图像：

人物统一要求：所有场景中的女性必须是同一个人，具有相同的面部特征、发型和身材。亚洲女性，长直黑发，优雅气质，健康匀称身材。

布局结构：

- 底层：3列 × 3行网格

- 每个单元格大小相等

- 单元格之间有干净的白色边框（2px）

- 顶层：一个站立的3D渲染女性图像叠加在整个网格中央

第1行（顶部行 - 三个独立场景，同一位女性）：

[单元格 1-1] 左：同一位优雅亚洲女性站在平静的高山湖边，身穿时尚的棕色印花夹克搭配米色阔腿裤，手轻触夹克领口，侧身站立。背景是壮丽的雪山倒映在湖面上，黄昏时分的柔和蓝调光线，湖面如镜，天空有淡淡晚霞，整体色调偏冷调蓝绿色，宁静梦幻，高级时尚摄影风格，电影级构图。

[单元格 1-2] 中：同一位女性站在海边礁石上，身穿飘逸的藕粉色薄纱长裙（裙摆随风轻扬），侧身回眸或仰望远方，姿态优雅放松。背景是壮观的日落海景，太阳缓缓落入海平面，天空呈现橙粉色渐变，海浪轻拍礁石，海面波光粼粼，暖色调黄金时刻光线，浪漫梦幻，时尚杂志封面级别。

[单元格 1-3] 右：同一位女性站在阳光穿透的松树林中，身穿米白色V领连体阔腿裤，一只手轻触头发或自然垂放，姿态轻松优雅。背景是高大的松树林，黄昏时分的金色阳光从树林间斜射进来，形成梦幻光束，地面有绿色蕨类植物，光影斑驳，温暖金色调，宁静唯美。

---

第2行和第3行（所有三列都是完整照片的水平切割）：

关键：第2行和第3行的每一列都是一张完整照片在服装边界或水平线处切割成的上下两部分。所有人物必须是同一个女性。

---

[单元格 2-1, 3-1] 左列 - 同一位女性的完整照片（水平切割）：

🔴**关键：这是同一张完整的人物摄影照片，在低腰裤腰带位置（背心下摆和裤子腰带的交界处）水平切割成上下两部分，必须完美对齐衔接。切割线位于服装边界，不在裸露皮肤上。人物和背景都是连续的。**🔴

**完整照片描述：**

- 同一位女性的全身照片，从头部到脚部完整展现

- 背景：阳光洒落的森林空地，温暖的自然光从侧面照射，背景有虚化的绿色植物和金色光斑，户外自然环境

- 视角：半侧面拍摄角度（3/4侧面视角），展现女性优雅的半侧面轮廓和身体曲线

- 服装：上半身穿明黄色字母印花短款露脐背心（NOMBRE3字样），紧身设计，露出腰部和腹部；下半身穿浅蓝色低腰紧身牛仔裤，从腰部到脚部，修身剪裁

- 姿势：双手优雅抬起轻触头发或托头，手臂自然弯曲，身体略微呈S形站姿，展现从头到脚的优美曲线

- 整体：运动健康身材，腰部完全露出，展现纤细腰线

🔴**切割说明：**🔴

- 🔴第2行（上半部分）：完整照片从头部到低腰裤腰带位置的上半部分。包含头部、双手、手臂、肩颈、胸部、整个明黄色短款背心（包括背心下摆）、露出的腰部和腹部皮肤。背景是虚化的绿色植物和金色光斑上半部分。**切割线位于背心下摆与低腰裤腰带的交界处**。🔴

- 🔴第3行（下半部分）：完整照片从低腰裤腰带位置到脚部的下半部分。包含低腰裤腰带（从腰带顶部开始）、臀部、腿部、脚部。背景是虚化的绿色植物和金色光斑下半部分。**切割线位于低腰裤腰带的顶部边缘**。🔴

🔴**对齐要求：2-1和3-1必须在低腰裤腰带位置（背心下摆与裤腰带交界处）完美切割，就像用一把刀将完整照片水平切开。切割线位于服装边界（浅蓝色裤腰带的顶部边缘），上下两格必须无缝衔接，裤腰带上下完美对齐，人物身体连续，背景连续，光线一致，没有任何错位或色差。**🔴

---

[单元格 2-2, 3-2] 中列 - 完整的海边日落风景照片（水平切割）：

**关键：这是同一张完整的海边日落风景照片，在海平面或海水中部的水平线位置切割成上下两部分，必须完美对齐衔接。**

**完整照片描述：**

一张完整的海边日落风景照片，从上到下依次包含：傍晚天空（橙粉色渐变）→ 深色海水（深蓝/暗青色，接近傍晚的深色海洋，海面平静或有轻微波纹）→ 浅色沙滩（浅米色或金色）。与第1行1-2场景相呼应，同样的海滩和日落氛围。整体营造浪漫宁静的日落氛围。

**切割说明：**

- 第2行（上半部分）：完整照片的上半部分，从顶部天空到海平面附近。包含傍晚天空（橙粉色渐变）和深色海水上半部分（深蓝/暗青色）。

- 第3行（下半部分）：完整照片的下半部分，从海平面到沙滩底部。包含深色海水下半部分和浅色沙滩。

**对齐要求：2-2和3-2必须在海平面或海水中部的水平线处完美切割，就像用一把刀将完整风景照片水平切开，上下两格必须无缝衔接，天空-海水-沙滩的过渡连续流畅，没有任何错位或色差。右侧边缘的海水颜色渐变为更深色调，与右侧绿色植物背景形成自然深色过渡。**

注：这个区域会被站立的3D女性图像大部分遮挡

---

[单元格 2-3, 3-3] 右列 - 同一位女性的完整照片（水平切割）：

🔴**关键：这是同一张完整的人物摄影照片，在运动裤腰带位置（运动背心下摆和运动裤腰带的交界处）水平切割成上下两部分，必须完美对齐衔接。切割线位于服装边界（白色或浅灰色腰带位置）。人物和背景都是连续的。**🔴

**完整照片描述：**

- 同一位女性的全身照片，从头部到脚部完整展现

- 背景：户外自然环境，柔和日光，虚化的绿色植物和树木背景（类似公园或林间小道），自然光从侧面照射，温暖明亮的氛围

- 视角：右侧面拍摄角度，展现女性的右侧轮廓

- 服装：上半身穿深灰色或黑色无袖紧身运动背心；下半身穿黑色运动紧身裤，腰部有浅灰色或白色宽腰带装饰

- 姿势：侧身站立，朝向右边，面部朝向画面右侧，右手优雅向上伸展，手臂舒展呈柔美弧线，左手自然垂放。头部随着手臂动作自然后仰或侧仰，面部朝向右侧（可能闭眼或仰望），双腿自然并拢站立，身体挺直

- 整体：运动健康身材，从右侧面展现从头到脚的优美身体曲线

🔴**切割说明：**🔴

- 🔴第2行（上半部分）：完整照片从头部到运动裤腰带位置的上半部分。包含头部、右手臂伸展、肩颈、胸部、整个深灰色/黑色运动背心、腰部。背景是虚化的绿色植物和自然光上半部分。**切割线位于运动背心下摆与运动裤腰带（浅灰色或白色宽腰带）的交界处**。🔴

- 🔴第3行（下半部分）：完整照片从运动裤腰带位置到脚部的下半部分。包含运动裤腰带（浅灰色或白色宽腰带，从腰带顶部开始）、臀部、腿部、脚部。背景是虚化的绿色植物和自然光下半部分（可能有地面小路或草地）。**切割线位于运动裤腰带的顶部边缘**。🔴

🔴**对齐要求：2-3和3-3必须在运动裤腰带位置（运动背心下摆与腰带交界处）完美切割，就像用一把刀将完整照片水平切开。切割线位于服装边界（浅灰色或白色宽腰带的顶部边缘），上下两格必须无缝衔接，腰带上下完美对齐，人物身体连续，背景连续，光线一致，没有任何错位或色差。**🔴

---

站立3D图层（最重要）：

同一位女性的高质量3D渲染全身图像

位置：站立在整个9宫格中央位置，双脚踩在底部网格线上（第3行底部边缘），身体从底部延伸向上，覆盖中间列的2-2和3-2区域以及部分周边

风格：超现实主义3D数字渲染，C4D或Blender高级渲染效果，性感时尚风格

服装：

- 上衣：灰白迷彩图案无袖背心吊带，修身剪裁，露背低背设计

- 下装：浅蓝色超短牛仔热裤，磨白做旧效果，后口袋缝线细节明显，极短长度露出大部分修长美腿

- 鞋履：白色运动鞋搭配白色短袜

姿势：

- 侧身站立，身体呈3/4侧面角度，背对镜头为主

- 头部微微侧转回望镜头，展现侧脸或半侧脸

- 身体重心略偏向一侧，形成性感S形曲线

- 臀部微微向后突出，强调身材曲线

- 一只手自然放在身体侧面或轻触臀部腰部，动作自然放松

- 双腿自然站立，双脚稳稳地踩在地面上（网格底部边缘），展现站立姿态

- 长发自然垂落在肩部和背部

- 整体呈现性感但不做作的"回眸杀"pose

3D效果特征：

- 强烈的立体阴影投射在背景网格上，双脚与地面接触处有清晰的接地阴影

- 明显的景深效果，人物清晰，背景略微虚化

- 人物边缘有柔和的光晕或发光效果

- 皮肤和服装材质有3D渲染的高级质感（高光、反射、次表面散射）

- 周围有漂浮的几何元素、粒子或光效

- 光影：3D人物实体且清晰，投射自然柔和的阴影，特别是双脚与地面接触处有明显的接地感，人物像是真实站立在网格之上

---

技术要求：

- 所有单元格必须是完美的正方形且大小相等

- 所有场景的女性必须是同一个人，面部特征、发型、身材完全一致

- 第1行三个场景：超高清画质，色调统一协调，电影级光影效果

- 🔴所有三列（2-1/3-1, 2-2/3-2, 2-3/3-3）：都是完整照片在服装边界或水平线处的水平切割，切割线位于衣服边缘（裤腰带位置），上下两格必须像被刀切开的照片一样完美对齐衔接🔴

- 所有三列的背景都必须上下连续，人物身体连续，光线一致

- 3D站立图像必须有强烈的空间层次感、接地感和性感时尚感

- 阴影、光晕、景深效果自然真实

- 超清晰焦点，4K质量

- 整体色调和谐统一，现代时尚高级感

```

- ## 我将大佬的九宫格模板改成了萌宠的版本，这个效果的亮点在于打破2D跟3D放之间的界限，小动物就像冲出来一样
- https://x.com/Leslieyu0/status/2000481003023057133

```prompt
Surreal 3x3 grid collage with THICK WHITE LINES.
Background shows [小动物详细描述] in 8 different cute behaviors and angles (yawning, sleeping, playing, tilting head, close-up of paws). CENTER CELL HIDDEN.
OVERLAIID by a massive hyper-realistic full-body 3D cut-out of the SAME [小动物详细描述] jumping forward out of the grid playfully. 
ALL elements sharp, deep depth of field f/16, no bokeh, bright softbox lighting to highlight fur texture, tactile fluffy details, strong 3D pop-out effect, 8k resolution, C4D render style --qr 2:3 --v 6.1
```

- 这个做法要用分层逻辑：上下两层
  - 最大的问题是：你告诉模型生成9宫格就会生成12个
  - 原因是9宫格中间那个被挡住了，模型会幻觉

```prompt
Create a 2:3 portrait fashion poster featuring THE SAME WOMAN in THE SAME OUTFIT shown in 9 different magazine editorial styles with 3D pop-out effect:
CHARACTER CONSISTENCY (CRITICAL - HIGHEST PRIORITY):
THE SAME female fashion model appears in ALL 9 positions:
- Same face, same facial features, same skin tone, same body type
- Cold-beauty aesthetic: sharp jawline, high cheekbones, aloof minimalist expression
- Early-20s Chinese/Korean fashion model with editorial face
- Her identity NEVER changes across all 9 appearances
```

- ## [Comparison of Seedream 4.5 vs Nano Banana Pro using the same prompt : r/createimg](https://www.reddit.com/r/createimg/comments/1pdxgl1/comparison_of_seedream_45_vs_nano_banana_pro/)
  - Five shimmering goldfish weave through crevices between stones; four are red-and-white, while one is silver-white. By the pond's edge, a golden-shaded British Shorthair cat watches them intently, counting on blind luck. Watercolor style.

- ## [New stealth model "microwave" now available - free during alpha : r/CLine](https://www.reddit.com/r/CLine/comments/1pcasak/new_stealth_model_microwave_now_available_free/)
  - 饱和度很高的油画

- ## [Flux2: decreased style decay from long prompting! (part 1.5) : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1pb7hbf/flux2_decreased_style_decay_from_long_prompting/)
  - 风格统一的插画

- ## [Even more improved Z-Image Turbo variation : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1p9mypu/even_more_improved_zimage_turbo_variation/)

- ## [This is offiZially crazy! (Z_Image) : r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/comments/1p9f7ic/this_is_offizially_crazy_z_image/)
  - 手掌里面显示logo字母
