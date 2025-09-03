
##### Algorithm

Input: A universal relation R and a set of FDs F on the attributes of R.

```
SetD={R}
While there is a relation schema Q in D that is not in BCNF
do {
    choose a relation schema Q in D that is not in BCNF; 
    find an FD X → Y in Q that violates BCNF;
    replace Q in D by two relations (Q − Y) and (X ∪ Y);
 }
```

##### 判断一个关系是否满足BCNF

对每个函数依赖X->Y的左侧求闭包，如果对于每一个函数依赖，左侧的闭包都包含关系R中的所有属性，那么这个关系R满足BCNF范式

##### 例题

R(C, T, H, R, S), F={C->T, HR->C, HT->R, HS->R}

1. 对R(C,T,H,R,S)
2. 求候选码为HS
3. 考察{C->T}，不是BCNF, 分解，把FD中的T用C代换
   1. R1(CT), F1={C->T} 二元的，是BCNF
   2. R2(HRCS), F2={HR->C, HS->R, HC->R},关键字为HS，依赖中存在左侧不为HS的，所以不是BCNF
   3. ==继续==
      1. 对R2(H,R,C,S)，F2={HR->C, HS->R, HC->R}
      2. 求候选码为HS
      3. 考察{HR->C}, 不是BCNF, 分解
         1. R3(HRC), F3={HR->C, HC->R}，是BCNF
         2. R4(HRS), F4={HS->R}，是BCNF
         3. ==结束==

**结果为R1(CT), R2(HRC), R4(HRS)**

