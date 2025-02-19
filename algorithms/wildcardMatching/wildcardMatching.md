[44. 通配符匹配](https://leetcode.cn/problems/wildcard-matching/)

- `'?'` 可以匹配任何单个字符。
- `'*'` 可以匹配任意字符序列（包括空字符序列）。

判定匹配成功的充要条件是：字符模式必须能够 **完全匹配** 输入字符串（而不是部分匹配）。

 

**示例 1：**

```
输入：s = "aa", p = "a"
输出：false
解释："a" 无法匹配 "aa" 整个字符串。
```

**示例 2：**

```
输入：s = "aa", p = "*"
输出：true
解释：'*' 可以匹配任意字符串。
```



### 法一：DP

   - **初始化**：
     - `f = true`：空字符串匹配空模式。
     - 处理模式 `p` 的前缀 `*`：如果 `p` 的前 `j` 个字符都是 `*`，则 `f[j] = true`。
   - **状态转移**：
     - 如果 `p[j]` 是普通字符或 `?`：
       - `f[i][j] = (s[i] == p[j] || p[j] == '?') && f[i-1][j-1]`。
     - 如果 `p[j]` 是 `*`：
       - `f[i][j] = f[i][j-1]`（`*` 匹配空字符）。
       - 或 `f[i][j] = f[i-1][j]`（`*` 匹配 `s[i]`）。
   - **最终结果**：
     - `f[n][m]` 表示 `s` 和 `p` 是否完全匹配。



```cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int n = s.size(), m = p.size();
        s = ' ' + s, p = ' ' + p; // 添加哨兵，方便处理边界
        vector<vector<bool>> f(n + 1, vector<bool>(m + 1, false));
        f = true; // 空字符串匹配空模式
        // 处理模式 p 的前缀 *
        for (int j = 1; j <= m; j++) {
            if (p[j] == '*') f[j] = f[j - 1];
        }
        // 动态规划
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (p[j] != '*') {
                    f[i][j] = (s[i] == p[j] || p[j] == '?') && f[i - 1][j - 1];
                } else {
                    f[i][j] = f[i][j - 1] || f[i - 1][j];
                }
            }
        }
        return f[n][m];
    }
};
```

- **时间复杂度**：O(n⋅m)
- **空间复杂度**：O(n⋅m)（可优化为 O(m)，滚动数组）