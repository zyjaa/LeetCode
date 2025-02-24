O(log n)

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;

        // 二分查找峰值元素
        while (l < r) {
            int m = l + r >> 1; // 计算中间位置
            if (nums[m] > nums[m + 1]) r = m; // 如果 nums[m] > nums[m+1]，说明峰值在左半部分
            else l = m + 1; // 否则，峰值在右半部分
        }

        // 返回峰值元素的下标
        return r;
    }
};
```

