### 1、二分

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;

        // 如果数组没有旋转，直接返回第一个元素
        if (nums[l] < nums[r]) return nums[l];

        // 二分查找旋转点
        while (l < r) {
            int m = l + r >> 1; // 计算中间位置
            if (nums[m] < nums[0]) r = m; // 如果 nums[m] < nums[0]，说明最小值在左半部分，画个图
            else l = m + 1; // 否则，最小值在右半部分
        }

        // 返回最小值
        return nums[r];
    }
};
```

