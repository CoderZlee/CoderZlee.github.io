---
title: Objective-c单例
date: 2016-08-25 17:15:20
tags:
---

#### 关于系统单例
```
//系统单例同步数据
[[NSUserDefaults standardUserDefaults] synchronize];
```
上面这段代码是系统同中的代码接口，为啥要把这句代码给出来呢，熟悉一点设计模式的都知道自己写的接口最好是跟系统接口的写法类似，这样才方便别人调用你的接口，减少很多沟通成本.在这就不多说，举个例子就好。
>补充一点：系统单例(NSUserdefaults)不能存放自定义对象，只能存放OC系统的对象
```
存值和取值都很简单
单例取值
NSDictionary * dic = [[NSUserDefaults standardUserDefaults] objectForKey:@"user”];
单例存值
[[NSUserDefaults standardUserDefaults] setObject:dic forKey:@"user"];
```

#### 自定义单例

* ARC实现单例
```objective-c
// gcd写法
+ (instancetype)sharedSingleton
{
    static Singleton *singlenton =nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        singlenton = [[Singleton alloc] init];
    });
    return singlenton;
}
// 原生写法
+ (instancetype)sharedSingleton
{
    static Singleton *singlenton =nil;
    if (!singlenton) {
        singlenton = [[Singleton alloc] init];
    }
    return singlenton;
}
```
* MRC单例写法
```objective-c
+ (instancetype)defaultSingleton
{
    static Singleton * singlenton = nil;
    if (!singlenton) {
        singlenton = [[Singleton alloc] init];
    }
    return singlenton;
}
//alloc
+ (instancetype)allocWithZone:(struct _NSZone *)zone
{
    if (!singlenton) {
        singlenton = [super allocWithZone:zone];
    }
    return teacher;// 第一种写法

}
//retain
- (instancetype)retain
{
    return self;
}
//copy
+ (id)copyWithZone:(struct _NSZone *)zone
{
    return self;
}
//release
- (oneway void)release
{
    // 这儿不能释放
}
//autorelease
- (instancetype)autorelease
{
    return self;
}
//retainCount
- (NSUInteger)retainCount
{
    return NSUIntegerMax;
}
```
需要什么功能只需要給这个类增加方法或者属性就好。
