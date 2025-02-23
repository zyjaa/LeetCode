### 1、链表

最近最少使用的淘汰

```cpp
class LRUCache {
public:
    struct Node {
        int key, val;
        Node *left, *right;
        Node(int _key, int _val): key(_key), val(_val), left(NULL), right(NULL) {}
    } *L, *R;
    int n; // 缓存容量
    unordered_map<int, Node*> hash; // 哈希表，存储键到节点的映射

    // 移除节点
    void remove(Node* p) {
        p->right->left = p->left;
        p->left->right = p->right;
    }

    // 插入节点到链表头部
    void insert(Node* p) {
        p->right = L->right;
        L->right->left = p;
        p->left = L;
        L->right = p;
    }

    // 构造函数
    LRUCache(int capacity) {
        n = capacity;
        L = new Node(-1, -1), R = new Node(-1, -1);
        L->right = R;
        R->left = L;
    }

    // 获取键对应的值
    int get(int key) {
        if (!hash.count(key)) return -1; // 键不存在
        auto p = hash[key];
        remove(p); // 移除节点
        insert(p); // 插入到链表头部
        return p->val;
    }

    // 插入或更新键值对
    void put(int key, int value) {
        if (hash.count(key)) { // 键已存在
            auto p = hash[key];
            p->val = value; // 更新值
            remove(p); // 移除节点
            insert(p); // 插入到链表头部
        } else { // 键不存在
            if (hash.size() == n) { // 缓存已满
                auto p = R->left; // 找到链表尾部的节点
                remove(p); // 移除节点
                hash.erase(p->key); // 从哈希表中删除
                delete p; // 释放内存
            }
            auto p = new Node(key, value); // 创建新节点
            hash[key] = p; // 添加到哈希表
            insert(p); // 插入到链表头部
        }
    }
};
```

- **时间复杂度**：`get` 和 `put` 均为 **O(1)**。
- **空间复杂度**：**O(N)**，其中 `N` 是缓存容量。



