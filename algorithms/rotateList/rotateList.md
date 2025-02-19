[61. 旋转链表](https://leetcode.cn/problems/rotate-list/)

给你一个链表的头节点 `head` ，旋转链表，将链表每个节点向右移动 `k` 个位置。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg)

```
输入：head = [1,2,3,4,5], k = 2
输出：[4,5,1,2,3]
```



### 1、模拟

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
class Solution {
public:
    ListNode* rotateRight(ListNode* head, int k) {
        if(!head)return nullptr;
        ListNode* tail;
        int n=0;
        for(auto p=head;p;p=p->next){
            n++;
            tail=p;
        }
        k%=n;
        ListNode* p=head;
        for(int i=0;i<n-k-1;i++){
            p=p->next;
        }
        tail->next=head;
        head=p->next;
        p->next=nullptr;
        return head;
    }
};
```

- 时间：O(n)
- 空间：O(1)