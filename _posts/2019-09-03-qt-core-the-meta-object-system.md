---
title: Qt 核心之元对象系统
tags: Qt The-Meta-Object-System moc
comments: true
key: C-2019090301
---

Qt 的元对象系统（The Meta-Object System）由它的元对象编译器（Meta-Object Compiler，moc）帮忙实现，moc 通过读取头文件中的 Q_OBJCET 宏来判断是否需要生成元对象代码。如果需要，则生成以 moc\_ 开头的源文件，在连接（Linking）时会和源文件一起生成可执行文件。



## 是什么

- 从 Qt 新增的关键字（signals、slots、emit）可以看出 Qt 并不是标准的 C++ 语言，而是对其进行了一定程度的扩展。

- 元对象系统是 Qt 核心的一部分，用于支持 Qt 的 C++ 扩展（Qt's C++ extensions），它提供了用于对象间通信的信号与槽、运行时类型信息以及动态属性系统。



## 为什么

由于 Qt 是标准 C++ 的一个扩展，所以编译源代码时就需要将这些扩展的语法去掉，然后交给标准 C++ 编译器，诸如 GCC、MinGW、Clang 等。



## 怎么实现

元对象系统基于以下 3 件事：

1. `QObject`类为使用元对象系统的 Qt 对象提供了一个基类。

2. `Q_OBJECT` 宏用来在类中启用元对象特性，例如动态属性、信号、槽。

3. `moc` 为每个 QObject 子类提供实现元对象特性所需要的代码。

moc 工具读取 C++ 源文件。如果发现源文件中有一个类或者多个类的声明中包含 Q_OBJECT 宏，它就生成一个包含了这些类所需要的元对象代码的源文件。这个新源文件的文件名为源文件名前加上 moc\_。新生成的源文件必须被 #include 到源文件中，或者更常见的是编译和连接到类的实现中。



## 怎么用

元对象系统有以下特性：

- `signals and slots` 一个用于对象间通信的信号与槽机制（Qt 引入元对象系统最主要的原因）。
- `QObject::metaObject()` 用来返回类关联的元对象。
- `QMetaObject::className()` 用来在运行时获取类名，**这个方法不需要原生 C++ 编译器的运行时类型信息（Runtime type information，RTTI）支持**。
- `QObject::inherits()` 用来判别一个对象是否是 QObject 继承树中的特定类的对象。
- `QObject::tr()` 和 `QObject::trUtf8()` 提供 Qt 国际化中翻译字符串的支持。
- `QObject::setProperty()` 和 `QObject::property()` 提供动态地设置和获取属性名。
- `QMetaObject::newInstance()` 用于构造一个类的新实例。
- `qobject_cast` 处理继承自 QObject 类的动态转换。它不需要 RTTI 支持，并且支持跨动态库转换。转换成功返回非零指针，失败返回 nullptr。

在 QObject 的派生类中，不使用 Q_OBJECT 宏以及没有元对象代码，上述元对象系统特性也能用。需要注意的是，QMetaObject::className() 只会返回离它最近且拥有元对象代码的祖先（即最近一个声明 Q_OBJECT 的祖先）的类名。所以建议 QObject 的派生类一律添加 Q_OBJECT 宏！



## 限制

这里的限制主要是指 moc 工具的限制，主要表现在以下几方面：

- 模板类中不能使用 Q_OBJECT。

  ```c++
  class SomeTemplate<int> : public QFrame
  {
      Q_OBJECT  // WRONG
      ...

  signals:
      void mySignal(int);
  };
  ```

- 多重继承时 QObject 必须是第一个，且不支持 QObject 的虚继承。

  ```c++
  // CORRECT
  class SomeClass : public QObject, public OtherClass
  {
      ...
  };
  ```

