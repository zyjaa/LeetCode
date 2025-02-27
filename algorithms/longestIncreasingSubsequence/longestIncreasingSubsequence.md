```
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> q;  // 用于存储当前的最长递增子序列

        for (auto x : nums) {
            if (q.empty() || x > q.back()) {
                // 如果 x 大于 q 的最后一个元素，直接添加到 q 中
                q.push_back(x);
            } else {
                if (x <= q) {
                    // 如果 x 小于等于 q 的第一个元素，更新 q
                    q = x;
                } else {
                    // 否则，使用二分查找找到第一个大于等于 x 的位置
                    int l = 0, r = q.size() - 1;
                    while (l < r) {
                        int mid = l + r + 1 >> 1;
                        if (q[mid] < x) {
                            l = mid;
                        } else {
                            r = mid - 1;
                        }
                    }
                    // 更新 q[r + 1] 为 x
                    q[r + 1] = x;
                }
            }
        }

        // 返回 q 的长度，即为最长递增子序列的长度
        return q.size();
    }
};
```

nlogn
