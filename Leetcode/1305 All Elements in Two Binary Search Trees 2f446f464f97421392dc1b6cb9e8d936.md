# 1305. All Elements in Two Binary Search Trees

Algorithm: DFS, Sorting
Data Structure: Binary Search Tree, Binary Tree
Difficulty: Medium
Last Review Time: September 5, 2022 1:41 PM
No: 1305

## 中序遍历加归并

`O(n+m),O(n+m)`

inorder traversal + merge

时间复杂度：O(n+m)O(n+m)，其中 nn 和 mm 分别为两棵二叉搜索树的节点个数。

空间复杂度：O(n+m)O(n+m)。存储数组以及递归时的栈空间均为 O(n+m)O(n+m)。

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
    vector<int> getAllElements(TreeNode* root1, TreeNode* root2) {
        vector<int> t1;
        temp(root1, t1);
        vector<int> t2;
        temp(root2, t2);
        vector<int> ans;
        for(int i = 0, j = 0; i < t1.size() || j < t2.size();){
            if(i >= t1.size()  && j < t2.size()){
                ans.push_back(t2[j]);
                j++;
            }
            else if (i < t1.size() && j >= t2.size()){
                ans.push_back(t1[i]);
                i++;
            }
            else if(t1[i] < t2[j]){
                ans.push_back(t1[i]);
                i++;
            }
            else{
                ans.push_back(t2[j]);
                j++;
            }
        }
        return ans;
    }
};
```