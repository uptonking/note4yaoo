---
title: lib-search-blog
tags: [blog, search]
created: 2023-01-03T14:52:42.477Z
modified: 2023-01-03T14:52:51.355Z
---

# lib-search-blog

# guide
- tips
  - 传统全文搜索的效果不如llm，因为llm可以用英文数据训练，然后用中文搜索
# blogs-search-engine

## [全文检索的索引设计 - 知乎](https://zhuanlan.zhihu.com/p/520001238)

- 全文检索是一种检索方式，通过扫描每个token生成term, 并为每个term来构建索引，并指出每个term在文档中的数量以及位置。它按照内容进行检索，检索的对象为文档。
- 检索的目标是判断查询与候选文档集的匹配程度。在现实生活中，我们评价事物之间的相关性是基于掌握的知识。目前存在几种模型来评价查询与文档之间的匹配度。比如：布尔模型，向量空间模型和概率模型
- 向量空间模型把查询和文档以向量的形式表示，从而将检索相关性转化为向量空间中向量的相似性。
- 向量空间模型由如下要素组成：
  - 查询
  - 文档
  - 分词term
  - 分词term的权重
- 计算文档相似度传统方法是将文档转换为向量，然后根据线性代数来计算相似性。
  - 将文档看成一系列词Term，每一个词Term都有一个权重，不同的词根据自己在文档中的权重来影响文档相关性的计算。
  - 我们将所有搜索出的文档向量与查询向量放一个N维空间中，每个词代表一个维度。
  - 二个向量之间夹角越小，相关性就越大。通过计算夹角的余弦值作为相关性的打分，夹角越小，余弦值越大，打分越高，相关性越大
  - 向量空间模型是检索系统中最常见且重要的模型。

## [全文搜索基本原理（倒排索引、搜索结果排序） - March On - 博客园](https://www.cnblogs.com/z-sm/p/12071009.html)

- 结构化数据有固定格式或有限长度，故容易构建索引，从而搜索很快；
  - 而非结构化数据（也称全文数据）无固定格式或长度无限制，故搜索慢。
- 如何有效检索非结构化数据？整体思路是从非结构化数据中提取一些信息组织成方便检索的结构化数据，这些提取出的信息就是非结构化数据的索引。
- 全文搜索（也称非结构化数据搜索，因为非结构化数据另一叫法即全文数据）可以认为是搜索引擎最重要的功能，涉及的最重要的原理有两个：倒排索引、搜索结果排序

## [文本挖掘的分词原理 - 刘建平Pinard - 博客园](https://www.cnblogs.com/pinard/p/6677078.html)

- 现代分词都是基于统计的分词，而统计的样本内容来自于一些标准的语料库。
  - 利用语料库建立的统计概率，对于一个新的句子，我们就可以通过计算各种分词方法对应的联合分布概率，找到最大概率对应的分词方法，即为最优分词。
- 我们一般称只依赖于前一个词的模型为二元模型(Bi-Gram model)，而依赖于前两个词的模型为三元模型。
  - 以此类推，我们可以建立四元模型，五元模型, ... 一直到通用的NN元模型。越往后，概率分布的计算复杂度越高。当然算法的原理是类似的。
  - 在实际应用中，NN一般都较小，一般都小于4，主要原因是N元模型概率分布的空间复杂度为O(|V|N)O(|V|N)，其中|V||V|为语料库大小，而NN为模型的元数，当NN增大时，复杂度呈指数级的增长。
- NN元模型的分词方法虽然很好，但是要在实际中应用也有很多问题，
  - 首先，某些生僻词，或者相邻分词联合分布在语料库中没有，概率为0。这种情况我们一般会使用拉普拉斯平滑，即给它一个较小的概率值，这个方法在朴素贝叶斯算法原理小结也有讲到。
  - 第二个问题是如果句子长，分词有很多情况，计算量也非常大，这时我们可以用下一节维特比算法来优化算法时间复杂度。
- 对于一个有很多分词可能的长句子，我们当然可以用暴力方法去计算出所有的分词可能的概率，再找出最优分词方法。
  - 但是用维特比算法可以大大简化求出最优分词的时间。
  - 大家一般知道维特比算法是用于隐式马尔科夫模型HMM解码算法的，但是它是一个通用的求序列最短路径的方法，不光可以用于HMM，也可以用于其他的序列最短路径算法，比如最优分词。
  - 维特比算法采用的是动态规划来解决这个最优分词问题的，动态规划要求局部路径也是最优路径的一部分，很显然我们的问题是成立的。
