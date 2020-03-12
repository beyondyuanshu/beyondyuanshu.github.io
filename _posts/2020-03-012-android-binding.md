---
title: Android 学习笔记 004：View.findViewById()、View Binding、Data Binding
tags: Android
comments: true
key: C-2020031201

---

**仅作为学习记录，内容有待完善**



## findViewById

通过 findViewById 方法在 Activity 或者 Fragment 中引用布局中的视图。

```java
Button myButton = (Button) findViewById(R.id.my_button);
```

这种方式引用布局有以下缺点：

* 布局中每一个用到的视图都需要通过 findViewById 实例化，代码重复
* 参数 id 可能写错，或者 id 不存在
* 类型转换可能写错
* 参数和类型转换只能在运行时检查出错误



## View Binding

通过视图绑定，系统自动为 layout 文件生成绑定类，layout 中指定了 id 的视图都在会绑定类中实例化。

大多数情况下，视图绑定可以取代 findViewById。

### 启动

```java
// 在 build.gradle 文件中启用
android {
    viewBinding {
        enabled = true
    }
}

// 在绑定类中忽略某个 layout 文件，在根视图中声明
<LinearLayout
...
tools:viewBindingIgnore="true">
...
</LinearLayout>
```

### 用法

```kotlin
// 获取实例
binding = XXBinding.inflate(layoutInflater)

// 引用视图
binding.button.setOnClickListener { viewModel.userClicked() }

// 加载视图
setContentView(binding.root)
```

### 与 findViewById 的区别

* Null 安全
* 类型安全



## Data Binding

用于在布局文件中直接绑定应用中的数据源。

### 启动

```java
// 在 build.gradle 文件中启用
android {
    dataBinding {
        enabled = true
    }
}
```

### 使用

需要布局文件以根标记 layout 开头，后跟 data 元素和 view 根元素。

data 中的 user 变量些布局中用到的数据源属性，布局中的表达式用 “@{}” 来指定数据来源。



## 参考

https://developer.android.google.cn/topic/libraries/view-binding

[https://developer.android.google.cn/topic/libraries/data-binding](https://developer.android.google.cn/topic/libraries/data-binding) 





