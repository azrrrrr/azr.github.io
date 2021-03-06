---
layout:     post
title:      删除macOS自带的英文输入法
subtitle:  
date:      2019-03-18
author:     Azr
header-img: img/post-bg-universe.jpg
catalog: true
tags:
    - Mac
    - 小技巧
    - 输入法
---

## 删除macOS自带的英文输入法

macOS自带的输入法支持的语言很多，但是词库不够丰富，所以我们一般都会安装搜狗输入法。

搜狗输入法是支持中文和英文输入的，有时候我们处在英文状态，想要切换到中文。如果我们不查看状态栏的输入法状态的话很难判断当前是搜狗的英文输入法还是系统自带的英文输入法。这个时候我一般会直接尝试用快捷键进行切换。

问题在于系统输入法切换的快捷键是`Option + Space`，而搜狗输入法中英文切换的快捷键是`Shift`，这样的话我们有一半的概率会需要这个快捷键都按才会切换到中文输入法。这样是很难受的。

这种情况我们自然而然的就会想要在输入法管理器当中删掉系统自带的英文输入法。然而，系统并不允许我们这么做。

![img](http://skx926.me/2018/10/19/remove-default-input-source/gray.png)

其实细想一下系统这么设计也是合理的，如果我们一不小心把所有输入法都删除了，岂不是没办法用了？

系统这么设计是合理的，因为设计者是美国人，他们当然无法体会我们的痛苦。我们要删掉也是合理的，因为每天都这么切来切去确实很痛苦！

我记得在很早以前，大概是在macOS 10.6还是10.7吧，那个时候还可以删掉系统自带的输入法，方法很奇葩：先添加一下越南输入法，然后删掉英文输入法，最后再删掉越南输入法就可以了。

后来系统升级之后这个方法就失效了。那还有什么办法呢？Here is the way：

1. 在输入法管理器中删掉多余的输入法，只保留我们要用的搜狗输入法和自带的ABC输入法
2. 把当前输入法切换到ABC输入法
3. 把`~/Library/Preferences/`路径下的`com.apple.HIToolbox.plist`文件拷贝到桌面，然后用Xcode打开它，找到并删除`AppleEnabledInputSources`中`KeyboardLayout Name`为`ABC`的那一项，保存文件

![img](http://skx926.me/2018/10/19/remove-default-input-source/abc.png)

4. 用修改后的文件替换`~/Library/Preferences/`路径下文件

5. 重启电脑

大功告成!

![](http://skx926.me/2018/10/19/remove-default-input-source/removed.png)



## 完

本文首次发布于 [凯旋的博客](http://skx926.me/), 作者 [@凯旋](https://github.com/skx926) ,转载请保留原文链接.

原文链接： [http://skx926.me/2018/10/19/remove-default-input-source/](http://skx926.me/2018/10/19/remove-default-input-source/)
