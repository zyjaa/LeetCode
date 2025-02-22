 

[124. 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/)

给你一个二叉树的根节点 `root` ，返回其 **最大路径和** 。

### 1、DFS

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
class Solution {
public:
    int ans;
    int maxPathSum(TreeNode* root) {
        ans=INT_MIN;
        dfs(root);
        return ans;
    }
    int dfs(TreeNode* root){
        if(!root)return 0;
        int left=max(0,dfs(root->left)),right=max(0,dfs(root->right));
        ans=max(ans,root->val+left+right);
        return root->val+max(left,right);
    }
};
```

- 时间：n
- 空间：h
