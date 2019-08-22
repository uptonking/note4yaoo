---
title: note-pm-excelbox
created: '2019-05-15T03:30:55.244Z'
modified: '2019-07-03T05:25:56.432Z'
tags: [pm, yaoo]
---

# note-pm-excelbox

## target

## todo

## reference

### jackson-core & jackson-databind
- 通过JsonFactory创建parser和generator
- `createParser(InputStream in)` 
    - The input stream will <b>not be owned</b> by the parser
    - 解析器不直接拥有stream，通过拥有IOContext来操作流
