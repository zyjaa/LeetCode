### 1、DP+DFS

DP：第一问倒着拆

DFS：打印所有答案

```cpp 
class Solution {
public:
    vector<string> res; // 存储所有可能的拆分方案
    int n; // 字符串的长度
    unordered_set<string> hash; // 用哈希表存储字典中的单词
    vector<bool> f; // 动态规划数组，f[i] 表示 s[i..n-1] 是否可以被拆分

    vector<string> wordBreak(string s, vector<string>& wordDict) {
        n = s.size();
        // 将字典中的单词存入哈希表
        for (auto x : wordDict) hash.insert(x);

        // 动态规划预处理
        f.resize(n + 1, false); // 初始化动态规划数组
        f[n] = true; // 空字符串可以被拆分
        for (int i = n - 1; ~i; i--) {
            for (int j = i; j < n; j++) {
                // 如果 s[i..j] 在字典中，且 s[j+1..n-1] 可以被拆分，则 s[i..n-1] 可以被拆分
                if (hash.count(s.substr(i, j - i + 1)) && f[j + 1]) {
                    f[i] = true;
                    break; // 找到一个满足条件的分割点即可
                }
            }
        }

        // 回溯法生成所有可能的拆分方案
        dfs(s, 0, "");
        return res;
    }

    void dfs(string& s, int u, string path) {
        if (u == n) {
            // 如果已经遍历完字符串，将当前路径加入结果集
            path.pop_back(); // 去掉末尾多余的空格
            res.push_back(path);
        } else {
            // 尝试从 u 开始的所有可能分割点
            for (int i = u; i < n; i++) {
                // 如果 s[u..i] 在字典中，且 s[i+1..n-1] 可以被拆分，则继续递归
                if (hash.count(s.substr(u, i - u + 1)) && f[i + 1]) {
                    dfs(s, i + 1, path + s.substr(u, i - u + 1) + ' ');
                }
            }
        }
    }
};
```

- 时间：O($$n^2$$)
- 空间：n
