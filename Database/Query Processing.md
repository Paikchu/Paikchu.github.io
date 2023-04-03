DBMS prefer left deep tree plan: facilitate pipelining

Query rewriting: transforming one logical plan into another without using statistics
Advantage: Eliminating redundant conditions/operators reduce optimization time, improve performance

Some Query Rewrite rule
+ Push-down slection predicates
+ Do projects early
+ Avoid cross-products if possible
+ Leveraging RA equivalences 利用RA等效性
	+ Commutativity 交换律：R⨝S=S⨝R
	+ Asociativity 结合律：(R⨝S)⨝T=R⨝(S⨝T)
	+ 对于其他的操作也一样适用
#### Rules for Projection
P and Q contain join attributes:
$$∏_M(𝑅⨝𝑆)= ∏_M((∏_M𝑅) ⨝ ( ∏_Q < 𝑆))$$

M ⊆ N: 
$$∏_M (∏_N𝑅) = ∏_M𝑅$$

![[Pasted image 20230402110431.png]]

#### Optimizing query plan

遍历所有可能的physical plans，算出每种计划的COST，选取COST最小的计划

##### Cost-based optimizers
##### Selinger Optimizer
Consider the left deep join tree

Choose an order for join
Step 1: 枚举每一个关系scan关系的cost，保留每个关系中最低消耗的scan操作（最低操作需要考虑到排序等操作，例如，乱序遍历一个关系可能比顺序遍历快，但上层需要排序操作，此时优先选择可实现排序的scan）
Step 2: 选出两个relation，来评估他们join的cost，当使用join算法的时候

![[Pasted image 20230403000122.png]]