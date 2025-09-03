---
layout: post
title: "Binary Tree Paths"
date: 2025-09-30
categories: leetcode
tags: [leetcode, algorithm]
---
# 257. Binary Tree Paths

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:41 PM
No: 257

`O(n^2),O(n^2)`

```cpp
class Solution {
public:

    void dfs(TreeNode* root, vector<string>& ans, string a){
        if(root != nullptr && root->left == nullptr && root->right == nullptr){
            a.append(to_string(root->val));
            ans.push_back(a);
            cout << a << endl;
            return;
        }
        if(root!=nullptr){
            string c = to_string(root->val);
            a.append(c);
            //a.push_back(root->val + '0');
            a.push_back('-');
            a.push_back('>');
            dfs(root->left, ans, a);
            dfs(root->right, ans, a);
        }
        if(root == nullptr){
            return;
        }
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<string> ans;
        string a;
        dfs(root, ans, a);
        return ans;
    }
};
```
