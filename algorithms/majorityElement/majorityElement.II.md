### 1、摩尔投票

```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int r1 = 0, r2 = 0, c1 = 0, c2 = 0; // 候选元素 r1, r2 及其计数 c1, c2

        // 第一次遍历：找到可能的候选元素
        for (auto x : nums) {
            if (c1 && r1 == x) c1++;       // 如果 x 等于 r1，增加 c1
            else if (c2 && r2 == x) c2++;  // 如果 x 等于 r2，增加 c2
            else if (!c1) r1 = x, c1++;    // 如果 c1 为 0，设置 r1 = x，并初始化 c1
            else if (!c2) r2 = x, c2++;    // 如果 c2 为 0，设置 r2 = x，并初始化 c2
            else c1--, c2--;               // 如果 x 不等于 r1 或 r2，减少 c1 和 c2，这里2个都要减少，因为都不相等，要进行低效
        }

        // 第二次遍历：统计 r1 和 r2 的实际出现次数
        c1 = 0, c2 = 0;
        for (auto x : nums) {
            if (r1 == x) c1++;
            else if (r2 == x) c2++;
        }

        // 结果筛选：将出现次数超过 n/3 的元素加入结果数组
        vector<int> res;
        int n = nums.size();
        if (c1 > n / 3) res.push_back(r1);
        if (c2 > n / 3) res.push_back(r2);

        // 返回结果数组
        return res;
    }
};
```
