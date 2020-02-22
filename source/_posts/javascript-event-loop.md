---
title: EventLoop 之 宏任务与微任务
date: 2018-07-12 19:05:58
tags: 
    - javascript
header-img: wallhalla-Bwxp3rLhQnl.jpg
---
## 题记
关于EventLoop的执行顺序，在初识JS的时候，还是懵懵懂懂也没有太在意。
后面有一次在网上冲浪，看到了一道例题，看了解析再加上翻阅了一些网上的其他文章，才对其加深了印象。

## 例题
```javascript
setTimeout(function() {
    console.log(1)
},0);
new Promise(function(a, b) {
    console.log(2);
    for (var i = 0; i < 10; i++) {
        i == 9 && a();
    }
    console.log(3);
}).then(function() {
    console.log(4)
});
console.log(5)
```

## 答案

`2 3 5 4 1`

## 疑问
那么，为何不是`1 2 3 4 5`呢。

## 解析思路

### 1、理清主线程的执行优先级：

JS优先执行主线程中的代码，
即`setTimeout(...)`、`new Promise(...)`与`console.log(5)`，
那么就应该执行如下：

```javascript
// 1.setTimeout向事件队列投入一个任务。然而什么也不输出

// 2.执行new Promise中代码的（Note：Promise内的程序是同步的）
console.log(2);
a(); // 这里只是执行了resolve，并没有执行回调的具体then中的代码，
     // 粗暴得可以理解成a()的作用只是用来告诉Promise：“Hi，接下来你要执行then里面的第一个回调函数哦~”
console.log(3); 

// 3.主线程代码的代码
console.log(5)

```
理解完第一点，我们可以得出`2 3 5`是如何来的。

### 2、事件队列的执行优先级：

在JS里主线程执行完后会从事件队列中取出任务来执行，所以我们抛开答案先来想一想接下来的结果应该是，

1.  取出队列的任务：settimeout 来执行
2.  取出队列的任务：promise的then 来执行

那么接下来应该输出是`1 4`
而答案为何是`4 1`呢？

### 3、微任务，宏任务的执行优先级：

微任务，宏任务在JS的执行流程中，执行的顺序如下：

>  → 加载可执行的任务到主线程中
> ↑　　　↓
> ↑　　　执行刚才加载的任务（如果有的话），同时执行主线程内容（这时候可以注册事件到事件队列）
> ↑　　　↓
> ↑　　　执行微任务 
> ↑　　　↓
> ↑←←←回到开始再一遍


那么，这里我们的```then(...)```中的回调，就是`微任务`
而第一步中加载的就是`宏任务`，这里`setTimeout`注册的就是`宏任务`啦。

## 结论
所以，真正的执行顺序是：
0.  程序初始，没有可以加载的`宏任务`，执行主程序的内容
1.  `setTimeout`注册定时事件的任务
2.  执行`Promise`中的代码，即`console.log(2)`,`a()`,`console.log(3)`
3.  执行`console.log(5)`
4.  执行`微任务`，即`then`中的`console.log(4)`
5.  进入下一轮
6.  加载`宏任务`到主线程，即`setTimeout`注册的任务
7.  执行主线程
8.  执行`setTimeout`注册的任务，即`console.log(1)`
9.  主程序没有其他可以执行的内容，运行结束...

