---
title: toc-app-vscode-xp
tags: [app, ide, tool, vscode, xp]
created: 2020-08-30T13:08:19.102Z
modified: 2023-02-08T10:47:19.056Z
---

# toc-app-vscode-xp

# guide
- [Open VSX Registry faq](https://www.eclipse.org/legal/open-vsx-registry-faq/)
  - https://open-vsx.org/
  - The Open VSX Registry offers a community driven, fully open platform for publishing and consuming VS Code extensions. 
  - The Registry is built on Eclipse Open VSX
# nice-to-have
- search-通过ctrl+p搜索文件名时，没有像在左边搜索文字那样方便，左边搜文字时可以一次性展示所有文件及匹配点

- search面板
  - 对文件名的二次搜索过滤不支持模糊匹配

- 编辑器
  - js注释 // 与 /** */ 一键转换

- 侧边栏最小宽度
# keyboard-shortcuts
- navigate
  - back:    Ctrl+Alt+-
  - forward: Ctrl+Shift+-

- 选中括号内内容 shift+alt+right
  - [keyboard shortcuts - Select everything between matching brackets in VS Code](https://stackoverflow.com/questions/37835012/select-everything-between-matching-brackets-in-vs-code)
# extensions-stars
- ## import sorter

- [Option to allow for only sorting](https://github.com/daidodo/format-imports-vscode/issues/36)
  - I guess what you want is that the extension formats imports/exports first, and then prettier format the whole file?
  - If yes, you could install prettier AFTER this extension in VSCode, e.g. uninstall prettier and then install again. (I'm not sure how to specify formatter orders in VSCode but did once enter the situation that prettier ran after this extension.)

```JSON
{
   "tsImportSorter.configuration.wrappingStyle": {
    "maxBindingNamesPerLine": 0,
    "maxDefaultAndBindingNamesPerLine": 0,
    "maxLineLength": 0
  }
}
```

- ## region folding /maptz.regionfolder
- 优点是利用文件格式支持的注释来确定fold的范围，自身不会渲染显示出来
- 无法fold的格式
  - css，但scss能fold

- ## markdown

- https://github.com/condorheroblog/auto-front-matter
  - Automatically insert lastmod and duration when saving the md file.
  - roadmap
    - 支持自定义字段名称、ignore部分文件

- Markdown yaml Preamble
  - Renders yaml front matter as a table in the built-in markdown preview
# extensions
- https://github.com/RandomFractals/tabular-data-viewer
  - provides fast DSV data loading and custom Table Views
- https://github.com/RandomFractals/vscode-data-preview
  - extension for importing outbox_tray viewing mag_right slicing hocho dicing game_die charting bar_chart & exporting inbox_tray large .json array .arrow .avro .parquet data files, .config .env .properties .ini .yml configurations files, .csv/.tsv & .xlsx/.xlsb Excel files and .md markdown tables with Perspective - streaming data analytics WebAssembly library.
# guide
- 下载vscode时，可将地址中的 az764295.vo.msecnd.net 更换为  vscode.cdn.azure.cn 使用国内的镜像服务器加速

- [The Visual Studio Code Roadmap 2020](https://github.com/microsoft/vscode/wiki/Roadmap)
# ref
- [一个vscode的模拟界面，仅界面和编辑，不能跳转文件和点击菜单](https://remoteok.io/vscode)

- vscode类似chrome的任务管理器
  - [Process explorer as a separate renderer window · Issue #41045 · microsoft/vscode](https://github.com/microsoft/vscode/issues/41045)
  - process explorer
# discuss-features-request
- ## 侧边面板宽度
- [Sidebar defaultWidth, View-Specific Sidebar widths, & View-Specific Sidebar defaultWidths](https://github.com/microsoft/vscode/issues/158603)
- [Find a way to fit panel headers into the smaller minimum width](https://github.com/microsoft/vscode/issues/87347)
