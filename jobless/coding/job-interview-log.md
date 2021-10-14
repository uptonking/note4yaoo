---
title: job-interview-log
tags: [interview, job]
created: '2021-10-13T13:23:25.535Z'
modified: '2021-10-13T13:25:26.289Z'
---

# job-interview-log

# guide

# 20211013-投光编辑器-一面

> 面试官：雪碧

## 两数之和

```JS
function twoSum(nums, target) {
  const map = {};

  for (let i = 0; i < nums.length; i++) {
    const curr = target - nums[i];
    if (map[curr] !== undefined) return [i, map[curr]];

    map[nums[i]] = i;

  }
}
```

## 超长文档、超宽画布，如何优化性能

- 文档可先分页、再利用virtualized只渲染可见区部分

- 局部/分层渲染（只渲染当前视图的内容，或按照主次异步渲染不同图层），
- 离屏渲染/双缓冲（提前完成下一帧计算，并加入到缓冲池中）

## 给你很多坐标点，怎么查找一个点附近的poi元素

- 思路1：geohash
- 思路2：基于现有数据库的spatial sql语句
- 思路3：基于成熟产品，如es

### [谈谈你对 geohash 的理解和如何实现附近人功能呢？](https://xie.infoq.cn/article/ed42f43b93e724321b292a6b8)

- geohash 就是一种地理位置编码。
  - 通过将地球看成一个二维的平面图，然后将平面递归切分成更小的模块，然后将空间经纬度数据进行编码生成一个二进制的字符串，再通过 base32 将其转换为一个字符串。最终是通过比较geohash的值的相似程度查询附近目标元素。
- 利用递归思想 找出经纬度的二进制编码
- 偶数位放经度，奇数位放纬度
- 在base32编码

- Geohash 实战系列 附近人查询
  - select * from `user` where `geohash` like 'geohash%' order by id asc limit 100

### [GeoHash核心原理解析](https://www.cnblogs.com/LBSer/p/3310455.html)

- 一提到索引，大家脑子里马上浮现出B树索引，因为大量的数据库（如MySQL、oracle、PostgreSQL等）都在使用B树。
  - B树索引本质上是对索引字段进行排序，然后通过类似二分查找的方法进行快速查找，即它要求索引的字段是可排序的。
  - 但是对于空间上的一个点（二维，包括经度和纬度），如何排序呢？又如何索引呢？解决的方法很多，下文介绍一种方法来解决这一问题。

- GeoHash将二维的经纬度转换成字符串, 
  - 下图展示了北京9个区域的GeoHash字符串，分别是WX4ER，WX4G2、WX4G3等等，每一个字符串代表了某一矩形区域。也就是说，这个矩形区域内所有的点（经纬度坐标）都共享相同的GeoHash字符串
  - 这样既可以保护隐私（只表示大概区域位置而不是具体的点），又比较容易做缓存
- 字符串越长，表示的范围越精确。 
- 字符串相似的表示距离相近，这样可以利用字符串的前缀匹配来查询附近的POI信息。

- GeoHash算法的步骤
  - 根据经纬度计算GeoHash二进制编码
  - 地球纬度区间是[-90, 90]， 北海公园的纬度是39.92816
  - 区间[-90, 90]进行二分为[-90, 0), [0, 90]，称为左右区间，可以确定39.928167属于右区间[0, 90]，给标记为1；
  - 接着将区间[0, 90]进行二分为 [0, 45), [45, 90]，可以确定39.928167属于左区间 [0, 45)，给标记为0；
  - 递归上述过程39.928167总是属于某个区间[a, b]。随着每次迭代区间[a, b]总在缩小，并越来越逼近39.928167；
- 如果给定的纬度x（39.928167）属于左区间，则记录0，如果属于右区间则记录1，这样随着算法的进行会产生一个序列1011100，序列的长度跟给定的区间划分次数有关。
- 通过上述计算，纬度产生的编码为10111 00011，经度产生的编码为11010 01011。偶数位放经度，奇数位放纬度，把2串编码组合生成新串
- 最后使用用0-9、b-z（去掉a, i, l, o）这32个字母进行base32编码(每5位处理一次)，首先将11100 11101 00100 01111转成十进制，对应着28、29、4、15，十进制对应的编码就是wx4g

