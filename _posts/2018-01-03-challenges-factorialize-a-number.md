---
layout:     post
title:      FreeCodeCamp 初级算法题 - 计算整数阶乘
subtitle:   02.Basic Algorithm Scripting - Factorialize a Number
date:      2018-01-02
author:     Azr
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - FreeCodeCamp
    - 初级
    - 算法
---


> 如果用字母n来代表一个整数，阶乘代表着所有小于或等于n的整数的乘积。

## 题目Link

- [中文Link](https://freecodecamp.cn/challenges/factorialize-a-number)
- [英语Link](https://www.freecodecamp.com/challenges/factorialize-a-number)
- 级别： Basic Algorithm Scripting

## Factorialize a Number

如果用字母n来代表一个整数，阶乘代表着所有小于或等于n的整数的乘积。

阶乘通常简写成 `n!`

例如: `5! = 1 * 2 * 3 * 4 * 5 = 120`

当你完成不了挑战的时候，记得开大招'Read-Search-Ask'。

这是一些对你有帮助的资源:

- [Arithmetic Operators](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)

> `factorialize(5)` 应该返回一个数字
>
> `factorialize(5)` 应该返回 120.
>
> `factorialize(10)` 应该返回 3628800.
>
> `factorialize(20)` 应该返回 2432902008176640000.
>
> `factorialize(0)` 应该返回 1.

 ```
function factorialize(num) {
  // 请把你的代码写在这里
  return num;
}
factorialize(5);
 ```

## 问题解释

1. `func`接受一个整数为参数，返回阶乘的计算结果

2. e.g. ： 3！= 1 * 2 * 3 = 6 

   ​            4！= 1 * 2 * 3 * 4  = 24 

   ​	    5！ = 1 * 2 * 3 * 4  * 5 = 120

## 基本解法

> 思路

1. 需要一个循环，把每一步的数字相乘
2. 注意：0 和 1 的阶乘都是1 

> 代码for循环

```
function factorialize(num) {
 var result = 1;
 for (var i = 1 ; i <= num; i++ ){
     result *= num;
 }
 return result;
}
factorialize(5);
```

> 解释

1. `result`的初始值是1，0 和 1 的阶乘都是1 
2. `var i = 1`,可以让0和1不进入循环
3. `result * = num`，进行计算并重新赋值

> 代码 while循环

```
function factorialize(num) {
  var result = 1;
  while( num > 1 ) {
      result * = num;
      num--;
  }
  return result;
}
factorialize(5);
```

> 解释

1. `result`的初始值是1，0 和 1 的阶乘都是1 
2. `num > 1`，可以让0和1不进入循环
3. `result * = num`，进行计算并重新赋值
4. 为了防止死循环，一定要写`num--`的终止条件

## 使用 reduce

> 思路

1. 使用`reduce`，需要根据`num`创建一个数组
2. 可以使用`Array.from`来创建数组

> Link

1. [Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
2. [Array.keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/keys)
3. [Array.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
4. [Array.reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

> 代码

```
function factorialize(num) {
  return Array.from(Array(num).keys()).map(e => e + 1).reduce((prev, next) => {
        retrun prev * next;
    }, 1);
}
factorialize(5);
```

> 解释

1.  `.keys()` 返回的是类数组，从 `0` 开始，而我们需要返回从 `1` 开始的数组。所以，需要在 `map` 里面加上 `1`

## 递归

> 代码

```
function factorialize(num) {
    // 初始及弹出条件
    if (num === 0) {
        return 1;
    }
    // 递归调用
    return num * factorialize(num - 1)
}
```

> 解释

1. 初始判断条件：如果设置为 `if (num === 1)` 是不行的，这样传入 0 的时候就不能得到 1 
2. 注意：传入的数字比较大，会发生`stack overflow`，可以使用[尾调用优化](http://www.ruanyifeng.com/blog/2015/04/tail-call.html)

## 完

本文首次发布于 [Azr的博客](http://amor9.cn), 作者 [@azrrrrr](https://github.com/azrrrrr/) ,转载请保留原文链接.

原文链接：[http://amor9.cn/2018/01/03/challenges-factorialize-a-number/](http://amor9.cn/2018/01/03/challenges-factorialize-a-number/)


