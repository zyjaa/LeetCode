题意：完成图的深拷贝



### 1、DFS

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    unordered_map<Node*, Node*> hash; // 哈希表，用于存储原节点和克隆节点的映射
    Node* cloneGraph(Node* node) {
        if (!node) return NULL; // 如果输入节点为空，直接返回空
        dfs(node); // 深度优先搜索，克隆所有节点
        for (auto [s, d] : hash) // 遍历哈希表
            for (auto ver : s->neighbors) // 遍历原节点的邻居
                d->neighbors.push_back(hash[ver]); // 将克隆节点的邻居指向克隆后的邻居
        return hash[node]; // 返回克隆图的起始节点
    }
    void dfs(Node* node) {
        hash[node] = new Node(node->val); // 创建新节点，并存储到哈希表中
        for (auto ver : node->neighbors) // 遍历当前节点的邻居
            if (hash.count(ver) == 0) dfs(ver); // 如果邻居未被克隆，递归克隆
    }
};
```

- 时间：n+m，所有点和边都遍历一次
- 空间：n，哈希表+递归栈空间
