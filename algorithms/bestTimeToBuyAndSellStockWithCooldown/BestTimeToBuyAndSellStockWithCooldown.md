### 1、DP

```
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        if (n == 0) return 0;

        // 初始化状态
        int noStockPrev = 0;          // 前一天不持有股票的最大利润
        int withStockPrev = INT_MIN;  // 前一天持有股票的最大利润
        int noStockPrev2 = 0;         // 前两天不持有股票的最大利润（用于冷冻期）

        for (int i = 0; i < n; i++) {
            // 当前不持有股票的最大利润
            int noStock = max(noStockPrev, withStockPrev + prices[i]);
            // 当前持有股票的最大利润
            int withStock = max(withStockPrev, noStockPrev2 - prices[i]);
            // 更新前两天的状态
            noStockPrev2 = noStockPrev;
            noStockPrev = noStock;
            withStockPrev = withStock;
        }

        return noStockPrev;
    }
};
```

