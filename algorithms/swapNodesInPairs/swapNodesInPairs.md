**24、题意**：两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

题目要求不要耍小聪明，把值换一下，那没有考的必要了



**示例 1**：

![img](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

**示例 2：**

```
输入：head = []
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
    ListNode* swapPairs(ListNode* head) {
        auto dummy=new ListNode();
        dummy->next=head;
        //p->next p->next->next：保证至少2个节点存在
        for(auto p=dummy;p->next && p->next->next;){
            auto a=p->next,b=p->next->next;
            p->next=b;
            a->next=b->next;
            b->next=a;
            p=a;
        }
        return dummy->next;
    }
};
```

- 时间：O($$n$$)
- 空间：O($$1$$)