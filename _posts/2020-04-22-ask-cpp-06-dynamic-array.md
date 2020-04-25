---
title: 可变长度数组
tags: AskCPP100 CPP
comments: true
key: C-2020042201
---

## 什么是可变长数组？

是否遇到过定义一个数组，但长度不确定，因为这个长度是根据其他条件来确定的，这种情况下就需要定义一个变长数组。

**可变长数组是指数组对象的长度在运行时（而不是编译时）确定。**

## 两种方式使用

* 用 new

  ```c++
  int len = 6;
  int *p = new int[len]; // 运行时确定的长度
  ```

* 用 vector

  ```c++
  std::vector<int> v = {1, 2};
  v.push_back(3); // 改变了数组长度
  ```

## 还可以自定义可变长度数组类

从略

## 参考

[https://zh.wikipedia.org/wiki/%E5%8F%AF%E5%8F%98%E9%95%BF%E6%95%B0%E7%BB%84](https://zh.wikipedia.org/wiki/%E5%8F%AF%E5%8F%98%E9%95%BF%E6%95%B0%E7%BB%84)
[https://zh.cppreference.com/w/cpp/container/vector](https://zh.cppreference.com/w/cpp/container/vector)