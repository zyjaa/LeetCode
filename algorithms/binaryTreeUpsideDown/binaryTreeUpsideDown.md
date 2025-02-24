题目：https://blog.csdn.net/qq_29051413/article/details/108615815 

### 1、递归

1. **递归实现**：
   - 从根节点开始，递归地翻转左子树。
   - 将当前节点的左子节点作为新的根节点。
   - 将当前节点的右子节点作为新的左子节点的左子节点。
   - 将当前节点作为新的左子节点的右子节点。
2. **终止条件**：
   - 如果当前节点为空，或者当前节点没有左子节点，则直接返回当前节点。
3. **返回结果**：
   - 返回新的根节点。

```cpp
class Solution {
public:
    TreeNode* upsideDownBinaryTree(TreeNode* root) {
        // 终止条件
        if (root == nullptr || root->left == nullptr) {
            return root;
        }

        // 递归翻转左子树
        TreeNode* newRoot = upsideDownBinaryTree(root->left);

        // 将当前节点的左子节点作为新的根节点
        root->left->left = root->right;
        root->left->right = root;

        // 断开当前节点的左右子节点
        root->left = nullptr;
        root->right = nullptr;

        // 返回新的根节点
        return newRoot;
    }
};
```

1. **时间复杂度**：
   - 每个节点只会被访问一次，时间复杂度为 **O(n)**，其中 `n` 是二叉树的节点数。
2. **空间复杂度**：
   - 递归调用栈的深度为树的高度，最坏情况下为 **O(n)**。
