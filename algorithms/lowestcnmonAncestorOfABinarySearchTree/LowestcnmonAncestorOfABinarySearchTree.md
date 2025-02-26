```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(!root)return NULL;
        int a=root->val,b=p->val,c=q->val;
        if(b<a && c<a)return lowestCommonAncestor(root->left,p,q);
        if(b>a && c>a)return lowestCommonAncestor(root->right,p,q);
        return root;
    }
};
```

 
