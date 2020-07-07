---
tags: [draft, todo]
title: draft-pieces
created: '2019-11-11T06:57:46.101Z'
modified: '2020-06-22T08:05:05.869Z'
---

# draft-pieces


- state-multi-context
  - diegohaz/constate
  - CharlesStover/react-multi-context
  - dai-shi/react-context-global-state
- state-状态管理技术选型
  - recoil (要等到API稳定、功能齐全)
  - constate
  - unstated-next
  - react-hooks-global-state
  - [RFC: Context selectors](https://github.com/reactjs/rfcs/pull/119)
  - [Four different approaches to non-Redux global state libraries](https://blog.axlight.com/posts/four-different-approaches-to-non-redux-global-state-libraries/)
    - whether context based or external store
    - whether subscriptions based or context propagation

- constate
  - With Constate, you'll have multiple contexts provided at different levels of your component tree (depending on each components use them). 
  - Also, it's a seamlessly migration from local state (with React hooks) to shared ones, which is not supported by Redux (so easily).
  - ref
    - https://github.com/diegohaz/constate/issues/81

- concurrent mode重点关注的是UX，之前的feature如hooks大多关注的的是DX
  - 国内对于使用concurrent mode并不热情，因为用户体验难以量化

- **SWR与前端数据依赖请求**
- 数据依赖关系其实是一个 DAG（有向无环图）。有些数据依赖于其他，有的则无依赖性，对数据的请求则是对这个有向无环图的遍历。
- 最高效的请求方式一定是在拓扑序上尽可能地并行（每当一个数据的依赖都就绪时，立即发起请求）
- 大部分时候（请求并不复杂时），我们用 `Promise.all` 来描述这个 DAG
- `Promise.all([fetchA(), fetchB()]).then([a, b] => fetchC(a, b))`
- swr只需要描述 DAG 中，每一个点的被指向边即可（数据依赖）。
- 每次渲染的时候，SWR会试着执行取数函数（例如 `()=> '/api/c?a=' + A.id` )
  - 如果这个函数抛出异常，那么就意味着它的依赖还没有就绪（A === undefined），SWR将暂停这个数据的请求。
  - 在任一数据完成加载时，由于 `setState` 触发重渲染，上述Hooks会被重选执行一遍（再次检查数据依赖是否就绪），然后对就绪的数据发起新的一轮请求。
  - SWR allows you to fetch data that depends on other data. It ensures the maximum possible parallelism (avoiding waterfalls), as well as serial fetching when a piece of dynamic data is required for the next data fetch to happen.

- **stale-while-revalidate**
- ref
  - [深入浅出 useSWR 原理](https://zhuanlan.zhihu.com/p/93824106)

- **waterfall图展示的请求时间过长的问题**
  - an unintentional request sequence that should have been parallelized
  - 本可以并行执行的并行执行的请求却串行执行了
  - chrome的Waterfall列列出了每个网络请求对应的开始时间和结束时间
    - 从图中可以看出，这一系列请求有明显的先后关系。除了个别请求的时间范围（色块）存在重叠，大部分的都是前后相连的。这就说明它们之间有串行关系
    - 假如所有的网络请求都能改成并行的话，我们能将网络IO需要的时间降低至原来的1/10左右。
    - 首先，将被诊断页面的网络请求按照数据依赖关系分成几个组。如请求B的参数来自于请求A的结果，则B必须在A之后的组中。然后，组内并行请求，组间串行请求。

``` JS
// 这是串行写法
async fetchData1() {
  // 执行完一个再执行下一个
  await fetchStudent()
  await fetchTeacher()
  await fetchSchool()
}

// 这是并行写法
async fetchData2() {
  await Promise.all([
    // 互相之间无等待关系
    fetchStudent(),
    fetchTeacher(),
    fetchSchool()
  ])
}

// 当不易一次全部处理时，可以将arr的定义和Promise.all操作分开
async fetchData3() {
  let arr = []
  // something
  arr.push(fetchStudent())
  //other things
  arr.push(fetchTeacher())
  //...
  arr.push(fetchSchool())
  await Promise.all(arr)
}
```

  - 浏览器根据html中外连资源出现的顺序，依次放入队列Queue, 然后根据优先级确定向服务器获取资源的顺序。同优先级的资源根据html中出现的先后顺序来向服务器获取资源
  - Queueing: 出现下面的情况时，浏览器会把当前请求放入队列中进行排队
    - 有更高优先级的请求时.
    - 和目标服务器已经建立了6个TCP连接（最多6个，适用于HTTP/1.0和HTTP/1.1）
    - 浏览器正在硬盘缓存上简单的分配空间
  - 提高性能方法
    - 首先, 减少所有资源的加载时间. 亦即减小瀑布图的宽度. 
    - 其次, 减少请求数量，也就是降低瀑布图的高度. 瀑布图越矮越好.
    - 最后, 通过优化资源请求顺序来加快渲染时间. 
  - ref
    - [Chrome的Waterfall](https://www.cnblogs.com/shengulong/p/7449927.html)
    - [优化前端应用性能 — 网络篇](https://medium.com/@banyudu/%E4%BC%98%E5%8C%96%E5%89%8D%E7%AB%AF%E5%BA%94%E7%94%A8%E6%80%A7%E8%83%BD-%E7%BD%91%E7%BB%9C%E7%AF%87-b94feefeb8b0)

- race conditions问题
  - Race conditions are bugs that happen due to incorrect assumptions about the order in which our code may run
  - Race Condition 是开发中经常遇到的问题，比如查询天气的时候，先输入“北京”，再输入“深圳”，这时将发起 2 个请求。很可第一个请求花的时间比第二个请求长，如果不做处理，最终看到的是北京的天气，而不是深圳
  - 即前面请求的响应结果，在靠后的时机返回，后面请求结果先返回
  - 竞态条件出现的原因是无法保证异步操作的完成会按照他们开始时同样的顺序
  - 解决方式很简单，在useEffect返回的cleanup函数中清理数据或设置失效标记，然后在更新数据前根据标记判断其有效性
  - 上面这种方案虽然解决了问题，但体验并不好。
    - 在输入数据的过程中，并不能看到输入过程中返回的结果，只能看到最终的结果。我们期望的效果是输入过程中能实时展示有效的结果
    - 可以引入2个全局变量，一个变量用来标识当前请求的序号，另一个记录上一个有效请求的序号。只有序号比上一个有效序号大的时候，才展示数据。这样就保证了旧的请求不会覆盖新的请求
  - 还可以将setState的第一个参数设为函数来解决 
  - ref
    - [React Hooks 搞定 Race Condition](https://segmentfault.com/a/1190000019893237)
    - [Race conditions in React and beyond](https://wanago.io/2020/03/02/race-conditions-in-react-and-beyond-a-race-condition-guard-with-typescript/)
    - [化解使用 Promise 时的竞态条件](https://efe.baidu.com/blog/defusing-race-conditions-when-using-promises/)
    - [How to fetch data with React Hooks?](https://www.robinwieruch.de/react-hooks-fetch-data)
- react-concurrent-mode新特性
  - Suspense/SuspenseList
    - 指定组件的loading状态/loading组件出现顺序
  - useTransition
    - 更新时先pending，展示现有信息不变部分，loading变化部分
  - useDeferredValue
    - 让占性能的组件先使用旧值
  - Priority-based Rendering 策略
    - 优先执行需要立刻响应的状态更新，延迟占性能的更新，先看旧内容
- Priority-based Rendering
  - 将需要立刻渲染的 `setState` 放在 `startTransition` 外，将占性能的操作及计算放在 `startTransition` 内
  - [Splitting High and Low Priority State](https://reactjs.org/docs/concurrent-mode-patterns.html#splitting-high-and-low-priority-state)

 
------  

- class extends

``` js
class B {
  print = () => {
    console.log('print b');
  }
}

class D extends B {
  print() {
    console.log('before-super-print');
    super.print();
    console.log('after-super-print');
    console.log('print d');
  }
}

const d = new D();
d.print();
d.__proto__.print()
// print b
// before-super-print
```

- musicbrainz-rename

``` 
$if2(%albumartist%,%artist%)/
$if(%albumartist%,%album%/,)
$if($gt(%totaldiscs%,1),%discnumber%-,)$if($and(%albumartist%,%tracknumber%),$num(%tracknumber%,2) ,)$if(%_multiartist%,%artist% - ,)%title%
```

- maven-aliyun: https://maven.aliyun.com/repository/central 
- emotion的button

``` 
 const renderButton = (Root: React.ElementType<any> = 'button') => (
    <Root
      ref={forwardRef}
      type={Root === 'button' ? 'button' : undefined}
      {...(rest as HTMLElementProps<any>)}
      {...commonProps}
    >
      <span
        className={css`
          // Usually for this to take effect, you would need the element to be
          // "positioned". Due to an obscure part of CSS spec, flex children
          // respect z-index without the position property being set.
          //
          // https://www.w3.org/TR/css-flexbox-1/#painting
          z-index: 1;
        `}
      >
        {children}
      </span>
    </Root>
  );

  if (usesCustomElement(props)) {
    return renderButton(props.as);
  }

  if (usesLinkElement(props)) {
    return renderButton('a');
  }

  return renderButton();
```

- bootstrap 4的breakpoints

``` 
$font-size-base:  1rem !default; // Assumes the browser default, `16px`
$font-size-lg: $font-size-base * 1.25 !default;
$font-size-sm: $font-size-base * .875 !default;

$grid-breakpoints: (
  xs: 0,
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1200px
) !default;
```

- react-data-grid使用的className
  - 不确定的类
      - row-selected， has-tooltip，has-error
  - 使用了的样式
      - pull-right
      - glyphicon-remove form-control-feedback
  - ChildRowDeleteButton组件使用了glyphicon glyphicon-remove-sign 
  - FilterableHeaderCell组件使用了form-group/control
