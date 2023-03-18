# 94. Binary Tree Inorder Traversal

Algorithm: DFS
Data Structure: Binary Tree
Difficulty: Easy
Last Review Time: January 10, 2023 9:02 PM
No: 94

## Recursion

```cpp
class Solution {
public:

    void temp(TreeNode* root, vector<int>& ans){
        if(root == nullptr)
            return;
        temp(root->left, ans);
        ans.push_back(root->val);
        temp(root->right, ans);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        temp(root, ans);
        return ans;
    }
};
```

```cpp

class Solution {
 public:
  vector<int> inOrder(TreeNode* root) {
    // write your solution 
    vector<int> ans;
    if(root == nullptr){
      return ans;
    }
    vector<int> left = inOrder(root->left);
    ans.insert(ans.end(), left.begin(), left.end());
    ans.push_back(root->value);
    vector<int> right = inOrder(root->right);
    ans.insert(ans.end(), right.begin(), right.end());
    return ans;
  }
};
```

## iterative

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> res;

        while(root != nullptr || !res.empty()){
            while(root != nullptr){
                res.push(root);
                root = root->left;   // 注意这两句的顺序不能变
            }
            ans.push_back(res.top()->val);
            root = res.top() -> right;
            res.pop();

            
        }
        return ans;

    }
```