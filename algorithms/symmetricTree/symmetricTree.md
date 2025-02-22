[101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

给你一个二叉树的根节点 `root` ， 检查它是否轴对称。

 

**示例 1：**

![img](https://pic.leetcode.cn/1698026966-JDYPDU-image.png)

```
输入：root = [1,2,2,3,4,4,3]
输出：true
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
    bool isSymmetric(TreeNode* root) {
        if(!root)return true;
        return dfs(root->left,root->right);//看根节点左右子树是否一样
    }
    bool dfs(TreeNode* p,TreeNode* q){
        if(!p && !q)return true;// 2个空，true
        if(!p && q || !q && p)return false;// 1个空，1个非空，false
        if(p->val!=q->val)return false;//值不相等，false
        return dfs(p->left,q->right) && dfs(p->right,q->left);//我的左边和你的右边是否一样，我的右边和你的左边是否一样
    }
};
```

- 时间：n，所有节点都要遍历
- 空间：O($$h$$)
  - 树平衡：h=logn
  - 不平衡：h=n（最坏情况退化为链表）