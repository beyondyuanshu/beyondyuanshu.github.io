---
title: Android 学习笔记 001：Intent 的使用
tags: Android Intent
comments: true
key: C-2020022801
---

## 是什么?

Intent（意图） 是一个消息传递对象，不仅可用于应用间传递，还可用于应用内传递。

应用内信息传递主要有 3 种：

* 启动 Activity
* 启动服务
* 传递广播



## 使用方式

### 显式使用

```java
Intent intent = new Intent(FirstActivity.this, SecondActivity.class); // public Intent(Context packageContext, Class<?> cls)
startActivity(intent);
```



### 隐式使用

```java
Intent intent = new Intent("com.example.activitytest.ACTION_START"); // public Intent(String action)
startActivity(intent);
```



## 传递数据

### 发送数据

```java
// FisrtActivity
Intent intent = new Intent(FirstActivity.this, SecondActivity.class); 
intent.putExtra(); // 需要传递的数据，Intent 提供了一系列的方法重载
startActivity(intent);
```



### 接收数据

```java
// SecondActivity
Intent intent = getIntent();
String data = intent.getStringExtra("extra_data"); // 接收数据
```



### 返回数据

1. 启动时设置结果回调

```java
// FirstActivity
Intent intent = new Intent(FirstActivity.this, SecondActivity.class); 
startActivityForResult(intent, 1); // 第二个参数为请求码，用于回调中判断数据来源
```

2. 跳转过去的活动中添加返回数据

```java
// SecondActivity
Intent intent = new Intent();
intent.putExtra("data_return", "Hello FirstActivity");
setResult(RESULT_OK, intent);
finish();
```

3. 重写 onActivityResult() 方法

```java
// FirstActivity
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	switch (requestCode) {
		case 1:
			if (resultCode == RESULT_OK) {
				String returnedData = data.getStringExtra("data_extra"); // 得到返回的数据
			}
			break;
		default:
	}
}
```



## 常用的系统 Intent 

可以参考 API 文档中的 Constants 列表，每一项对应一个 Intent。

例如拨打电话：

```java
Uri uri = Uri.parse("tel:10086");
Intent intent = new Intent(Intent.ACTION_DIAL, uri);
startActivity(intent);

// 注意申请拨打电话的权限！
```

