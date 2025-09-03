---
layout: post
title: "Binary Tree Level Order Traversal"
date: 2025-09-06
categories: leetcode
tags: [leetcode, algorithm]
---
# 102. Binary Tree Level Order Traversal

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Medium
Last Review Time: September 5, 2022 1:40 PM
No: 102

## DFS

`O(n),O(n)`

```cpp
class Solution {
public:
    vector<vector<int>> res;
    void temp(TreeNode* root, int level){
        if(root == nullptr)
            return;
        level+=1;
        if(res.size() < level)
            res.push_back(vector<int>());
        res[level-1].push_back(root->val);
        temp(root->left, level);
        temp(root->right, level);

    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        temp(root, 0);
        return res;
    }
};
```
