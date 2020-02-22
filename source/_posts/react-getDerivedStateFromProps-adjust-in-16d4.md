---
title: 在16.4版本中针对getDerivedStateFromProps的调整
date: 2018-06-20 20:53:52
tags:
  - react
  - 小笔记
header-img: wallhalla-96w3rNOcGmv.jpg
---

## 来自官方 Issues

> It is expected. See for details:
>
> https://reactjs.org/blog/2018/05/23/react-v-16-4.html#bugfix-for-getderivedstatefromprops > https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html
>
> If this change breaks your code, it means your code already has a bug that causes state to reset too often.

---

> 在 16.4 版本之前，getDerivedStateFromProps 的执行是只在 props 更新是才执行，然而在 16.4 版本中，FB 对其中进行了调整：`每次渲染组件时都会调用getDerivedStateFromProps`。

## 总结

在旧版本（**16.4 以前**）中，`getDerivedStateFromProps` **只会在 props 更新时执行**而并且**不会**因组件`setState`而触发。_（FB 指出这是最初实施过程中的疏忽，现在已经得到纠正。）_

而，在**16.4 版本**中，组件执行`setState`时**也会触发**`getDerivedStateFromProps`。
