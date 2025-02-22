[112. 路径总和](https://leetcode.cn/problems/path-sum/)



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
    bool hasPathSum(TreeNode* root, int targetSum) {
        if(!root)return false;
        targetSum-=root->val;
        if(!root->left && !root->right)return !targetSum;
        return root->left && hasPathSum(root->left,targetSum) || root->right && hasPathSum(root->right,targetSum);
    }
};
```

- 时间：n
- 空间：h