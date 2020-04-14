---
title: 代码在内存中的什么位置？
tags: AskCPP100
comments: true
key: C-2020041401
---

## 内存分区

C/C++ 内存其实只分为两个区：代码区和数据区。

* 数据区：栈、堆、全局/静态存储区、常量区。

  * 栈（Stack）：由编译器自动分配和释放，存放函数参数、局部变量等。

  * 堆（Heap）：由程序员分配释放，管理不力可能造成内存泄露。
  
* 代码区：存放函数体的二进制代码，只读。

  <img src="https://img-blog.csdn.net/20180308174726462?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3hzeWRqbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" style="zoom: 50%;" />

so，代码存在代码区！

## 参考
