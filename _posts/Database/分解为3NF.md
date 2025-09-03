# 分解为3NF

#### 第三范式分解

##### Algorithm

1. 找到候选键 CK
   1. Find Attribute Closure
   2. The Closure can include all the attributes
2. 获得最小依赖集 Minimal Cover
3. 分解为3NF

##### 例题

R(A, B, C, D, E, F) A->D; BE->A; C->F; CE->D; D->A

1. Find Candidate keys: BCE

   1. L（左边出现）: B, C, E
   2. LR（左右都出现）: A, D
   3. R（右边出现）: F

   因为BCE只在左边出现，所以BCE一定是CK的一部分，因为只有他们自己能推出自己。

   找BCE的闭包：BCE+ : B, C, E, A, F, D	 -->可以包含全部属性，所以BCE是唯一的候选键

2. 找最小依赖集：

   1. 先找出来左边有多个键的
      1. BE -> A, CE -> D
   2. 查组合键能不能分解
      1. B -> A ? E -> A ? No, BE->A, B和E一个都不能少
      2. C -> D? E -> D? No, CE -> D, C和E一个都不能少
   3. 查剩余键
      1. BE -> A 查在没有这条规则的情况下，BE是否还能推得A，不能，所以保留
      2. CE -> D 保留
      3. A -> D 保留
      4. C -> F 保留
      5. D -> A 保留

3. 查看CK是否在最小依赖集中 (BEA), (CED), (AD), (CF), (DA)

   1. 不在：则需要将CK添加到其中

4. 结果为 (BCE), (BEA), (CED), (AD), (CF), (DA)