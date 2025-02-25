### 1、Trie+DFS

```
class Solution {
public:
    // 定义字典树的节点结构
    struct Node {
        int id; // 记录单词的索引
        Node* son; // 26个子节点，对应a-z
        Node() { // 构造函数
            id = -1; // 默认没有单词
            for (int i = 0; i < 26; i++) son[i] = NULL; // 初始化子节点为空
        }
    } *root; // 根节点

    vector<vector<char>> g; // 存储字符矩阵
    unordered_set<int> ids; // 存储找到的单词索引
    int dx = {0, 1, 0, -1}, dy = {1, 0, -1, 0}; // 四个方向
    int m, n; // 矩阵的行数和列数

    // 插入单词到字典树
    void insert(string& word, int i) {
        auto p = root; // 从根节点开始
        for (auto c : word) { // 遍历单词的每个字符
            int u = c - 'a'; // 计算字符对应的索引（a=0, b=1, ..., z=25）
            if (!p->son[u]) p->son[u] = new Node(); // 如果子节点不存在，创建它
            p = p->son[u]; // 移动到子节点
        }
        p->id = i; // 记录单词的索引
    }

    // 主函数
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        root = new Node(); // 初始化字典树
        g = board; // 存储字符矩阵
        m = board.size(), n = board.size(); // 获取矩阵的行数和列数
        for (int i = 0; i < words.size(); i++) insert(words[i], i); // 插入所有单词
        for (int i = 0; i < m; i++) { // 遍历矩阵的每一行
            for (int j = 0; j < n; j++) { // 遍历矩阵的每一列
                int u = board[i][j] - 'a'; // 计算当前字符的索引
                if (root->son[u]) dfs(root->son[u], i, j); // 如果字典树中有匹配的字符，开始DFS
            }
        }
        vector<string> res; // 存储结果
        for (auto id : ids) res.push_back(words[id]); // 把找到的单词加入结果
        return res; // 返回结果
    }

    // DFS搜索
    void dfs(Node* p, int x, int y) {
        if (p->id != -1) ids.insert(p->id); // 如果当前节点是单词结尾，记录单词索引
        char t = g[x][y]; // 保存当前字符
        g[x][y] = '.'; // 标记当前字符为已访问
        for (int i = 0; i < 4; i++) { // 遍历四个方向
            int a = x + dx[i], b = y + dy[i]; // 计算下一个位置
            if (a >= 0 && a < m && b >= 0 && b < n && g[a][b] != '.') { // 如果位置合法且未访问
                int u = g[a][b] - 'a'; // 计算字符的索引
                if (p->son[u]) dfs(p->son[u], a, b); // 如果字典树中有匹配的字符，继续DFS
            }
        }
        g[x][y] = t; // 恢复当前字符
    }
};
```

 时间复杂度：

1. **建树**：O(L)，其中 L 是所有单词的总长度。
2. **DFS**：O(m × n × 4^L)，其中 m 和 n 是矩阵的行数和列数，L 是单词的最大长度。
