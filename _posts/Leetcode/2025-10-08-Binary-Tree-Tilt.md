---
layout: post
title: "Binary Tree Tilt"
date: 2025-10-08
categories: leetcode
tags: [leetcode, algorithm]
---
# 563. Binary Tree Tilt

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:42 PM
No: 563

`O(n),O(n)`

```cpp
class Solution {
public:
    int ans = 0;
    int temp(TreeNode* root){
        if(root == nullptr)
            return 0;
        int l = temp(root->left);
        int r = temp(root->right);
        ans += abs(l - r);
        return l + r + root->val;
    }
    int findTilt(TreeNode* root) {
        int l = temp(root);
        return ans;

    }
};
```
