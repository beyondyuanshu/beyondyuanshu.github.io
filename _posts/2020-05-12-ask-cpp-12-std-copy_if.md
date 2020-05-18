---
title: 由 std::copy_if 想到的
tags: AskCPP100
comments: true
key: C-2020051201
typora-copy-images-to: upload
---

> \#AskCpp12 how to convert a float array to a double array in C++？

有一种方法是利用标准库中的算法库。

## std::copy_if

![image-20200512205836245](https://tva1.sinaimg.cn/large/007S8ZIlgy1gepyr8p49aj31eg0jkq94.jpg)

C++ 11 中只能用 copy_if。前三个参数好理解，两个源迭代器 + 一个目标迭代器，第三个参数称之为**一元谓词**。

### 何为谓词？

> ###  Effective STL
>
> "A predicate is a function that returns bool (or something that can be implicitly converted to bool). Predicates are widely used in the STL. The comparison functions for the standard associative containers are predicates, and predicate functions are commonly passed as parameters to algorithms like find_if and the various sorting algorithms."

> ### C++ concepts: Predicate 
>
> The `Predicate` concept describes a function object that takes a single iterator argument that is dereferenced and used to return a value testable as a bool.
>
> In other words, if an algorithm takes a `Predicate pred` and an iterator `first`, it should be able to test the iterator using the predicate via a construct like if (pred(*first)) {...}.
>
> The function object `pred` shall not apply any non-constant function through the dereferenced iterator. This function object may be a pointer to function or an object of a type with an appropriate function call operator.

简而言之，C++ 里的谓词是指一个能返回 True 或 False 的函数对象，通常用在标准库的算法库中。

测试代码：

```c++
#include <algorithm>
#include <iostream>

using namespace std;

int main() {
  float fArray[3] = {1.0, 2.0, 3.0};
  double dArray[3];

  // 此处 Lambda 表达式为谓词
  copy_if(fArray, fArray + 3, dArray, [](float arg) { return true; });

  for (size_t i = 0; i < 3; i++) {
    cout << dArray[i] << endl;
  }

  return 0;
}
```

输出

![image-20200512215306389](https://tva1.sinaimg.cn/large/007S8ZIlgy1geq0c349dpj30bo04e74a.jpg)

copy_if 源码

```c++
// copy_if
template<class _InputIterator, class _OutputIterator, class _Predicate>
inline _LIBCPP_INLINE_VISIBILITY
_OutputIterator
copy_if(_InputIterator __first, _InputIterator __last,
        _OutputIterator __result, _Predicate __pred)
{
    for (; __first != __last; ++__first)
    {
        if (__pred(*__first))  // 通过谓词过滤结果
        {
            *__result = *__first;
            ++__result;
        }
    }
    return __result;
}
```



## 参考

参考《STL 源码解析》

https://zhuanlan.zhihu.com/p/79088038

https://www.fluentcpp.com/getthemap/