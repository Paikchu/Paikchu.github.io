# 226. Invert Binary Tree

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:41 PM
No: 226

`O(n),O(n)`

```cpp
class Solution {
public:

    TreeNode* invertTree(TreeNode* root) {
        if(root == nullptr){
            return root;
        }
        TreeNode* left = invertTree(root->right);
        TreeNode* right = invertTree(root->left);
        root->left = left;
        root->right = right;
        return root;
    }
};
```