## 目标

* 了解 js 的能力
* 在 QML 中运用 js 毫无障碍
* 能用 js 写 Sketch 插件
* 了解 React 库、Material-UI 库

## 代码规范

[Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html) 

[一份有点过时的 JS 风格指南 - Google JavaScript Style Guide 中文版](https://github.com/wayou/wayou.github.io/issues/21)

## 语法

* 标出与 C++ 不一样的地方

## 读书笔记

### JavaScript DOM 编程艺术

* JS 使网页具备交互能力

#### 1. 简史

* 是 Netscape 与 Sun 公司联合开发，需要 WEB 浏览器进行解释和执行的语言。实际上指的是 ECMAScript。

#### 2. 语法

#### 3. DOM

#### 4. 最佳实践

* 平稳退化：确保网页在没有 JS 时也能正常工作
* 分离：HTML 与 JS 分离
* 向后兼容：兼容老版本浏览器
* 性能考虑：性能最优

#### 5. HTML5

Web 设计三层：

* 结构层：HTML
* 样式层：CSS
* 行为层：JS + DOM





### [JavaScript 教程](https://wangdoc.com/javascript/index.html)

#### 入门篇

#### 语法专题

##### 数据类型转换

* 强制转换：Number()、String()、Boolean()
* 自动转换
  * 注意特殊值的转换：object、‘’、0、NaN、undefined、null 等	

##### 编程风格

* 不要将不同目的的语句，合并成一行

  ```javascript
  // 不使用
  a = b
  if (a = b) {
      // ...
  }
  
  // Nice
  a = b
  if (a = b) {
      // ...
  }
  ```

* switch...case 写成对象结构

  ```js
  function doAction(action) {
    switch (action) {
      case 'hack':
        return 'hack';
      case 'slash':
        return 'slash';
      case 'run':
        return 'run';
      default:
        throw new Error('Invalid action.');
    }
  }
  
  function doAction(action) {
    var actions = {
      'hack': function () {
        return 'hack';
      },
      'slash': function () {
        return 'slash';
      },
      'run': function () {
        return 'run';
      }
    };
  
    if (typeof actions[action] !== 'function') {
      throw new Error('Invalid action.');
    }
  
    return actions[action]();
  }
  ```

##### console 对象与控制台

* 会为输出结尾自动添加换行符
* 格式占位符输出：%c CSS 格式字符串
* *有很多有意思的接口*

#### 标准库

##### String

* trim() 去除首尾空格（包括 \t \v \n \r），返回新字符串
* charAt() 参数为负数或大于长度时，返回空
* slice()，substring()，substr()，优先用 slice()
* **实例方法都是返回新字符串**

  







## 问

* JavaScript 是什么？
* 

