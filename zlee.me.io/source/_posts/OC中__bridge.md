layout: 'title:{{zlee}}'
title: Objective-c中__bridge
date: 2016-08-15 19:33:22
tags:
---


### __bridge只做类型转换，但是不修改对象（内存）管理权；

__bridge_retained（也可以使用CFBridgingRetain）将Objective-C的对象转换为Core Foundation的对象，同时将对象（内存）的管理权交给我们，后续需要使用CFRelease或者相关方法来释放对象；

__bridge_transfer（也可以使用CFBridgingRelease）将Core Foundation的对象转换为Objective-C的对象，同时将对象（内存）的管理权交给ARC
