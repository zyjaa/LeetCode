**25、题意**：K 个一组翻转链表



**示例 1**：

![img](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

```
输入：head = [1,2,3,4,5], k = 2
输出：[2,1,4,3,5]
```

**示例 2**：

![img](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

```
输入：head = [1,2,3,4,5], k = 3
输出：[3,2,1,4,5]
```





### 法一：模拟（分组）

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
    ListNode* reverseKGroup(ListNode* head, int k) {
        auto dummy=new ListNode();
        dummy->next=head;
        for(auto p=dummy;;){
            auto q=p;
            // 满足k个
            for(int i=0;i<k && q;i++)q=q->next;
            if(!q)break;
            // k个节点反转
            auto a=p->next,b=a->next;
            for(int i=0;i<k-1;i++){
                auto c=b->next;
                b->next=a;
                a=b,b=c;
            }
            //反转后的尾指针指向b(下一组开头)
            auto c=p->next;
            c->next=b;
            p->next=a;//模拟下
            p=c;//下一组的前一个，p是一组开头的前一个
        }
        return dummy->next;
    }
};
```

- 时间：O($$n$$)，n是链表长度
- 空间：O($$1$$)，用了常数个额外指针变量