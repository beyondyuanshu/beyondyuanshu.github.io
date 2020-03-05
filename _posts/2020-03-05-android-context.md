---
title: Android 学习笔记 003：关于 Context 的理解
tags: Android Context
comments: true
key: C-2020030501
---

**仅作为学习记录，内容有待完善**



## 官方文档定义

>Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.

需要理解 3 点：

1. 是应用环境的全局信息接口
2. 由 Android 系统实现
3. 用来访问特定资源和类，以及提供启动 Activity、进行广播、接收 Intent 等操作



## 三个重要方法

* **getContext()**

   返回 Activity 的上下文

* **getApplicationContext()**

  返回 Application 的上下文

* **getBaseContext()**

  和 ContextWrapper 有关



## 其他

* 一个应用程序中有多少个 Context?

  Context 有三种类型：Application、Activity、Service，故 `Context数量 = Activity数量 + Service数量 + 1`



[1]https://medium.com/@banmarkovic/what-is-context-in-android-and-which-one-should-you-use-e1a8c6529652