- 同理，将编码转换成经纬度的解码算法与之相反

- GeoHash Base32编码长度与精度
  - 当geohash base32编码长度为8时，精度在19米左右，
  - 而当编码长度为9时，精度在2~4米左右

- 为什么分别给经度和维度编码？为什么需要将经纬度两串编码交叉组合成一串编码？
  - 我们将二进制编码的结果填写到空间中，当将空间划分为四块时候，编码的顺序分别是左下角00，左上角01，右下脚10，右上角11，也就是类似于Z的曲线，当我们递归的将各个块分解成更小的子块时，编码的顺序是自相似的（分形），每一个子快也形成`Z曲线`，这种类型的曲线被称为`Peano空间填充曲线`。
  - 这种类型的空间填充曲线的优点是将二维空间转换成一维曲线（事实上是分形维），对大部分而言，编码相似的距离也相近， 但Peano空间填充曲线最大的缺点就是突变性，有些编码相邻但距离却相差很远，比如0111与1000，编码是相邻的，但距离相差很大。

- 除Peano空间填充曲线外，还有很多空间填充曲线，如图所示，其中效果公认较好是`Hilbert空间填充曲线`，相较于Peano曲线而言，Hilbert曲线没有较大的突变。
  - 为什么GeoHash不选择Hilbert空间填充曲线呢？可能是Peano曲线思路以及计算上比较简单吧，事实上，Peano曲线就是一种四叉树线性编码方式。

- 解决geohash字符串前缀相同但可能存在突变的问题
  - 我们查询时，除了使用定位点的GeoHash编码进行匹配外，还使用周围8个区域的GeoHash编码，这样可以避免这个问题。
  - geohash只是空间索引的一种方式，特别适合点数据，而对线、面数据采用R树索引更有优势

- 成熟方案
- kdbush
  - A very fast static spatial index for 2D points based on a flat KD-tree. 
  - Compared to RBush:
    - points only — no rectangles
    - static — you can't add/remove items
    - indexing is 5-8 times faster

```JS
const index = new KDBush(points); // make an index
const ids1 = index.range(10, 10, 20, 20); // bbox search - minX, minY, maxX, maxY
const ids2 = index.within(10, 10, 5); // radius search - x, y, radius
```

## 为什么在map中查找key比在数组中查找元素更快？

- 可以分析hashtable的一种实现
  - 在hashtable数据结构中，可以用 数组+链表 或 二维数组 保存kv键值对
  - 每次添加新元素到map时，调用一个散列函数hash(key)得到哈希值，通过取模等运算可得到在数组中的位置，
  - 然后若位置不为空，就可以将新元素添加到该位置链表的末尾或数组末尾

- map比数组快因为不用逐个全部查找，特别时当map初始空间够大时，hash(key)能直接找到元素的位置
  - 但map的时间复杂度并不一定是O(1)，哈希冲突的概率 P collision = n / capacity

- [Why are maps faster than arrays?](https://itqna.net/questions/1560/why-are-maps-faster-arrays)
- Javascript map is implemented using a hash table, which is a data structure specially designed for element to be fast. 
  - Generally, the number of operations required is constant or logarithmic in the number of elements, rather than being directly proportional.

- The idea is that the `indexOf` method will scroll each element of the array by checking if the value matches, in which case the cost of that function is `O(N)` ; 
  - You can check here in the V8 code, that the search is always incremental.
- for Hash, the key is mapped to the value, 
  - that is, when doing the search what happens is that the search value is transformed into an index (using a function) that is used to fetch the value. 
  - Therefore the cost of accessing the value of a hash is `O(1)`.

- HashTable is usually much slower than HashMap because it does much the same thing but is also synchronized.

- [java simple hash table example](https://www.algolist.net/Data_structures/Hash_table/Simple_example)

## typescript discriminated unions

```typescript
interface Square { 
  kind: "square";
  size: number; 
  }
  
interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number; 
  } 
  
type Shape = Square | Rectangle;

function area(s: Shape) {
    if (s.kind === "square") {
        // Now TypeScript *knows* that `s` must be a square ;)
        // So you can use its members safely :)
        return s.size * s.size;
    }
    else {
        // Wasn't a square? So TypeScript will figure out that it must be a Rectangle ;)
        // So you can use its members safely :)
        return s.width * s.height;
    }
}
```
