---
layout: post
title: "Binary Tree Postorder Traversal"
date: 2025-09-16
categories: leetcode
tags: [leetcode, algorithm]
---
# 145. Binary Tree Postorder Traversal

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:41 PM
No: 145

## Recursion

`O(n),O(n)`

```cpp
class Solution {
public:
    void temp(TreeNode* root, vector<int>& ans){
        if(root == nullptr)
            return;
        temp(root->left, ans);
        temp(root->right, ans);
        ans.push_back(root->val);
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> ans;
        temp(root, ans);
        return ans;
    }
};
```
