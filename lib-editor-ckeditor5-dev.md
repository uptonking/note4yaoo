---
title: lib-editor-ckeditor5-dev
tags: [ckeditor, editor]
created: '2021-10-25T09:33:19.901Z'
modified: '2021-10-25T09:33:39.528Z'
---

# lib-editor-ckeditor5-dev

# 2021
- not-yet
  - URL.createObjectURL(file)每次返回的url都不相同，即时对于同一个文件
  - 文档rxdb保存图片的ArrayBuffer时，去重是如何实现的？很难

- 不同方式读取图片文件的ArrayBuffer得到的数据是否相等
  - 难以比较2个ArrayBuffer对象是否相等，因为是js对象
  - imgFileReaderRetArrayBuffer === fileArrayBuffer 
  - 通过下面的工具方法，可以比较得出上面两种方式读出的文件数据相等

- [How to test for equality in ArrayBuffer, DataView, and TypedArray](https://stackoverflow.com/questions/21553528)

```JS
// compare ArrayBuffers
function arrayBuffersAreEqual(a, b) {
  return dataViewsAreEqual(new DataView(a), new DataView(b));
}

// compare DataViews
function dataViewsAreEqual(a, b) {
  if (a.byteLength !== b.byteLength) return false;
  for (let i = 0; i < a.byteLength; i++) {
    if (a.getUint8(i) !== b.getUint8(i)) return false;
  }
  return true;
}

// compare TypedArrays
function typedArraysAreEqual(a, b) {
  if (a.byteLength !== b.byteLength) return false;
  return a.every((val, i) => val === b[i]);
}
```

```JS
export function compareByteArrayData(a, b) {
  a = dataToUint8Array(a);
  b = dataToUint8Array(b);
  if (a.byteLength != b.byteLength) return false;
  return a.every((val, i) => val == b[i]);
}

// It will not copy any underlying buffers, instead it will create a view into them.
function dataToUint8Array(data) {
  let uint8array;
  if (data instanceof ArrayBuffer || Array.isArray(data)) {
    uint8array = new Uint8Array(data);
  } else if (data instanceof Buffer) {
    // Node.js Buffer
    uint8array = new Uint8Array(data.buffer, data.byteOffset, data.length);
  } else if (ArrayBuffer.isView(data)) {
    // DataView, TypedArray or Node.js Buffer
    uint8array = new Uint8Array(data.buffer, data.byteOffset, data.byteLength);
  } else {
    throw Error('Data is not an ArrayBuffer, TypedArray, DataView or a Node.js Buffer.');
  }
  return uint8array;
}
```

# guide
- features

- who is using ckeditor 5
  - drupal
