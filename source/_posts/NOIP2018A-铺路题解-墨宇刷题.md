---
title: '[NOIP2018A]铺路题解-墨宇刷题'
date: 2020-07-06 15:09:32
tags: 题解
---

核心思想：贪心

# 题目描述

<!--more-->

![](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200706150809.png)

# 题意梳理
首先，有一个很长很长的地平线

![](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200706151328.png)

一天 工程师春春发现了好多坑😨
![](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200706151739.png)

现在，他必须填平这些坑。

![](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200706152257.png)

每个坑都有一个深度$d_i$,
春春每天可以选择一段连续区间[L,R] ，填充这段区间中的每块区域，让其下陷深度减少1。在选择区间时，需要保证，区间内的每块区域在填充前下陷深度均不为0。

春春希望你能帮他设计一种方案，可以在最短的时间内将整段道路的下陷深度都变为0

如选择[1,6]

![](https://gitee.com/inkuniverse/picture_bed/raw/master/img/20200706152627.png)

# 解法
此题有多种做法，都是基于贪心的做法。

这里只介绍一种做法。

考虑贪心，使用f[]记录当前（就是耗费多少），a[]记录以前。
若此坑深度比前一坑小或相同，则在填好d[i-1]时，可以顺便填好d[i].
否则，此坑只要填a[i]-a[i-1]次。
即
$$
f_i = a_i - a_{i-1}
$$
看一下具体实现
```cpp
#include<iostream>
using namespace std;
int n,a[100001],f[100001],ans;//a[]指原始下陷值，f[]指当前剩多少下陷值
int main()
{
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i];
        f[i]=a[i];//先一个一个填
    }
    for(int i=1;i<=n;i++)
    {
        if(a[i]>=a[i-1]) f[i]-=a[i-1];//将d(i)的一些操作在d(i-1)的操作里一起完成，偷点懒
        else f[i]=0; //可以完全填平
    }
    for(int i=1;i<=n;i++)
    {
        ans+=f[i];
    }
    cout<<ans;
    return 0;
}
```

[快捷下载1](https://raw.githubusercontent.com/inkuniverse/OI-code/a6371fb88c3217d6e1bce27e20e40ad59572e588/OI-Code.cpp)
[快捷下载2](https://raw./inkuniverse/OI-code/a6371fb88c3217d6e1bce27e20e40ad59572e588/OI-Code.cpp)