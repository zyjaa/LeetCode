[92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```
输入：head = [1,2,3,4,5], left = 2, right = 4
输出：[1,4,3,2,5]
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
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        auto dummy=new ListNode();
        dummy->next=head;
        auto a=dummy;
        for(int i=0;i<left-1;i++)a=a->next;
        auto b=a->next,c=b->next;
        for(int i=0;i<right-left;i++){
            auto t=c->next;
            c->next=b;
            b=c,c=t;
        }
        a->next->next=c;
        a->next=b;
        return dummy->next;
    }
};
```

- 时间：n
- 空间：1