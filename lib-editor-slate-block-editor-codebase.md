---
title: lib-editor-slate-block-editor-codebase
tags: [block-editor, codebase, slate]
created: 2022-05-27T09:43:58.962Z
modified: 2022-05-27T09:44:18.922Z
---

# lib-editor-slate-block-editor-codebase

# guide

# block-editor-codebase
- block-editor的plugin设计
  - 在Plugin构造函数中注册各类事件监听器，在editor render-root中执行所有RENDER事件
  - 在editor-block中，也可以注册事件到全局hooks

- BlockEditor
  - 准备编辑器相关配置包括blocks和plugins，初始化 BlockEditor 实例
  - RenderRoot 传入BlockEditor实例
  - RenderBlock 传入root_block_id
  - mock未传入root_id时，手动先创建page再渲染editor

- RenderRoot
  - 获取editor最外层的div元素ref，挂到editor.container属性下
    - editor的内容blocks会作为children渲染
  - editor.getHooks().render(); 
    - 执行所有render类型的hooks，此时plugins中的document.createElement已经创建了容器但内容可能未渲染
  - 注册全局鼠标事件到editor最外层div
    - onMouseUp/Down/Move/Out，注册的事件是所有hooks回调函数集合
  - 创建 SelectionRect 元素

- RenderBlock
  - 异步获取业务block对象
  - 每个block最外层都是div，div ref会挂到block.dom属性下
  - 通过 block_util?.createView({ block, editor }) 渲染block视图
    - 会执行业务block如 Heading1/DividerBlock 的createView方法
  - 注册当前block的 onMouseMove 事件到editor全局
  - 提供了block层级的选区事件 useOnSelect/useOnSelectionChange

- useBlock
  - 返回AsyncBlock对象
  - 返回的block对象会自动触发block重渲染，实现通过 node.on('change', () => { requestReRender(); }); 

- BlockEditor
  - PluginManager
  - SelectionManager
  - CacheManager
  - StorageManager
  - hooks: this.hooks = new Hooks(); 
  - block_utils  支持的所有blocks
  - workspace_id
  - root_block_id
  - readonly
  - ui_container
  - 提供了编辑器的对外操作方法

- Hooks 用来保存和操作回调函数
  - `hooks_map: Map<string, PluginHookInfo[]> = new Map()` 键值对 (init/render/onEvent/resize, 回调函数)
  - 提供了回调函数的操作方法 addHook/removeHook/run_hook/init/render/onRootNodeMouseMove

- PluginManager 用来保存和操作plugin对象
  - `plugins: Record<string, Plugin> = {};` 键值对
  - const plugin: Plugin = new createPlugin(this.editor, this.hooks); 
    - 每个plugin对象创建时，都能拿到所有hooks
  - 提供了plugin的操作方法 register/deregister/dispose

- page-block
  - createPageView
# block-editor-codebase-v20220429-legacy-slash-menu-基础结构变化不大
- db层的设计
  - getContent 用来获取block内容
  - getChildren 用来构建block间的关系

- 全局共享的editor对象，只在db初始化时创建一次，并未对外暴露修改自身的方法，所以可以直接在editor对象上添加新属性

- BlockEditorEntry
  - editor.loadBlock(rootId)
  - editor.setRootBlock( editor.getBlockById(rootId) )
  - 提供editor默认插件和配置

- EditorRoot
  - 将全局共享的editor对象通过 EditorContext. Provider 传递下去
  - 触发编辑器的渲染 editor.pluginManager.runHook('render'); 

- RenderBlock
  - `return <RenderBlockContent {...props} />;` 直接把props传过去渲染Content
  - 注册 content 和 children 的监听器，触发block的重渲染

- RenderBlockContent
  - 渲染 `<View {...context}></View>` ，所有View都传入editor和RenderChildren/Map方法

- 在renderBlockContent中，如何将react组件的ref保存到全局editor
  - 作用是，可以在全局拿到react组件内通过useImperativeHandle对外暴露的方法
  - 然后在全局通过类似 editor.getBlockCompById(id).getSelectionByOffset() 这样的方法直接更新react组件

```tsx
const ref = useRef(null);

const context = {
    editor: editor,
    block: block,
    renderNode: renderNode,
    RenderBlock: RenderBlock,
    useBlock: getOrCreateUseBlock(editor),
    RenderChildren: RenderChildren,
    RenderChildrenMap: RenderChildrenMap,
    ...customProps
};

context.ref = block.ref = renderNode.ref = ref;

return {View ? <View {...context}></View> : null}

// view block
const Page = forwardRef((props: Props, ref) => {

  useImperativeHandle(ref, () => ({
        open: () => {
            return linkRef.current?.open?.();
        },
        getSelectionByOffset: (offset: number) => {
            return containerRef.current?.getSelectionByOffset?.(offset);
        }
    }));

    return isRootNode ? <PageContainer  ref={containerRef} {...props} /> : <PageAsLink block={block} />;

}
```
