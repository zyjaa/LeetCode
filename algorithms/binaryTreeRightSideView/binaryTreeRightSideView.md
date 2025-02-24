当前层的最后一个节点，加入结果数组

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
    vector<int> rightSideView(TreeNode* root) {
        if (!root) return vector<int>(); // 如果根节点为空，返回空数组

        queue<TreeNode*> q; // 使用队列进行层序遍历
        q.push(root); // 将根节点入队
        vector<int> res; // 存储右视图的结果

        while (q.size()) { // 队列不为空时循环
            int len = q.size(); // 当前层的节点数
            while (len--) { // 遍历当前层的所有节点
                auto t = q.front(); // 获取队首节点
                q.pop(); // 队首节点出队

                if (!len) res.push_back(t->val); // 如果是当前层的最后一个节点，加入结果数组

                if (t->left) q.push(t->left); // 左子节点入队
                if (t->right) q.push(t->right); // 右子节点入队
            }
        }

        return res; // 返回右视图结果
    }
};
```

 
