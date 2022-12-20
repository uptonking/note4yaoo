---
title: spec-format-apache-arrow-blog
tags: [apache-arrow, blog]
created: 2021-07-24T08:16:58.416Z
modified: 2021-07-24T08:18:08.017Z
---

# spec-format-apache-arrow-blog

# guide

# [streamlit: All in on Apache Arrow_202107](https://blog.streamlit.io/all-in-on-apache-arrow/)

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

## What is Arrow, and how does it work

- Arrow is a memory format for DataFrames, as well as a set of libraries for manipulating DataFrames in that format from all sorts of programming languages.
- A critical component of Apache Arrow is its in-memory columnar format, a standardized, language-agnostic specification for representing structured, table-like datasets in-memory. 
  - This data format has a rich data type system (including nested and user-defined data types) designed to support the needs of analytic database systems, data frame libraries, and more.
- It's column-oriented: so doing things like computing the sum of a column of your DataFrame is lightning fast.
- It's designed to be memory-mapped: so serialization/deserialization are basically free. Just send the bytes over the wire as they are.
- It's language-agnostic: so it's well-supported both in Python and JavaScript.
- Plus it supports all those DataFrame features that our custom module never got around to. 

## Faster and more efficient DataFrames

- In our legacy serialization format, as DataFrame size grew, the time to serialize also increased significantly. 
  - Iterating through the DataFrame, converting all its data into formats we could use, packing them into a whole hierarchy of Protobufs, that's a whole lot of work 

## Other benefits to using Arrow

- As new features are introduced to Arrow, Streamlit can support them with much less work. 
  - we just added a bunch of them now: table captions, categorical indices, interval indices, multi-index Styler objects, and more!
- If your app uses Arrow Tables, Streamlit will now accept them anywhere a Pandas DataFrame is accepted. 
- we get to delete over 1k lines of code from our codebase. 

## Sharp edges

- Arrow is a bit more strict than Pandas about keeping your DataFrames organized. 
  - For example, elements in the same column of a DataFrame must all have the same data type. 
  - But we find that this is an overall benefit to your data model, and valid reasons for breaking this rule are rare.
- Some features such as `PeriodIndex` and `TimedeltaIndex` are not yet fully supported. 
  - But, as mentioned earlier, adding them is easier than ever.
- Styler concatenation is no longer supported when using `add_rows()`. 
  - This is not really an Arrow-specific issue, but more that when you concatenate Styler objects it may not do what you wanted: if the Styler is configured to draw the max of a column in red, for example, then a correct concatenation would require recomputing the max for the entire column. Which is... suboptimal.
- This is a big change, and even though we tested it thoroughly, there may still be bugs lurking around.

## Wrapping it up

- Arrow is the new hotness, and it's where we believe the ecosystem is moving. 
  - So we're super excited to finally jump on that rocketship and help propel it forward with all of you.
# blogs

- [Apache Arrow：一种适合异构大数据系统的内存列存数据格式标准 | 伴鱼技术团队](https://tech.ipalfish.com/blog/2020/12/08/apache_arrow_summary/)
  - 因为 Parquet 和 ORC 是为磁盘而设计，支持高压缩率的压缩算法，如 snappy、gzip、zlib 等压缩技术就十分必要。
  - 而 Arrow 为内存而设计，对压缩算法几乎没有要求，更倾向于直接存储原生的二进制数据。面向磁盘与面向内存的另一个不同点在于：尽管磁盘和内存的顺序访问效率都要高于随机访问，但在磁盘中，这个差异在 2-3 个数量级，而在内存中通常在 1 个数量级内。
  - 因此要均摊一次随机访问的成本，需要在磁盘中连续读取上千条数据，而在内存中仅需要连续读取十条左右的数据。
  - 这种差异意味着 内存场景下的 batch 大小 (如 Arrow 的 64KB) 要小于磁盘场景下的 batch 大小。
# more
