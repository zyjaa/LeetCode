[110. 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)

判断它是否是 平衡二叉树 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
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
    bool res=true;
    bool isBalanced(TreeNode* root) {
        if(!root)return true;
        dfs(root);
        return res;
    }
    int dfs(TreeNode* root){
        if(!root)return 0;
        int l=dfs(root->left),r=dfs(root->right);
        if(abs(l-r)>1)res=false;
        return max(l,r)+1;
    }
};
```

- 时间：n
- 空间：n