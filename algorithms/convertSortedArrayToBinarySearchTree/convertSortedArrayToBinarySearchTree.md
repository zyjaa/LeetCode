[108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

答案不唯一

**例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg)

```
输入：nums = [-10,-3,0,5,9]
输出：[0,-3,9,-10,null,5]
```



### 1、DFS构建

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if(nums.empty())return {};
        return dfs(nums,0,nums.size()-1);
    }
    TreeNode* dfs(vector<int>& nums,int l,int r){
        if(l>r)return nullptr;
        int m=l+r>>1;
        auto root=new TreeNode(nums[m]);
        root->left=dfs(nums,l,m-1);
        root->right=dfs(nums,m+1,r);
        return root;
    }
};
```

- 时间：n
- 空间：logn