---
title: Qt 处理字符串的类
tags: AskCPP100 Qt
comments: true
key: C-2020051501
---

> \#AskCpp13 Qt 操作字符的类有哪些？QString、QByteArray、...，何时使用何种类，搞不清楚哇！！

## Qt 字符串相关的类

| 类                                                           | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [QByteArray](https://doc.qt.io/qt-5/qbytearray.html)         | Array of bytes                                               |
| [QByteArrayList](https://doc.qt.io/qt-5/qbytearraylist.html) | List of byte arrays                                          |
| [QByteArrayMatcher](https://doc.qt.io/qt-5/qbytearraymatcher.html) | Holds a sequence of bytes that can be quickly matched in a byte array |
| [QChar](https://doc.qt.io/qt-5/qchar.html)                   | 16-bit Unicode character                                     |
| [QCollator](https://doc.qt.io/qt-5/qcollator.html)           | Compares strings according to a localized collation algorithm |
| [QCollatorSortKey](https://doc.qt.io/qt-5/qcollatorsortkey.html) | Can be used to speed up string collation                     |
| [QLatin1Char](https://doc.qt.io/qt-5/qlatin1char.html)       | 8-bit ASCII/Latin-1 character                                |
| [QLatin1String](https://doc.qt.io/qt-5/qlatin1string.html)   | Thin wrapper around an US-ASCII/Latin-1 encoded string literal |
| [QLocale](https://doc.qt.io/qt-5/qlocale.html)               | Converts between numbers and their string representations in various languages |
| [QStaticByteArrayMatcher](https://doc.qt.io/qt-5/qstaticbytearraymatcher.html) | Compile-time version of QByteArrayMatcher                    |
| [QString](https://doc.qt.io/qt-5/qstring.html)               | Unicode character string                                     |
| [QStringList](https://doc.qt.io/qt-5/qstringlist.html)       | List of strings                                              |
| [QStringMatcher](https://doc.qt.io/qt-5/qstringmatcher.html) | Holds a sequence of characters that can be quickly matched in a Unicode string |
| [QStringRef](https://doc.qt.io/qt-5/qstringref.html)         | Thin wrapper around QString substrings                       |
| [QStringView](https://doc.qt.io/qt-5/qstringview.html)       | Unified view on UTF-16 strings with a read-only subset of the QString API |
| [QTextBoundaryFinder](https://doc.qt.io/qt-5/qtextboundaryfinder.html) | Way of finding Unicode text boundaries in a string           |
| [QTextStream](https://doc.qt.io/qt-5/qtextstream.html)       | Convenient interface for reading and writing text            |

## QString & QByteArray

QString 的内部其实是以 QChar 存储，QChar 是一个 16 位的 Unicode 字符集。

QByteArray 的内部存储的是元数据（包括 '\0'）以及传统的 8 位以 '\0' 结尾的字符串。

**通常情况，用 QString 即可！以下两情况使用 QByteArray：**

1. 当你要处理元数据时
2. 在内存紧张的时候，比较嵌入式系统中。

## 怎样高效的使用 QString？

直接说结论，具体解释可以去看 [Using QString Effectively](https://wiki.qt.io/Using_QString_Effectively/zh)。

1. 与 C 字符串的等号判断用 QLatin1String() 包裹。

   ```cpp
   // if (fruit == "apple") { … } // possibly hidden malloc
   
   if (fruit QLatin1String("apple")) { … } // fast and mentions encoding
   ```

2. 操作 QString 时，尽量用 QStringRef 来获取 QString 部分引用。

3. 调用 QString::append () 之前考虑用 QString::reserve() 来分配足够多的内存，调用完用 QString::squeeze() 来释放多余的内存。

   **Qt 文档中说，通常不需要调用这两个函数！只有在处理很长的字符串，且需要避免重复申请内存的时候才用到。**

   ```cpp
   // 示例代码
   QString result;
   int maxSize;
   bool condition;
   QChar nextChar;
   
   result.reserve(maxSize);
   
   while (condition)
       result.append(nextChar);
   
   result.squeeze();
   ```

4. 字符串的连接用 “%” 代替 “+”。

   ```cpp
   // if (foo.startsWith("(" + type + ")"))
     
   if (foo.startsWith("(" % type % ")")) // 更快！前提是引用了头文件 #include <QStringBuilder>，或者在 pro 文件里添加宏 QT_USE_QSTRINGBUILDER，添加宏后 Qt 会自动将 “+” 当前 "%" 处理。
   ```

5. 用 QStringMatcher 类进行字符串的快速匹配？

6. QStringLiteral() 宏能将字面交的字符串在编译器确定。

   ```cpp
   // hasAttribute takes a QString argument
   if (node.hasAttribute("http-contents-length")) //...
     
   if (node.hasAttribute(QStringLiteral(u"http-contents-length"))) //...
   ```

**1 2 4 点可以牢记于心，随手做到。**

## 参考

https://wiki.qt.io/Using_QString_Effectively

https://wiki.qt.io/Basics_of_String_Encoding

https://wiki.qt.io/Using_QByteArray

Qt 文档之《Classes for String Data》