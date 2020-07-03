---
tags: [react, typescript]
title: note-react-typescript
created: '2020-06-24T08:39:45.804Z'
modified: '2020-06-24T08:40:39.069Z'
---

# note-react-typescript

## guide

- ref
  - [精读《@types react 值得注意的TS技巧》](https://zhuanlan.zhihu.com/p/129632306)

- 组件相关

``` typescript
interface ComponentClass<P = {}, S = ComponentState> extends StaticLifecycle<P, S> {
    new (props: P, context?: any): Component<P, S>;
    propTypes?: WeakValidationMap<P>;
    contextType?: Context<any>;
    contextTypes?: ValidationMap<any>;
    childContextTypes?: ValidationMap<any>;
    defaultProps?: Partial<P>;
    displayName?: string;
}

interface FunctionComponent<P = {}> {
    (props: PropsWithChildren<P>, context?: any): ReactElement | null;
    propTypes?: WeakValidationMap<P>;
    contextTypes?: ValidationMap<any>;
    defaultProps?: Partial<P>;
    displayName?: string;
}

interface StaticLifecycle<P, S> {
    getDerivedStateFromProps?: GetDerivedStateFromProps<P, S>;
    getDerivedStateFromError?: GetDerivedStateFromError<P, S>;
}
```

- `type ComponentType<P = {}> = ComponentClass<P> | FunctionComponent<P>;`
  - `type FC<P = {}> = FunctionComponent<P>;` SFC is deprecated for FC
  - `type ComponentState = any;`
- `interface Component<P = {}, S = {}, SS = any> extends ComponentLifecycle<P, S, SS> { }`
  - SS is the user defined type of the snapshot returned by your custom implementation of getSnapshotBeforeUpdate, which gets passed to componentDidUpdate so you can preserve some application specific details from the last render
- 类组件

``` typescript
class Component<P, S> {
  constructor(props: Readonly<P>);
  state: Readonly<S>;
}
```

- `class PureComponent<P = {}, S = {}, SS = any> extends Component<P, S, SS> { }`
- 元素相关

``` typescript
type ElementType<P = any> =
    {
        [K in keyof JSX.IntrinsicElements]: P extends JSX.IntrinsicElements[K] ? K : never
    }[keyof JSX.IntrinsicElements] |
    ComponentType<P>;
// ReactType is deprecated for ElementType

interface ReactElement<P = any, T extends string | JSXElementConstructor<any> = string | JSXElementConstructor<any>> {
    type: T;
    props: P;
    key: Key | null;
}
```

- Node相关

``` typescript
type ReactText = string | number;
type ReactChild = ReactElement | ReactText;

interface ReactNodeArray extends Array<ReactNode> {}
type ReactFragment = {} | ReactNodeArray;
type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;
```
