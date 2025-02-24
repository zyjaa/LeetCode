### 1、二分

有重复值，无所谓

```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int l = 0, r = nums.size() - 1;

        // 去除右端与 nums 相同的元素
        while (r && nums == nums[r]) r--;

        // 如果数组没有旋转，直接返回第一个元素
        if (nums <= nums[r]) return nums;

        // 二分查找旋转点
        while (l < r) {
            int m = l + r >> 1; // 计算中间位置
            if (nums[m] < nums) r = m; // 如果 nums[m] < nums，说明最小值在左半部分
            else l = m + 1; // 否则，最小值在右半部分
        }

        // 返回最小值
        return nums[r];
    }
};
```

大家也能发现，LC考的很单一，所以很简单，难题一般都是稍微考coding能力的模拟题，都很常规
