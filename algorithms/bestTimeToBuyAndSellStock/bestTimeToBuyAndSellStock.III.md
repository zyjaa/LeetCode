 [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)

给定一个数组，它的第 `i` 个元素是一支给定的股票在第 `i` 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 **两笔** 交易。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

**示例 1:**

```
输入：prices = [3,3,5,0,0,3,1,4]
输出：6
解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```



### 1、DP

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<int> f(n + 2); // 用于存储前i天的最大利润
        // 第一遍遍历：计算前i天的最大利润
        for (int i = 1, minp = INT_MAX; i <= n; i++) {
            f[i] = max(f[i - 1], prices[i - 1] - minp); // 更新前i天的最大利润
            minp = min(minp, prices[i - 1]); // 更新前i天的最低价格
        }
        int res = 0; // 最终结果
        // 第二遍遍历：计算后i天的最大利润，并与前i天的利润结合
        for (int i = n, maxp = 0; i >= 1; i--) {
            res = max(res, f[i - 1] + maxp - prices[i - 1]); // 更新最大利润
            maxp = max(maxp, prices[i - 1]); // 更新后i天的最高价格
        }
        return res; // 返回最终结果
    }
};
```

- n
- n



下标从0更直观，从1开始主要防止f溢出

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n == 0) return 0; // 处理空数组的情况
        vector<int> f(n); // f[i] 表示前 i+1 天的最大利润
        // 第一遍遍历：计算前 i+1 天的最大利润
        for (int i = 0, minp = prices; i < n; i++) {
            if (i == 0) {
                f[i] = 0; // 前 1 天的最大利润为 0
            } else {
                f[i] = max(f[i - 1], prices[i] - minp); // 更新前 i+1 天的最大利润
            }
            minp = min(minp, prices[i]); // 更新前 i+1 天的最低价格
        }
        int res = 0; // 最终结果
        // 第二遍遍历：计算后 i+1 天的最大利润，并与前 i 天的利润结合
        for (int i = n - 1, maxp = prices[n - 1]; i >= 0; i--) {
            if (i == 0) {
                res = max(res, maxp - prices[i]); // 只进行一次交易的情况
            } else {
                res = max(res, f[i - 1] + maxp - prices[i]); // 更新最大利润
            }
            maxp = max(maxp, prices[i]); // 更新后 i+1 天的最高价格
        }
        return res; // 返回最终结果
    }
};
```

