[100. 相同的树](https://leetcode.cn/problems/same-tree/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg)

```
输入：p = [1,2,3], q = [1,2,3]
输出：true
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg)

```
输入：p = [1,2], q = [1,null,2]
输出：false
```



### 1、模拟

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
    bool isSameTree(TreeNode* p, TreeNode* q) {
        // 如果两棵树当前节点都为空，说明当前子树完全相同，返回 true
        if (!p && !q) return true;

        // 如果两棵树当前节点中只有一个为空，或者当前节点的值不相等，返回 false
        if (!p && q || !q && p || p->val != q->val) return false;

        // 递归检查左子树和右子树是否相同，只有左右子树都相同才返回 true
        return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```

- 时间：n
- 空间：h