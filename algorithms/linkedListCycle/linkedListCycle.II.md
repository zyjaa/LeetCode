### 1、快慢指针

找入环点

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
    ListNode *detectCycle(ListNode *head) {
        if(!head)return NULL;
        auto slow=head,fast=head;
        while(fast){
            slow=slow->next,fast=fast->next;
            if(!fast)return NULL;
            fast=fast->next;
            if(slow==fast){
                slow=head;
                while(slow!=fast){//入环点，可以数学证明
                    slow=slow->next,fast=fast->next;
                }
                return fast;
            }
        }
        return NULL;
    }
};
```

n,1

