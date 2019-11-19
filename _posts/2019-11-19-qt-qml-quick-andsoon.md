---
title: Qt QML 中各模块版本整理
tags: Qt QtQML
comments: true
key: C-2019111901
---

Qt QML 中有许多模块，每模块又有许多版本，傻傻分不清楚。

| Qt    | QtQml | QtQml.Models | QtQuick | QtQuick.Controls | QtQuick.Layouts | QtQuick.Dialogs | QtQuick.Particles |
| :---- | :---- | :----------- | :------ | :--------------- | :-------------- | :-------------- | ----------------- |
| 4.7.1 |       |              | 1.0     |                  |                 |                 |                   |
| 4.7.4 |       |              | 1.1     |                  |                 |                 |                   |
| 5.0   | 2.0   |              | 2.0     |                  |                 |                 | 2.0               |
| 5.1   | 2.1   | 2.1          | 2.1     | 1.0              | 1.0             | 1.0             | 2.0               |
| 5.2   | 2.2   | 2.1          | 2.2     | 1.1              | 1.1             | 1.1             | 2.0               |
| 5.3   | 2.2   | 2.1          | 2.3     | 1.2              | 1.1             | 1.2             | 2.0               |
| 5.4   | 2.2   | 2.1          | 2.4     | 1.3              | 1.1             | 1.2             | 2.0               |
| 5.5   | 2.2   | 2.2          | 2.5     | 1.4              | 1.2             | 1.2             | 2.0               |
| 5.6   | 2.2   | 2.2          | 2.5     | 1.5              | 1.3             | 1.2             | 2.0               |
| 5.7   | 2.2   | 2.2          | 2.7     | 2.0              | 1.3             | 1.2             | 2.0               |
| 5.8   | 2.2   | 2.2          | 2.7     | 2.1              | 1.3             | 1.2             | 2.0               |
| 5.9   | 2.2   | 2.2          | 2.7     | 2.2              | 1.3             | 1.2             | 2.0               |
| 5.10  | 2.2   | 2.2          | 2.7     | 2.3              | 1.3             | 1.3             | 2.0               |
| 5.11  | 2.11  | 2.11         | 2.11    | 2.4              | 1.11            | 1.3             | 2.11              |
| 5.12  | 2.12  | 2.12         | 2.12    | 2.5              | 1.12            | 1.3             | 2.12              |
| 5.13  | 2.13  | 2.13         | 2.13    | 2.13             | 1.13            | 1.3             | 2.13              |
| ...   | ...   | ...          | ...     | ...              | ...             | ...             | ...               |



## QtQML

QtQML 模块为使用 QML 语言开发应用程序和库提供一个框架。它定义和实现了 QML 语言以及 QML 引擎的基础架构，使开发者能够使用自定义类型来扩展 QML 语言，并将 QML 代码与 JS、C++ 进行集成。	

**如何使用？**

```c++
// .pro 文件中
QT += qml
    
// C++ 中
#include <QtQml>

// QML 中
import QtQml 2.13
```



## QtQml.Models

从 Qt 5.1 开始，将模型类型变成了 QtQML 的子模块，包含了定义数据模型的类型。有以下几种：

- DelegateModel
- DelegateModelGroup
- ItemSelectionModel
- ListElement
- ListModel
- ObjectModel

**如何使用？**

同 QtQml



## QtQuick

Qt Quick 是 QML 语言的标准库。

Qt 4 是对应 QtQuick 1.x，Qt 5 对应 QtQuick 2.x。

**如何使用？**

```c++
// .pro 文件中
QT += quick
    
// C++ 中
#include <QQuickView>
#include <...>

// QML 中
import QtQuick 2.13
```



## QtQuick.Controls

是一组基于 Qt Quick 的 UI 控件。

**如何使用？**

```c++
// .pro 文件中
QT += quickcontrols2
    
// C++ 中
#include <QtQuickControls2>

// QML 中
import QtQuick.Controls 2.13
```



## QtQuick.Layouts  

包含以下 5 个类型的布局类型：

- ColumnLayout
- GridLayout
- Layout
- RowLayout
- StackLayout

**如何使用？**

同 QtQuick



## QtQuick.Dialogs

包含以下 5 个类型的对话框：

- ColorDialog
- Dialog
- FileDialog
- FontDialog
- MessageDialog

**如何使用？**

同 QtQuick



## QtQuick.Particles

QML 中的粒子系统。	

**如何使用？**

同 QtQuick



