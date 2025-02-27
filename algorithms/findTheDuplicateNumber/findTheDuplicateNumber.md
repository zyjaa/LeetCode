你设计的解决方案必须 **不修改** 数组 `nums` 且只用常量级 `O(1)` 的额外空间。

### 1、快慢指针

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow = 0, fast = 0;  // 初始化慢指针和快指针

        // 寻找相遇点
        while (true) {
            slow = nums[slow];          // 慢指针每次移动一步
            fast = nums[nums[fast]];    // 快指针每次移动两步
            if (slow == fast) {
                break;  // 找到相遇点
            }
        }

        // 寻找重复数字
        slow = 0;  // 将慢指针重置为 0
        while (slow != fast) {
            slow = nums[slow];  // 慢指针每次移动一步
            fast = nums[fast];  // 快指针每次移动一步
        }

        return slow;  // 返回重复数字
    }
};
```

