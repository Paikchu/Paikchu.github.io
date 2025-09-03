---
layout: post
title: "Binary Tree Preorder Traversal"
date: 2025-09-15
categories: leetcode
tags: [leetcode, algorithm]
---
# 144. Binary Tree Preorder Traversal

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: January 10, 2023 9:02 PM
No: 144
Note: 差两种

## 二叉树模板

`O(n),O(n)`

```cpp
class Solution {

public:
    void temp(TreeNode* root, vector<int>& ans){
        if(root == nullptr){
            return;
        }
        ans.push_back(root->val);
        temp(root->left, ans);
        temp(root->right, ans);

    }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        temp(root, ans);
        return ans;
    }
};
```
