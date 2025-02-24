### 1、基数排序

n,n

```cpp 
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        // 找到数组中的最小值和最大值
        auto [m, M] = ranges::minmax(nums);

        // 如果最大值和最小值的差值小于等于1，直接返回差值
        if (M - m <= 1) {
            return M - m;
        }

        int n = nums.size();
        // 计算桶的大小 d，至少为 (M - m) / (n - 1)
        int d = (M - m + n - 2) / (n - 1);

        // 初始化桶，每个桶存储一个区间内的最小值和最大值
        vector<pair<int, int>> buckets((M - m) / d + 1, {INT_MAX, INT_MIN});

        // 将元素分配到桶中
        for (int x : nums) {
            auto& [mn, mx] = buckets[(x - m) / d]; // 找到对应的桶
            mn = min(mn, x); // 更新桶内的最小值
            mx = max(mx, x); // 更新桶内的最大值
        }

        // 计算最大间距
        int ans = 0;
        int pre_max = INT_MAX;
        for (auto [mn, mx] : buckets) {
            if (mn != INT_MAX) { // 如果桶非空
                ans = max(ans, mn - pre_max); // 计算当前桶的最小值与上一个非空桶的最大值的差值
                pre_max = mx; // 更新上一个非空桶的最大值
            }
        }
        return ans;
    }
};
```