- 简单的英文分词不需要任何工具，通过空格和标点符号就可以分词了，而进一步的英文分词推荐使用nltk。对于中文分词，则推荐用结巴分词（jieba）。

- 在做了分词后，如果我们是做文本分类聚类，则后面关键的特征预处理步骤有向量化或向量化的特例Hash Trick
- 词袋模型(Bag of Words, 简称BoW)。词袋模型假设我们不考虑文本中词与词之间的上下文关系，仅仅只考虑所有词的权重。而权重与词在文本中出现的频率有关。
- 词袋模型首先会进行分词，在分词之后，通过统计每个词在文本中出现的次数，我们就可以得到该文本基于词的特征，如果将各个文本样本的这些词与对应的词频放在一起，就是我们常说的向量化。
  - 向量化完毕后一般也会使用TF-IDF进行特征的权重修正，再将特征进行标准化。 
  - 再进行一些其他的特征工程后，就可以将数据带入机器学习算法进行分类聚类了。
- 总结下词袋模型的三部曲：分词（tokenizing），统计修订词特征值（counting）与标准化（normalizing）。
- 与词袋模型非常类似的一个模型是词集模型(Set of Words, 简称SoW)，和词袋模型唯一的不同是它仅仅考虑词是否在文本中出现，而不考虑词频。也就是一个词在文本在文本中出现1次和多次特征处理是一样的。在大多数时候，我们使用词袋模型
- 词袋模型有很大的局限性，因为它仅仅考虑了词频，没有考虑上下文的关系，因此会丢失一部分文本的语义。但是大多数时候，如果我们的目的是分类聚类，则词袋模型表现的很好。
- 由于大部分的文本都只会使用词汇表中的很少一部分的词，因此我们的词向量中会有大量的0。也就是说词向量是稀疏的。在实际应用中一般使用稀疏矩阵来存储。
- 向量化的方法很好用，也很直接，但是在有些场景下很难使用，比如分词后的词汇表非常大，达到100万+，此时如果我们直接使用向量化的方法，将对应的样本对应特征矩阵载入内存，有可能将内存撑爆，在这种情况下我们怎么办呢？第一反应是我们要进行特征的降维，说的没错！而Hash Trick就是非常常用的文本特征降维方法。
- 我们会定义一个特征Hash后对应的哈希表的大小，这个哈希表的维度会远远小于我们的词汇表的特征维度，因此可以看成是降维
- 在将文本分词并向量化后，我们可以得到词汇表中每个词在各个文本中形成的词向量
- TF-IDF是Term Frequency -  Inverse Document Frequency的缩写，即“词频-逆文本频率”。它由两部分组成，TF和IDF。
- IDF反应了一个词在所有文本中出现的频率，如果一个词在很多的文本中出现，那么它的IDF值应该低
- TF-IDF是非常常用的文本挖掘预处理基本步骤，但是如果预处理中使用了Hash Trick，则一般就无法使用TF-IDF了，因为Hash Trick后我们已经无法得到哈希后的各特征的IDF的值。使用了IF-IDF并标准化以后，我们就可以使用各个文本的词特征向量作为文本的特征，进行分类或者聚类分析。
- TF-IDF不光可以用于文本挖掘，在信息检索等很多领域都有使用

## [Elasticsearch中为什么选择倒排索引而不选择B树索引](https://www.cnblogs.com/lonely-wolf/p/15464556.html)

- 关系型数据库，如 MySQL，其选择的是 B+ 树索引
  - 最底层叶子节点除了存储索引值还会存储整条数据（InnoDB 引擎），而根节点和枝节点不会存储数据，
  - B+ 树之所以这么设计就是为了使得根节点和枝节点能够存储更多的节点，因为搜索的时候从根节点开始搜索，每查询一个节点就是一次 IO 操作，所以一个节点能存储更多的索引值能减少磁盘 IO 次数。
