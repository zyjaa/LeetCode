**23、题意**：合并k个有序链表

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。



**示例 1：**

```
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
```

**示例 2：**

```
输入：lists = []
输出：[]
```



### 法一：优先队列

k个链表先全加入到小根堆，每次找堆顶（最小的）加入到dummy，串一遍

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
    struct cmp{
        bool operator()(ListNode* a,ListNode* b){
            return a->val>b->val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*,vector<ListNode*>,cmp> q;//小根堆
        auto dummy=new ListNode(),tail=dummy;
        for(auto l:lists)
            if(l)q.push(l);
        while(q.size()){
            auto t=q.top();
            q.pop();
            tail=tail->next=t;
            if(t->next)q.push(t->next);
        }
        return dummy->next;
    }
};
```

- 时间：O($$nlogk$$)，n是所有链表节点数量，k是链表数量
- 空间：O($$k$$)，小根堆只存k个元素，最大是k个