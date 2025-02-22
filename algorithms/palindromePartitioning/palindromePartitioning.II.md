###  1、DP

为什么最后-1？因为前面加了个空格，题目又要求分割为子串，不分割肯定是0了，举个例子

"a"：0，不需要分割，也割不了

"_a"：f[n-1]=1，割了一次（f[1]=min(f[1],f[0]+1)=1)，但实际上不需要割，所以-1

```cpp
class Solution {
public:
    int minCut(string s) {
        s = ' ' + s; // 使下标从 1 开始
        int n = s.size();
        vector<vector<bool>> g(n, vector<bool>(n, false)); // g[i][j] 表示 s[i..j] 是否是回文串
        vector<int> f(n, 1e8); // f[i] 表示将 s[1..i] 分割成回文子串的最小切割次数
        f = 0; // 空字符串不需要切割

        preprocess(g, s); // 动态规划预处理回文串
        calculateMinCuts(f, g, s); // 动态规划求解最小切割次数

        return f[n - 1] - 1; // 返回结果
    }

    void preprocess(vector<vector<bool>>& g, const string& s) {
        int n = s.size();
        for (int j = 1; j < n; j++) {
            for (int i = 1; i <= j; i++) {
                if (i == j) g[i][j] = true; // 单个字符是回文串
                else if (s[i] == s[j]) {
                    if (i + 1 > j - 1 || g[i + 1][j - 1]) { // 两端字符相同，且中间部分是回文串
                        g[i][j] = true;
                    }
                }
            }
        }
    }

    void calculateMinCuts(vector<int>& f, const vector<vector<bool>>& g, const string& s) {
        int n = s.size();
        for (int i = 1; i < n; i++) {
            for (int j = 1; j <= i; j++) {
                if (g[j][i]) { // 如果 s[j..i] 是回文串
                    f[i] = min(f[i], f[j - 1] + 1); // 更新最小切割次数
                }
            }
        }
    }
};
```

- 时间：n^2
- 空间：n^2
