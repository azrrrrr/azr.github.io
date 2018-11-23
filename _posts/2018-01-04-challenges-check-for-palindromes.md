---
layout:     post
title:      FreeCodeCamp 初级算法题 - 检查回文字符串
subtitle:   03.Basic Algorithm Scripting - Check for Palindromes
date:      2018-01-04
author:     Azr
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - FreeCodeCamp
    - 初级
    - 算法
---


> 检查回文字符串

## 题目Link

- [中文Link](https://freecodecamp.cn/challenges/check-for-palindromes)
- [英语Link](https://www.freecodecamp.com/challenges/check-for-palindromes)
- 级别： Basic Algorithm Scripting

## Check for Palindromes

检查回文字符串

如果给定的字符串是回文，返回`true`，反之，返回`false`。

如果一个字符串忽略标点符号、大小写和空格，正着读和反着读一模一样，那么这个字符串就是palindrome(回文)。

**注意**你需要去掉字符串多余的标点符号和空格，然后把字符串转化成小写来验证此字符串是否为回文。

函数参数的值可以为`"racecar"`，`"RaceCar"`和`"race CAR"`。

这是一些对你有帮助的资源:

- [String.replace()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)

- [String.toLowerCase()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)

> `palindrome("eye")` 应该返回一个布尔值
>
> `palindrome("eye")` 应该返回 true.
>
> `palindrome("race car")` 应该返回 true.
>
> `palindrome("not a palindrome")` 应该返回 false.
>
> `palindrome("A man, a plan, a canal. Panama")` 应该返回 true.
>
> `palindrome("never odd or even")` 应该返回 true.
>
> `palindrome("nope")` 应该返回 false.
>
> `palindrome("almostomla")` 应该返回 false.
>
> `palindrome("My age is 0, 0 si ega ym.")` 应该返回 true.
>
> `palindrome("1 eye for of 1 eye.")` 应该返回 false.
>
> `palindrome("0_0 (: /-\ :) 0-0")` 应该返回 true.

```
function palindrome(str) {
  // 请把你的代码写在这里
  return true;
}
palindrome("eye");
```

## 问题解释

1. 这个`func`接收一个字符串参数，返回一个Boolean
2. 回文字符串： 正与反是一样的字符
3. e.g.：`‘book’  --> false`   `'eye' --> true`
4. 需要忽略符号和空格，只需要考虑数字和英文字符

## Knowledge point

1. [Reg](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)
2. [String.toLowerCase()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase)
3. [String.replace()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
4. [String.split()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)
5. [Array.reverse()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/reverse)
6. [Array.join()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)

## 基本解法-翻转字符串后比较

> 思路

1. 使用`Reg`去掉干扰项
   * 去掉特殊符号和空格
   * 将字符串转换为小写
2. 逻辑
   * 翻转字符串并与之前去掉干扰项的字符串进行对比，相等返回`true`，反之，返回`false`
   * 双指针。用两个变量代表`两个指针`，一个从左向右移动，一个从右向左移动，比较每次指向的是否相等，相等返回`true`，反之，返回`false`
3. 递归
   * 边界条件
   * 跳出条件

1. 代码

```
function palindrome (str) {
    // 转换成小写
    var lowerStr = str.toLowerCase();
    // 替换掉干扰项
    var replacedStr = lowerStr.replace(/[^a-z0-9]/g, "");
    // 分割成数组
    var strArr = replacedStr.split("");
    // 翻转数组
    var reversedArr = strArr.reverse();
    // 合并成字符
    var reversedStr = reversedArr.join("");
    // 返回判断结果
    return replacedStr === reversedStr;
}
```

> 解释

1. 注意比较对象是与去除干扰项的字符串，不是传入参数的字符串

## 优化-链式编程

> 代码

```
function palindrome (str) {
    // 边界判断
    if (str.length === 1) {
        return true;
    }
    var replacedStr = str.toLowerCase().replace(/[^a-z0-9]/g, "");
    var reversedStr = replacedStr.split("").reverse().join("");
    return replacedStr === reversedStr;
}
```

> 解释

1. 边界判断：如果 `str` 的长度为 1，那么就是回文字符串，直接返回 `true` 
2. `toLowerCase()`返回了一个字符串，`.replace`也返回了一个字符串，连用得到去除干扰项后的字符串
3. `.split()` 返回分割后的数组，`.reverse()` 返回翻转后的数组，`.join()`返回合并后的字符串，连用得到的就是翻转后的字符串

## 双指针解法

> 代码

```
function palindrome(str) {
    if (str.length === 1) {
        return true;
    }
    var replacedStr = str.toLowerCase().replace(/[^a-z0-9]/g, "");
    // 双指针 i ， j，用来代表当前判断位置的索引
    for (var i = 0, j = replacedStr.length - 1; i < replacedStr.length / 2; i++,j--) {
        // 有不相等的
        if (replacedStr[i] !== replacedStr[j]) {
            // 返回 false
            return false
        }
    }
    // 全部相等，返回 true
    return true;
}
```

> 解释

1. 初始值： `.length - 1`
2. 循环跳出条件：  `i < replacedStr.length / 2` 
   * `/2`可以减少一次的循环判断，只要两个指针相遇，就是已经判断完毕。
   * 不管字符串是长度是奇数，还是偶数都没有影响

## 递归解法

> 代码

```
function palindrome(str) {
    // 排除干扰项
    str = str.toLowerCase().replace(/[^a-z0-9]/g, '');
    // 设置边界条件
    if (str.length < 2) {
        return true;
    }
    // 检测首尾是否相等不相等，如果不等就直接返回 false
    if (str[0] !== str[str.length - 1]) {
        return false;
    }
    // 递归调用
    return palindrome(str.slice(1, -1));
}
```

> 解释

1. 判断字符串的首尾是否相等
2. 如果相等，就排除掉首尾字符，继续判断首尾是否相等，注意在最后的 `return` 那里，传入参数的改变
3. 边界条件： 设置为 `str.length < 2`，因为当 `length` 为 0 或者 1 的时候就表示这个字符是回文字符串
4. 递归调用：能到这一步，前面的`if`判断就没有生效。一旦前面的判断生效了，就会直接跳出

## 完

本文首次发布于 [Azr的博客](http://amor9.cn), 作者 [@azrrrrr](https://github.com/azrrrrr/) ,转载请保留原文链接.

原文链接： [http://amor9.cn/2018/01/04/challenges-check-for-palindromes](http://amor9.cn/2018/01/04/challenges-check-for-palindromes)
