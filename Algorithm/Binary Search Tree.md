# Binary Search Tree

## Binary Search Tree (BST)

Binary search tree is a data structure which base on binary tree.

It is a binary tree because each tree node has a maxmum of two children.

It is called a search tree because it can be used to search for the presence of a number in `O(log(n))`.

## Properties

1. All nodes of left subtree are less than the root node
2. All nodes of right subtree are more than the root node
3. Both subtree of each node have the above two properties

## Operation

### Search

If the value below the root value, we can not make sure this value must have but this value must not be in right subtree. If the value more than the root value, this value is not in left subtree. 

```cpp
if ( root == nullptr )
	return nullptr;
if( value == root->val )
	return root;
if ( value < root->val )
	return search(root->left);
if ( value > root->val )
	return search(root->right);
```

### Insert

Insert operation is similar to search operation because we need to maintain the properties of the binary search tree. We do the same operate like search until we reach a node which left or right subtree is null, we put the new node there.

```cpp
if ( root == nullptr )
	return createNode(data)
if ( data < root->val )
	root->left = insert(root->left, data)
else if ( data > root->val )
	root->right = insert(root->right, data)
return root;
```