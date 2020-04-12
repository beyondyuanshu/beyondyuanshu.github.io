## 介绍下 C++ 11？

C++ 基本上是每 3 年更新一个版本，C++ 98、C++ 11、C++ 14、C++17、C++ 20。

C++ 11 可以从几个方面来介绍：语言的革新、语法糖、标准库的扩充以及老语法 bug 的修复。

大概有 30 几个新的语法特性（从最常用的说起）：

* move semantics（move 语义）
* variadic templates（可变参数）
* rvalue references（右值引用）
* forwarding references（转发引用）？？
* initializer list（初始化列表）
* static assertions（静态断言）
* auto（自动类型）
* lambda expressions（lambda 表达式）
* decltype（声明的类型）
* type aliases（类型别名）
* nullptr（空指针）
* strongly-typed enums（强类型枚举）
* attributes（属性）？？
* constexpr（常类型表达式）
* delegating constructors（委托构造函数）
* user-defined literals（自定义文字？）
* explicit virtual overrides（显示虚函数重写）
* final specifier（final 指定符）
* default functions（默认成员函数）
* deleted functions（删除成员函数）
* range-based for loops（基于范围的 for 循环）
* special member functions for move semantics（move 语义下特殊的成员函数）？？
* converting constructors（转换构造函数）？？
* explicit conversion functions（显示转换函数）？？
* inline-namespaces（内联命名空间）
* non-static data member initializers（非静态数据成员初始化）
* right angel brackets（右括号）
* ref-qualified member functions（？？）
* trailing return types（尾随返回类型）
* noexcept specifier（noexcept 标志符）

10 几个新的库特性：

* std::move
* std::forward
* std::thread
* std::to_string
* type traits
* smart pointers
* std::chrono
* tuples
* std::tie
* std::array
* unordered containers
* std::make_shared
* std::ref
* memory model
* std::async
* std::begin/end