[106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
输出：[3,9,20,null,null,15,7]
```



### 1、模拟

注意边界

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
    unordered_map<int,int> q;
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        for(int i=0;i<inorder.size();i++)q[inorder[i]]=i;
        return dfs(inorder,postorder,0,inorder.size()-1,0,postorder.size()-1);
    }
    TreeNode* dfs(vector<int>& inorder,vector<int>& postorder,int il,int ir,int pl,int pr){
        if(il>ir)return nullptr;
        auto root=new TreeNode(postorder[pr]);
        int k=q[postorder[pr]];
        root->left=dfs(inorder,postorder,il,k-1,pl,pl+k-1-il);
        root->right=dfs(inorder,postorder,k+1,ir,pl+k-1-il+1,pr-1);
        return root;
    }
};
```

- n
- n