 [127. 单词接龙](https://leetcode.cn/problems/word-ladder/)



### 1、BFS

```cpp
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> S(wordList.begin(), wordList.end()); // 将 wordList 存入哈希表
        if (!S.count(endWord)) return 0; // 如果 endWord 不在 wordList 中，直接返回 0

        queue<string> q;
        unordered_map<string, int> dist; // 存储每个单词到 beginWord 的最短距离
        q.push(beginWord);
        dist[beginWord] = 1; // 序列长度从 1 开始

        while (!q.empty()) {
            string t = q.front();
            q.pop();

            // 尝试修改每一个字符
            for (int i = 0; i < t.size(); i++) {
                char originalChar = t[i]; // 保存原始字符
                for (char j = 'a'; j <= 'z'; j++) {
                    if (j == originalChar) continue; // 跳过原始字符
                    t[i] = j;
                    if (S.count(t) && !dist.count(t)) { // 如果新单词合法且未被访问过
                        dist[t] = dist[t] + 1; // 更新距离
                        if (t == endWord) return dist[t]; // 如果找到 endWord，返回结果
                        q.push(t); // 将新单词加入队列
                    }
                }
                t[i] = originalChar; // 恢复原始字符
            }
        }

        return 0; // 未找到 endWord
    }
};
```

- 时间：n*L，L是单词列表wordList长度
- 空间：n
