[109. 有序链表转换二叉搜索树](https://leetcode.cn/problems/convert-sorted-list-to-binary-search-tree/)

答案不唯一

**示例 1:**

![img](https://assets.leetcode.com/uploads/2020/08/17/linked.jpg)

```
输入: head = [-10,-3,0,5,9]
输出: [0,-3,9,-10,null,5]
```





```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
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
    TreeNode* sortedListToBST(ListNode* head) {
        if(!head)return nullptr;
        int n=0;
        for(auto p=head;p;p=p->next)n++;//链表长度
        if(n==1)return new TreeNode(head->val);
        auto p=head;
        for(int i=0;i<n/2-1;i++)p=p->next;//中点前一个位置
        auto root=new TreeNode(p->next->val);//奇数：正中点，偶数：后中点
        root->right=sortedListToBST(p->next->next);//中点后一个位置
        p->next=nullptr;
        root->left=sortedListToBST(head);//左边的作头结点
        return root;
    }
};
```

- 时间：n
- 空间：logn