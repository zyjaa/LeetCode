```
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
    vector<string> res;
    vector<int> path;
    vector<string> binaryTreePaths(TreeNode* root) {
        if(!root)return res;
        dfs(root);
        return res;
    }
    void dfs(TreeNode* root){
        path.push_back(root->val);
        if(!root->left && !root->right){
            string a=to_string(path[0]);
            for(int i=1;i<path.size();i++)a+="->"+to_string(path[i]);
            res.push_back(a);
        }else{
            if(root->left)dfs(root->left);
            if(root->right)dfs(root->right);
        }
        path.pop_back();
    }
};
```

n,h
