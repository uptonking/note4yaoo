---
title: lib-excel-luckysheet-codebase
tags: [codebase, luckysheet]
created: 2021-05-06T09:59:31.399Z
modified: 2022-08-21T09:57:39.501Z
---

# lib-excel-luckysheet-codebase

# guide

# fortune-sheet

## architecture

- init初始化流程
  - initSheetData: convert SheetType to CellMatrix
  - const tableCanvas = new Canvas(refs.canvas.current!, context); 
  - tableCanvas.drawMain

- update更新流程
  - Redraw canvas When context changes
  - All context changes will trigger this
  - 每次context-change都会重新创建实例
  - tableCanvas.drawMain

## model-layer

- sheetData的类型是CellMatrix

```typescript
type CellMatrix = (Cell | null)[][];

export type Cell = {
  v?: string | number | boolean;
  m?: string | number;
  mc?: { r: number; c: number; rs?: number; cs?: number };
  f?: string;
  ct?: { fa?: string; t?: string; s?: any };
  qp?: number;
  spl?: any;
  bg?: string;
  lo?: number;
  rt?: number;
  ps?: {
    left: number | null;
    top: number | null;
    width: number | null;
    height: number | null;
    value: string;
    isShow: boolean;
  };
  hl?: { r: number; c: number; id: string };
} & CellStyle;

```

- Canvas
  - drawRowHeader
  - drawColumnHeader
  - drawMain
  - cellRender
  - cellTextRender

## view-layer

- canvas.drawMain
  - 计算可见范围
  - this.cellRender
  - 处理各种条件
    - 对齐
    - 条件格式

- cellRender
  - renderCtx.beginPath(); 
  - renderCtx.moveTo
  - renderCtx.lineTo
  - renderCtx.stroke
  - renderCtx.closePath
  - renderCtx.drawImage
  - overflow

- workbook
  - toolbar
  - sheet
  - contextMenu
  - filterMenu
  - sheetTabContextMenu
  - moreItemInToolbar
  - selection
# luckysheet

# more
