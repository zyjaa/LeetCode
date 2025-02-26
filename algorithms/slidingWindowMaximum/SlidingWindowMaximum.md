```
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        if (nums.empty() || k > nums.size()) return {};

        vector<int> result;
        deque<int> window;

        for (int i = 0; i < nums.size(); i++) {
            // 移除不在当前窗口范围内的索引
            if (!window.empty() && window.front() <= i - k) {
                window.pop_front();
            }

            // 维护单调递减队列
            while (!window.empty() && nums[i] >= nums[window.back()]) {
                window.pop_back();
            }

            // 将当前索引加入队列
            window.push_back(i);

            // 记录窗口最大值
            if (i >= k - 1) {
                result.push_back(nums[window.front()]);
            }
        }

        return result;
    }
};
```

n，k