- 假如索引值本身就很大，那么 B+ 树是不是性能会急剧下降呢？答案是肯定的，
  - 因为当索引值很大的话，一个节点能存储的数据会大大减少（一个节点默认是 16kb 大小），B+ 树就会变得更深，每次查询数据所需要的 IO 次数也会更多。
  - 而且全文索引就是需要支持对大文本进行索引的，从空间上来说 B+ 树不适合作为全文索引，
  - 同时 B+ 树因为每次搜索都是从根节点开始往下搜索，所以会遵循最左匹配原则，而我们使用全文搜索时，往往不会遵循最左匹配原则，所以可能会导致索引失效。
- 总结起来 B+ 树不适合作为全文搜索索引主要有以下两个原因：
  - 全文索引的文本字段通常会比较长，索引值本身会占用较大空间，从而会加大 B+ 树的深度，影响查询效率。
  - 全文索引往往需要全文搜索，不遵循最左匹配原则，使用 B+ 树可能导致索引失效。
- 在全文检索当中，我们需要对文档进行分词处理，切好之后再将切出来的词和文档进行关联，并进行索引，那么这时候我们应该如何存储关键字和文档的对应关系呢？
- 正排索引又称之为前向索引（forward index）。我们以一篇文档为例，那么正排索引可以理解成他是用文档 id 作为索引关键字，同时记录了这篇文档中有哪些词（经过分词器处理），每个词出现的次数已经每个词在文档中的位置。
  - 但是我们平常在搜索的时候，都是输入一个词然后要得到文档，所以很显然，正排索引并不适合于做这种查询，所以一般我们的全文检索用的都是倒排索引，但是倒排索引却并不适合用于聚合运算，所以其实在 es 中的聚合运算用的是正排索引。
- 倒排索引又称之为反向索引（inverted index）。和正排索引相反，倒排索引使用的是词来作为索引关键字，并同时记录了哪些文档中有这个词。

- 建立索引的目的是什么？最直接的目的肯定是为了加快检索速度，而为了达到这个目的，那么在不考虑其他因素的情况下，必然是需要占用的空间越少越好，而为了减少占用空间，可能就需要压缩之后再进行存储
- FOR 压缩算法即 Frame Of Reference。这种算法比较简单，也有一定的局限性，因为其对存储的文档 id 有一定要求。
  - 假设现在有一亿个文档，对应的文档 id 就是从 1 开始自增。
  - FOR 算法并不直接存储文档 id，而是存储差值，像这种这么规律的文档 id，差值都是 1，而 1 转成二进制就可以只使用 1 个 bit 进行存储，这样就只需要 1000W 个 bit 的空间来进行存储就够了，相比较直接存储原始文档 id 的情况下，这种场景采用 FOR 算法大大减少了空间。
- RBM 压缩算法即 Roaring Bitmap，
  - RBM 压缩算法的核心思想是：将 32 位无符号整数按照高 16 位进行划分容器，即最多可能有 65536 个 container。因为 65536 实际上就是 2 的 16 次方，而一个无符号 int 类型正好是需要 32 位进行存储，划分为高低位正好两边都是 16 位，也就是最多 65536 个。
  - 那就是容器最多有 65536 个，而每个容器内的元素也恰好最多是 65536 个元素。

- 压缩之后的数据是如何落地到磁盘的呢？采用的是什么数据结构呢？
- 字典树(Trie Tree)又称之为前缀树（Prefix Tree），是一种哈希树的变种，可以用于搜索时的自动补全、拼写检查、最长前缀匹配等。
- 字典树有以下三个特点：
  - 根节点不包含字符，除根节点外的其余每个节点都只包含一个字符。
  - 从根节点到某一节点，将路径上经过的所有字符连接起来，即为该节点对应的字符串。
  - 每个节点的所有子节点包含的字符都不相同。
  - 字典树没有解决后缀共用问题，只解决了前缀共用（这也是字典树又被称之为前缀树的原因）。当数据量达到一定级别的时候，只共享前缀不共享后缀也会带来很多空间的浪费
- 要解决上面字典树的缺陷其实思路也很简单，就是除了利用字符串的前缀，同时也将相同的后缀进行利用，这就是 FST，在了解 FST 之前，我们先了解另一个概念，那就是 FSM
  - FST，其实就是通过 FSM 演化而来。

- 本文主要讲解了在 Elasticsearch 中是如何利用倒排索引来进行数据检索的，并讲述了倒排索引中的 FOR 和 RBM 两种压缩算法的原理以及使用场景，最后对比了字典树（前缀树）和 FST 两种数据结构存储的区别，并最终得出了为什么 es 中选择 FST 而不是选择字典树来进行存储索引数据的原因。

