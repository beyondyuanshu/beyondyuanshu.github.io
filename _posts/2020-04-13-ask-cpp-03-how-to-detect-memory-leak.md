---
title: 怎样检测内存泄露？
tags: AskCPP100
comments: true
key: C-2020041302
---

## 何为内存泄露？

内存泄露（Memory leak）：指动态申请的内存没有及时释放。

## 后果

泄露导致可用内存越来越少，最终程序奔溃。

## 如何检测？

### 手动检测

* 简单地在 malloc/free，new/delete 处加日志记录。

* 重载 malloc/free，new/delete，记录调用的次数，在程序结束时进行检测。

## 运用工具

* Valgrind 等。
* 或通过 IDE，如 vs 的调试功能等。

## 参考

[https://zh.wikipedia.org/wiki/%E5%86%85%E5%AD%98%E6%B3%84%E6%BC%8F](https://zh.wikipedia.org/wiki/内存泄漏)

[https://yq.aliyun.com/articles/337106](https://yq.aliyun.com/articles/337106)

