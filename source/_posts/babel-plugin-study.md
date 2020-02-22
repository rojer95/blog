---
title: Babel 插件开发学习
date: 2018-07-20 13:09:45
tags: 
    - Babel
header-img: wallhalla-Bwxp3rLhQnl.jpg
---

# 介绍
Babel 是一个通用的多功能的 JavaScript 编译器。此外它还拥有众多模块可用于不同形式的静态分析。
> 静态分析是在不需要执行代码的前提下对代码进行分析的处理过程 （执行代码的同时进行代码分析即是动态分析）。 静态分析的目的是多种多样的， 它可用于语法检查，编译，代码高亮，代码转换，优化，压缩等等场景。
你可以使用 Babel 创建多种类型的工具来帮助你更有效率并且写出更好的程序。

# Babel 的处理步骤
Babel 的三个主要处理步骤分别是： 解析（parse），转换（transform），生成（generate）。
