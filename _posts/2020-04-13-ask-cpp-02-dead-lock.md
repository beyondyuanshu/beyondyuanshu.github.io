---
title: 死锁是指什么？
tags: AskCPP100
comments: true
key: C-2020041301
---

## 定义

死锁通常是指操作系统中进程的死锁，在多线程程序中也可能发现死锁。

多个进程同时获取系统资源，但是互不相让，造成都在等待，谁也不能继续住下运行，这种状态就称为死锁。

> 举例理解：
>
> 两个人相向而行（两个进程在运行）
>
> 正好面对面碰上（两进程均占有资源，并需要对方占有的资源，这里的资源即道路）
>
> 互不相让（都不愿意释放占有的资源）
>
> 两人都无法继续前进（死锁）
>
> 两人相互礼让，但恰好同时站在同一边让路，再次相让，仍是同一边，不断重复，最终还是无法前进（活锁）

## 四种必要条件

* **禁止抢占**：系统资源不能被其他进程抢过去，只能由当前进程释放。
* **持有和等待**：一个进程可以在等待的时候持有系统资源。
* **互斥**：资源不能同时分配给多个进程。
* **循环等待**：一系列进程互相持有其他进程所需要的资源。

## 如何解锁？

破坏死锁的条件即可以解锁。

基本思路：预防-避免-检测-解除，对死锁的防范程序依次减弱，但对系统资源的利用率依次提高，也就是并发程序依次提高。

## 实际编程中应该怎样做？

良好的编码设计，比如一次性获取所有的资源等

用银行家算法来判断死锁

超时就强制退出进程

## 参考

[https://zh.wikipedia.org/wiki/%E6%AD%BB%E9%94%81](https://zh.wikipedia.org/wiki/死锁)

[https://www.cnblogs.com/noteless/p/10354664.html#10](https://www.cnblogs.com/noteless/p/10354664.html#10)

[https://zhuanlan.zhihu.com/p/26945588](https://zhuanlan.zhihu.com/p/26945588)

[https://zh.wikipedia.org/zh-hans/%E9%93%B6%E8%A1%8C%E5%AE%B6%E7%AE%97%E6%B3%95](https://zh.wikipedia.org/zh-hans/银行家算法)

[https://www.computerworld.com/article/2585107/the-deadly-embrace.html](https://www.computerworld.com/article/2585107/the-deadly-embrace.html)