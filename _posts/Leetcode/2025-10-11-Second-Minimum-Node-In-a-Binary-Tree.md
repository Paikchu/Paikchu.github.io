---
layout: post
title: "Second Minimum Node In a Binary Tree"
date: 2025-10-11
categories: leetcode
tags: [leetcode, algorithm]
---
# 671. Second Minimum Node In a Binary Tree

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:42 PM
No: 671

`O(n),O(n)`

```cpp
class Solution {
public:
    int root_val;
    int ans;
    // 第二小的值，一定挨着第一小的值
    void temp(TreeNode* root){
        if(root == nullptr)
            return;
        temp(root->left);
        temp(root->right);
        if(root->val > root_val && root->val < ans || root->val > root_val && ans == -1){
            ans = root->val;
        }
    }

    int findSecondMinimumValue(TreeNode* root) {
        root_val = root->val;
        ans = -1;
        temp(root);
        return ans;

    }
};
```

```cpp
class Solution {
public:
    
    void temp(TreeNode* root, vector<int>& ans){
        if(root == nullptr)
            return;
        temp(root->left,ans);
        temp(root->right,ans);
        ans.push_back(root->val);
    }

    int findSecondMinimumValue(TreeNode* root) {
        vector<int> ans;
        temp(root, ans);
        sort(ans.begin(), ans.end());
        for(int i = 0; i < ans.size(); ++i){
            if(ans[i]!=ans[0]){
                return ans[i];
            }
        }
        return -1;

    }
};
```
