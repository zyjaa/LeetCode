[126. 单词接龙 II](https://leetcode.cn/problems/word-ladder-ii/) 

### 1、DFS+BFS

1. **BFS**：计算每个单词到 `beginWord` 的最短距离。
2. **DFS**：根据 BFS 的结果，回溯所有最短路径。

```cpp
class Solution {
public:
    unordered_set<string> hash; // 存储 wordList 中的单词
    unordered_map<string, int> dist; // 存储每个单词到 beginWord 的最短距离
    vector<vector<string>> ans; // 存储所有最短路径
    vector<string> path; // 存储当前路径
    string beginWord; // 起始单词

    vector<vector<string>> findLadders(string _beginWord, string endWord, vector<string>& wordList) {
        beginWord = _beginWord;
        hash = unordered_set<string>(wordList.begin(), wordList.end()); // 初始化哈希表
        if (!hash.count(endWord)) return ans; // 如果 endWord 不在 wordList 中，直接返回空结果

        bfs(); // BFS 计算最短距离
        if (dist.count(endWord) == 0) return ans; // 如果无法到达 endWord，返回空结果

        path.push_back(endWord); // 从 endWord 开始回溯
        dfs(endWord); // DFS 查找所有最短路径
        return ans;
    }

    void bfs() {
        queue<string> q;
        q.push(beginWord);
        dist[beginWord] = 0; // 初始化距离

        while (!q.empty()) {
            string t = q.front();
            q.pop();

            // 尝试修改每一个字符
            for (int i = 0; i < t.size(); i++) {
                char originalChar = t[i]; // 保存原始字符
                for (char j = 'a'; j <= 'z'; j++) {
                    if (j == originalChar) continue; // 跳过原始字符
                    t[i] = j;
                    if (hash.count(t) && dist.count(t) == 0) { // 如果新单词合法且未被访问过
                        dist[t] = dist[t] + 1; // 更新距离
                        q.push(t); // 将新单词加入队列
                    }
                }
                t[i] = originalChar; // 恢复原始字符
            }
        }
    }

    void dfs(string t) {
        if (t == beginWord) { // 如果回溯到 beginWord，将路径加入结果集
            reverse(path.begin(), path.end());
            ans.push_back(path);
            reverse(path.begin(), path.end());
        } else {
            string r = t;
            for (int i = 0; i < t.size(); i++) {
                t = r;
                for (char j = 'a'; j <= 'z'; j++) {
                    t[i] = j;
                    if (dist.count(t) && dist[t] + 1 == dist[r]) { // 如果 t 是 r 的前驱节点
                        path.push_back(t); // 将 t 加入路径
                        dfs(t); // 继续回溯
                        path.pop_back(); // 回溯
                    }
                }
            }
        }
    }
};
```

1. **时间复杂度**：
   - BFS 的时间复杂度为 O(N×L)，其中 N是单词列表的长度，L是单词的长度。
   - DFS 的时间复杂度为 O(K×M)，其中 K 是最短路径的数量，M是路径的平均长度。
   - 总时间复杂度为 O(N×L+K×M)。
2. **空间复杂度**：
   - 哈希表 `hash` 和距离表 `dist` 的空间复杂度为 O(N)
   - DFS 的递归栈空间复杂度为 O(M)
   - 总空间复杂度为 O(N+M)
