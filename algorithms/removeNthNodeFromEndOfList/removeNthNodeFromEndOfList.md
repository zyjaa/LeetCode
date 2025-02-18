**19、题意**

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```





### 法一：链表模拟

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        auto dummy=new ListNode();
        dummy->next=head;
        int k=0;
        for(auto p=head;p;p=p->next)k++;

        auto p=dummy;
        for(int i=0;i<k-n;i++){
            p=p->next;
        }
        p->next=p->next->next;
        return dummy->next;
    }
};
```

- 时间复杂度：O(L)，L是链表长度
- 空间复杂度：O(1)