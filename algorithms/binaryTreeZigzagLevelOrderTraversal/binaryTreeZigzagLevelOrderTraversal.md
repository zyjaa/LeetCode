[103. 二叉树的锯齿形层序遍历](https://leetcode.cn/problems/binary-tree-zigzag-level-order-traversal/)

先左再右，然后先右再左，和102基本一样，就判断个奇偶



### 1、层次遍历

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if(!root)return {};
        int cnt=0;
        queue<TreeNode*> q;
        q.push(root);
        vector<vector<int>> res;
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
            if(++cnt%2==0)reverse(level.begin(),level.end());
            res.push_back(level);
        }
        return res;
    }
};
```

- 时间：n
  - 遍历所有节点n，反转n，O(n)+O(n)=O(n)
- 空间：n