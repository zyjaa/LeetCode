### 1、DP

```
class Solution {
public:
    int nthSuperUglyNumber(int n, vector<int>& primes) {
        vector<long> dp(n + 1); // dp[i] 表示第 i 个超级丑数
        int m = primes.size(); // 质数列表的长度
        vector<int> pointers(m, 0); // 指针数组，pointers[j] 表示 primes[j] 在 dp 中的位置
        vector<long> nums(m, 1); // nums[j] 表示 primes[j] 当前生成的候选超级丑数

        for (int i = 1; i <= n; i++) {
            // 找到当前最小的候选超级丑数
            long minNum = INT_MAX;
            for (int j = 0; j < m; j++) {
                minNum = min(minNum, nums[j]);
            }
            dp[i] = minNum; // 将最小的候选超级丑数存入 dp[i]

            // 更新指针和候选超级丑数
            for (int j = 0; j < m; j++) {
                if (nums[j] == minNum) {
                    pointers[j]++; // 移动指针
                    nums[j] = dp[pointers[j]] * primes[j]; // 生成新的候选超级丑数
                }
            }
        }

        return dp[n]; // 返回第 n 个超级丑数
    }
};
```

