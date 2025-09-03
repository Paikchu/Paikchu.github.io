---
layout: post
title: "External merge sort algorithm"
date: 2025-09-07
categories: database
tags: [database, sql]
---
#### Problem
The data cannot be loaded into the memory at one time
Suppose the memory size has M pages and relation R has B blocks and B > M.

Phase 1: sort data in sublists
+ Fill the M pages buffer with tuples in R.
+ Sort them
+ Write them back to the disk as a sublist
![[Pasted image 20230402100051.png]]
Phase 2: merge the sorted sublists
+ allocate one ==input== page from each sorted sublist, M pages support us allocate M-1 pages to sublists，每个input包括一个sublist的部分tuples
+ allocate one page to the output
+ merge sort tuples in input pages
	+ 选出M-1的input pages中的最小的tuple，放入output中
	+ 被拿走tuple的input page再从sublist中补充一个tuple进到input page里
	+ 如果sublist中没有剩余tuple了，就空余这块buffer
	+ 当output被填满，就将output的内容写入到disk中，初始化output page，来接收后续的写入
![[Pasted image 20230402100038.png]]
在上述条件下，每个sublist有M pages的大小，sublists的总数为 B/M，B/M <= M - 1
Cost: 
+ Read B blocks from disk
+ Write B blocks of the sorted sublists to disk 
+ Read B blocks sorted sublists to merge
+ Total 3B

当数据量特别大时，可以把数据分成大小为M(M-1)的块，对每块进行Merge sort，直到处理完所有数据。
![[Pasted image 20230402100619.png]]Suppose the file has M blocks, 一共只有3个buffer，2个用于sublist， 1个用于output
每个Pass的cost是M + M，一共 $log_2M$个passes。
Pass数量为$log_nM$, n为每次合并，内存中能容纳的sublist的个数，本题中buffer大小为3，所以最多能放下2个sublist。


#### Cost
M 为 内存中的buffer数量，M-1用于存放sublist，1 用于 output
$2B(log_{M}B)$ 
$2B(log_{M-1}\frac{B}{M}+1)$
log均向上取整


通常会在排序好的数据中，留下几个空位置，方便插入操作

