---
title: Qt 核心之属性系统
tags: Qt The-Property-System
comments: true
key: C-2019090801
---

属性可以是通常的位置（x/y）、宽高（width/height）或者颜色（color）等，也可以是某种特定类型，比如单选框的选中状态（checked）。一个类的属性通常是指它的成员变量。这些属性有它自己的一些行为，比如读取（read）、设置（set）、变化通知（notify signal）等。用来管理这些行为的系统称为属性系统，Qt 的属性系统是基于元对象系统的。

Qt 的属性系统主要有以下方面的应用：

* 用于 Qt Designer，提供属性的编辑。
* 与 QtScript 集成。
* 现在广泛用于 QML 中，用于获取 C++ 对象。



## 怎样声明属性？

用 Q_PROPERTY() 宏声明，它是定义在 QObject 类中的宏，所以只有 QObject 类或者继承自它的类才能使用。

```c++
// Q_PPROPERTY 宏
Q_PROPERTY(type name
           (READ getFunction [WRITE setFunction] |
            MEMBER memberName [(READ getFunction | WRITE setFunction)])
           [RESET resetFunction]
           [NOTIFY notifySignal]
           [REVISION int]
           [DESIGNABLE bool]
           [SCRIPTABLE bool]
           [STORED bool]
           [USER bool]
           [CONSTANT]
           [FINAL])
```

| 参数       | 对参数的理解                                                 |
| ---------- | ------------------------------------------------------------ |
| READ       | 指定读取属性值的函数，最好是一个 const 函数，函数返回值是该属性的类型或者该属性类型的引用。**在没有指定 MEMBER 时，READ 必须指定！** |
| WRITE      | 指定修改属性值的函数，函数参数有且仅有一个，参数类型必须是属性类型或者该属性类型的指针或引用，无返回值（或者说返回 void 值）。**可选参数**！ |
| MEMBER     | 导出成员变量为属性值，使得成员变量不需要读函数和写函数的支持也能读写。读写用的是QObject 的函数：property() 和 setProperty()。**不能与 READ/WRITE 同时使用**！ |
| RESET      | 重置属性值为某个默认值，该函数是一个没有参数且返回值是 void 的函数。**可选参数！** |
| NOTIFY     | 定义一个信号，当属性值已经变化后，Qt 会发出这个信号。当存在参数为 MEMBER 时，这个信号应该不带参数或者带一个参数，带一个参数时参数为属性的新值。**可选参数！** |
| REVISION   | 定义 API 的版本号，使得读/写接口和信号只能在特定的版本中使用。**默认值是 0，可选参数！** |
| DESIGNABLE | 指定 Qt Designer 中是否能编辑这个属性。**默认值是 true，可选参数！** |
| SCRIPTABLE | 指定 QtScript 是否可以访问这个属性。**默认值是 true，可选参数！** |
| STORED     | 指定属性是独立属性还是依赖于值其他属性，比如 QWidget::minimumWidth() 依赖于 QWidget::minimumSize()。**默认值是 true，可选参数！** |
| USER       | 指定类的这个属性为用户只读或者可编辑，一个类中只能定义一个 USER 属性。**默认值是 false，可选参数！** |
| CONSTANT   | 属性指定了 CONSTANT 即成为了一个常量属性。类的不同对象这个属性值必须有不同的值。常量属性没有 write 方法和信号。 |
| FINAL      | 属性指定了 FIANL 将不能被派生类重写。                        |

READ、WRITE、ERSET 指定的函数可以被继承，也能被定义为虚函数。当被多重继承时，取第一个父类的值。



## 怎么读取和修改属性？

声明属性的两种方式对应着两种操作属性的方法：

* 自定义读/写函数
* QObject::property() 以及 QObject::setProperty()

前一种方法中的写操作性能要优于第二种，因为他是在编译期完成的。自定义写函数的缺点在于需要你在编译期间知道有这种方法的存在。假如你不知道类中有什么方法可以读/写属性，Qt 提供了 QObject、QMetaObject、以及 QMetaProperties 类帮助你得到属性名及其操作方法。

```c++
QObject *object = ...
const QMetaObject *metaobject = object->metaObject();
int count = metaobject->propertyCount();
for (int i=0; i<count; ++i) {
    QMetaProperty metaproperty = metaobject->property(i);
    const char *name = metaproperty.name();
    QVariant value = object->property(name);
    ...
}
```

## 怎样动态添加属性？

QObject::setProperty() 可以在运行时给实例添加属性值。

* 属性已经存在于对象中

  给的属性值类型正确，这个值就被添加到对象中了，函数返回 true。否则属性值不改变，函数返回 false。

* 类中没有这个属性

  自动在对象中添加新属性，并赋值，但是函数返回 false。

**动态属性只是添加到 QObject 中，而不是 QMateObject 中，故无法通过 QMetaProperties 方法获取到。**

**移除动态属性可以通过给 setProperty 传入一个无效的 QVariant 参数**



## 自定义类型怎样用到属性系统中？

```c++
bool QObject::setProperty(const char *name, const QVariant &value)
```

由于 setProperty() 中值的类型是 QVariant，所以自定义的类型用 Q_DECLARE_METATYPE() 宏注册，使它能存储到 QVariant 中就行了。



## 给类添加额外的信息

Q_CLASSINFO() 宏给类的元对象添加其他信息，添加的方式为 `name--value`，以下是示例：

```c++
Q_CLASSINFO("Version", "3.0.0")
```