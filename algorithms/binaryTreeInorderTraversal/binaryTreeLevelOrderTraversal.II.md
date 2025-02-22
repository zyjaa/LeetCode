[107. 二叉树的层序遍历 II](https://leetcode.cn/problems/binary-tree-level-order-traversal-ii/)

**自底向上的层序遍历** 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[15,7],[9,20],[3]]
```



### 1、层次遍历

最后反转下就ok了

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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        if(!root)return {};
        vector<vector<int>> res;
        queue<TreeNode*> q;
        q.push(root);
        while(q.size()){
            int len=q.size();
            vector<int> level;
            while(len--){
                auto t=q.front();
                q.pop();
                level.push_back(t->val);
                if(t->left)q.push(t->left);
                if(t->right)q.push(t->right);
            }
            res.push_back(level);
        }
        reverse(res.begin(),res.end());
        return res;
    }
};
```

- 时间：n
- 空间：n