题意：2个用链表表示的数从前向后相加



**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
```

**Example 2:**

```
Input: l1 = [0], l2 = [0]
Output: [0]
```

**Example 3:**

```
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto dummy=new ListNode(),cur=dummy;
        int t=0;
        while(l1 || l2 || t){
            if(l1)t+=l1->val,l1=l1->next;
            if(l2)t+=l2->val,l2=l2->next;
            cur=cur->next=new ListNode(t%10);
            t/=10;
        }
        return dummy->next;
    }
};
```



- 时间复杂度：O(max{m,n})，m,n分别为2个链表长度，只循环较长链表次（注意不是m+n，总执行次数是m+n，但每次执行2次时间复杂度是O(1),while循环执行max{m,n}次）
- 空间复杂的：O(max(n, m)+1)，多了个虚拟头结点



