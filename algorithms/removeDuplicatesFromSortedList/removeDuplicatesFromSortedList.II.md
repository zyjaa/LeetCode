[82. 删除排序链表中的重复元素 II](https://leetcode.cn/problems/remove-duplicates-from-sorted-list-ii/)

给定一个已排序的链表的头 `head` ， *删除原始链表中所有重复数字的节点，只留下不同的数字* 。返回 *已排序的链表* 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```
输入：head = [1,2,3,3,4,4,5]
输出：[1,2,5]
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
    ListNode* deleteDuplicates(ListNode* head) {
        auto dummy=new ListNode();
        dummy->next=head;
        auto p=dummy;
        while(p->next){
            auto t=p->next->next;
            while(t && t->val==p->next->val)t=t->next;//预知下两个节点
            if(t==p->next->next)p=p->next;// 没有重复，p向下走
            else p->next=t;
        }
        return dummy->next;
    }
};
```

- 时间：n
- 空间：1，没有new就是几个指针