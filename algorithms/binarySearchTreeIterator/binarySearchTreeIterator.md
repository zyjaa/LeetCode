### 1、栈

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
class BSTIterator {
public:
    stack<TreeNode*> stk; // 用于存储节点的栈

    // 构造函数，初始化迭代器
    BSTIterator(TreeNode* root) {
        while (root) {
            stk.push(root); // 将当前节点压入栈
            root = root->left; // 移动到左子节点
        }
    }

    // 返回下一个最小的值
    int next() {
        auto t = stk.top(); // 获取栈顶节点
        stk.pop(); // 弹出栈顶节点
        int res = t->val; // 获取当前节点的值

        // 处理右子树
        if (t->right) {
            t = t->right; // 移动到右子节点
            while (t) {
                stk.push(t); // 将右子节点及其左子节点压入栈
                t = t->left;
            }
        }
        return res; // 返回当前节点的值
    }

    // 检查是否还有下一个值
    bool hasNext() {
        return stk.size(); // 如果栈不为空，说明还有下一个值
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```

- **构造函数**的时间复杂度为 **O(h)**。
- **`next()` 方法**的**摊还时间复杂度为 O(1)**，但单次调用最坏情况下为 **O(h)**。
- **`hasNext()` 方法**的时间复杂度为 **O(1)**。
- **空间复杂度**为 **O(h)**，其中 `h` 是树的高度。
