### 1、区间DP

```
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int maxCoins(vector<int>& nums) {
        int n = nums.size(); // 气球的数量
        vector<int> a(n + 2, 1); // 扩展数组，左右边界为 1
        vector<vector<int>> f(n + 2, vector<int>(n + 2, 0)); // DP 数组

        // 将 nums 复制到 a 中，并在左右边界添加 1
        for (int i = 1; i <= n; i++) {
            a[i] = nums[i - 1];
        }

        // 动态规划求解
        for (int len = 3; len <= n + 2; len++) { // 枚举区间长度
            for (int i = 0; i + len - 1 <= n + 1; i++) { // 枚举区间起点
                int j = i + len - 1; // 区间终点
                for (int k = i + 1; k < j; k++) { // 枚举区间内最后一个戳破的气球
                    f[i][j] = max(f[i][j], f[i][k] + f[k][j] + a[i] * a[k] * a[j]);
                }
            }
        }

        return f[0][n + 1]; // 返回最终结果
    }
};
```

- 当是最后一个被戳破的气球时，它的左边和右边气球分别是：
  - **左边气球**：`i`（因为区间 `(i, k)` 内的气球已经被戳破，`i` 是最近的未戳破气球）。
  - **右边气球**：`j`（因为区间 `(k, j)` 内的气球已经被戳破，`j` 是最近的未戳破气球）。