- 函数指针不能作为信号或槽的参数，可以用 typedef 简化函数指针，建议用继承或虚函数代替函数指针。

  ```c++
  // WRONG
  class SomeClass : public QObject
  {
      Q_OBJECT

  public slots:
      void apply(void (*apply)(List *, void *), char *);
  };
  ```

  ```c++
  // CORRECT
  typedef void (*ApplyFunction)(List *, void *);

  class SomeClass : public QObject
  {
      Q_OBJECT

  public slots:
      void apply(ApplyFunction, char *);
  };
  ```

- 枚举类型或 Typedefs 作为信号和槽的参数时必须是`完全限定名称`。原因是 QObject::connect() 检测参数签名时，是比较的数据类型的字面意思。例如，Alignment 和 Qt::Alignment 会当作两种不同的参数类型。

  ```c++
  class MyClass : public QObject
  {
      Q_OBJECT

      enum Error {
          ConnectionRefused,
          RemoteHostClosed,
          UnknownError
      };

  signals:
      void stateChanged(MyClass::Error error);
  };
  ```

- 内嵌的类不能有信号与槽。

  ```c++
  class A
  {
  public:
      class B
      {
          Q_OBJECT

      public slots:  // WRONG
          void b();
      };
  };
  ```

- 信号槽的返回类型不能是引用。

- 在类的 signals 和 slots 代码块中，只能是信号和槽函数的声明，而不能是其他的声明。



## moc 工具使用

1. 如果你在编译程序时出现以下错误时有可能是没有编译进你由 moc 生成的源文件：

- YourClass::className() is undefined

- YourClass lacks a vtable

此时一般运行一下 qmake 来更新 makefile 即可。

2. 一般来讲，qmake 会从头文件中读取 Q_OBJECT 宏来生成 moc 源文件。假如你没有头文件，qmake 则无法知道怎样生成 moc 源文件，你可以手动生成并源文件末尾 #include moc 源文件，否则会报错。

   - 手动生成方法如下：

     ```bash
     /path/to/moc yourclass.cpp -o moc_yourclass.cpp
     ```

   - 添加到源文件中示例：

     ```c++
     class NoHeaderClass : public QObject
     {
         Q_OBJECT
     public:
         explicit NoHeaderClass(QObject *parent = nullptr);

     signals:

     public slots:
     };

     #include "moc_noheader.cpp"  // 必须加到末尾，不然会提示找不到 NoHeaderClass 等定义。
     ```

3. moc 工具主要实现以下功能

   - 信号与槽
   - 对象属性
   - 普通枚举类型
   - 可以进行位与操作的枚举类型
   - 类的额外信息，用于 QObject::metaObject() 返回

   ```c++
   #include <QObject>

   class MyClass : public QObject
   {
       Q_OBJECT
       Q_PROPERTY(Priority priority READ priority WRITE setPriority)
       Q_CLASSINFO("Author", "Oscar Peterson")
       Q_CLASSINFO("Status", "Active")

   public:
       enum Priority { High, Low, VeryHigh, VeryLow };
       Q_ENUMS(Priority)

       enum LoadHint {
           ResolveAllSymbolsHint = 0x01,
           ExportExternalSymbolsHint = 0x02,
           LoadArchiveMemberHint = 0x04
       };
       Q_DECLARE_FLAGS(LoadHints, LoadHint)
       Q_FLAG(LoadHints)

       MyClass(QObject *parent = 0);
       ~MyClass();

       void setPriority(Priority priority)
       {
           m_priority = priority;
       }
       Priority priority() const
       {
           return m_priority;
       }

   signals:
       void mySignal();

   public slots:
       void mySlot();

   private:
       Priority m_priority;
   };
   ```



## 参考

1. [https://en.wikipedia.org/wiki/Meta-object_System](https://en.wikipedia.org/wiki/Meta-object_System)
2. [https://doc.qt.io/qt-5/metaobjects.html](https://doc.qt.io/qt-5/metaobjects.html)
3. [https://doc.qt.io/qt-5/moc.html](https://doc.qt.io/qt-5/moc.html)
4. [https://blog.51cto.com/devbean/355100](https://blog.51cto.com/devbean/355100)
