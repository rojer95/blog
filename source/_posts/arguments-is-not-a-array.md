---
title: arguments其实他不是个数组
date: 2018-07-12 19:25:00
tags: 
    - javascript
    - 小笔记
header-img: wallhalla-96w3rNOcGmv.jpg
---
## 题记
一次在编写某个函数时，出现了`arguments.slice is not a function`的错误，翻阅官方的文档才知道，`arguments`对象不是一个 `Array` 。它类似于`Array`，但除了`length`属性和`索引元素`之外没有任何`Array`属性。

## 正确使用方法

想要对arguments进行分割等操作时，不能直接使用slice，需要先进行转换：

```javascript
function(){
    var args1 = Array.prototype.slice.call(arguments);
    var args2 = [].slice.call(arguments);

    // ES2015
    const args3 = Array.from(arguments);
}
```