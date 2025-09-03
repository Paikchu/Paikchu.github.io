#### 插入
1. 计算$h(k)$
2. 插入一条记录，r = r + 1
3. 取$h(k)$结果的后i位，作为bucket number($m$)
   1. $m < n$ : 把记录放入到块m中
   2. $n <= m < 2^i$: 块m不存在，把记录放入到bucket $m-2^{i-1}$中
   3. 如果在条件1或者2中，没有空余的位置，则添加一个overflow的块在原有块后
4. $r/n > threshold$
   1. 添加一个新的bucket到index中，n = n + 1
      1. 当$n$超过$2^i$，i = i + 1, 所有的bucket number前面都补0
   2. 重新分配所有的块数据