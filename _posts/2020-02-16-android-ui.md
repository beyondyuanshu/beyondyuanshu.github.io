---
title: Android 学习笔记 000：创建 Android UI 
tags: Android
comments: true
key: C-2020022601
---

## 概述

所有界面都是由 View（微件）和 ViewGroup（布局）对象构建出来的。

* View 类是所有控件的基类，TextView、Button 等
* View 也是 ViewGroup 的基类

![img](https://developer.android.com/images/viewgroup.png?hl=zh-cn)

如上图，再复杂的界面也是一层一层包裹嵌套组成的。**应使控件之间关系清晰简单，能提升性能。**



## 两种写界面的方法

1. 在 XML 文件中声明界面元素

   在工程目录的 res/layout/ 路径下新建 .xml 文件。

2. 在代码中实例化布局元素



## 代码中加载界面文件

```java
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main_layout); // Activity 启动时会自动调用 onCreate 方法，也就加载了 UI
}
```



## 代码中操作界面文件中的控件

```java
Button myButton = (Button) findViewById(R.id.my_button); // 通过 id 获得控件对象
```