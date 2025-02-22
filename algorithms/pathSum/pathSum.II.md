[113. 路径总和 II](https://leetcode.cn/problems/path-sum-ii/)

**从根节点到叶子节点**

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
    vector<vector<int>> res;
    vector<int> path;
    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        if(root)dfs(root,sum);
        return res;
    }
    void dfs(TreeNode* root,int sum){
        path.push_back(root->val);
        sum-=root->val;
        if(!root->left && !root->right){
            if(!sum){
                res.push_back(path);
            }
        }else{
            if(root->left)dfs(root->left,sum);
            if(root->right)dfs(root->right,sum);
        }
        path.pop_back();
    }
};
```

- 时间：n
- 空间：h