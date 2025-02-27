```
class Solution {
public:
    int hIndex(vector<int>& citations) {
        // 初始化二分查找的左右边界
        int l = 0, r = citations.size();
        int n = citations.size();

        // 二分查找
        while (l < r) {
            int m = l + r + 1 >> 1;  // 计算中间值
            if (citations[n - m] >= m) {  // 检查是否满足 H 指数的条件
                l = m;  // 如果满足，尝试更大的 h
            } else {
                r = m - 1;  // 否则，尝试更小的 h
            }
        }

        // 返回 H 指数
        return r;
    }
};
```

