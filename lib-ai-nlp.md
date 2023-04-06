---
title: lib-ai-nlp
tags: [ai, nlp]
created: 2023-03-03T08:06:19.133Z
modified: 2023-03-03T08:06:36.592Z
---

# lib-ai-nlp

# guide

- [NLP新宠——浅谈Prompt的前世今生 - 知乎](https://zhuanlan.zhihu.com/p/399295895)
- [通俗易懂地理解Prompt - 知乎](https://zhuanlan.zhihu.com/p/436340881)
  - Prompt是给input加的一段文字或一组向量，让模型根据input和外加的prompt做masked language modeling (MLM)。
# nlp-products

# translation
- https://github.com/mozilla/firefox-translations
  - a webextension that enables client side translations for web browsers.
  - 不支持中文
  - [Support Chinese translations](https://github.com/mozilla/firefox-translations/issues/583)

- https://github.com/jelmervdl/translatelocally-web-ext
  - https://translatelocally.com/
  - a web-extension that enables client side in-page translations for web browsers.
  - 不支持中文
  - Differences from Firefox Translations
    - Uses models from https://github.com/browsermt/students
    - Translation engine and memory is shared among all tabs and webpages
  - [Google Chrome](https://github.com/jelmervdl/translatelocally-web-ext/issues/10)

- 使用Google翻译（Translate）的离线翻译功能？有前提：你必须先在联网状态下将需要且支持离线翻译的语言下载。
  - 而离线翻译的结果会与联网翻译的结果存在结果差距。特别是翻译同一个字词语句下

- 全文翻译比较期待类似firefox做的这种离线本地翻译
  - [Firefox Translations – Get this Extension for 🦊 Firefox (en-US)](https://addons.mozilla.org/en-US/firefox/addon/firefox-translations/)

## translate-api

- https://github.com/LibreTranslate/LibreTranslate
  - https://libretranslate.com/
  - Free and Open Source Machine Translation API. 
  - Self-hosted, offline capable and easy to setup.
  - its translation engine is powered by the open source Argos Translate library.
  - 依赖flask
- https://github.com/argosopentech/argos-translate
  - Open-source offline translation library written in Python
  - Argos Translate uses OpenNMT for translations
  - 支持中日韩
# blogs

## [Large language model - Wikipedia](https://en.wikipedia.org/wiki/Large_language_model)

- A large language model (LLM) is a language model consisting of a neural network with many parameters (typically billions of weights or more), trained on large quantities of unlabelled text using self-supervised learning. 
  - LLMs emerged around 2018 and perform well at a wide variety of tasks. 
  - This has shifted the focus of natural language processing research away from the previous paradigm of training specialized supervised models for specific tasks.

## [Sage Gpt-4 Claude+ ChatGPT Dragonfly五个AI的各自特点 - 知乎](https://zhuanlan.zhihu.com/p/614720305)

- 看来回答和之前聊天的内容相关性非常高，复制你的问题问了2遍，吐给我的内容每个格子都很不一样

- [Claude生不逢时！谷歌想扶持自己的OpenAI实在太难了\_腾讯新闻](https://new.qq.com/rain/a/20230318A03HF300)
  - 由前OpenAI员工创办的新公司Anthropic打造的Claude正式宣布开放申请，也是为数不多能跟ChatGPT打个平手的模型
  - Claude模型并没有图像处理的能力，Anthropic也没有这方面的技术积累，而OpenAI发布的DALL-E 2在图像生成领域依然是领军者。
  - Claude 和 ChatGPT 都依赖于强化学习(RL)来训练偏好（preference）模型，被选中的回复内容将在后续用于模型的微调，只不过具体的模型开发方法不同。
  - Quora 通过人工智能聊天应用程序Poe 向用户提供Claude的对话能力。
  - Claude 与 Notion 合作以提高工作和学习场景中的生产力。

## [通向AGI之路：大型语言模型（LLM）技术精要 - 知乎](https://zhuanlan.zhihu.com/p/597586623)

- 通用人工智能 （AGI，Artificial General Intelligence）

### 范式转换1.0: 从深度学习到两阶段预训练模型

- 这个范式转换所涵盖的时间范围，大致在深度学习引入NLP领域（2013年左右），到GPT 3.0出现之前（2020年5月左右）。
- 在Bert和GPT模型出现之前，NLP领域流行的技术是深度学习模型，而NLP领域的深度学习，主要依托于以下几项关键技术：以大量的改进LSTM模型及少量的改进CNN模型作为典型的特征抽取器；以Sequence to Sequence（或叫encoder-decoder亦可）+Attention作为各种具体任务典型的总体技术框架。
- 在这些核心技术加持下，NLP领域深度学习的主要研究目标，如果归纳一下，是如何有效增加模型层深或模型参数容量。就是说，怎么才能往encoder和decoder里不断叠加更深的LSTM或CNN层，来达成增加层深和模型容量的目标。这种努力，尽管确实不断增加了模型层深，但是从解决具体任务的效果角度看，总体而言，不算很成功，或者说和非深度学习方法相对，带来的优势不算大。
- 深度学习之所以不够成功，我认为主要原因来自于两个方面：
  - 一方面是某个具体任务有限的训练数据总量。随着模型容量的增加，需要靠更大量的训练数据来支撑，否则即使你能把深度做起来，任务效果也做不上去。而在预训练模型出现之前，很明显这是NLP研究领域一个严重问题；
  - 另外一个方面是LSTM／CNN特征抽取器，表达能力不够强。意思是就算给你再多的数据也没用，因为你不能有效地吸收数据里蕴含的知识。主要应该是这两个原因，阻碍了深度学习在NLP领域的成功突围。

- Bert/GPT这两个预训练模型的出现，无论在学术研究角度看，还是工业应用角度来看，都代表了NLP领域的一个技术飞跃，并带来了整个领域研究范式的转换。
- 这种范式转换带来的影响，体现在两个方面：
  - 首先，是部分NLP研究子领域的衰退乃至逐步消亡；
  - 其次，NLP不同子领域的技术方法和技术框架日趋统一，在Bert出现后一年左右，技术栈基本收敛到两种技术模式中。 

- 影响一：中间任务的消亡
  - 典型的中间任务包括：中文分词、词性标注、NER、句法分析、指代消解、语义Parser等，这类任务一般并不解决应用中的实际需求，大多数是作为那些解决实际需求任务的中间阶段或者辅助阶段存在的
  - 但是自从Bert／GPT出现之后，其实就没有必要做这些中间任务了，因为通过大量数据的预训练，Bert／GPT已经把这些中间任务作为语言学特征，吸收到了Transformer的参数里，此时我们完全可以端到端地直接解决那些最终任务，而无须对这种中间过程专门建模。

- 影响二：不同研究方向技术路线的统一
  - 大多数NLP子领域的研发模式切换到了两阶段模式：模型预训练阶段+应用微调（Fine-tuning）或应用Zero／Few Shot Prompt模式。
  - 更准确地说，NLP各种任务其实收敛到了两个不同的预训练模型框架里：
  - 对于自然语言理解类任务，其技术体系统一到了以Bert为代表的“双向语言模型预训练+应用Fine-tuning”模式；
  - 而对于自然语言生成类任务，其技术体系则统一到了以GPT 2.0为代表的“自回归语言模型（即从左到右单向语言模型）+Zero /Few Shot Prompt”模式。

### 范式转换2.0: 从预训练模型走向通用人工智能 （AGI，Artificial General Intelligence）

- 这个范式转换所涵盖的时间范围，大致在GPT3.0出现之后（20年6月左右），一直到目前为止，我们应该正处于这个范式转换过程中。
- ChatGPT是触发这次范型转换的关键节点，但是在InstructGPT出现之前，其实LLM处于这次范式转换前的一个过渡期。
- 过渡期：以GPT 3.0为代表的“自回归语言模型+Prompting”模式占据统治地位
- 在预训练模型发展的早期，技术框架收敛到了Bert模式和GPT模式这两种不同的技术范型，而且人们普遍更看好Bert模式一些
- 随着技术的继续发展，你会发现，目前规模最大的LLM模型，几乎清一色都是类似GPT 3.0这种“自回归语言模型+Prompting”模式的，比如GPT 3、PaLM、GLaM、Gopher、Chinchilla、MT-NLG、LaMDA等，没有例外。
- 我认为可能主要源于两个原因。
- 首先，Google的T5模型，在形式上统一了自然语言理解和自然语言生成任务的外在表现形式。在T5模型里，这些自然语言理解问题在输入输出形式上和生成问题保持了一致，也就是说，可以把分类问题转换成让LLM模型生成对应类别的字符串，这样理解和生成任务在表现形式就实现了完全的统一。
- 第二个原因，如果想要以零示例提示语（zero shot prompting）或少数示例提示语（few shot prompting）的方式做好任务，则必须要采取GPT模式。
  - 现在已有研究（参考：On the Role of Bidirectionality in Language Model Pre-Training）证明：
  - 如果是以fine-tuning方式解决下游任务，Bert模式的效果优于GPT模式；
  - 若是以zero shot/few shot prompting这种模式解决下游任务，则GPT模式效果要优于Bert模式。
  - 这说明了，生成模型更容易做好zero shot/few shot prompting方式的任务，而Bert模式以这种方式做任务，是天然有劣势的。这是第二个原因。

- 如果理解了上述逻辑，很容易得出如下结论：few shot prompting（也被称为In Context Learning）只是一种过渡时期的技术。如果我们能够更自然地去描述一个任务，而且LLM可以理解，那么，我们肯定会毫不犹豫地抛弃这些过渡期的技术，原因很明显，用这些方法来描述任务需求，并不符合人类的使用习惯。
- 这也是为何我将GPT 3.0+Prompting列为过渡期技术的原因，ChatGPT的出现，改变了这个现状，用Instruct取代了Prompting，由此带来新的技术范式转换，并产生若干后续影响。
# discuss
- ## 

- ## If I were to learn about convolutional networks, residual networks, and automatic differentiation, how much do those relate to large language models?
- https://twitter.com/fabiospampinato/status/1637835546738212867
- Convolutions(卷积): they seem to be mainly used for vision, as they are kinda based on the assumption that closer together "pixels" are related, not much to do with LLMs. Although where vision ends and language starts is blurry.
- ResNet: I don't know how this works, but I don't think it's used in LLMs much, if at all, the main building block should be the "Transformer".
- Autodiff: I think that's basically how ~all these neural networks are trained, propagating inputs forward all the way, then at each layer from the output layer calculating the error, and nudging weights and biases toward what you want.
- After that I'm not sure, because that's more or less where I'm at at the moment 🤣 It may be worth checking out LSTMs, maybe RNNs... at some point transformers... generally trying to reproduce existing tiny things, building intuition, should be would be super useful for learning.

- ## I just used OpenAI embeddings to embed half a million tweets and ended up paying ... $3!!!
- https://twitter.com/fleuria__/status/1634125805717704704
- 本义是说把过往做法中维度成千上万的特征（每个词项以及数十种人工特征构造一个巨大的one-hot）像镶钻一样嵌入(embed)一个低维流形（想象一个2维描述的三维球面），优化算法会想办法调整这些特征在球面上嵌入的位置。每个词项就需要对应它的低维表示，存下来的东西实质上就是个KV查询表(embedding)。
  - 只不过发展到现在不一定这个embedding就真的是低维度了（
  - 几十个词把embedding设成256等等之类的也很常见（
  - 甚至有研究表示over-parameterize才是正道（
