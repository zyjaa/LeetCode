- `i != j`,
- `abs(i - j) <= indexDiff`
- `abs(nums[i] - nums[j]) <= valueDiff`

```
class Solution {
public:
    bool containsNearbyAlmostDuplicate(vector<int>& nums, int indexDiff, int valueDiff) {
        typedef long long ll; // 定义long long类型
        multiset<ll> S; // 有序集合
        S.insert(1e8), S.insert(-1e8); // 插入两个边界值，避免越界

        for (int i = 0, j = 0; i < nums.size(); i++) { // 滑动窗口
            if (i - j > indexDiff) S.erase(S.find(nums[j++])); // 如果窗口大小超过indexDiff，删除窗口最左边的元素
            int x = nums[i]; // 当前元素
            auto it = S.lower_bound(x); // 查找第一个大于等于x的元素
            if (*it - x <= valueDiff) return true; // 如果满足条件，返回true
            it--; // 查找前一个元素
            if (x - *it <= valueDiff) return true; // 如果满足条件，返回true
            S.insert(x); // 插入当前元素
        }

        return false; // 没有找到满足条件的元素，返回false
    }
};
```

 
