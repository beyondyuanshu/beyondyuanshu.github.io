---
title: Android 学习笔记 002：Activity 的生命周期
tags: Android Activity
comments: true
key: C-2020030201
---

## 四种状态

Activity 整个生命周期可分为以下四种状态：

1. 运行
2. 暂停
3. 停止
4. 不存在



## 状态切换

Activity 状态切换时系统会进行相应方法的调用。

1. 运行 & 暂停
   * 运行 -> 暂停 onPause()
   * 暂停 -> 运行 onResume()
2. 暂停 & 停止
   * 暂停 -> 停止  onStop()
   * 停止 -> 暂停 onStart()
3. 停止 & 不存在
   * 停止 -> 不存在 onDestroy()
   * 不存在 -> 停止 onCreate()



## Tips

* 停止的 Activity 随时可能被系统回收内存
* 按 HOME 键 Activity 会调用 onStop() 进入停止状态，按后退键会调用 onDestory() 进入不存在状态
* 旋转设备会销毁当前 Activity，并重新创建新的 Activity