---
layout: post
title: "Is Subsequence"
date: 2025-10-04
categories: leetcode
tags: [leetcode, algorithm]
---
# 392. Is Subsequence

Algorithm: 动态规划, 双指针
Data Structure: String
Difficulty: Easy
Last Review Time: September 5, 2022 1:42 PM
No: 392
Note: 没有考虑到两个字符串都为空的情况

# 判断子序列

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。

## 题目分析思路

遍历字符串t，s也从前向后遍历，遇到一个state标记往前走一个。

当state等于s.size()时返回true

当s和t都为空字符串的时候返回true

其余情况返回false

## 题目存在的为想到的知识点
