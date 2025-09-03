---
layout: post
title: "Minimum Depth of Binary Tree"
date: 2025-09-09
categories: leetcode
tags: [leetcode, algorithm]
---
# 111. Minimum Depth of Binary Tree

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:40 PM
No: 111
Note: BFS没写

## DFS

`O(n),O(n)`

```cpp
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == nullptr)
            return 0;
        else if(root->left == nullptr){
            return minDepth(root->right) + 1;
        }
        else if(root->right == nullptr){
            return minDepth(root->left) + 1;
        }
        return min(minDepth(root->left), minDepth(root->right)) + 1;
    }
};
```

```cpp
class Solution {
public:
    int ans = 10000;

    void temp(TreeNode* root, int level){
        if(root == nullptr)
        {
            return;
        }
        level += 1;
        if(root->left == nullptr && root->right == nullptr){
            ans = min(ans, level);
        }
        temp(root->left, level);
        temp(root->right, level);
    }

    int minDepth(TreeNode* root) {
        if(root == nullptr)
            return 0;
        temp(root, 0);
        return ans;
    }
};
```
