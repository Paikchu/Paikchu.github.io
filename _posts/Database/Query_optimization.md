
## Optimization for join

1. Nested Loop Join
	+ Simple
	+ Block
	+ Index 
1. Sort-Merge Join 
2. Hash Join

Given a relation R:
T(R): the number of tuples in R
P(R): the number of pages in R

#### Nested Loop Join(NLJ) 

``` python
for tuple r in R:
	for tuple s in S:
		if r[A] == s[A]:  # Assume join on A, r matches s
			yield(r, s)
```

Cost: $P(R) + T(R) * P(S) + OUT$
对于R中的每条记录，整个Page(S)都需要被完整遍历一遍。把相同的输出存储到空间中。
较小数据量的relation要放在outer loop中。

#### Block Nested Loop Join (BNLJ) 

假设分配 B Pages (注： 该Page为内存中的Page，并不是储存表的Page) 大小的buffer，该内存中 B-2 pages 分配给缓存R中的数据，1 page 分配给缓存S中的数据，1 page分配给输出的数据。

``` python
for B-2 pages pr in R:	# 每次从R中加载 B-1 pages 大小的数据到内存中
	for page ps in S:  # 每次从S中加载一个 1 page 大小的数据到内存中
		foreach tuple r in pr:
			foreach tuple s in ps:
				if r[A] == s[A]:
					yield(r, s)
```

Cost: $P(R) + \frac{P(R)}{B-2}P(S) + OUT$

S需要被读取$\frac{P(R)}{B-2}$次，与NLJ相比，减少了读全部S数据的次数，但是消耗了更多的内存空间，并且这两种都需要计算Cross-product

Follow up: 如果outer loop中的关系的所有数据都可以放入内存中，I/O cost 会变成 $P(R) + P(S)$。

#### Index Nested Loop Join(INLJ)

NLJ和BNLJ速度慢的原因是，在寻找匹配tuple时，我们都需要遍历整个关系（cross product），整个join的过程是二维的复杂度。
可以使用数据库建立时创建的index来加速join的匹配过程。可以使用index去查找满足condition的数据，来避免对两个进行完全的（cross-product）计算。

``` python
foreach tuple r in R:
	foreach tuple s in S and Index(r.A == s.A) # Assume the index on A
		yield (r, s)
```

Cost: $P(R) + (T(R) \times C) + OUT$ ，$C$ 为每次使用index查找tuple的消耗


#### Sort Merge Join(SMJ) ==Only equality join==

+ 当一个表或者两个表已经对于join的key进行过排序
+ 输出必须为有序
+ 待join的关系可以被排序

Phase 1: Sort
+ Sort both tables on the join key(s) with [[[external merge sort algorithm]]].
Phase 2: Merge
+ Step through the two sorted tables in parallel, and yield the matching tuples.

```
do{
	if(!mark){
		while(r<s) r++;
		while(s<r) s++;
		mark = s;
	}
	if(r == s){
		emit result<r, s>
		s++;
	}
	else{
		s = mark;
		r++;
		mark = null;
	}
}
```

Cost: 
$Sort(R) + Sort(S) + Merge$
$=2P(R) * (log_BP(R)) + 2P(S) * (log_BP(S)) + (P(R)+P(S))$
Worst case: for the merging phase is when join attribute of all of the tuples in both relations contain the same value.
$=2P(R) * (log_BP(R)) + 2P(S) * (log_BP(S)) + (P(R)*P(S))$

#### Hash Join ==Only equality join==

Phase 1: Build
+ 构建一个hash table使用hash function $h_1$ 对于join的属性。

Phase 2: Probe
+ 对于另一个表使用相同的hash function $h_2$ 对于每个tuple进行哈希，映射到hash table中的某个位置，然后找匹配的tuple

``` python
build hash table HTr for R
foreach tuple s in S
	if h1(s) in HTr
		yield
```

![[Pasted image 20230401205707.png]]
Hash join is highly parallelizable but sensitive to skew. 
Hash function 设计不好，导致不同的key都分在同一个bucket中。
1. Hash partition: split R and S into buckets using $h_B$ on A (partition)
2. Per-partition join: join tuples in the same partition (same hash value)

Hash table contents:
Key: The attribute(s) that the query is joining the tables on.
Value: Depends on implementation. 
1. Full Tuple: avoid retrieve from the disk, but take more space in memory.
2. Tuple Identifier: Ideal for column stores or join selectivity is low.

##### Cost
Partitioning Phase:
$2(P(R) + P(S))$
Probing Phase:
$P(R)+P(S)$
The total I/O cost:
$3(P(R) + P(S)) + OUT$


#### Grace Hash Join
R hash h1 到 一组 buckets, S hash h1 到一组buckets，然后对这两组buckets做hash 使用h2，从而避免，内存占用过大的问题，并且解决overflow的问题


## Optimization of Operators other than Join

### Optimization of Projection

#### Sorting

**Modify Pass 1** to elminate unwanted fields. Thus, tuples in runs are smaller than input tuples. (Size ratio depends on # and size of fields that are dropped.)

**Modify merging passes** to elminate duplicates. Thus, number of result tuples smaller than input. 怎么消除重复

Cost: In Pass 1, read original relation (size M), write out same or smaller number of smaller tuples. In merging passes, fewer tuples written out in each pass.

#### Hashing

Partitioning phase

Duplicate elimination phase

Cost: For partitioning, read R, write out each tuple, but with fewer fields. This output is read in the next phase: 4*P(R)

#### More

Sorted-based approach is the standard and better for handling of skew and result is sorted

如果一个关系的index包括所有需要的字段，可以使用index-only scan，不需要花费读取的I/O



### Optimization of Aggregation

Without grouping:
+ In general, requires scanning the relation. 
+ Given an index whose search key includes all attributes in the SELECT clause (if there is no WHERE), we can do index-only scan.

With grounding:
+ Sort on group-by attributes, then scan relation and compute aggregate for each group
+ Use hashing on group-by attributes
+ 如果一个关系的index包括所有需要的字段，可以使用index-only scan
+ 如果包括一部分，可以取出数据根据group-by的顺序