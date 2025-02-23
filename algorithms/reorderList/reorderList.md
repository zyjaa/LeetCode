### 1、模拟

首尾转圈是吧，跟蛇形矩阵一样

- 如果链表长度为奇数，`mid` 是中间节点；如果长度为偶数，`mid` 是前半部分的最后一个节点。

```cpp 
class Solution {
public:
    void reorderList(ListNode* head) {
        if (!head) return; // 链表为空，直接返回

        // 1. 计算链表长度
        int n = 0;
        for (auto p = head; p; p = p->next) n++;

        // 2. 找到链表的中点
        auto mid = head;
        for (int i = 0; i < (n + 1) / 2 - 1; i++) mid = mid->next;

        // 3. 反转链表的后半部分
        auto a = mid, b = mid->next;
        while (b) {
            auto next = b->next;
            b->next = a;
            a = b;
            b = next;
        }

        // 4. 重排链表
        auto p = head;
        for (int i = 0; i < n / 2; i++) {
            auto anext = a->next;
            auto pnext = p->next;
            a->next = p->next;
            p->next = a;
            a = anext;
            p = pnext;
        }

        // 5. 处理链表的末尾
        if (n % 2) mid->next = NULL; // 链表长度为奇数
        else mid->next->next = NULL; // 链表长度为偶数
    }
};
```

n,1
