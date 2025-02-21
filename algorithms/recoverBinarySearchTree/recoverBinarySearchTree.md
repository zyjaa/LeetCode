[99. 恢复二叉搜索树](https://leetcode.cn/problems/recover-binary-search-tree/)

给你二叉搜索树的根节点 `root` ，该树中的 **恰好** 两个节点的值被错误地交换。*请在不改变其结构的情况下，恢复这棵树* 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/28/recover1.jpg)

```
输入：root = [1,3,null,null,2]
输出：[3,1,null,null,2]
解释：3 不能是 1 的左孩子，因为 3 > 1 。交换 1 和 3 使二叉搜索树有效。
```



### 1、中序遍历

开辟一个新数组*nums*来记录中序遍历得到的值序列，然后线性遍历找到两个位置*i*和*j*，并重新遍历原二叉搜索树修改对应节点的值完成修复

```cpp
class Solution {
public:
    void inorder(TreeNode* root, vector<int>& nums) {
        if (root == nullptr) {
            return;
        }
        inorder(root->left, nums);
        nums.push_back(root->val);
        inorder(root->right, nums);
    }

    pair<int,int> findTwoSwapped(vector<int>& nums) {
        int n = nums.size();
        int index1 = -1, index2 = -1;
        for (int i = 0; i < n - 1; ++i) {
            if (nums[i + 1] < nums[i]) {
                index2 = i + 1;
                if (index1 == -1) {
                    index1 = i;
                } else {
                    break;
                }
            }
        }
        int x = nums[index1], y = nums[index2];
        return {x, y};
    }
    
    void recover(TreeNode* r, int count, int x, int y) {
        if (r != nullptr) {
            if (r->val == x || r->val == y) {
                r->val = r->val == x ? y : x;
                if (--count == 0) {
                    return;
                }
            }
            recover(r->left, count, x, y);
            recover(r->right, count, x, y);
        }
    }

    void recoverTree(TreeNode* root) {
        vector<int> nums;
        inorder(root, nums);
        pair<int,int> swapped= findTwoSwapped(nums);
        recover(root, 2, swapped.first, swapped.second);
    }
};
```

- 时间：n
- 空间：n



### 2、Morris遍历

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
    void recoverTree(TreeNode* root) {
        TreeNode* first=nullptr,*second=nullptr,*pre=nullptr;
        while(root){
            if(!root->left){
                if(pre && root->val<pre->val){
                    if(!first)first=pre,second=root;
                    else second=root;
                }
                pre=root;
                root=root->right;
            }else{
                auto p=root->left;
                while(p->right && p->right!=root)p=p->right;
                if(!p->right){
                    p->right=root;
                    root=root->left;
                }else{
                    p->right=nullptr;
                    if(pre && pre->val>root->val){
                        if(!first)first=pre,second=root;
                        else second=root;
                    }
                    pre=root;
                    root=root->right;
                }
            }
        }
        swap(first->val,second->val);
    }
};
```

- 时间：n
- 空间：1