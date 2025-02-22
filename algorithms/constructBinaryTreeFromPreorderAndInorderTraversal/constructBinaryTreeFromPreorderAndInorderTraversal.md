[105. 从前序与中序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)



**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]
```



### 1、模拟

划分好区间，注意边界

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
    unordered_map<int,int> pos;
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        for(int i=0;i<inorder.size();i++)pos[inorder[i]]=i;
        return build(preorder,inorder,0,preorder.size()-1,0,inorder.size()-1);
    }
    TreeNode* build(vector<int>& preorder, vector<int>& inorder,int pl,int pr,int il,int ir){
        if(pl>pr)return nullptr;
        auto root=new TreeNode(preorder[pl]);
        int k=pos[preorder[pl]];
        root->left=build(preorder,inorder,pl+1, pl+1+k-il-1 ,il,k-1);
        root->right=build(preorder,inorder,pl+1+k-il+1-1,pr,k+1,ir);
        return root;
    }
};
```

- 时间：n
- 空间：n