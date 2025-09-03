# 110. Balanced Binary Tree

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: September 5, 2022 1:40 PM
No: 110
Note: 关联104题

## Recursion

`O(n^2),O(n)`

拆解为最大深度问题，递归判断每个子树的最大深度，最大深度的差值小于1，即为平衡二叉树。

```cpp
class Solution {
public:

    int maxDepth(TreeNode* root){
        if(root == nullptr){
            return 0;
        }
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }

    bool isBalanced(TreeNode* root) {
        if(root == nullptr){
            return true;
        }
        return abs(maxDepth(root->left)-maxDepth(root->right)) <= 1 && isBalanced(root->left) && isBalanced(root->right);
    }
};
```