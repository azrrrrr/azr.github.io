---
layout:     post
title:      FreeCodeCamp 初级算法题 - 翻转字符串 
subtitle:   01.Basic Algorithm Scripting - Reverse a String
date:      2018-01-02
author:     Azr
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - FreeCodeCamp
    - 初级
    - 算法
---


> 先把字符串转化成数组，再借助数组的reverse方法翻转数组顺序，最后把数组转化成字符串。

## 题目Link

* [中文Link](https://freecodecamp.cn/challenges/reverse-a-string#)
* [英语Link](https://www.freecodecamp.com/challenges/reverse-a-string)
* 级别： Basic Algorithm Scripting

##  Reverse a String

翻转字符串

先把字符串转化成数组，再借助数组的reverse方法翻转数组顺序，最后把数组转化成字符串。

你的结果必须得是一个字符串

当你完成不了挑战的时候，记得开大招'Read-Search-Ask'。

这是一些对你有帮助的资源:

- [Global String Object](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String)

- [String.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)

- [Array.reverse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)

- [Array.join()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

> `reverseString("hello")` 应该返回一个字符串
>
> `reverseString("hello")` 应该返回 `"olleh"`.
>
> `reverseString("Howdy")` 应该返回 `"ydwoH"`.
>
> `reverseString("Greetings from Earth")` 应该返回 `"htraE morf sgniteerG"`.

```
function reverseString(str) {
  // 请把你的代码写在这里
  return str;
}

reverseString("hello");
```

##  初级解法

>  思路

1. 先将字符串进行分割
2. 进行翻转
3. 把翻转之后的数组合并为字符串

> 代码

```
function reverseString(str) {
    var strArr = str.split('');
    var reversedArr = strArr.reverse();
    return reversedArr.join('');
}
```

> 解释

1. 把传入的 `str` 分割，并赋值给 `strArr`
2. 把数组翻转，并赋值给 `reversedArr`
3. 返回合并之后的字符
4. `.split` 和 `.join` 都不会改变原来的字符串或数组，但 `reverse` 会改变原来的数组

## 优化

> 代码

```
function reverseString(str) {
    return str.split('').reverse().join('');
}
```

> 解释

1. `.split` 返回分割后的数组，直接调用 `.reverse`
2. `.reverse()` 方法返回的是翻转后的数组，直接调用 `.join`
3. `.join` 之后就是我们想要的字符串，直接返回
4. ` Method Chaining`(链式调用)，可以不用创建这么多变量

## 中级解法

> 思路

1. 直接利用字符串的方法，不需要转换为数组
2. 使用获取字符串中 `str` 的 `str[i]`方法

> 代码

```
function reverseString(str) {
    var result = "";
    for (var i = str.length - 1; i >= 0; i--) {
        result += str[i];
    }
    return result;
}
```

> 解释

1. 先创建一个变量 `result`，用于保存输出结果
2. 从右边开始遍历字符串
3. 把每次遍历到的字符加到 `result` 
4. 注意：边界条件的确定，因为字符串的索引同样是从 0 开始的，因此遍历的初始值要设置为 `str.length - 1`，结束值为 0

## 高级算法

> 思路

1. 字符串方法以及递归来翻转

> 代码

```
function reverseString(str) {
    // 设置递归终点(弹出条件)
	if (str.length === 1) {
        return str;
    }
    else {
        // 递归调用
        return reverseString(str.substr(1)) + str[0];
    }
}
```

> 解释

1. 递归涉及到两个因素，递归调用`reverseString(str.substr(1))`以及弹出过程`str[0]`
2. 代码在执行到 `reverseString(str.substr(1))` 的时候，会重新调用 `reverseString`，并传入 `str.substr(1)` 作为参数。后面的 `+ str[0]` 暂时不会执行
3. 直到传入的字符串长度为 `1`，就不会再去调用 `reverseString` 了，而是会执行 `if` 里面的部分，返回当前传入的 `str`。然后就会一步一步地执行之前的 `+ str[0]`，也就是弹出过程



# （完）

本文首次发布于 [Azr的博客](http://amor9.cn), 作者 [@azrrrrr](https://github.com/azrrrrr/) ,转载请保留原文链接.

原文链接： http://amor9.cn/2018/01/02/challenges-reverse-a-string/
