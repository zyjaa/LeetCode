### 1、DP

- 定义 `f[i]` 表示偷窃第 `i` 个房屋时的最大金额。
- 定义 `g[i]` 表示不偷窃第 `i` 个房屋时的最大金额。

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        if (n == 0) return 0; // 如果没有房屋，返回0
        if (n == 1) return nums[0]; // 如果只有一个房屋，返回它的金额

        vector<int> f(n), g(n); // f和g数组，大小是n

        // 第一种情况：不偷第0个房屋，偷剩下的房屋
        for (int i = 1; i < n; i++) { // i从1到n-1
            f[i] = g[i - 1] + nums[i]; // 偷第i个房屋，金额是nums[i]
            g[i] = max(g[i - 1], f[i - 1]); // 不偷第i个房屋
        }
        int res = max(f[n - 1], g[n - 1]); // 第一种情况的最大值

        // 第二种情况：不偷第n-1个房屋，偷前面的房屋
        f[0] = nums[0]; // 偷第0个房屋，f = nums
        g[0] = INT_MIN; // 不偷第0个房屋，g = INT_MIN（表示不偷）
        for (int i = 1; i < n; i++) { // i从1到n-1
            f[i] = g[i - 1] + nums[i]; // 偷第i个房屋，金额是nums[i]
            g[i] = max(g[i - 1], f[i - 1]); // 不偷第i个房屋
        }
        res = max(res, g[n - 1]); // 取两种情况的最大值

        return res; // 返回结果
    }
};
```

 

房屋是**环形排列**的，也就是说，第一个房屋和最后一个房屋是相邻的。这意味着：

1. 如果你偷了第一个房屋，就不能偷最后一个房屋。
2. 如果你偷了最后一个房屋，就不能偷第一个房屋。

因此，我们需要把问题**拆分成两种情况**，分别计算最大值，最后取两者中的较大值。
