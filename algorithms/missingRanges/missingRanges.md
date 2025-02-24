题目：https://blog.csdn.net/qq_21201267/article/details/107186322

```cpp
class Solution {
public:
    vector<string> findMissingRanges(vector<int>& nums, int lower, int upper) {
        vector<string> result;
        int n = nums.size();

        // 如果数组为空，直接返回 [lower, upper]
        if (n == 0) {
            result.push_back(formatRange(lower, upper));
            return result;
        }

        // 处理 lower 小于数组第一个元素的情况
        if (lower < nums[0]) {
            result.push_back(formatRange(lower, nums[0] - 1));
        }

        // 遍历数组，检查相邻元素的差值
        for (int i = 1; i < n; i++) {
            if (nums[i] > nums[i - 1] + 1) {
                result.push_back(formatRange(nums[i - 1] + 1, nums[i] - 1));
            }
        }

        // 处理 upper 大于数组最后一个元素的情况
        if (upper > nums[n - 1]) {
            result.push_back(formatRange(nums[n - 1] + 1, upper));
        }

        return result;
    }

private:
    // 格式化区间为字符串
    string formatRange(int start, int end) {
        if (start == end) {
            return to_string(start);
        } else {
            return to_string(start) + "->" + to_string(end);
        }
    }
};
```

- 时间：n
- 空间：k，缺失区间的数量
