[94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,3,2]
```





### 1、迭代遍历

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        stack<TreeNode*> stk;
        while(root || stk.size()){
            while(root){
                stk.push(root);
                root=root->left;
            }
            root=stk.top();
            stk.pop();
            res.push_back(root->val);
            root=root->right;
        }
        return res;
    }
};
```

- 时间：n
- 空间：n
  - 可能是链表，一路直下来