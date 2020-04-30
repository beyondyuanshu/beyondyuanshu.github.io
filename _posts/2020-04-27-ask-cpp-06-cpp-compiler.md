---
title: C++编译器傻傻分不清楚？
tags: AskCPP100
comments: true
key: C-2020042701
---

> \#AskCpp06 C++编译器傻傻分不清楚？

## 编译器是什么？

编译器是一种将源代码编译成目标代码的程序。

这里的源代码通常指高级语言写的程序，目标代码为汇编语言或者机器码。

* 现代编译器系统的一般流程：

  **源代码（source code）→ 预处理器（preprocessor）→ 编译器（compiler）→ 汇编程序（assembler）→ 目标代码（object code）→ 链接器（linker）→ 可执行文件（executables）**

* 编译器的分类：
  * 本地编译器（编译出与编译器所在系统平台相同的程序）
  * 交叉编译器（编译出在不同平台上运行的程序）

## C++ 编译器

C++ 编译器有很多，不同的编译器由于其源码不同，故其对 C++ 标准的支持不同，编译速度也有区别。

* MSVC（Microsoft Visual C++，cl.exe）

  微软的 VC（Visual C++） 编译器，同时支持现代 C++ 标准，一般集成在 VS 中。

* GCC

  > **GNU 编译器套装**（英语： **GNU Compiler Collection**，缩写为 **GCC** ），指一套[编程语言](https://zh.wikipedia.org/wiki/編程語言)[编译器](https://zh.wikipedia.org/wiki/编译器)，以 [GPL](https://zh.wikipedia.org/wiki/GPL) 及 [LGPL](https://zh.wikipedia.org/wiki/LGPL) 许可证所发行的 [自由软件](https://zh.wikipedia.org/wiki/自由軟體)，也是 [GNU 计划](https://zh.wikipedia.org/wiki/GNU計劃)的关键部分，也是 [GNU 工具链](https://zh.wikipedia.org/wiki/GNU工具链)的主要组成部分之一。GCC（特别是其中的 C 语言编译器）也常被认为是跨平台编译器的事实标准。

  属于 GNU 项目，主要针对类 Unix 平台，通过 Cygwin 和 MinGW 提供对 Windows 的支持。

* Clang

  > **Clang**（发音为 /ˈklæŋ/ 类似英文单字*[clang](https://zh.wiktionary.org/wiki/clang)*[[1\]](https://zh.wikipedia.org/wiki/Clang#cite_note-1)） 是一个 [C](https://zh.wikipedia.org/wiki/C語言)、[C++](https://zh.wikipedia.org/wiki/C%2B%2B)、[Objective-C](https://zh.wikipedia.org/wiki/Objective-C) 和 [Objective-C++](https://zh.wikipedia.org/wiki/Objective-C%2B%2B) 编程语言的 [编译器](https://zh.wikipedia.org/wiki/編譯器)前端。它采用了 [LLVM](https://zh.wikipedia.org/wiki/LLVM) 作为其后端，而且由 LLVM2.6 开始，一起发布新版本。它的目标是提供一个 [GNU 编译器套装](https://zh.wikipedia.org/wiki/GCC)（GCC）的替代品，支持了 GNU 编译器大多数的编译设置以及非官方语言的扩展。
  >
  > 性能：测试证明 Clang 编译 Objective-C 代码时速度为 GCC 的 3 倍 [[4\]](https://zh.wikipedia.org/wiki/Clang#cite_note-4)，还能针对用户发生的编译错误准确地给出建议 [[5\]](https://zh.wikipedia.org/wiki/Clang#cite_note-5)。

* Intel C++ 编译器

  Intel C++ 编译器可以为各种 Intel CPU（包括 Xeon，Core 和 Atom 处理器）生成高度优化的代码。

~~其他的不管~~



由编译器想到 C++ 生态，编译器、IDE、工具链，测试等等，这些概念其实还区分不清楚！



## 参考

[https://zh.wikipedia.org/wiki/%E7%B7%A8%E8%AD%AF%E5%99%A8](https://zh.wikipedia.org/wiki/編譯器)

[[https://blog.hotwill.cn/C++%E7%94%9F%E6%80%81-%E7%BC%96%E8%AF%91%E5%99%A8-IDE-%E5%B7%A5%E5%85%B7-%E6%B5%8B%E8%AF%95%E7%AD%89-%E5%89%AF%E6%9C%AC.html](https://blog.hotwill.cn/C++生态-编译器-IDE-工具-测试等-副本.html)](https://blog.hotwill.cn/C++%E7%94%9F%E6%80%81-%E7%BC%96%E8%AF%91%E5%99%A8-IDE-%E5%B7%A5%E5%85%B7-%E6%B5%8B%E8%AF%95%E7%AD%89-%E5%89%AF%E6%9C%AC.html)

