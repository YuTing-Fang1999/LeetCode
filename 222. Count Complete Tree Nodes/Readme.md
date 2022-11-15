## 222. Count Complete Tree Nodes

## Description
Given the `root` of a complete binary tree, return the number of the nodes in the tree.  

## Solution
`DFS`

## Code
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
 int DFS(TreeNode* root){
     if(root==NULL) return 0;
     int n=1;
     n+=DFS(root->left);
     n+=DFS(root->right);
     return n;
 }
class Solution {
public:
    int countNodes(TreeNode* root) {
        return DFS(root);
    }
};
```

### one-line solution  
https://leetcode.com/problems/count-complete-tree-nodes/solutions/2815866/1-row-dfs-c-solution-time-o-n-space-o-logn/  
```cpp
class Solution {
public:
    int countNodes(TreeNode* root) {
        return !root ? 0 : 1 + countNodes(root->left) + countNodes(root->right);
    }
};
```
