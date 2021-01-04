---
tags: [react, typescript]
title: note-react-typescript
created: '2020-06-24T08:39:45.804Z'
modified: '2020-06-24T08:40:39.069Z'
---

# note-react-typescript

# guide

- `ReactElement` and `JSX.Element` are the result of invoking `React.createElement` directly or via JSX transpilation. 
  - It is an object with `type` , `props` and `key` . 
  - JSX. Element is ReactElement, whose `props` and `type` have type `any` , so they are more or less the same.
  - You can assign almost everything to `ReactNode` . I usually would prefer stronger types, but there might be some valid cases to use it.
  - A ReactElement is an object with a type and props. 
    - React reads these objects and uses them to construct the DOM. 
    - JSX.Element, on the other hand, is a ReactElement with generic type for props and type being any.
    - Even though JSX can be used in React to create React elements, React does not require JSX to work, you could replace it with vanilla JavaScript.
- Why do the render methods of class components return `ReactNode` , but function components return `ReactElement`
  - It is a current TS type incompatibility not related to core React.
    - TS class component: returns ReactNode with render(), more permissive than React/JS
    - TS function component: returns JSX.Element | null, more restrictive than React/JS
  - In principle, render() in React/JS class components supports the same return types as a function component. 
  - With regard to TS, the different types are a type inconsistency still kept due to historical reasons and the need for backwards-compatibility.

