 [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。



### 1、模拟

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int res=0;
        int minn=prices[0];
        for(int i=1;i<prices.size();i++){
            minn=min(minn,prices[i]);
            res=max(res,prices[i]-minn);
        }
        return res;
    }
};
```

- 时间：n
- 空间：1
