---
layout: post
title: "Extensible Hash Tables"
date: 2025-09-06
categories: database
tags: [database, sql]
---
Growing directory(buckets) by doubling

![image-20230401110712004](image-20230401110712004.png)

#### 插入

目标：插入一条关键字为k的记录
1. 计算$h(k)$
2. 取$h(k)$的前$i$位，去到相对应的bucket中
3. 根据directory(buckets)中的指针，找到对应的数据块$B$
   1. 如果数据块$B$中有剩余空间，则将记录放入$B$中，结束
   2. 如果数据块$B$中没有剩余空间，根据nub的值来做出对应的操作
      1. nub < i
         1. 将该数据块分成两个
         2. 将原数据块中的数据，根据前nub+1位来分配数据
         3. 将拆分后的两个数据块的nub值标为nub+1
         4. 调整directory中的指针
      2. nub = i
         1. i = i + 1，两倍原directory的长度，将entry的数量变为$2^{i+1}$
         2. 将原本要插入的数据块(overflow的数据块)分成两个，此时(nub < i)，与上述操作方法相同
         3. 将拆分后的两个数据块的nub值标为nub+1
         4. 调整directory中的指针，根据前i位来决定指针指向

例子：

nub < i 的情况

![IMG_26C78CF1D569-1](IMG_26C78CF1D569-1.jpeg)

nub = i 的情况

![IMG_394BABF82540-1](IMG_394BABF82540-1.jpeg)

#### 优点

Directory存储在内存中，查找只需要1次I/O

#### 缺点

在对directory进行翻倍的时候需要时间，会降低插入操作的速度
Directory在翻倍之后可能没法再存入到内存中



