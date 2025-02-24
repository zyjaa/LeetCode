###  1、链表模拟

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
    ListNode* insertionSortList(ListNode* head) {
        // 创建一个虚拟头节点，方便在链表头部插入节点
        auto dummy = new ListNode();
        
        // 遍历原始链表
        for (auto p = head; p;) {
            // 保存当前节点的下一个节点
            auto next = p->next;
            
            // 从虚拟头节点开始，找到插入位置
            auto cur = dummy;
            while (cur->next && cur->next->val <= p->val) {
                cur = cur->next;
            }
            
            // 将当前节点插入到正确的位置
            p->next = cur->next;
            cur->next = p;
            
            // 移动到下一个节点
            p = next;
        }
        
        // 返回排序后的链表头节点
        return dummy->next;
    }
};
```

n,1
