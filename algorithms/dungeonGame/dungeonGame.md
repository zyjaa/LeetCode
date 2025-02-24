### 1、DP

- `f[i][j]` 表示从 `(i, j)` 到终点所需的最小初始生命值。

```cpp
class Solution {
public:
    int calculateMinimumHP(vector<vector<int>>& w) {
        int n = w.size(), m = w.size(); // 获取地图的行数和列数
        vector<vector<int>> f(n, vector<int>(m, 1e8)); // 初始化动态规划数组

        // 从终点开始反向动态规划
        for (int i = n - 1; i >= 0; i--)
            for (int j = m - 1; j >= 0; j--) {
                if (i == n - 1 && j == m - 1) {
                    // 终点：骑士的生命值至少为 1，且需要满足 1 - w[i][j]
                    f[i][j] = max(1, 1 - w[i][j]);// 终点可能是负数
                } else {
                    // 如果可以从下方移动过来
                    if (i < n - 1) f[i][j] = f[i + 1][j] - w[i][j];//从(i,j)移动到(i+1,j)需要加上w[i][j]，反过来自然是减了
                    // 如果可以从右方移动过来，取最小值
                    if (j < m - 1) f[i][j] = min(f[i][j], f[i][j + 1] - w[i][j]);
                    // 骑士的生命值至少为 1
                    f[i][j] = max(1, f[i][j]);
                }
            }
        return f[0][0]; // 返回起点所需的最小生命值
    }
};
```

- 时间：m*n
- 空间：m*n
