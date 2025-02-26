```
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next) return true;

        // 找到链表的中间节点
        ListNode* slow = head;
        ListNode* fast = head;
        while (fast->next && fast->next->next) {
            slow = slow->next;
            fast = fast->next->next;
        }

        // 反转后半部分链表
        ListNode* prev = nullptr;
        ListNode* curr = slow->next;
        while (curr) {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }

        // 比较前半部分和反转后的后半部分
        ListNode* p = head;
        ListNode* q = prev;
        bool isPalin = true;
        while (q) {
            if (p->val != q->val) {
                isPalin = false;
                break;
            }
            p = p->next;
            q = q->next;
        }

        // 恢复链表结构
        curr = prev;
        prev = nullptr;
        while (curr) {
            ListNode* next = curr->next;
            curr->next = prev;
            prev = curr;
            curr = next;
        }
        slow->next = prev;

        return isPalin;
    }
};
```

