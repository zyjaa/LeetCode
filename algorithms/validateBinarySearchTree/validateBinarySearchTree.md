[98. 验证二叉搜索树](https://leetcode.cn/problems/validate-binary-search-tree/)

**有效** 二叉搜索树定义如下：

- 节点的左子树只包含 **小于** 当前节点的数。
- 节点的右子树只包含 **大于** 当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
输入：root = [2,1,3]
输出：true
```



### 1、中序遍历

中序遍历：正序数组，后面的树都必须比当前数大

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
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> stk;
        long long x=LONG_MIN;
        while(root || stk.size()){
            while(root){
                stk.push(root);
                root=root->left;
            }
            root=stk.top();
            stk.pop();
            if(root->val<=x)return false;
            x=root->val;
            root=root->right;
        }
        return true;
    }
};
```

- 时间：O($$n$$)
- 空间：O($$h$$)，树高