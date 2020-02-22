---
title: "React16.8稳定版本发布，提供Hooks新功能"
date: 2019-02-12 23:04:45
tags:
  - react
  - 小笔记
header-img: wallhalla-96w3rNOcGmv.jpg
---

## 题记

在 React 的 16.8 稳定版本中，我们可以使用 React 提供的 Hooks 了！

## 什么是 Hooks？

React 提供的 Hooks 功能能够让我们在非函数式的组件中使用`state`和 React 的其他功能。甚至你可以构建自定义 Hooks 在不同的组件中复用他们。

## 如何使用 Hooks？

### useState

```jsx
import React, { useState } from "react";

function Example() {
  /**
   * 这个使用了useState创建一个名叫count初始值为0的state的hook
   * useState返回一个数组 第一个元素为创建的state
   * 第二个用来改变state的状态
   */
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

### useEffect

假如想要在 title 中显示 count 的数量，那么我们就要用到`useEffect`了。

改一下上面的例子

```jsx
import React, { useState, useEffect } from "react";

function Example() {
  const [count, setCount] = useState(0);

  /**
   * useEffect 提供两个参数 第一个数要执行的内容 第二个是在何时才执行
   * useEffect 在第一次渲染之后和每次更新之后执行。
   * useEffect 的第一个参数返回一个函数用于清除 useEffect
   *
   * 这里 仅仅在count改变时(因为第二个函数传了含count的数组 如果不传则每次更新都执行)改变title的内容 然后在控制台输出 effect over
   */
  useEffect(() => {
    document.title = `You clicked ${count} times`;
    return () => {
      console.log("effect over");
    };
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```
