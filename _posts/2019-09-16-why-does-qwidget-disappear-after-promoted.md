---
title: 为什么继承自 QWidget 的自定义控件无法显示背景图片？
tags: Qt QtQuestion
comments: true
key: C-2019091601
---

你可能遇到过在 Qt Designer 中新建一个继承自 QWidget 的 `Qt 设计师界面类` 或者手动写一个 QWidget 的派生类时，设置它的背景样式没有生效的情况。

![Snipaste_2019-09-14_21-30-21](https://tva1.sinaimg.cn/large/006y8mN6ly1g715fr6o4nj30tu0bbjsr.jpg)

由于是 QWidget 的派生类，我们先看看 QWidget 的 [样式参考](https://doc.qt.io/qt-5/stylesheet-reference.html#) ：

```c++
If you subclass from QWidget, you need to provide a paintEvent for your custom QWidget as below:

  void CustomWidget::paintEvent(QPaintEvent *)
  {
      QStyleOption opt;
      opt.init(this);
      QPainter p(this);
      style()->drawPrimitive(QStyle::PE_Widget, &opt, &p, this);
  }

The above code is a no-operation if there is no stylesheet set.
Warning: Make sure you define the Q_OBJECT macro for your custom widget.
```

**得到方法一：重写 `void QWidget::paintEvent(QPaintEvent *event)` 函数。**



**方法二是启用 Widget 使用 QSS 进行样式设置：` setAttribute(Qt::WA_StyledBackground, true);`**

QWidget 默认可能是禁用 styled background 的。查看 QWidget 源码确实能发现在绘制背景时对	Qt::WA_StyledBackground 标志进行了判断：

![Snipaste_2019-09-14_23-03-35](https://tva1.sinaimg.cn/large/006y8mN6ly1g715frwda4j30fq0e3q55.jpg)<u></u>



另外还需要注意的是：如果在 Qt Designer 中改变样式表来设置背景图的话，最好别用 objectName 来作为 QSS 的选择器。因为提升后的 widget 对象名已经改变！可以用类名作为选择器。

```css
// Not recommended, will invalid after promoted.
#form {	
	background-image: url(:/resources/moon.jpeg);
}

// Right
Form {	
	background-image: url(:/resources/moon.jpeg);
}
```



其他：

* 设计师中的样式可以和代码中的样式叠加使用。

```c++
setStyleSheet(styleSheet().append("Your New Styles"));
```

​	   但是上面这条语句在构造函数里执行可能不能生效，原因不知。解决办法是先将样式清空下，再设置。

```c++
QString style = styleSheet().append("Your New Styles");
setStyleSheet("");  // clear first
setStyleSheet(style);  // reset new     
```

