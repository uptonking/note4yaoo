---
title: algs-tree-trie
tags: [data-structure, tree, trie]
created: 2023-01-15T11:41:00.816Z
modified: 2023-01-15T11:41:37.722Z
---

# algs-tree-trie

# guide

- who is using #trie
  - linvodb-fts
  - level-trie
  - ndx-search
  - router for fastify/feathers

- who is using #merkle-tree
  - cassandra
  - dynamodb-amazon
# Tree
- 小结
  - trie前缀树，每个节点采用基数长度的空间存储
  - Patricia trie，对每个节点，若该节点只有一个孩子节点，则将其合并到父节点中
  - 哈希树无序，单向增加，但查找快速

- [Js实现Trie 字典树 - 掘金](https://juejin.cn/post/7067388014766325774)
  - 未实现delete
- [Trie树的JS或TS实现 - 简书](https://www.jianshu.com/p/ba70ca95c33b)
- [Implementing Merkle Tree and Patricia trie](https://medium.com/coinmonks/implementing-merkle-tree-and-patricia-trie-b8badd6d9591)
  - https://github.com/kashishkhullar/merkel-and-patricia

- [What is the difference between radix trees and Patricia tries?](https://cs.stackexchange.com/questions/63048)
  - PATRICIA tries are radix tries with radix equals 2, which means that each bit of the key is compared individually and each node is a two-way (i.e., left versus right) branch.
- [What is the difference between trie and radix trie data structures?](https://stackoverflow.com/questions/14708134)
  - A PATRICIA trie is a variant of radix tries for which there should only ever be n nodes used to contain n items.
  - Donald R. Morrison found (in 1968) an innovative way to use binary trie to depict N keys using only N nodes and he named this data structure PATRICIA.

- ref
  - [015-数据结构-树形结构-其他树 LSM - bjlhx15 - 博客园](https://www.cnblogs.com/bjlhx/p/10929036.html)
  - [013-数据结构-树形结构-决策树 - bjlhx15 - 博客园](https://www.cnblogs.com/bjlhx/p/10912153.html)
  - [bjlhx15 - 博客园](https://www.cnblogs.com/bjlhx/?page=11)

## [012-数据结构-树形结构-哈希树[hashtree]、字典树[trietree]、后缀树 - bjlhx15 - 博客园](https://www.cnblogs.com/bjlhx/p/10903926.html)

### Trie 前缀树

- Tire树称为字典树，又称单词查找树，是一种哈希树的变种。
- Tire树的三个基本性质：
  1) 根节点不包含字符，除根节点外每一个节点都只包含一个字符；
  2) 从根节点到某一节点，路径上经过的字符连接起来，为该节点对应的字符串；
  3) 每个节点的所有子节点包含的字符都不相同。
- 典型应用是用于统计，排序和保存大量的字符串（但不仅限于字符串），所以经常被搜索引擎系统用于文本词频统计。
- 它的优点是：利用字符串的公共前缀来减少查询时间，最大限度地减少无谓的字符串比较，查询效率比哈希树高。　

- Trie的核心思想是空间换时间，利用字符串的公共前缀来降低查询时间的开销以达到提高效率的目的。
  - 假设字符的种数有m个，有若干个长度为n的字符串构成了一个 Trie树 ，则每个节点的出度为 m（即每个节点的可能子节点数量为m），Trie树 的高度为n。很明显浪费了大量的空间来存储字符，此时Trie树的最坏空间复杂度为O(m^n)
  - 也正由于每个节点的出度为m，所以才能够沿着树的一个个分支高效的向下逐个字符的查询，而不是遍历所有的字符串来查询，此时Trie树的最坏时间复杂度为O(n)。

- 一个文本文件，大约有一万行，每行一个词，要求统计出其中最频繁出现的前10个词，请给出思想，给出时间复杂度分析
  - 提示：用trie树统计每个词出现的次数，时间复杂度是O(n*le)（le表示单词的平均长度），然后是找出出现最频繁的前10个词。当然，也可以用堆来实现，时间复杂度是O(n*lg10)。所以总的时间复杂度，是O(n*le)与O(n*lg10)中较大的哪一个。
- 寻找热门查询
  - 搜索引擎会通过日志文件把用户每次检索使用的所有检索串都记录下来，每个查询串的长度为1-255字节。假设目前有一千万个记录，这些查询串的重复读比较高，虽然总数是1千万，但是如果去除重复和，不超过3百万个。一个查询串的重复度越高，说明查询它的用户越多，也就越热门。请你统计最热门的10个查询串，要求使用的内存不能超过1G。
  - 利用trie树，关键字域存该查询串出现的次数，没有出现为0。最后用10个元素的最小推来对出现频率进行排序。

### 后缀树

- 后缀树（Suffix Tree）则首先是一棵 Compressed Trie，其次，后缀树中存储的关键词为所有的后缀。
- 构建后缀树的抽象过程：
  - 根据文本 Text 生成所有后缀的集合；
  - 将每个后缀作为一个单独的关键词，构建一棵 Compressed Trie。
- 隐式后缀树(implicit suffix tree)：后缀可能终止于叶子结点，也可能隐藏在内部结点中。如果输入串中最后一个字符不同于其他字符，那么所有的后缀都终止于叶子结点，不会有后缀隐藏在内部结点中。这就是为什么ukk算法中最后一个字符必须是特殊字符的原因。
- 显示后缀树：如果不希望这样的上述情形发生，可以在每个后缀的结尾加上一个特殊字符，比如 "$" 或 "#" 等，这样我们就可以使得后缀保持唯一性。
- 上述是使用一种分析的方式来构建一个后缀树，但是如果字符串长度较大，上述方式可能不太可能
- Ukkonen算法（简称ukk算法）是一个online算法，它与mcc算法的一个显著区别是每次只对S的一个前缀生成隐式后缀树(implicit suffix tree)，然后考虑S的下一个字符S[i+1]并将S[0...i+1]的所有后缀加入到上一个阶段中生成的隐式后缀树中，形成一个新的隐式后缀树。最后用一个特殊字符将隐式后缀树自动转换成真实的后缀树。这样ukk的一个最大优点就是不需要事先知道输入字串的全部内容，只需使用增量方式生成后缀树。和mcc算法类似，也是采用压缩存储Trie，以达到节省空间的目的。通过使用implicit extensions和suffix link两大技巧，时间复杂度可以达到线性。

### Hash Tree 哈希树

- [HASH树](https://www.cnblogs.com/hjw201983290498/p/12770943.html)

- 定理1: 质数分辨定理
  - 质数分解定律，任何一个数都可以分解为几个不同素数额乘积P1，P2，P3... 到Pn; 
  - 每一个比1大的自然数N只能有一种方式分解成质数的乘积。
  - 我一直理解irreducible＝质数，prime＝素数。UFD的很重要的一条性质就是，每个irreducible的元素都是prime的。翻译过来就是在UFD中，所有质元素都是素元素。但是到一般的环上，不是所有的质元素（irreducible）都是素元素（prime）。反例《近世代数》或《代数数论》应该会讲。
  - 质数： 即只能被 1 和 本身 整除的数。
  - 为什么用质数：因为N个不同的质数可以 ”辨别“ 的连续整数的数量，与这些质数的乘积相同。
  - 从2起的连续质数，连续10个质数就可以分辨大约M(10) =2*3*5*7*11*13*17*19*23*29= 6464693230 个数，已经超过计算机中常用整数（32bit）的表达范围。
  - 连续100个质数就可以分辨大约M(100) = 4.711930 乘以10的219次方。

- 定理2: 余数分辨定理
  - 可以简单的表述为：n个不同的数可以“分辨”的连续整数的个数不超过他们的最小公倍数。超过这个范围就意味着冲突的概率会增加。定理1是定理2的一个特例。

- 使用不同的分辨算法可以组织不同的哈希树，一般来说，每一个哈希树的节点下的子节点数是和分辨数列一致的。哈希树的最大深度就是特征空间的维度。

- 可以选择质数分辨算法来建立一棵哈希树。
  - 选择从2开始的连续质数来建立一个十层的哈希树。
  - 第一层结点为根结点，根结点下有2个结点；第二层的每个结点下有3个结点；
  - 依此类推，即每层结点的子节点数目为连续的质数【1，2，3，5，7，11……】。每层节点的子节点的数目为连续的素数
  - 到第十层，每个结点下有29个结点。 
- 原则：求余看对应位置的结点，如果为空则在空处插入一个新节点，如果被逻辑删除了替换值再逻辑恢复，如果有值就继续往下找，继续求余判断。

- 哈希树是一种可以自适应的树。通过给出足够多的不同质数，我们总可以将所有已经出现的关键字进行区别。而质数本身就是无穷无尽的。这种方式使得关键字空间和地址空间不再是压缩对应方式，而是完全可以等价的。

- 优点：
  - 结构简单，注意hash树是单向增加的，即使删除也不会减少hash树的结构 
  - 查找迅速，对于int的数据 最多查找10次 
  - 结构不变，即使删除属于也不会改变结构，
- 缺点：非排序性，就是数据时没有顺序的

## [014-数据结构-树形结构-基数树、Patricia树、默克尔树、梅克尔帕特里夏树( Merkle Patricia Tree, MPT) - bjlhx15 - 博客园](https://www.cnblogs.com/bjlhx/p/10929024.html)

### Radix 树

- Radix树，即基数树，也称压缩前缀树，是一种提供key-value存储查找的数据结构。
  - 与Trie不同的是，它对Trie树进行了空间优化，只有一个子节点的中间节点将被压缩。
  - 同样的，Radix树的插入、查询、删除操作的时间复杂度都为O(k)。

- 对于长整型数据的映射。怎样解决Hash冲突和Hash表大小的设计是一个非常头疼的问题。
- radix树就是针对这样的稀疏的长整型数据查找，能高速且节省空间地完毕映射。借助于Radix树，我们能够实现对于长整型数据类型的路由。　　
- 利用radix树能够依据一个长整型（比方一个长ID）高速查找到其相应的对象指针。
  - 这比用hash映射来的简单，也更节省空间，使用hash映射hash函数难以设计，不恰当的hash函数可能增大冲突，或浪费空间。
- radix tree是一种多叉搜索树。树的叶子结点是实际的数据条目。每一个结点有一个固定的、2^n指针指向子结点（每一个指针称为槽slot，n为划分的基的大小）

- Radix树在Linux中的应用
  - Linux基数树（radix tree）是将long整数键值与指针相关联的机制，它存储有效率。而且可高速查询，用于整数值与指针的映射（如：IDR机制）、内存管理等。
  - IDR（ID Radix）机制是将对象的身份鉴别号整数值ID与对象指针建立关联表。完毕从ID与指针之间的相互转换。
  - Linux radix树最广泛的用途是用于内存管理。结构address_space通过radix树跟踪绑定到地址映射上的核心页，该radix树同意内存管理代码高速查找标识为dirty或writeback的页。

- 基数树另一个主要的缺陷是低效。即使你只想存一个键值对，但其中的键长度有几百字符长，那么每个字符的那个层级你都需要大量的额外空间。每次查找和删除都会有上百个步骤。在这里我们引入Patricia树来解决这个问题。

### Patricia 树

- Patricia树，或称Patricia trie，或 crit bit tree，压缩前缀树，是一种更节省空间的Trie。
  - 对于基数树的每个节点，如果该节点是唯一的儿子的话，就和父节点合并。

### Merkle Tree

- Merkle Tree，通常也被称作Hash Tree，顾名思义，就是存储hash值的一棵树。Merkle树的叶子是数据块(例如，文件或者文件的集合)的hash值。非叶节点是其对应子节点串联字符串的hash。
- Merkle Tree 由 Hash List演化而来：在点对点网络中作数据传输的时候，会同时从多个机器上下载数据，而且很多机器可以认为是不稳定或者不可信的。为了校验数据的完整性，更好的办法是把大的文件分割成小的数据块（例如，把分割成2K为单位的数据块）。这样的好处是，如果小块数据在传输过程中损坏了，那么只要重新下载这一快数据就行了，不用重新下载整个文件。

- Merkle Tree 可以看做Hash List的泛化（Hash List可以看作一种特殊的Merkle Tree，即树高为2的多叉Merkle Tree。

- Merkle Tree和HashList的主要区别是，可以直接下载并立即验证 Merkle Tree的一个分支。因为可以将文件切分成小的数据块，这样如果有一块数据损坏，仅仅重新下载这个数据块就行了。如果文件非常大，那么Merkle tree和Hash list都很到，但是Merkle tree可以一次下载一个分支，然后立即验证这个分支，如果分支验证通过，就可以下载数据了。而Hash list只有下载整个hash list才能验证。

### MPT(Merkle Patricia Tree)树

- 提供了一个基于加密学的，自校验防篡改的数据结构，用来存储键值对关系。后文中将简称为MPT
- MPT树中的节点包括空节点、叶子节点、扩展节点和分支节点
- MPT 树中另一个重要的概念是十六进制前缀(hex-prefix, HP)编码，用来对key进行编码。因为字母表是16进制的，所以每个节点可能有16个孩子。因为有两种[key, value]节点(叶节点和扩展节点)，引进一种特殊的终止符标识来标识key所对应的是值是真实的值，还是其他节点的hash。如果终止符标记被打开，那么key对应的是叶节点，对应的值是真实的value。如果终止符标记被关闭，那么值就是用于在数据块中查询对应的节点的hash。
# Trie
- [字典树之旅_极客志](https://zhuanlan.zhihu.com/p/444048441)
- https://github.com/patricklaux/perfect-code
  - StandardTrie, PatriciaTrie, PatriciaBinaryTrie, AvlTree, BTree, RedBlackTree, SkipList
- https://github.com/patricklaux/xtool
  - Java 工具集，字符串、数值、集合、IO等工具类；支持并发的高性能的字典树

## [字典树之旅01. 开篇 - 知乎](https://zhuanlan.zhihu.com/p/444043562)

- 字典树（Trie），又称为前缀树（prefix tree），用于从集合中定位特定键的树数据结构。
  - Trie 是“检索”的英文单词 retrieval 的一部分，名称最早由 E. Fredkin 提出，其发音同“try”。
- 常见的应用场景如搜索引擎的输入框：输入“trie”，会列出以“trie”为前缀的搜索推荐信息。
  - 此外，还有诸如词典分词、词频统计、拼写检查、数据压缩、倒排索引、字符串排序、关键字过滤……等等应用场景

- Trie操作
  - 字符合并
  - 字符切分
  - 无数组
  - 动态数组
  - 双数组

- Trie演变
  - Trie -> Suffix tree
  - Trie -> 单模式匹配之KMP -> AC自动机
  - Trie -> 单模式匹配之BM  -> Wu-Manber
  - B-tries

## [字典树之旅02. Trie 的标准实现 - 知乎](https://zhuanlan.zhihu.com/p/444048441)

- 建立树形结构，每个单词/键是一个字符序列，每个字符是一个节点
- 基本性质
  - 根节点不包含字符，非根节点包含一个字符；
  - 一个节点的所有子节点包含的字符均不相同；
  - 非根节点有且仅有一个指向它的父节点；
  - 值保存在键的最后一个字符所在的节点。
- 推论
  - 一个节点的所有子节点都具有相同前缀；
  - 从根节点到任意节点所经过的路径构成一个字符串，且该字符串在这棵树中是唯一的；
  - 值可以存在于叶子节点，也可以存在于内部节点。

- 查找以输入字符串为前缀的键，先找到前缀节点，然后遍历其子节点。
  - StandardTrie中所有节点的数组容量相同，其大小与字符表的大小相等。
  - 如使用 UTF-16 字符集，其字符数是65536，那么数组容量 R 为65536，则正好可以不重复地映射到数组的位置区间 [0, 65535]。
  - 每个数组的容量均为 R，因此可以将字典树看作是 R 叉树中的一部分
  - 能会有大量空链接存在，这意味着可能会有大量的空间被浪费

- Trie特有方法
  - prefixMatch 查找给定字符串的最长前缀
  - keysWithPrefix 查找以给定字符串为前缀的所有键
  - matchAll 查找给定文本中包含的键

- StandardTrie 有三个非常明显的特点：
  - StandardTrie 是动态查找树，支持在查找期间更新数据元素。
  - 增删查都只跟字符串的长度 m 相关，且其时间复杂度最好和最坏的情况都是 O(m)。
  - 随着树的高度增加，其空间消耗是平方级增长。

## [字典树之旅03. Patricia Trie(一) 字符比较 - 知乎](https://zhuanlan.zhihu.com/p/444061702)

- 标准实现有一个非常大的缺点：每个字符一个节点，每个节点有一个容量为R的数组，因此在稀疏数据集中会有严重的空间浪费。
- Patricia Trie 或是 Patricia Tree， 在一些论文中又称其为 compact trie（紧凑trie），或 compressed trie（压缩 trie）。
- Patricia 的全称是”检索字母数字编码信息的实用算法“（practical algorithm to retrieve information coded in alphanumeric），是 Morrison 于1968年提出的数据结构，原论文是二进制位比较的形式
- Patricia Trie 是 Trie 的一种简单变体，如果一个非根节点仅有一个子节点，则将其子节点与该节点合并。
  - 即将子节点移除，将原子节点内容保存到其父节点或祖先节点
- 对比前文的 StandardNode，我们可以看到多了一个 String 类型的 subKey 字段，该字段用于存储节点合并之后的字符串，其它没有变化。
- 对比 StandardTrie，代码稍微复杂了一些，多了与子节点进行字符比较的逻辑。另外，从代码也可以看出，其时间复杂度依然是O(m)，m 为字符串长度

- Patricia Trie 优化了空间性能，但依然没有完全解决稀疏数据的空间浪费问题——减少了数组的创建，但数组依然可能会有大量的空链接。
  - Patricia Trie 我采用了字符比较的方式去实现，而原论文是位比较的方式

## [字典树之旅04. Patricia Trie(二) 位比较 - 知乎](https://zhuanlan.zhihu.com/p/447442920)

- 基数(radix)，在定位数系(positional numeral system)中表示不重复编码(digit)的数量。
  - 譬如在16进制中，有 {0, 1, 2, ... , e, f} 共16个编码，那么基数就是16
  - 我们还可以采用 ASCII 字符编码来作为不重复编码的集合，那么其基数就是256；
  - 采用 UTF-16 字符集来作为不重复编码的集合，那么其基数就是65536
  - 也可以设计出一个26进制，譬如用小写英文字母 {a, b, c, ... , y, z} 来作为不重复编码的集合，那么其基数就是26；
  - 可以根据需要定义一套编码集，而这个基数就是这套编码集的数量。
- 注：其实这里的基数(radix)，也可以看作是集合论中的基数(cardinal)，而编码集即是序对集。

- 基数概念推广到树中，那么这个基数就是 R 的大小。譬如，我们在前两篇文章中的节点定义中都有一个 R，用来表示数组大小。
  - 16进制中每个编码可以用4个二进制位表示
  - 推出公式 基数R = 2^r, r代表表示位数
  - 16 bit，R 就是65536，正好是 UTF-16 字符集
- 于是，如果我们把 R 设为256 或 65536，我们就又回到了字符编码的世界，位与字符的转换由编程语言帮我们处理了。

- 原论文描述的几乎是一个完整的检索系统，因此包含了许多术语和概念，但其算法的核心思想是合并单路分支。因此，无论字符比较方式还是二进制比较方式，只要是合并单路分支，都可以认为是 Patricia trie。

- 二进制位比较是如何推广到字符比较方式的？
  - 如果看作是基数树，位比较推广到字符比较，只是基数大小变化而已。
- 二进制位比较与字符比较，两者分别有哪些优点和缺点？
  - 二进制位比较，减少了空链接，但增加了树的高度，查找的时间性能会变差。同时，虽然空链接少了，但一个bit一个节点的方式依然会耗费大量内存。在上面介绍的这么多结构中，<2.4.2. R为16> 是相对合理的，在时间和空间上找到了一个比较完美的平衡点。
# Merkle Tree
- ref
  - [优秀数据结构--默克尔树 go语言实现](https://blog.hujm.net/post/%E4%BC%98%E7%A7%80%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84-%E9%BB%98%E5%85%8B%E5%B0%94%E6%A0%91/)

## [Merkle Tree学习](https://www.cnblogs.com/fengzhiwu/p/5524324.html)

- 创建Merkle Tree是O(n)复杂度(这里指O(n)次hash运算)，n是数据块的大小。得到Merkle Tree的树高是log(n)+1。
- 检索数据块 - O(log(n))
- 更新操作其实是很简单的，更新完数据块，然后接着更新其到树根路径上的Hash值就可以了，更新所有的hash实际上可以在O(lgn)时间内完成，因为要改变的所有节点都是相关联的
- 插入和删除操作肯定会改变Merkle Tree的结构，插入和删除操作其实是一个工程上的问题，不同问题会有不同的插入方法。
- 实际上Merkle Tree的结构(是否平衡，树高限制多少)在大多数应用中并不重要，而且保持数据块的顺序也在大多数应用中也不需要。因此，可以根据具体应用的情况，设计自己的插入和删除操作。一个通用的Merkle Tree插入删除操作是没有意义的。

## [区块链技术架构分析（3）-默克尔树（merkle tree）](https://zhuanlan.zhihu.com/p/39271872)

- 应用场景
- 快速比较大量数据：当两个默克尔树根相同时，则意味着所代表的数据必然相同（哈希算法决定的）
- 快速定位修改
- 零知识证明：例如如何证明某个数据（D0……D3）中包括给定内容 D0，很简单，构造一个默克尔树，公布 N0，N1，N4，Root，D0拥有者可以很容易检测 D0 存在，但不知道其它内容。
- 在分布式存储系统中的应用原理
  - 为了保持数据一致，分布系统间数据需要同步，如果对机器上所有数据都进行比对的话，数据传输量就会很大，从而造成“网络拥挤”。
  - 为了解决这个问题，可以在每台机器上构造一棵Merkle Tree，这样，在两台机器间进行数据比对时，从Merkle Tree的根节点开始进行比对，
  - 如果根节点一样，则表示两个副本目前是一致的，不再需要任何处理；
  - 如果不一样，则沿着hash值不同的节点路径查询，很快就能定位到数据不一致的叶节点，只用把不一致的数据同步即可，这样大大节省了比对时间以及数据的传输量。
- 比特币区块链系统中的采用的是Merkle二叉树，
  - 它的作用主要是快速归纳和校验区块数据的完整性，它会将区块链中的数据分组进行哈希运算，向上不断递归运算产生新的哈希节点，最终只剩下一个Merkle根存入区块头中，每个哈希节点总是包含两个相邻的数据块或其哈希值。
  - 区块头只需包含根哈希值而不必封装所有底层数据，这使得哈希运算可以高效地运行在智能手机甚至物联网设备上
  - Merkle树可支持“简化支付验证协议”（SPV），即在不运行完整区块链网络节点的情况下，也能够对交易数据进行检验。所以，在区块链中使用Merkle树这种数据结构是非常具有意义的。
# more
- [Autocomplete using Trie datastructure with Typescript](https://www.pierrehedkvist.com/posts/autocomplete-using-trie-data-structure)

- [java - 一文搞懂字典树](https://segmentfault.com/a/1190000040801084)
- [Trie树 - 掘金](https://juejin.cn/post/6844903641799720974)
- [字典树的几种实现方式以及应用 | 酱猪蹄的博客](http://jiangzhuti.me/posts/%E5%AD%97%E5%85%B8%E6%A0%91%E7%9A%84%E5%87%A0%E7%A7%8D%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F%E4%BB%A5%E5%8F%8A%E5%BA%94%E7%94%A8)
# discuss-tree
- ## 

- ## 

- ## 
# discuss-tree-alternatives
- ## 

- ## 

- ## I often see hash tables used for object sets needing:
- https://x.com/awesomekling/status/1877324622665748800
  - O(1) insert
  - O(1) remove
  - O(1) check if the set contains an object
  - Iterate over all objects
- If you're okay with these constraints:
  - Objects grow by three pointers (next, prev, and containing list)
  - Each object is in at most one list
  - Objects have well-defined lifetimes
  - You can use an intrusive linked list instead, achieving all operations in a handful of instructions and with no allocations
- there's definitely some nuances to consider, like impact on cache locality
  - Most people never consider using a intrusive linked lists for anything, which is why I like this tip.. Just to put the idea in their head, then let them decide if it's useful in their scenario
- If I'm not mistaken, Linux is using this heavily.
  - Yeah it’s super useful in embedded/kernel programming
