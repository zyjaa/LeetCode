[83. 删除排序链表中的重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)

```
输入：head = [1,1,2]
输出：[1,2]
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
        if(!head)return nullptr;
        auto cur=head;
        for(auto p=head->next;p;p=p->next){//只需要判断当前数和后面的数值是否相等
            if(cur->val != p->val)cur=cur->next=p;
        }
        cur->next=nullptr;
        return head;
    }
};
```

- 时间：n
- 空间：1
  - 小总结： p->next = new ListNode(curr->val); // 动态分配新节点，除了这种new的基本链表空间复杂度基本都是1