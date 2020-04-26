---
title: 时间复杂度和空间复杂度
tags: AskCPP100 Algorithm
comments: true
key: C-2020042501
---

#AskCpp04 如何考量算法的效率？

## 时间复杂度

**算法的时间复杂度（Time complexity）是一个定性描述该算法运行时间的函数，记作 `T(n)`。**

但是，一个算法的运行时间必须得在计算机上运行测试才能确定，无法从理论上计算出来。实际中，我们只需要比较算法花费时间的差别即可，并不需要每个算法都上机测试。并且，算法花费的时间与算法中语句执行的次数成正比，这个执行次数称为语句频度或时间频度，也记为`T(n)`。

**通常表示为 `T(n) = O(f(n))` **

*  大 O 符号用来表述时间复杂度。
* f(n) 是一个辅助函数，随着算法的输入大小 n 的增大，其执行时间的增长速度可以用 f(n) 来描述。

**举例**

```c++
void func(int n) {
    for(int i = 0; i < n; i++) { // 需要执行 (n + 1) 次
        printf("Hello, World!\n"); // 需要执行 n 次
    }
}
```

上面的函数总共需要执行`（n + 1 + n）= 2n + 1`次，其时间复杂度为 O(n)。

**计算时间复杂度有以下原则：**

* 时间频度为常数时，记为 O(1)。
* 只保留时间频度的的最高阶项。
* 若最高阶项存在，则去掉最高阶项前面的系数。

**常见时间复杂度排序**

***\*Ο(1)＜Ο(log\*2n\*)＜Ο(n)＜Ο(nlog\*2n\*)＜Ο(\*n\*2)＜Ο(\*n\*3)＜…＜Ο(\*2\*n)＜Ο(n!)\****

**常见时间复杂度列表**

![computational-complexity-of-algorithm](https://tva1.sinaimg.cn/large/007S8ZIlly1ge7iciqxxoj30u10h7jwt.jpg)

## 空间复杂度

**算法空间复杂度 (Space Complexity) 是对一个算法在运行过程中临时占用存储空间大小的量度，记做`S(n) = O(f(n))`。**

这里的存储空间主要包含两部分：

* 为参数表中形参变量分配的存储空间。
* 为函数体中局部变量分配的存储空间。

## 参考

[https://zh.wikipedia.org/wiki/%E6%97%B6%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6](https://zh.wikipedia.org/wiki/时间复杂度)

[https://blog.csdn.net/zolalad/article/details/11848739](https://blog.csdn.net/zolalad/article/details/11848739)

[https://www.cxyxiaowu.com/5323.html](https://www.cxyxiaowu.com/5323.html)

[https://baike.baidu.com/item/%E7%A9%BA%E9%97%B4%E5%A4%8D%E6%9D%82%E5%BA%A6](https://baike.baidu.com/item/空间复杂度)

