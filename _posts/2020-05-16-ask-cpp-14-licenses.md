---
title: 开源许可
tags: AskCPP100 Qt
comments: true
key: C-2020051601
---

> \#AskCpp14 这么多开源协议都有什么区别呀？Qt 的许可协议有 LGPL、GPL、商业授权，那么基于开源的 Qt 开发的程序也需要开源吗？

**你可以在“开源计划”的官网上查看所有协议的详细内容**

https://opensource.org/



**以下是阮一峰老师的开源许可证教程，对相关概念讲得比较清晰**

http://www.ruanyifeng.com/blog/2017/10/open-source-license-tutorial.html



**假如你要为自己的开源项目选择协议，可以通过 GitHub 提供的“开源协议选择器”，会一步一步带领你选择**

https://choosealicense.com/

https://ufal.github.io/public-license-selector/

**这里介绍了如何在你的 GitHub 仓库中添加 License**

https://help.github.com/cn/github/building-a-strong-community/adding-a-license-to-a-repository



**这个网站提供各个 License 的通俗解释（英文）**

https://tldrlegal.com/



**Qt 的许可证**

**三种：LGPL、GPL、商业授权**

* 商业授权也好理解，需要购买，一年将近 3 万！

  <img src="https://tva1.sinaimg.cn/large/007S8ZIlgy1geu4sk2ql1j30l80t0dhv.jpg" alt="dfd" align=left style="zoom: 33%;" />

* LGPL：如果项目采用动态链接调用该许可证的库，项目可以不用开源。

* GPL：如果项目包含了 GPL 许可证的代码，那么整个项目都必须使用 GPL 许可证。

**结论：能使用开源的 Qt 库进行商业开发，但需要做一些工作，比如只能用 DLL 库，需要添加协议说明等等等等。**

下面的文章详细说明了 Qt 中的许可证的使用。

https://blog.csdn.net/zhouqt/article/details/91975943

  

