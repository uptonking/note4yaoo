---
title: spec-format-apache-arrow-blog
tags: [apache-arrow, blog]
created: 2021-07-24T08:16:58.416Z
modified: 2021-07-24T08:18:08.017Z
---

# spec-format-apache-arrow-blog

# guide

# blogs

## [Apache Arrow简介](https://zhuanlan.zhihu.com/p/339132159)

- 由于历史原因，Snowflake一直使用了JSON作为结果集（ResultSet）的序列化方式，引起了许多问题。
  - 首先，JSON的序列化/反序列化的成本实在是太高了：许多cpu cycle都被浪费在了字符串和其他数据类型之间的转换。
  - 不仅仅是cpu，内存的消耗也是十分巨大的，尤其像是Java这样的语言，对内存的压力非常大。
  - 其次，使用JSON进行序列化，会导致某些数据类型（浮点数）的精度丢失。

- ✨ arrow定义了一种在内存中表示tabular data的格式。
  - 这种格式特别为数据分析型操作（analytical operation）进行了优化。
  - 比如说列式格式（columnar format），能充分利用现代cpu的优势，进行向量化计算（vectorization）。
  - 不仅如此，Arrow还定义了IPC格式，序列化内存中的数据，进行网络传输，或者把数据以文件的方式持久化。
  - arrow定义的格式是与语言无关的，所以任何语言都能实现Arrow定义的格式。
- arrow其实和protobuf很像，只不过protobuf是为了structured data提供内存表示方式和序列化方案。可是两者的使用场景却很不一样。
  - protobuf主要是序列化structured data，有很多的键值对和非常深的nested structure。
  - arrow序列化的对象主要还是表格状数据。

- arrow在内存中表示数据的最基本单元是array，它代表了一连串长度已知、类型相同的数据。
  - 而多个长度相同、类型相同或者不同的array就可以用来表示结果集（或者一部分的结果集）。
- arrow限制了array的最大长度，当结果集（或者表）的大小超过了array的最大长度，就需要把结果集水平切分成多个有序集合。

- 多个长度相同的array组成的有序集合可以用来表示结果集的子集（或者部分的表），arrow称这个有序集合为Record Batch。
  - Record Batch也是序列化的基本单元。
  - arrow定义了一个传输协议，能把多个record batch序列化成一个二进制的字节流，并且把这些字节流反序列化成record batch，从让数据能在不同的进程之间进行交换。

- 在传统的编程世界中，数据只存放于oltp database中（比如说MySQL），application通过JDBC或者ODBC等标准接口和数据库进行交互。
- arrow适用的场景可能有一下几个：
  - 同一个系统，多个节点：由于云计算的普及，数据库上云也得到了越来越多的关注。在一个分布式数据库的实现中，可能会有许多的query executor节点并行产生结果集。arrow的格式可以让客户端并行读取各个节点产生的结果集。
  - 多个系统可能会同时读取同一份数据：企业可能会需要data warehouse生成报表，需要spark做一些机器学习。为了能让不同的系统之间进行数据的交互，企业经常把数据以文件的形式存放于一些分布式的文件系统（AWS S3）之上。

- > discussion

- 跟pandas的dataframe似乎很类似
  - 是的，但dataframe还是主要帮助data scientist 执行各种 select aggregate操作； 
  - arrow主要还是focus在帮助data序列化以便在各种system之间transfer
- arrow还解决了类型共享计算格式不统一的问题，是高性能计算的基础

## [Apache Arrow：一种适合异构大数据系统的内存列存数据格式标准 | 伴鱼技术团队](https://tech.ipalfish.com/blog/2020/12/08/apache_arrow_summary/)

- 因为 Parquet 和 ORC 是为磁盘而设计，支持高压缩率的压缩算法，如 snappy、gzip、zlib 等压缩技术就十分必要。
  - 而 Arrow 为内存而设计，对压缩算法几乎没有要求，更倾向于直接存储原生的二进制数据。