## [The technology behind GitHub’s new code search | The GitHub Blog_202302](https://github.blog/2023-02-06-the-technology-behind-githubs-new-code-search/)

- To solve code search at GitHub's scale, we built a search engine from scratch in Rust that can run regex searches across 45 million repositories in seconds. Learn how.

- Our ingest pipeline can publish around 120, 000 documents per second, so working through those 15.5 billion documents should take about 36 hours. 
  - But delta indexing reduces the number of documents we have to crawl by over 50%, which allows us to re-index the entire corpus in about 18 hours.
  - There are some big wins on the size of the index as well.

- To determine the optimal ingest order, we need a way to tell how similar one repository is to another (similar in terms of their content), so we invented a new probabilistic data structure to do this in the same class of data structures as MinHash and HyperLogLog. This data structure, which we call a geometric filter, allows computing set similarity and the symmetric difference between sets with logarithmic space. 
# blogs

## [Introducing DoorDash’s In-House Search Engine - DoorDash Engineering Blog _202402](https://doordash.engineering/2024/02/27/introducing-doordashs-in-house-search-engine/)

- 
- 

- https://twitter.com/spinscale/status/1762838817457721569
- DoorDash implementing their own search engine on top of Apache Lucene.
  - The trend of splitting storage and compute to not pay indexing costs more than once keeps going. Also Ranking phases and resource isolation in addition to cost savings played a role.
- A common pattern: LinkedIn have written at least three Lucene-based stacks over the years.
- Zero-interest rate problem IMHO
  - 50% agreement on my side. Other half is lack of a standardized/highly adopted search engine providing separation of indexing and search (aka being cloud native[tm]) plus reranking. I’m sure you have a suggestion

- [Kaldb: serverless lucene at petabyte scale :: Berlin Buzzwords 2023 :: pretalx](https://program.berlinbuzzwords.de/berlin-buzzwords-2023/talk/KPELMM/)
## [The holistic(整体的；全盘的) UX of integrated search filters](https://rystorm.com/blog/integrated-search-filters)

- What is an integrated search filter?
  - It is a search that goes across the entire toolset you are using, and filters down to the features that are possible. 
  - It filters the results down to what the user is intending
  - I think macOS and its apps have this kind of search done in a fantastically good way. 

- the search does also need to be made fuzzy enough so that if someone searches for a particular feature, they find what they intend
# blogs-recsys
- [推荐系统常用算法总结（适合刚入门的同学）-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/1614209)
# discuss-recsys
- ## 

- ## 

- ## 

- ## [推荐算法和机器学习算法之间是什么关系？ - 知乎](https://www.zhihu.com/question/53040164)
- 推荐系统可以说是机器学习的一种应用，比如针对特定的电影打分模型，通过线性回归代价函数，迭代获取用户特征θ和电影特征x，用于推荐电影给用户。

- 看项亮的《推荐系统实践》
# more-blog
- [【总结】推荐系统——召回篇【1】 - 知乎](https://zhuanlan.zhihu.com/p/351716045)
  - 召回阶段负责从海量数据中快速筛选出部分数据，供后面排序阶段使用
  - 本质上，召回和后面的粗排、精排、重排都属于排序，之所以分成召回阶段和后面3个排序阶段，主要原因之一是基于工程上的考虑。

- [深入理解推荐系统：召回 - 知乎](https://zhuanlan.zhihu.com/p/115690499)
  - 召回是推荐系统的第一阶段，主要根据用户和商品部分特征，从海量的物品库里，快速找回一小部分用户潜在感兴趣的物品，然后交给排序环节。
  - 这部分需要处理的数据量非常大，速度要求快，所有使用的策略、模型和特征都不能太复杂。
- 四种常见的召回方法
  - 基于内容的召回
  - 协同过滤
  - 基于FM模型召回
  - 基于深度神经网络的方法

- [常见的分词方法与文本向量化 | littleji](https://blog.littleji.com/2019/03/05/20190305DataWhaleNLPTask2/)
  1 词典分词算法
  1.1 前向最大匹配算法、后向最大匹配、双向匹配、最小切分
  2 基于统计的分词算法
  2.1 NGram
  3 词袋模型与文本向量化
  3.1 词袋模型
