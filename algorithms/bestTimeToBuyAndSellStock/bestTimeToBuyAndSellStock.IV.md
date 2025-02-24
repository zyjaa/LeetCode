### 1、DP

最多进行k次交易，你必须在再次购买前出售掉之前的股票

- `f[j][0]` 表示最多进行 `j` 次交易且当前**未持有股票**的最大利润。
- `f[j][1]` 表示最多进行 `j` 次交易且当前**持有股票**的最大利润。正在进行第j次交易，没有卖出，卖出才是完整的j次交易，留了个小尾巴

```cpp 
class Solution {
public:
    int f[110][2]; // 动态规划数组
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size(); // 获取股票价格数组的长度
        memset(f, -0x3f, sizeof f); // 初始化动态规划数组为负无穷
        f[0][0] = 0; // 初始状态：未持有股票，利润为 0

        // 动态规划过程
        //在每一天，更新所有可能的交易次数 j 对应的状态。
        for (int i = 0; i < n; i++) {
            for (int j = k; j; j--) {
                // 状态转移方程
                f[j][0] = max(f[j][0], f[j][1] + prices[i]);// 卖出股票（已经进行了j次交易并且现在手上有股票，要把第j次交易完成）
                f[j][1] = max(f[j][1], f[j - 1][0] - prices[i]);// 买入股票
            }
        }

        // 找到最大利润
        int ans = 0;
        for (int i = 0; i <= k; i++) ans = max(ans, f[i][0]);
        return ans;
    }
};
```

- 时间：n*k
- 空间：k
