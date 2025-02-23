### 1、快慢指针

判断链表中是否有环

```cpp 
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head || !head->next)return false;
        auto l=head,f=head->next;
        while(f){
            l=l->next,f=f->next;
            if(!f)return false;
            f=f->next;
            if(l==f)return true;
        }
        return false;
    }
};
```

n，1

快慢指针最多转2圈就相遇
