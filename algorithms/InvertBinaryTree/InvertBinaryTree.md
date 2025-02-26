### 1、递归

```
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
    TreeNode* invertTree(TreeNode* root) {
        if(!root)return NULL;
        swap(root->left,root->right);
        invertTree(root->left);
        invertTree(root->right);
        return root;
    }
};
```

 对于 `TreeNode*` 这样的指针类型，`swap` 会直接交换指针的值

- 时间：n，每个点都会遍历
- 空间：h



迭代实现

```
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (!root) return nullptr;

        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            TreeNode* node = q.front();
            q.pop();

            // 交换当前节点的左右子树
            swap(node->left, node->right);

            // 将左右子节点加入队列
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }

        return root;
    }
};
```

1. **时间复杂度**：**O(n)**，每个节点被访问一次。
2. **空间复杂度**：**O(n)**，队列的最大长度为节点数。