- 面向磁盘与面向内存的另一个不同点在于：尽管磁盘和内存的顺序访问效率都要高于随机访问，但在磁盘中，这个差异在 2-3 个数量级，而在内存中通常在 1 个数量级内。
- 因此要均摊一次随机访问的成本，需要在磁盘中连续读取上千条数据，而在内存中仅需要连续读取十条左右的数据。
- 这种差异意味着 内存场景下的 batch 大小 (如 Arrow 的 64KB) 要小于磁盘场景下的 batch 大小。

## [streamlit: All in on Apache Arrow_202107](https://blog.streamlit.io/all-in-on-apache-arrow/)

> How we(streamlit) improved performance by deleting over 1k lines of code

- among the first few lines of code ever committed to Streamlit was a painstakingly crafted module that serialized Pandas DataFrames into a complex set of custom Protobufs — plus the inverse of that module to deserialize them back into arrays in the browser.
- Why is this even needed? 
  - As you know, a great portion of Streamlit commands receive DataFrames as input arguments. 
  - It makes sense: DataFrames are efficient, versatile, and easy to work with.
  - And while your DataFrames hung out in Python land, everything was hunky-dory.
- DataFrames were just not traditionally suited to be sent over-the-wire, and there was no standard JavaScript library to handle them on the browser side anyway. 
  - Hence, all the custom code.
  - Our custom format grew considerably slower as users pushed for larger and larger DataFrames. 
  - Furthermore, every time Pandas released new features, adding support for them in Streamlit meant undertaking a considerable amount of work. 
- Finally, we weren't big fans of our old custom module, to begin with!
- We spent months researching different solutions, trying out serialization formats, embarking on false starts, and going right back to where we started. 
  - Our old code still checked more boxes than all the options out there.
- Until finally, we found Apache Arrow, an efficient memory format and set of libraries that will handle Streamlit's DataFrame serialization from now on. We love it, and we think you will too.

### What is Arrow, and how does it work

- Arrow is a memory format for DataFrames, as well as a set of libraries for manipulating DataFrames in that format from all sorts of programming languages.
- A critical component of Apache Arrow is its in-memory columnar format, a standardized, language-agnostic specification for representing structured, table-like datasets in-memory. 
  - This data format has a rich data type system (including nested and user-defined data types) designed to support the needs of analytic database systems, data frame libraries, and more.
- It's column-oriented: so doing things like computing the sum of a column of your DataFrame is lightning fast.
- It's designed to be memory-mapped: so serialization/deserialization are basically free. Just send the bytes over the wire as they are.
- It's language-agnostic: so it's well-supported both in Python and JavaScript.
- Plus it supports all those DataFrame features that our custom module never got around to. 

### Faster and more efficient DataFrames

- In our legacy serialization format, as DataFrame size grew, the time to serialize also increased significantly. 
  - Iterating through the DataFrame, converting all its data into formats we could use, packing them into a whole hierarchy of Protobufs, that's a whole lot of work 

### Other benefits to using Arrow

- As new features are introduced to Arrow, Streamlit can support them with much less work. 
  - we just added a bunch of them now: table captions, categorical indices, interval indices, multi-index Styler objects, and more!
- If your app uses Arrow Tables, Streamlit will now accept them anywhere a Pandas DataFrame is accepted. 
- we get to delete over 1k lines of code from our codebase. 

### Sharp edges

- Arrow is a bit more strict than Pandas about keeping your DataFrames organized. 
  - For example, elements in the same column of a DataFrame must all have the same data type. 
  - But we find that this is an overall benefit to your data model, and valid reasons for breaking this rule are rare.
- Some features such as `PeriodIndex` and `TimedeltaIndex` are not yet fully supported. 
  - But, as mentioned earlier, adding them is easier than ever.
- Styler concatenation is no longer supported when using `add_rows()`. 
  - This is not really an Arrow-specific issue, but more that when you concatenate Styler objects it may not do what you wanted: if the Styler is configured to draw the max of a column in red, for example, then a correct concatenation would require recomputing the max for the entire column. Which is... suboptimal.
- This is a big change, and even though we tested it thoroughly, there may still be bugs lurking around.

### Wrapping it up

- Arrow is the new hotness, and it's where we believe the ecosystem is moving. 
  - So we're super excited to finally jump on that rocketship and help propel it forward with all of you.
# more
- [Apache Arrow的优势与使用](https://zhuanlan.zhihu.com/p/588400772)
