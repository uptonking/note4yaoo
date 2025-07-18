---
title: job-interview-log
tags: [interview, job]
created: 2021-10-13T13:23:25.535Z
modified: 2021-10-13T13:25:26.289Z
---

# job-interview-log

# guide

- 面试的目标
  - 不是要找一家最牛的公司，而是要找到一家最适合自己的公司，既能让你的优势得到充分发挥，又能满足你的职业规划
# self-intro
- 面试问题技巧
  - 技术、业务、团队
  - STAR

- 个人优点
  - 开发比较务实，业余时间会了解原理，开发工作大多都能高质量完成，业界难点需要额外的时间
  - 对各种编辑器开发比较熟悉，并且愿意持续投入时间精力
  - 能快速适应团队开发流程

- 个人缺点
  - 能写代码，但没有自己认为的那样能写代码，速度和效率都有待提高，编辑器的ot转换逻辑仍有挑战
  - 对深入技术仍比较执着，花费的精力较多，所以在产品设计、需求评审、需求调整上投入的精力相对不多，特别是争论要不要做、需求优先级是p0/p1/p2
  - 后端、运维、k8s的开发经验不多
  - 对不熟悉的技术有点不自信，但多花点时间一般都能解决
  - 算法题较弱

- 自我介绍
  - 大家好，我是金瑶，一个对开源项目和编辑器项目都很感兴趣的前端工程师，写过很多玩具demo，也写过一点Nodejs的后端。
  - 我最重要的工作经历也是最近的2份工作，我刚离职的工作是在已有的在线面试产品的基础上扩展新的云端AI Coding的产品，也就是Cursor的云端版。我主要负责开发AI相关的代码编辑器的插件，以及增强自研IDE的基础能力。另一份重要的工作是开发Affine协同办公的产品，主打文档与画板可以相互转换，我主要负责文档富文本元素的渲染及主要编辑交互逻辑的实现。
  - 我最近几份工作都是编辑器或IDE相关的，我本身对这个业务方向也很感兴趣，正好公司有相关的项目，希望有机会可以参与。

- 🤔 前两段工作离职的原因是什么
  - 22年affine是产品方向变动而裁员
  - 25年至简天成是盈利困难而裁员，为什么裁我，ide开发重点转向异步，编辑器插件会相互影响，添加功能时经常破坏已有功能，显得我的效率低
  - 🤼 不同老板对产品的理解和要求不同，前端很多时候都是够用就好，产品需求一直跟随市场需求在调整
# 20250717-海道教育/xbody-二面/boss
- ai产品竞争激烈的解决方法
  - 通过产品力、产品特色建立先发优势

- 有其他意向公司吗

- 有没有比较愉快的工作经历
  - 居然回答了没有
  - 实际的工作体验没想的那么重要，我在工作时最重视的是完成业务开发的同时积累技术，新工作正好有这方面的机会

- [Jenni AI](https://jenni.ai/)
  - Intelligent Research Assistant: The AI-powered workspace to help you read, write, and organize research with ease.
# 20250716-海道教育/xbody-一面/技术
- 技术问题
  - 为什么用slate及数据模型的结构
  - 编辑器框架如prosemirror的渲染原理
  - 动画编辑器、视频编辑器的了解，对直播实现是否了解

- 待改进
- 自我介绍

- 你在affine协同编辑产品中的工作内容，碰到的困难是如何解决的
  - 我在affine实现了块编辑器的富文本元素的渲染、slash斜杠菜单、文档评论、文档路由切换等功能。
  - 碰到的困难印象较深的是前端架构相关的，编辑器状态如何与外部组件通信，比如实现文档评论功能时，评论列表是在侧边栏，是否要作为编辑器插件实现，以及如何实现在选择文本时突出侧边栏的评论，可以将事件加在渲染的文本上，也可以根据编辑器的选区变化来确定评论位置。
  - 块编辑器自身如何设计块结构、扩展块至今仍是难题。
  - affine实现的编辑器在后来是自研架构，我一直在关注有所了解但不深入，包括分为业务层/blocksuite编辑层/yrs协作层，在2024年12月开始去掉blocksuite编辑层，不清楚是否重构完成。

- 你的编辑器或产品，相对于飞书有什么竞争力
  - 技术上，编辑器内提供多维表格block，实现简单且前端友好，易维护，易定制，可自定义字段
  - 产品特色主打 local-first, 方便私有化部署，数据可导出，交互体验会更快
  - 编辑器是非常通用的基础设施，可用于更多场景

- ai与文档结合的场景在业内有什么产品创意
  - 生产文本、图片
  - ask
  - 集成数据源

- 为什么想加入新产品
  - 很大程度是因为运气，碰到了我很感兴趣的工作内容

- 你有什么想问的
  - 新产品的核心形态、用户主要旅程，相关产品设计、需求交互相关的，团队是否有会议讨论，现在进展如何，我作为开发工程师这方面也不是很擅长
    - 从技术开发的角度，前端的核心架构是以文本编辑器为主还是画布为主，我的判断不准确，可能是画布
    - 新产品的业务场景中，对典型的多人协同编辑是否有需求，因为这一块技术复杂度高，代码很容易出bug，开发和维护成本都很高
  - 面向个人的toC ai产品 的市场竞争激烈，有考虑过获客方式吗，会和海道教育合作吗
  - 我对自己的评价，有一些缺点呢，看团队是否接受
  - 老板是否焦虑
# 202404-showmebug-一面
- 二叉树的构造 + 中序遍历
# 20211015-墨刀-一面/二面
- 墨刀产品系列
  - 思维导图、脑图
  - 流程图
  - 原型设计

- 脑图数据结构设计
  - 思路：树、sibling

- 流程图叶子节点增多时，动态调整布局的方法
  - 思路：深度优先计算高度、确定位置

- 文件管理器
  - 文件层数特别多 - 动态请求
  - 文件数量特别多 - 虚拟滚动

- 二面主要围绕产品
  - 原型设计基于 dom
  - 新产品 流程图、脑图基于canvas

## mipmap

- 在三维计算机图形的贴图渲染中有一个常用的技术被称为Mipmapping。
- 为了加快渲染速度和减少图像锯齿，贴图被处理成由一系列被预先计算和优化过的图片组成的文件, 这样的贴图被称为 MIP map 或者 mipmap。

- Mipmap中每一个层级的小图都是主图的一个特定比例的缩小细节的复制品。
  - 虽然在某些必要的视角，主图仍然会被使用，来渲染完整的细节。
  - 但是当贴图被缩小或者只需要从远距离观看时，mipmap就会转换到适当的层级。

- 因为mipmap的图片已经是做过抗锯齿处理的，从而减少了实时渲染的负担。放大和缩小也因为mipmap而变得更有效率。
# 20211015-投光编辑器-三面
- ot vs crdt

- 线性代数
# 20211014-投光编辑器-二面
- To define a type guard, we simply need to define a function whose return type is a type predicate

```typescript
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

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
