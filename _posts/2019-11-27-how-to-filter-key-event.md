---
title: QML 中如何捕获键盘事件？
tags: QtQML
comments: true
key: C-2019112701
---

比如你想要捕获 **Ctrl+C** 用来复制文件，应该怎么办？

## 方法一、KeyEvent

```c++
Item {
    focus: true
    Keys.onPressed: {
        if ((event.key == Qt.Key_C) && (event.modifiers & Qt.ControlModifier))
            doSomething();
    }
}
```

这种方法的缺点在于需要焦点在，但是很多时候都无法保证焦点在。

## 方法二、事件过滤 

用 C++ 方法在 QML 中注册一个类型或通过上下文（QQmlContext）将 C++ 数据暴露给 QML 引擎，并将 Windows 窗口设为被监听的对象，就可以全局监听键盘事件。

以下是实现代码，分别为 shortcutlistener.h，shortcutlistener.cpp，main.cpp，main.qml

```c++
#ifndef SHORTCUTLISTENER_H
#define SHORTCUTLISTENER_H

#include <QObject>

class ShortcutListener : public QObject
{
    Q_OBJECT

signals:
    void copyPressed();

public:
    explicit ShortcutListener(QObject *parent = nullptr);

    Q_INVOKABLE void listenTo(QObject *object);

public slots:

protected:
    bool eventFilter(QObject *object, QEvent *event) override;
};

#endif // SHORTCUTLISTENER_H

```

```c++
#include "shortcutlistener.h"
#include <QKeyEvent>
#include <QDebug>

ShortcutListener::ShortcutListener(QObject *parent) : QObject(parent)
{

}

void ShortcutListener::listenTo(QObject *object)
{
    if (!object)
        return;

    object->installEventFilter(this);
}

bool ShortcutListener::eventFilter(QObject *obj, QEvent *event)
{
    // filter the press key
    if (event->type() == QEvent::KeyPress) {
        QKeyEvent *keyEvent = static_cast<QKeyEvent *>(event);
        if (keyEvent->key() == Qt::Key_C && (keyEvent->modifiers() & Qt::ControlModifier)) {
            emit copyPressed();
        }
        return true;
    }

    // pass the event on to the parent class
    return QObject::eventFilter(obj, event);
}

```

```c++
#include <QGuiApplication>
#include <QQmlApplicationEngine>
#include <QQmlContext>
#include "shortcutlistener.h"

int main(int argc, char *argv[])
{
    QCoreApplication::setAttribute(Qt::AA_EnableHighDpiScaling);

    QGuiApplication app(argc, argv);

    QQmlApplicationEngine engine;

    // expose data to qml
    ShortcutListener shortcutListener;
    engine.rootContext()->setContextProperty("shortcutListener", &shortcutListener);

    const QUrl url(QStringLiteral("qrc:/main.qml"));
    QObject::connect(&engine, &QQmlApplicationEngine::objectCreated,
    &app, [url](QObject * obj, const QUrl & objUrl) {
        if (!obj && url == objUrl)
            QCoreApplication::exit(-1);
    }, Qt::QueuedConnection);
    engine.load(url);

    return app.exec();
}

```

```js
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    id: window
    visible: true
    width: 640
    height: 480
    title: qsTr("Hello World")

    Connections {
        target: shortcutListener
        onCopyPressed: {
            console.log("copy now")
        }
    }

    // set listen target
    Component.onCompleted: shortcutListener.listenTo(window)
}

```