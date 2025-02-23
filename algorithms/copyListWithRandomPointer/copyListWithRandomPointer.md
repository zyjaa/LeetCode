###  1、模拟

#### 1. **在原链表中插入新节点**

- 遍历原链表，为每个节点创建一个新节点，并将新节点插入到原节点的后面。
- 例如，原链表为 `A -> B -> C`，插入新节点后变为 `A -> A' -> B -> B' -> C -> C'`。

#### 2. **处理 `random` 指针**

- 遍历原链表，如果原节点的 `random` 指针不为空，则将新节点的 `random` 指针指向原节点 `random` 指针的下一个节点（即对应的新节点）。
- 例如，如果 `A->random = C`，则 `A'->random = C'`。

#### 3. **分离原链表和新链表**

- 创建一个虚拟头节点 `dummy`，用于构建新链表。
- 遍历原链表，将新节点从原链表中分离出来，并连接到新链表中。
- 同时，恢复原链表的 `next` 指针。

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/

class Solution {
public:
    Node* copyRandomList(Node* head) {
        if (!head) return NULL; // 如果链表为空，直接返回空

        // 第一步：在原链表中插入新节点
        for (auto p = head; p; p = p->next->next) {
            auto pl = new Node(p->val); // 创建新节点
            pl->next = p->next; // 新节点的 next 指向原节点的下一个节点
            p->next = pl; // 原节点的 next 指向新节点
        }

        // 第二步：处理 random 指针
        for (auto p = head; p; p = p->next->next) {
            if (p->random) p->next->random = p->random->next; // 新节点的 random 指向原节点 random 的下一个节点
        }

        // 第三步：分离原链表和新链表
        auto dummy = new Node(-1), cur = dummy; // 创建一个虚拟头节点
        for (auto p = head; p; p = p->next) {
            auto t = p->next; // t 是新节点
            p->next = t->next; // 恢复原链表的 next 指针
            cur = cur->next = t; // 将新节点连接到新链表中
        }

        return dummy->next; // 返回新链表的头节点
    }
};
```

n，1
