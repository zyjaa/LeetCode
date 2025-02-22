[131. 分割回文串](https://leetcode.cn/problems/palindrome-partitioning/)

- `f[i][j]` 表示字符串 `s` 的子串 `s[i..j]` 是否是回文串。

```CPP
class Solution {
public:
    vector<vector<bool>> f; // f[i][j] 表示 s[i..j] 是否是回文串
    vector<string> path; // 当前分割方案
    vector<vector<string>> res; // 所有分割方案

    vector<vector<string>> partition(string s) {
        int n = s.size();
        f = vector<vector<bool>>(n, vector<bool>(n, false)); // 初始化 f

        preprocess(s); // 动态规划预处理
        dfs(s, 0); // DFS 回溯
        return res;
    }

    void preprocess(const string& s) {
        int n = s.size();
        for (int j = 0; j < n; j++) {
            for (int i = 0; i <= j; i++) {
                if (i == j) f[i][j] = true; // 单个字符是回文串
                else if (s[i] == s[j]) {
                    if (i + 1 > j - 1 || f[i + 1][j - 1]) { // 两端字符相同，且中间部分是回文串
                        f[i][j] = true;
                    }
                }
            }
        }
    }

    void dfs(const string& s, int u) {
        if (u == s.size()) { // 如果分割到字符串末尾，将当前方案加入结果集
            res.push_back(path);
            return;
        }
        for (int i = u; i < s.size(); i++) {
            if (f[u][i]) { // 如果 s[u..i] 是回文串
                path.push_back(s.substr(u, i - u + 1)); // 将该子串加入当前方案
                dfs(s, i + 1); // 递归处理剩余部分
                path.pop_back(); // 回溯
            }
        }
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n^2$$)
