---
title: lib-viz-d3-dev
tags: [charting, d3, viz]
created: 2019-08-01T05:09:11.917Z
modified: 2020-12-08T13:32:22.331Z
---

# lib-viz-d3-dev

# guide

- d3-ecosystem
  - vega: academic supported
  - plotly: multi-lang, company-promoted
# faq

## `sel.datum()` vs `sel.data()`

- `sel.datum([value])` vs `sel.n.data([values[, key]])`
  - only the `data()` function accepts a `key`
  - data() performs a join, datum() does not

- [What is the difference D3 datum vs. data?](https://stackoverflow.com/questions/13728402)
- when you invoke selection.data and selection.datum with an input data parameter, different
  - Even in that scenario, the two behave differently if the selection is a single element versus when it contains multiple elements
- both can also be invoked without any input arguments, different again

- **When supplying data as an input argument**
- `selection.data(data)` will attempt to perform a data-join between the items of the data array with the selection resulting in the creation of enter(), exit() and update() selections that you can subsequently operate on. 
  - The end result of this is if you pass in an array `data = [1, 2, 3]`, an attempt is made to join each individual data item (i.e. datum) with the selection. 
  - Each element of the selection will only have a single datum item of data bound to it.
- `selection.datum(data)` bypasses the data-join process altogether. 
  - This simply assigns the entirety of data to all elements in the selection as a whole without splitting it up as in the case of data-joins. 
  - So if you want to bind an entire array data = [1, 2, 3] to every DOM element in your selection, then selection.datum(data) will achieve this.
- Many people believe that `selection.datum(data)` is equivalent to `selection.data([data])` but this is only true if selection contains a single element. 
- If selection contains multiple DOM elements, then `selection.datum(data)` will bind the entirety of data to every single element in the selection. 
  - In contrast,  `selection.data([data])` only binds the entirety of data to the first element in selection. This is consistent with the data-join behavior of selection.data.

- **When supplying no data input argument**
- `selection.data()` will take the bound datum for each element in the selection and combine them into an array that is returned. 
  - So, if your selection includes 3 DOM elements with the data "a", "b" and "c" bound to each respectively, selection.data() returns ["a", "b", "c"]. 
  - It is important to note that if selection is a single element with (by way of example) the datum "a" bound to it, then selection.data() will return `["a"]` and not "a" as some may expect.
- `selection.datum()` only makes sense for a single selection as it is defined as returning the datum bound to the first element of the selection. 
  - So in the example above with the selection consisting of DOM elements with bound datum of "a", "b" and "c", selection.datum() would simply return "a".
- Note that even if selection has a single element, selection.datum() and selection.data() return different values. 
  - The former returns the bound datum for the selection ("a" in the example above) whereas the latter returns the bound datum within an array (["a"] in the example above).

- [When to use .datum() and .data()?](https://stackoverflow.com/questions/13181194)
- the API reference on `selection.datum` gives the accepted answer:
  - Gets or sets the bound data for each selected element. 
  - Unlike the `selection.data` method, this method does not compute a join (and thus does not compute enter and exit selections).
  - Since it does not compute a join, it does not need to know a `key`.
- @Hugolpz' gist gives nice examples of the significance of "groups" vs "individuals". Here, json represents an array of data. 
  - Notice how datum binds the entire array to one element. 
  - If we want to achieve the same with data we must first put json inside another array.
- var chart = d3.select("body").append("svg").data([json])
- var chart = d3.select("body").append("svg").datum(json)

- ref
- [Understanding the difference between the d3 data and datum methods](https://www.intothevoid.io/data-visualization/understanding-d3-data-vs-datum/)
# pieces
- Mike Bostock的外边距约定
  - http://bl.ocks.org/mbostock/3019563
- 剪切路径clip-path会将svg边界上和边界外的元素超出svg矩形的部分隐藏
# summary
- d3绘图套路

```js
svg.selectAll('rect')
  .data(dataset)
  .enter()
  .append('circle')
  .attr()
```

- 核心api
  - data()
  - enter()
  - exit()
  - transition()
- data vs datum
  - data 将一个数组的各项分别绑定到各元素上
  - datum 将数组本身绑定到各元素上
- attr()用于设置DOM属性，style()用于设置css样式
  - 添加样式1 selection.attr('class', 'title')
  - 添加样式2 selection.style('width', 240px)
  - 添加样式3 selection.classed('title', true)
- 数据更新
  - 数量不变，值变化 enter()
  - 数量变多 enter()
  - 数量变少 exit()
- transition()默认插值间隔是250ms
  - duration() ms
  - ease() 
  - delay() ms
- 坐标轴3部分
  - 轴线(注意：坐标轴要与比例尺关联)
  - 刻度线
  - 文本标签

- d3.svg.arc()
  - disk 圆形
  - sector 扇形
  - annulus 圆环
  - annular sector 环形扇区
- 约定
  - tooltip 鼠标提示
  - label 数据标注
# blogging

## [mbostock: 10 Years of Open-Source Visualization](https://observablehq.com/@mbostock/10-years-of-open-source-visualization)

- In honor of D3 1.0’s tin anniversary, I thought I’d reflect on lessons learned.

### 1. Teaching is the most impactful aspect of tool building.

- When building a tool, it’s easy to forget how much you’ve internalized: how much knowledge and context you’ve assumed. 
- Your tool can feel familiar or even obvious to you while being utterly foreign to everyone else. 
- If your goal is for other people to use the darn thing, you gotta help people use it! 
- It doesn’t matter what’s possible or what you intended; all that matters is whether people actually succeed in practice.
- To maximize your impact, then, teaching must be central to your strategy. 
  - This means documentation, tutorials, examples, videos, tweets, and more. 
  - a library of material that teaches without requiring your time is the only way to scale as your audience grows.
  - I’m frequently inspired by (and occasionally envious of) the brilliant teaching styles of Rich Harris and Dan Abramov.
- **Of all forms of documentation, examples seem to be the most effective**.
- I’ve long espoused the merits of examples, and both Observable and its predecessor bl.ocks.org aim to help people produce and consume examples to accelerate learning.
- Yet perhaps examples are too powerful: they can compensate for a hard-to-use API and foster a dependency on copy-paste. 
  - Was D3 successful not because it was a great tool, but because it came with so many examples? 🤷‍♂️ 
  - Even though I’m the author, I can’t remember how to use d3.stack and copy-paste the stacked area example like everyone else. 
- Working backwards from an example rather than forwards from data can also be a mistake for visualization (see #5).
- And examples have limitations: an example teaching a specific technique may not be broadly representative of “real-world” usage.

### 2. Community support is a powerful means of research

- The only way to recognize — and then bridge — the gulf of understanding between you and people using your tool is to observe their struggles and talk to them. 
- It’s amazing how quickly glaring flaws are revealed this way. 
- Answering questions on Stack Overflow (or GitHub, Twitter, Slack, or wherever else) is not a selfless act of altruism(无私); 
  - it’s a chance to learn, to find where people struggle and hear their perspective.
- Each question is an opportunity to help one individual, 
  - but that question can also inspire a tutorial, an example, or even a feature that prevents others from hitting the same issue.
  - the countless ideas and criticisms from users that can be channeled into improvements and documentation by maintainers.
- But there’s also a limit. 
  - As one person, you can’t help everyone. 
  - And you can’t make everyone happy because your tool is only a tiny part of their life. 
- Don’t make that your goal: focus on learning and broadening your perspective.
- **If it stops being constructive for you, then stop**. Period. And don’t feel bad! 
- I have deep reservations about the way GitHub and other platforms enable issues by default, establishing the unreasonable expectation that unpaid maintainers must immediately, politely, and substantively respond to any and all requests for help. 
  - Yes, I can turn off issues, but as a community we need to rethink our norms if we are serious about addressing maintainer burnout.

### 3. Beware bells and whistles: interaction, animation, and other technical whiz-bangery(专家爆竹) have a cost

- Interaction and animation have a huge wow factor, especially for audiences who encounter them infrequently.
- Knowing this, you may be tempted to add these features to visualizations without fully appreciating the downsides, 
  - such as added complexity and hiding valuable information behind interactive controls. 
- And worse, because these features are often challenging to implement, **they may distract you from the far more important yet “boring” task** of finding and communicating insight!
- This is not a moral judgment. I’m not saying you’re bad for doing this. I’m guilty of this myself. But the pitfall is real. 
- **Focus on the static form first and foremost**. This may be the only thing some readers see. 
- Don’t allow technical matters (i.e., web development) to eat too much of your attention. 
- And don’t fear plain visualizations: it’s the insight that matters, not whether it’s gussied up(打扮得花枝招展).
- So where should interaction be used? Primarily exploratory visualization (see #4). 
  - Gregor Aisch’s [In Defense of Interactive Graphics](https://www.vis4.net/blog/2017/03/in-defense-of-interactive-graphics/) is a good post on the subject.

### 4. Visualization is a spectrum: from exploratory to explanatory.

- Not all visualizations serve the same purpose. 
  - Exploratory graphics you make for yourself to find new insights in data. 
  - Explanatory graphics in contrast communicate some already-known insight to an audience. 
  - **When designing, know where you are on the spectrum**.
- The goal of exploratory visualization is primarily speed: 
  - how quickly can you construct a view that answers your question? 
  - You can afford to cut corners when you’re the intended reader as you already have context. 
- Whereas you must provide explicit context for an explanatory graphic. 
  - A good explanatory graphic should know what it’s trying to say and say it. 
  - Explanatory graphics can include exploratory elements, for example allowing the reader to “see themselves” in the data, but ideally these shouldn’t detract from the primary message. 
  - Don’t make the reader work for insight; that’s your job as editor.

### 5. In most cases, working with data should be 80% of the work of visualization.

- Visualization is the end result of analysis — the visible manifestation of data, to be seen, shared, and appreciated by experts and non-experts alike — and as such it sometimes gets too much credit. 
- To produce a visualization, one must first find data, clean it, transform, join, model, etc. 
- Working with data is sometimes needlessly denigrated(贬低，诋毁) as “janitorial(看门人)” when it represents the critical step of understanding the data as it is, warts and all(包括所有缺点，不管什么缺点). 
- With data in the right form, the process of applying visual encodings may be comparatively straightforward (assuming you heed #3). 
- Hence the **D3 modules that I reach for most are d3-array and d3-dsv**. 
- And I’m delighted to see new JavaScript tools for data such as tidy.js and Arquero. 

### 6. Don’t commit to a specific visual form before seeing your data in it.

- A given visual form — say the pie chart or treemap — isn’t “good” or “bad” in an absolute sense, but it may or may not be appropriate to your data and the specific question you want answered. 
- **The only way to know whether a form is effective is if it communicates: you must put your data in it and see**. 
- So don’t set out to use a specific form; 
  - instead **set out to answer a specific question of your data**.
- If it’s hard to get your data into an example (see #1), you are incented(刺激，推动) to commit to a specific form before you can confirm its effectiveness
- The less effort it takes to sketch a visualization, the more variations you can afford to try and the better the final result. 
- This is why Observable tries to help you get your data in quickly, say replacing a file with one click, or letting your edit code without forking it. 
- Yet if your data has an incompatible structure, it might still be a lot of work (see #5). 
- And D3, being designed for bespoke explanatory graphics, requires more effort than something like Vega-Lite which is intended for exploratory graphics; 

### 7. 10% of code causes 90% of bugs.

- some code is far more bug-prone than other code. 
- That’s not because the buggy code is somehow lower quality 
  - but because it’s trying to do something inherently harder or underspecified.
- **For D3, the interactive behaviors are the big losers** (winners?) in the bug contest: d3-zoom, d3-drag, and d3-brush. 
- It’s hard to reason through, let alone test, all possible sequences of asynchronous events. 
- And interaction is ambiguous: are you clicking? dragging? panning? selecting? about to double-click?
- Compounding the challenge, browsers change and unilaterally “break the web” as Chrome did with passive event listeners.
- This suggests you may be able to save yourself some trouble by **choosing carefully which problems you try to solve and which you don’t**.
  - For example, if you can build your interface using Observable’s inputs and dataflow rather than low-level event listeners, you’ll have less to worry about.

### 8. The internet will make you feel bad.

- No matter how good your work is, if you put yourself out there someone on the internet will say something hurtful and make you feel bad.
- I am very proud of D3 but I maintain a collection of mean tweets people have shared about it. This is my process; don’t judge me
- So if you find yourself complaining on the internet, please think about the practical impact of your words. 
  - If it’ll only discourage and contribute to burnout, maybe vent offline? 
  - Or better: think about how you can personally contribute to **make the tool better**, either through pull requests or documentation or support. 
  - That, after all, is the beauty of open source.

### 9. Don’t go it alone.

- To avoid entrusting your emotional wellbeing to internet randos (see #8), you must develop relationships with a small, stable group of people that you respect. 
- In other words, find a team (or community) that can provide validation, feedback, support, and mentorship. 
- Maybe this is obvious to everyone but me — yes, Mike, friends are good — but I feel like it’s worth repeating today when so much human interaction happens at a distance. 
- I’m also excited about the potential for Observable to create shared virtual spaces for collaboration, where it’s not about showing off (as on Twitter) but about **working together with peers in realtime to find insight and solve problems**.

### 10. Try to have a good time.

- This is personal, but I try to reflect on which parts of my life and work I enjoy and spend more time doing that.
- It sounds simple and trite but it’s hard to do in practice! 
- If you know what you enjoy then you will have fewer regrets when and if you do fail (always an option)
- And paradoxically, rather than detracting from your goals it may help you succeed as you are better able to persevere: **work you enjoy is more easily sustained**
- I love building tools. I can’t predict if they will succeed, but I love solving puzzles and developing abstractions, and I love seeing what people do with my creations. 
- On the other hand I find public speaking anxiety-inducing, even knowing the positive impact talks can have
- So if you’re disappointed I’m not giving more talks, hopefully it’s because I’m heads-down building something new. 

- ### discuss
- https://twitter.com/mbostock/status/1364263392555327490
# ref
- [Adding Graphics to a React App with D3.js_202010](https://dev.to/search?q=Adding%20Graphics%20to%20a%20React%20App%20with%20D3&filters=class_name: Article&sort_by=published_at&sort_direction=desc)