- ref
  - [精读《@types react 值得注意的TS技巧》](https://zhuanlan.zhihu.com/p/129632306)

- ## hooks相关类型

``` typescript
type SetStateAction<S> = S | ((prevState: S) => S);
type Dispatch<A> = (value: A) => void;
type DispatchWithoutAction = () => void;
type Reducer<S, A> = (prevState: S, action: A) => S;
type ReducerWithoutAction<S> = (prevState: S) => S;
type ReducerState<R extends Reducer<any, any>> = R extends Reducer<infer S, any> ? S : never;
type DependencyList = ReadonlyArray<any>;
type EffectCallback = () => (void | (() => void | undefined));
interface MutableRefObject<T> {
        current: T;
    }

function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>];
function useState<S = undefined>(): [S | undefined, Dispatch<SetStateAction<S | undefined>>];

function useReducer<R extends ReducerWithoutAction<any>, I>(
        reducer: R,
        initializerArg: I,
        initializer: (arg: I) => ReducerStateWithoutAction<R>
    ): [ReducerStateWithoutAction<R>, DispatchWithoutAction];
 function useReducer<R extends ReducerWithoutAction<any>>(
        reducer: R,
        initializerArg: ReducerStateWithoutAction<R>,
        initializer?: undefined
    ): [ReducerStateWithoutAction<R>, DispatchWithoutAction];

function useContext<T>(context: Context<T>/*, (not public API) observedBits?: number|boolean */): T;

function useRef<T>(initialValue: T): MutableRefObject<T>;
function useRef<T>(initialValue: T|null): RefObject<T>;
function useImperativeHandle<T, R extends T>(ref: Ref<T>|undefined, init: () => R, deps?: DependencyList): void;

function useEffect(effect: EffectCallback, deps?: DependencyList): void;
function useLayoutEffect(effect: EffectCallback, deps?: DependencyList): void;

function useMemo<T>(factory: () => T, deps: DependencyList | undefined): T;
function useCallback<T extends (...args: any[]) => any>(callback: T, deps: DependencyList): T;

function useDebugValue<T>(value: T, format?: (value: T) => any): void;
```

- ## react组件及api相关类型
- `type ComponentType<P = {}> = ComponentClass<P> | FunctionComponent<P>;`
  - `type FC<P = {}> = FunctionComponent<P>;` SFC is deprecated for FC
  - `type ComponentState = any;`
- `type ReactInstance = Component<any> | Element;`
- `interface Component<P = {}, S = {}, SS = any> extends ComponentLifecycle<P, S, SS> { }`
  - SS is the user defined type of the snapshot returned by your custom implementation of getSnapshotBeforeUpdate, which gets passed to componentDidUpdate so you can preserve some application specific details from the last render

``` typescript
interface Props<T> {
    children?: ReactNode;
    key?: Key;
    ref?: LegacyRef<T>;
}
interface HTMLProps<T> extends AllHTMLAttributes<T>, ClassAttributes<T> { }
type DetailedHTMLProps<E extends HTMLAttributes<T>, T> = ClassAttributes<T> & E;
interface DOMAttributes<T> {
  children?: ReactNode;
  dangerouslySetInnerHTML?: {
    __html: string;
  };
  onChange?: FormEventHandler<T>;
  // ...
}

export interface CSSProperties extends CSS.Properties<string | number> {}
interface HTMLAttributes<T> extends AriaAttributes, DOMAttributes<T> {
  defaultChecked?: boolean;
  defaultValue?: string | number | string[];
  suppressContentEditableWarning?: boolean;
  suppressHydrationWarning?: boolean;
  className?: string;
  contentEditable?: Booleanish | "inherit";
  style?: CSSProperties;
  tabIndex?: number;
  // ...
}
interface AllHTMLAttributes<T> extends HTMLAttributes<T> {
  //  ...
 }
interface ReactHTML {
  a: DetailedHTMLFactory<AnchorHTMLAttributes<HTMLAnchorElement>, HTMLAnchorElement>;
  abbr: DetailedHTMLFactory<HTMLAttributes<HTMLElement>, HTMLElement>;
  address: DetailedHTMLFactory<HTMLAttributes<HTMLElement>, HTMLElement>;
  area: DetailedHTMLFactory<AreaHTMLAttributes<HTMLAreaElement>, HTMLAreaElement>;
  article: DetailedHTMLFactory<HTMLAttributes<HTMLElement>, HTMLElement>;
  aside: DetailedHTMLFactory<HTMLAttributes<HTMLElement>, HTMLElement>;
  audio: DetailedHTMLFactory<AudioHTMLAttributes<HTMLAudioElement>, HTMLAudioElement>;
  // ...
}
interface ReactDOM extends ReactHTML, ReactSVG { }

interface ReactPortal extends ReactElement {
    key: Key | null;
    children: ReactNode;
}

interface RefObject<T> {
    readonly current: T | null;
}
type RefCallback<T> = { bivarianceHack(instance: T | null): void }["bivarianceHack"];
type Ref<T> = RefCallback<T> | RefObject<T> | null;
function createRef<T>(): RefObject<T>;
function forwardRef<T, P = {}>(render: ForwardRefRenderFunction<T, P>): ForwardRefExoticComponent<PropsWithoutRef<P> & RefAttributes<T>>;
type PropsWithoutRef<P> ='ref' extends keyof P
            ? Pick<P, Exclude<keyof P, 'ref'>>
            : P;
type PropsWithRef<P> ='ref' extends keyof P
            ? P extends { ref?: infer R }
                ? string extends R
                    ? PropsWithoutRef<P> & { ref?: Exclude<R, string> }
                    : P
                : P
            : P;
type PropsWithChildren<P> = P & { children?: ReactNode };

interface ReactChildren {
    map<T, C>(children: C | C[], fn: (child: C, index: number) => T):
        C extends null | undefined ? C : Array<Exclude<T, boolean | null | undefined>>;
    forEach<C>(children: C | C[], fn: (child: C, index: number) => void): void;
    count(children: any): number;
    only<C>(children: C): C extends any[] ? never : C;
    toArray(children: ReactNode | ReactNode[]): Array<Exclude<ReactNode, boolean | null | undefined>>;
}

function createElement(
    type: "input",
    props?: InputHTMLAttributes<HTMLInputElement> & ClassAttributes<HTMLInputElement> | null,
    ...children: ReactNode[]): DetailedReactHTMLElement<InputHTMLAttributes<HTMLInputElement>, HTMLInputElement>;

function createElement<P extends HTMLAttributes<T>, T extends HTMLElement>(
    type: keyof ReactHTML,
    props?: ClassAttributes<T> & P | null,
    ...children: ReactNode[]): DetailedReactHTMLElement<P, T>;
  
 function createElement<P extends {}>(
    type: FunctionComponent<P>,
    props?: Attributes & P | null,
    ...children: ReactNode[]): FunctionComponentElement<P>;

function createElement<P extends {}>(
    type: ClassType<P, ClassicComponent<P, ComponentState>, ClassicComponentClass<P>>,
    props?: ClassAttributes<ClassicComponent<P, ComponentState>> & P | null,
    ...children: ReactNode[]): CElement<P, ClassicComponent<P, ComponentState>>;
    
interface ForwardRefRenderFunction<T, P = {}> {
    (props: PropsWithChildren<P>, ref: Ref<T>): ReactElement | null;
    displayName?: string;
    // explicit rejected with `never` required due to
    // https://github.com/microsoft/TypeScript/issues/36826
    /** defaultProps are not supported on render functions */
    defaultProps?: never;
    /** propTypes are not supported on render functions */
    propTypes?: never;
}

interface BaseSyntheticEvent<E = object, C = any, T = any> {
    nativeEvent: E;
    currentTarget: C;
    target: T;
    bubbles: boolean;
    cancelable: boolean;
    defaultPrevented: boolean;
    eventPhase: number;
    isTrusted: boolean;
    preventDefault(): void;
    isDefaultPrevented(): boolean;
    stopPropagation(): void;
    isPropagationStopped(): boolean;
    persist(): void;
    timeStamp: number;
    type: string;
}
interface SyntheticEvent<T = Element, E = Event> extends BaseSyntheticEvent<E, EventTarget & T, EventTarget> {}
```

- ## 函数组件

``` typescript
interface FunctionComponent<P = {}> {
    (props: PropsWithChildren<P>, context?: any): ReactElement | null;
    propTypes?: WeakValidationMap<P>;
    contextTypes?: ValidationMap<any>;
    defaultProps?: Partial<P>;
    displayName?: string;
}

type FC<P = {}> = FunctionComponent<P>;
```

- ## 类组件

``` typescript
class Component<P, S> {
  static contextType?: Context<any>;
  constructor(props: Readonly<P>);
  readonly props: Readonly<P> & Readonly<{ children?: ReactNode }>;
  state: Readonly<S>;
  context: any;
  setState<K extends keyof S>(
          state: ((prevState: Readonly<S>, props: Readonly<P>) => (Pick<S, K> | S | null)) | (Pick<S, K> | S | null),
          callback?: () => void
      ): void;
  forceUpdate(callback?: () => void): void;
  render(): ReactNode;
}

class PureComponent<P = {}, S = {}, SS = any> extends Component<P, S, SS> { }

interface Component<P = {}, S = {}, SS = any> extends ComponentLifecycle<P, S, SS> { }

interface ComponentClass<P = {}, S = ComponentState> extends StaticLifecycle<P, S> {
    new (props: P, context?: any): Component<P, S>;
    propTypes?: WeakValidationMap<P>;
    contextType?: Context<any>;
    contextTypes?: ValidationMap<any>;
    childContextTypes?: ValidationMap<any>;
    defaultProps?: Partial<P>;
    displayName?: string;
}

interface StaticLifecycle<P, S> {
    getDerivedStateFromProps?: GetDerivedStateFromProps<P, S>;
    getDerivedStateFromError?: GetDerivedStateFromError<P, S>;
}
type GetDerivedStateFromProps<P, S> = (nextProps: Readonly<P>, prevState: S) => Partial<S> | null;
type GetDerivedStateFromError<P, S> = (error: any) => Partial<S> | null;

interface ComponentLifecycle<P, S, SS = any> extends NewLifecycle<P, S, SS>, DeprecatedLifecycle<P, S> {
  componentDidMount?(): void;
  shouldComponentUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): boolean;
  componentWillUnmount?(): void;
  componentDidCatch?(error: Error, errorInfo: ErrorInfo): void;
}
interface NewLifecycle<P, S, SS> {
  getSnapshotBeforeUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>): SS | null;
  componentDidUpdate?(prevProps: Readonly<P>, prevState: Readonly<S>, snapshot?: SS): void;
}
interface DeprecatedLifecycle<P, S> {
  componentWillMount?(): void;
  componentWillReceiveProps?(nextProps: Readonly<P>, nextContext: any): void;
  componentWillUpdate?(nextProps: Readonly<P>, nextState: Readonly<S>, nextContext: any): void;
}

type ClassType<P, T extends Component<P, ComponentState>, C extends ComponentClass<P>> =
      C & (new (props: P, context?: any) => T);

interface ClassicComponent<P = {}, S = {}> extends Component<P, S> {
    replaceState(nextState: S, callback?: () => void): void;
    isMounted(): boolean;
    getInitialState?(): S;
}
interface ClassicComponentClass<P = {}> extends ComponentClass<P> {
    new (props: P, context?: any): ClassicComponent<P, ComponentState>;
    getDefaultProps?(): P;
}
```

- ## 元素相关

``` typescript
// ReactType is deprecated for ElementType
type ElementType<P = any> =
    {
        [K in keyof JSX.IntrinsicElements]: P extends JSX.IntrinsicElements[K] ? K : never
    }[keyof JSX.IntrinsicElements] |
    ComponentType<P>;

/** A ReactElement is an object with a type and props. */
interface ReactElement<P = any, T extends string | JSXElementConstructor<any> = string | JSXElementConstructor<any>> {
    type: T;
    props: P;
    key: Key | null;
}

type JSXElementConstructor<P> =
        | ((props: P) => ReactElement | null)
        | (new (props: P) => Component<P, any>);

interface ReactComponentElement<
    T extends keyof JSX.IntrinsicElements | JSXElementConstructor<any>,
    P = Pick<ComponentProps<T>, Exclude<keyof ComponentProps<T>, 'key' | 'ref'>>
> extends ReactElement<P, Exclude<T, number>> { }

interface FunctionComponentElement<P> extends ReactElement<P, FunctionComponent<P>> {
      ref?: 'ref' extends keyof P ? P extends { ref?: infer R } ? R : never : never;
  }

interface ComponentElement<P, T extends Component<P, ComponentState>> extends ReactElement<P, ComponentClass<P>> {
      ref?: LegacyRef<T>;
  }

interface DetailedReactHTMLElement<P extends HTMLAttributes<T>, T extends HTMLElement> extends DOMElement<P, T> {
        type: keyof ReactHTML;
    }

interface ReactHTMLElement<T extends HTMLElement> extends DetailedReactHTMLElement<AllHTMLAttributes<T>, T> { }

declare global {
  namespace JSX {
    /** JSX.Element is a ReactElement, with the generic type for props and type being any. 
    It exists, as various libraries can implement JSX in their own way */
    interface Element extends React.ReactElement<any, any> { }
    interface ElementClass extends React.Component<any> {
        render(): React.ReactNode;
    }
  }
}
```

- ## Node相关

``` typescript
type ReactText = string | number;
type ReactChild = ReactElement | ReactText;

interface ReactNodeArray extends Array<ReactNode> {}
type ReactFragment = {} | ReactNodeArray;

/** A ReactNode is a ReactElement, a ReactFragment, a string, a number or an array of ReactNodes, or null, or undefined, or a boolean */
type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;
```

# 类型示例examples

``` typescript
// Use type inference; inferred return type is `JSX.Element | null`
const MyComp1 = ({ condition }: { condition: boolean }) =>
    condition ? <div>Hello</div> : null

// Use explicit function return types; Add `null` , if needed
const MyComp2 = (): JSX.Element => <div>Hello</div>; 
const MyComp3 = (): React.ReactElement => <div>Hello</div>;  
// Option 3 is equivalent to 2 + we don't need to use a global (JSX namespace)

// Use built-in `FunctionComponent` or `FC` type
const MyComp4: React.FC<MyProps> = () => <div>Hello</div>;

```
