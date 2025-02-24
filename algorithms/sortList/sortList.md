`O(n log n)` 时间复杂度和常数级空间复杂度 

这个代码量挺大的，对coding和排序链表的迭代写法有要求

```cpp
class Solution {
public:
    ListNode* sortList(ListNode* head) {
        // 创建一个虚拟头节点，方便操作
        auto dummy = new ListNode(-1);
        dummy->next = head;

        // 计算链表的长度
        int n = 0;
        for (auto p = head; p; p = p->next) n++;

        // 外层循环：归并的步长从1开始，每次翻倍
        for (int i = 1; i < n; i *= 2) {
            auto cur = dummy; // cur用于连接合并后的链表
            // 内层循环：将链表分成大小为i的若干段，两两合并
            for (int j = 1; j + i <= n; j += i * 2) {
                auto p = cur->next, q = p; // p和q分别指向两段链表的起点
                // 将q移动到第二段的起点
                for (int k = 0; k < i; k++) q = q->next;

                int l = 0, r = 0; // l和r分别记录两段链表的合并进度
                // 合并两段链表
                while (l < i && r < i && p && q) {
                    if (p->val <= q->val) {
                        cur->next = p;
                        p = p->next;
                        l++;
                    } else {
                        cur->next = q;
                        q = q->next;
                        r++;
                    }
                    cur = cur->next;
                }
                // 处理剩余未合并的节点
                while (l < i && p) {
                    cur->next = p;
                    p = p->next;
                    l++;
                    cur = cur->next;
                }
                while (r < i && q) {
                    cur->next = q;
                    q = q->next;
                    r++;
                    cur = cur->next;
                }
                // 将cur连接到下一段的起点
                cur->next = q;
            }
        }
        // 返回排序后的链表头节点
        return dummy->next;
    }
};
```

