### 1、Trie

```
class WordDictionary {
public:
    // 定义字典树的节点结构
    struct Node {
        bool is_end; // 是否是单词的结尾
        Node* son; // 26个子节点，对应a-z
        Node() { // 构造函数
            for (int i = 0; i < 26; i++) son[i] = NULL; // 初始化子节点为空
            is_end = false; // 默认不是单词的结尾
        }
    } *root; // 根节点

    // 构造函数
    WordDictionary() {
        root = new Node(); // 初始化根节点
    }

    // 插入单词
    void addWord(string word) {
        auto p = root; // 从根节点开始
        for (auto x : word) { // 遍历单词的每个字符
            int t = x - 'a'; // 计算字符对应的索引（a=0, b=1, ..., z=25）
            if (!p->son[t]) p->son[t] = new Node(); // 如果子节点不存在，创建它
            p = p->son[t]; // 移动到子节点
        }
        p->is_end = true; // 标记单词的结尾
    }

    // 查找单词
    bool search(string word) {
        return dfs(root, word, 0); // 从根节点开始递归搜索
    }

    // 递归实现模糊搜索
    bool dfs(Node* p, string& word, int u) {
        if (u == word.size()) return p->is_end; // 如果遍历完单词，返回是否是单词结尾
        if (word[u] != '.') { // 如果当前字符不是通配符
            int t = word[u] - 'a'; // 计算字符对应的索引
            if (!p->son[t]) return false; // 如果子节点不存在，返回false
            return dfs(p->son[t], word, u + 1); // 递归搜索下一个字符
        } else { // 如果当前字符是通配符
            for (int i = 0; i < 26; i++) // 遍历所有可能的子节点
                if (p->son[i] && dfs(p->son[i], word, u + 1)) return true; // 递归搜索
            return false; // 如果没有匹配的，返回false
        }
    }
};
```

1. **插入单词**：O(L)，其中 `L` 是单词的长度。
2. 查找单词：
   - 如果没有 `.`，时间复杂度是 O(L)。
   - 如果有 `.`，最坏情况下需要遍历所有可能的路径，时间复杂度是 O(26^L)。
