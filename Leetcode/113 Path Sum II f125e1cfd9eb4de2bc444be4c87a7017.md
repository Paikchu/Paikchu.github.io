# 113. Path Sum II

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Medium
Last Review Time: September 5, 2022 1:41 PM
No: 113

`O(n^2),O(n)`

```cpp
class Solution {
public:

    void temp(TreeNode* root, int len, vector<int> ans, int target, vector<vector<int>>& res){
        if(root == nullptr)
            return;
        ans.push_back(root->val);
        len+=root->val;
        if(len == target && root->left == nullptr && root->right == nullptr){
            res.push_back(ans);
            return;
        }
        temp(root->left, len, ans,target,res);
        temp(root->right, len, ans,target,res);

    }

    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        int len = 0;
        vector<vector<int>> res;
        vector<int> ans;
        temp(root, len, ans, targetSum, res);
        return res;
    }
};
```