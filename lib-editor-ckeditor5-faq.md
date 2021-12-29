---
title: lib-editor-ckeditor5-faq
tags: [ckeditor, faq]
created: '2021-10-29T16:09:39.273Z'
modified: '2021-11-07T11:05:40.405Z'
---

# lib-editor-ckeditor5-faq

# faq-repeat

## data view vs editing view

- 都由model通过converter计算得到

- 使用场景不同
  - data侧重于粘贴、读写数据
  - editing侧重于编辑交互

- editor.data没有提供document属性，
  - editor.editing.view.document提供了虚拟dom的属性和操作方法

## [Dynamically update plugin view](https://github.com/ckeditor/ckeditor5/issues/1681)

- Generally speaking, the dynamic UI works using collections. 
  - `ViewCollections` can be bound to regular collections and work as view factories. 

- [Extending classes in plugins](https://github.com/ckeditor/ckeditor5/issues/7592)
  - EditingPlugin should be before UIPlugin

## image plugin

- [Support setting data attributes on image from upload adapters](https://github.com/ckeditor/ckeditor5/issues/5204)
  - For anyone interested, it's working fine providing that you extend the `imageBlock` schema.

- [How can i change all images src attributes inserted in editor?](https://github.com/ckeditor/ckeditor5/issues/1917)
  - You can use walker to iterate over a whole document.
  - Then check if `value.item.is( 'image' )` and then update it's `source` attribute

- [how to transform image's url post edit?](https://github.com/ckeditor/ckeditor5/issues/9056)
  - I have a use case where an article is first internal only, with image urls being internal url. When the article is published to public site, the images will be copied to public server and the url will be changed.
  -  You can use `TreeWalker` on the root to iterate over all elements in the document, filter `<image>` element and use `Writer` to change its model `src` attribute.

- [How can I add custom attribute and class on an Image after upload?](https://github.com/ckeditor/ckeditor5/issues/8943)
  - Hi! You can use e.g. `DowncastDispatcher` for listening on the image insertion and use `DowncastWriter` to add a proper class to your `<figure>` element (which by default wraps `<img>` element)

- [How to add custom attributes using custom upload adapter?](https://github.com/ckeditor/ckeditor5/issues/8192)

- [How can I set the alignment of a `<figcaption>`?](https://github.com/ckeditor/ckeditor5/issues/7848)
- Enabling the `AlignmentCommand` for a caption is tricky as image's caption is a limit element in the schema
  - The command limits itself to the content of a limit element so it does not even look up to the `<caption>` element.
  - So, the only options are: 
    - To rewrite AlignmentCommand and inject its replacement with e.g. webpack/normal-module-replacement-plugin
    - To override the existing command's `refresh()` logic directly in `editor.commands.get( 'alignment' )`. Uglier, but will work too.
    - To reconfigure the schema to allow blocks (e.g. paragraphs) inside `<caption>`. However, schema is not easily reconfigurable at the moment, so it might be tricky.
  - Also, as for the default alignment – this is controlled by the stylesheet. You can override it in your own stylesheet with a higher-specificity rule.

- [Pasted images should trigger upload if Image Upload plugin is enabled](https://github.com/ckeditor/ckeditor5/issues/2524)
  - a quite broad topic discussed already 

### image-toolbar

- [Can I modify, the default toolbar icon with custom text or icon](https://github.com/ckeditor/ckeditor5/issues/1702)
  - 官方faq提供了在webpack中配置toolbar图标的方法

- [How can I disable a custom toolbar button in CKEditor 5](https://github.com/ckeditor/ckeditor5/issues/8748)
  - Every item in the toolbar is an object created from ButtonView or DropdownView class
  - Those classes have isEnabled property. Setting it to false will disable this item. 
  - editor.ui.view.toolbar.items

- [how to remove all tooltip?](https://github.com/ckeditor/ckeditor5/issues/5452)
  - I can not find a way to remove the imagetoolbar tooltip.
  - .ck.ck-button .ck.ck-tooltip { display: none; }

### image-plugin-not-yet

- [Where is the event for deleting of image?](https://github.com/ckeditor/ckeditor5/issues/8738)
  - At the moment, I don't think that we'll be interested in adding an image-specific event. I'm happy to see, though
  - There's no specific event for image removal. Similar information may be obtained from event-change:data 
# faq-not-yet
- [Figure out how to expose utils API via plugins](https://github.com/ckeditor/ckeditor5/issues/8925)
# faq

## 

## 

## [Is there a conveniant way to add custom classes?](https://github.com/ckeditor/ckeditor5/issues/1462)

- You can read more about `attributeToAttribute()` conversion helper.

- Unfortunately,  `<ul>`s are more difficult because of the approach we took when implementing them. In the model, lists are represented the same way paragraphs are. This means that there is no actual `<ul>` element in the model, it is a flat structure, with indentation levels represented through attributes.
  - This gave us more stable algorithms for features like enter, removing selections spanning over multiple items, merging blocks, etc. 
  - The drawback is that you don't have the parent element - it is created "on the fly" during conversion.
  - One reasonable way to overcome this would be to assign anything that you'd like on `<ul>` to the first item in the list. We will use this approach when we will start implementing features like lists starting number or lists styles. But this requires writing a custom converter, it is more difficult than the example above.

## [Why is the `toWidget` only for container elements](https://github.com/ckeditor/ckeditor5/issues/7934)

- The main problem for this might be that different view elements have different purpose. The widget system, as for now, is prepared to handle blocks of content. Those usually resides directly in root (or in other block, but let's simplify that) alongside other content. This is true for images, tables, etc. 
- For instance,  `AttributeElement` is treated as an inline, most likely a text attribute, which is not distinguishable from any other `AttributeElement` (in majority of cases). Attribute elements of the same/similar type might be merged together. Most notably is that `<strong>foo</strong><strong>bar</strong>` should be one: `<strong>foobar</strong>` and using `AttributeElement` allows to achieve that. Even though you'd create two instances of `AttributeElement` it will be merged in the data (in the default behavior, but it can be changed)
- In this terms `AttributeElement` is not suited for widgets in my opinion. We do have explored inline widgets but we do not have official plugin that use that. In other words it is not 100% supported and we have only one approved pattern for this. In other words, we can't guarantee that other use-cases will work as we do not test them. If that worked it might be just a coincidence

- [RawElements cannot be widgets, even though documentation says they can](https://github.com/ckeditor/ckeditor5/issues/9687)

## [How to apply CKEditor 5 Bold Plugin to my own inline elements?](https://github.com/ckeditor/ckeditor5/issues/6033)

- Unfortunately, styling inline widgets isn't supported and introducing it will require some bigger changes. 

- [Inline widget styling](https://github.com/ckeditor/ckeditor5/issues/1633)
- I created a workaround for this. It's not optimal but instead of creating `<strong> or <em>` HTML elements inside the inline widget, I add a `strong="true", italic="true"` attributes in the widget element.

## [Why can I insert a custom element into ckeditor without modifying the schema](https://stackoverflow.com/questions/52156467)

- The reason for that is that it's a pretty low-level tool which implements ways to perform atomic operations on the model (OK, I'm lying here, because there's an even lower level underneath, represented by operations themselves, but that's a protected API). Anyway, the writer is pretty low-level.
  - when you implement a command or any other feature you may need to perform multiple operations to do all the necessary changes. The state in the meantime (between these atomic operations) may be incorrect. The writer must allow that.
  - we could solve by checking the schema at the end of a `change()` block 

## raw elements(能被选中) vs ui elements(不可选中)

- [raw elements](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_rawelement-RawElement.html)
  - Raw elements work as data containers but their children are not managed or even recognized by the editor.
  - 方便集成。Raw elements are a perfect tool for integration with external frameworks and data sources.
  - they are considered by the editor selection and they can work as widgets.
  - You should not use raw elements to render the UI in the editor content
  - 注意editingDowncast中，createRawElement('div', options)创建div作为react组件容器

- [ui elements](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_uielement-UIElement.html)
  - It should be used to represent editing UI which needs to be injected into the editing view
  - The editor will ignore your UI element
    - the selection cannot be placed in it, 
    - it is skipped (invisible) when the user modifies the selection by using arrow keys 
    - and the editor does not listen to any mutations which happen inside your UI elements.
  - The limitation is that you cannot convert a model element to a UI element. 
    - UI elements need to be created for markers or as additional elements inside normal container elements.

## [How to pass data to a plugin? ](https://github.com/ckeditor/ckeditor5/issues/5611)

- You should be able to use `editor.config` property
