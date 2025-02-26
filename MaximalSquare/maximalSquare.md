### 1、DP

```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int n = matrix.size(), m = matrix.size(); // 获取矩阵的行数和列数
        vector<vector<int>> f(n + 1, vector<int>(m + 1)); // 动态规划数组
        int res = 0; // 记录最大正方形的边长

        // 遍历矩阵
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (matrix[i - 1][j - 1] == '1') { // 如果当前元素是 '1'
                    // 更新 f[i][j]，取左方、上方和左上方的最小值加 1
                    f[i][j] = min(f[i - 1][j - 1], min(f[i - 1][j], f[i][j - 1])) + 1;
                    // 更新最大边长
                    res = max(res, f[i][j]);
                }
            }
        }

        // 返回最大正方形的面积
        return res * res;
    }
};
```







```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int n = matrix.size(), m = matrix.size();
        vector<vector<int>> f(n, vector<int>(m, 0)); // 动态规划数组，下标从 0 开始
        int res = 0; // 记录最大正方形的边长

        // 遍历矩阵
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == '1') { // 如果当前元素是 '1'
                    if (i == 0 || j == 0) {
                        // 第一行或第一列，最大边长只能是 1
                        f[i][j] = 1;
                    } else {
                        // 更新 f[i][j]，取左方、上方和左上方的最小值加 1
                        f[i][j] = min(f[i - 1][j - 1], min(f[i - 1][j], f[i][j - 1])) + 1;
                    }
                    // 更新最大边长
                    res = max(res, f[i][j]);
                }
            }
        }

        // 返回最大正方形的面积
        return res * res;
    }
};
```

- 时间：n*m
- 空间：n*m





空间优化

```cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int n = matrix.size(), m = matrix.size();
        vector<int> prev(m, 0); // 上一行的状态
        vector<int> curr(m, 0); // 当前行的状态
        int res = 0;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (matrix[i][j] == '1') {
                    if (i == 0 || j == 0) {
                        curr[j] = 1; // 第一行或第一列，最大边长只能是 1
                    } else {
                        curr[j] = min(prev[j - 1], min(prev[j], curr[j - 1])) + 1;
                    }
                    res = max(res, curr[j]);
                } else {
                    curr[j] = 0; // 如果当前元素是 '0'，则边长为 0
                }
            }
            prev = curr; // 更新上一行状态
            fill(curr.begin(), curr.end(), 0); // 重置当前行
        }

        return res * res;
    }
};
```

