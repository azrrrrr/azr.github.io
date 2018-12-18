layout:     post
title:      性能测试--Benchmark
subtitle:   掌握好浏览器的特性进行有针对性的性能调优是一项基本工作，同时，比较不同代码的执行速度也是一项关键的工作。
date:      2018-12-14
author:     Azr
header-img: img/post-bg-debug.png
catalog: true
tags:
    - Benchmark.js
    - 测试
    - 单元测试
    - 性能


Benchmark用压力测试挖掘整个系统的性能状况。

参考Link

- 官网Link
- JavaScript Benchmark Quality

了解

基准测试--性能测试

- 性能基准测试是一项系统性能测量工作。
- 基为混合业务性能场景的脚本线程配比计算提供依据。
- 一般的性能测试往往只在版本计划中或遭遇系统性能问题时进行，而基准测试在日常中进行，是因为当为系统创建性能基准后，基准数据作为性能指标的参照物，可用于判断任意一项变更为系统带来的具体影响。
- e.g. 某项配置优化后能够为系统带来的性能提升是多少、系统某项操作历史数据的增长与性能响应的关系、系统环境的变更对系统性能产生的影响。而且实施该项工作并不复杂。

Benchmark

	Benchmark是一个评价方式，在整个计算机领域有着长期的应用。正如维基百科上的解释“As computer architecture advanced, it became more difficult to compare the performance of various computer systems simply by looking at their specifications.Therefore, tests were developed that allowed comparison of different architectures.”Benchmark在计算机领域应用最成功的就是性能测试，主要测试负载的执行时间、传输速度、吞吐量、资源占用率等。

开始

文件结构

    ┌───────────src-──math.js
    │           
    ├──────────test┌──istanbul.test.js  -- istanbul测试
    |              └──test.js			-- 手动测试
    │              
    └──package.json

文件内容

1. 安装
       # mocha 是测试框架
       $ npm i mocha -D
       # should 是断言库
       $ npm i should -D
       # istanbul 是代码覆盖率工具 
       $ npm i istanbul -D
2. src/index.js
       module.exports = {
         num1 : n => parseInt(n),
         num2 : n => Number(n)
       }
       
3. test/test.js--手动测试
       const {num1,num2} = require('../src/index')
       
       //手动测试不准
       const s1 = Date.now()
       for(var i=0;i<10000;i++){
           num1("123456")
       }
       const e1 = Date.now()
       console.log(e1-s1)
       
       const s2 = Date.now()
       for(var i=0;i<10000;i++){
           num2("123456")
       }
       const e2 = Date.now()
       console.log(e2-s2)
   进入test目录，运行node  test.js，控制台显示每次测试的结果都是不一样的。
       ➜  test node test.js
       9
       0
       ➜  test node benchmark.test.js 
       1
       1
       ➜  test node benchmark.test.js
       0
       1
       ➜  test node benchmark.test.js
       2
       1
       ➜  test node benchmark.test.js
       0
       1

1. test/istanbul.test.js--Istanbul测试 
       const {num1,num2} = require('../src/index')
       
       const Benchmark = require('benchmark')
       
       var suite = new Benchmark.Suite;
       
       // add tests
       suite.add('parseInt',()=>{
           num1("123456")
       }).add('Number',()=>{
           num2("123456")
       }).on('cycle',event=>{
           console.log(String(event.target))
       }).on('complete',function(){
           console.log('Fastest is ' + this.filter('fastest').map('name'))
       }).run({'async':true})
2. 安装
       $ npm i benchmark -D
   进入test目录，运行node istanbul.test.js，控制台显示:
       ➜  test node benchmark.test.js
       parseInt x 32,670,031 ops/sec ±9.15% (65 runs sampled)
       Number x 36,378,068 ops/sec ±58.29% (54 runs sampled)
       Fastest is parseInt
   1. parseInt进行了65次采样。
   2. Number进行了54次采样。
   3. parseInt是比较快的。

代码

Benchmark

完

本文首次发布于 Azr的博客, 作者 @azrrrrr ,转载请保留原文链接.

原文链接： http://amor9.cn/2018/12/17/benchmark/


