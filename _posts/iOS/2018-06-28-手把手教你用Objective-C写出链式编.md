---
title: 手把手教你用Objective-C写出链式编程的感觉 
description: 阅读自动布局框架 - Masonry 提炼的一些感悟
categories:
 - iOS 
tags:
---

## 手把手教你用Objective-C写出链式编程

>  笔者也用封装了一个 [XTC_ChainKit](https://github.com/xtcmoons/XTC_ChainKit)，大家可以参考下！提高代码的逼格


### 回顾下Objective-C Block

```Objective-C
block 声明
  void(^blockName)(int arg1, int arg2);

block 定义

  void^(int arg1, int arg2) {
    //do something
  }

```

链式编程思想：是将多个操作（多行代码）通过点号(.)链接在一起成为一句代码,使代码可读性好。a(1).b(2).c(3)
1. 链式编程特点：方法的返回值是block,block必须有返回值（本身对象），block参数（需要操作的值）
2. 代表：Masonry框架。

### 实现原理
1. 链世语法每一次调用都会调用点语法。
2. 又因为通常OC调用方法当中，一般使用括号来调用，所以推测是用的Block。
3. 又因为链世编程的语法是连续调用，并且很多时候是无序的连续调用。所以推测，每次返回的应该是这个类的实例。

#### 先看看 Masonry 是怎么实现的

```Objective-C
- (MASConstraint * (^)(CGFloat))offset {
     return ^id(CGFloat offset){
         self.offset = offset;
         return self;
     };
 }
```
从上面可以看出，使用点语法、运用Block回调、返回值是调用的实例对象。

基于这个原理我们可以把我们的需要的类进行基本的实现
比如实现建一个UIView的分类：
```Objective-C

@interface UIView (Chain)
- (UIView * (^)(UIColor *color))xtc_backgroundColor;
@end

@implementation UIView (Chain)
- (UIView * _Nonnull (^)(UIColor * _Nonnull))xtc_backgroundColor {
    return ^id(UIColor *color) {
        NSCParameterAssert(color != nil);
        self.backgroundColor = color;
        return self;
    };
}
@end

```
上面我们定义了一个xtc_backgroundColor方法，返回值是一个Block，Block里的返回值是本身。这样我们调用这个方法是就可以使用点语法了。

## 使用场景
比如：
1，需要取得返回值之后不断的进行下一步运算，比如加减乘除计算器。
2，需要连续设置一个实例的参数，比如设置UILable的属性等，不再需要连篇累牍的多次书写点语法来设置属性。
