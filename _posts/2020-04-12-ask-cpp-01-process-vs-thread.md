---
title: 进程与线程的区别？
tags: AskCPP100
comments: true
key: C-2020041202
---

## 什么是进程？

众所周知，单个 CPU 一次只能运行一个任务，这里的单个任务就是指进程。

执行单个任务时，除了 CPU 外，还必须有构成这个任务的的执行环境，称为程序上下文（`Context`）。 一个任务的执行其实包含 3 个步骤：CPU 加载上下文、CPU 执行、CPU 保存上下文，这些步骤的耗时总和就是进程。

## 什么是线程？

线程包含在进程中，是进程中的实际运作单位。

通俗来讲，一个任务（进程）可能会有多个子任务（线程），比如你可以在 IDE 中进行代码编写、代码分析、智能提示等很多工作同时进行。

在多核或多 CPU 上使用多线程能提高程序的执行吞吐率。在单核、单 CPU 的计算机上，使用多线程通常能够把耗时计算与人机交互分开来执行，从来不会让 GUI 程序卡死，提高程序的执行效率。

## 进程和线程的区别

* 进程是资源分配的独立单位
* 线程是资源调度的独立单位

## 参考

[https://zh.wikipedia.org/wiki/%E8%A1%8C%E7%A8%8B](https://zh.wikipedia.org/wiki/行程)

[https://zh.wikipedia.org/wiki/%E7%BA%BF%E7%A8%8B](https://zh.wikipedia.org/wiki/线程)

[https://www.zhihu.com/question/25532384](https://www.zhihu.com/question/25532384)

[http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html](http://www.ruanyifeng.com/blog/2013/04/processes_and_threads.html)