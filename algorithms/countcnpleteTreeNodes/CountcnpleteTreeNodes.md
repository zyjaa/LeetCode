```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 * };
 */
class Solution {
public:
    int countNodes(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        int left = countLevel(root->left);  // 计算左子树的高度
        int right = countLevel(root->right); // 计算右子树的高度
        if (left == right) {
            return countNodes(root->right) + (1 << left); // 左子树是满的
        } else {
            return countNodes(root->left) + (1 << right); // 右子树是满的
        }
    }

private:
    // h
    int countLevel(TreeNode* root) {
        int level = 0;
        while (root != nullptr) {
            level++;
            root = root->left;
        }
        return level;
    }
};
```

- 时间：O($$h^2$$)
  - 每次调用countNodes h次，每次要看level O(h)，所以h平方
- 空间：O($$h$$)
