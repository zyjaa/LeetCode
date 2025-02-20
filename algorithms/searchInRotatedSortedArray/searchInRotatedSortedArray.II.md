[81. 搜索旋转排序数组 II](https://leetcode.cn/problems/search-in-rotated-sorted-array-ii/)

和1的区别就是2中的数可以重复

**示例 1：**

```
输入：nums = [2,5,6,0,0,1,2], target = 0
输出：true
```



### 1、二分

划分为2段

```cpp
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        // 去除数组末尾与开头相同的元素，避免干扰旋转点的判断
        int r = nums.size() - 1;
        while (r >= 0 && nums[r] == nums[0]) r--;
        // 如果所有元素都相同，直接判断目标值是否等于第一个元素
        if (r < 0) return target == nums[0];

        // 第一次二分查找：找到旋转点（即数组中的最大值）
        int l = 0, R = r;
        while (l < r) {
            int m = l + r + 1 >> 1; // 取中点，注意 +1 避免死循环
            if (nums[0] <= nums[m]) l = m; // 中点在前半部分，旋转点在右侧
            else r = m - 1; // 中点在后半部分，旋转点在左侧
        }

        // 根据目标值的位置，确定搜索范围
        if (nums[0] <= target) l = 0; // 目标值在前半部分
        else l = r + 1, r = R; // 目标值在后半部分

        // 第二次二分查找：在确定的范围内查找目标值
        while (l < r) {
            int m = l + r >> 1; // 取中点
            if (nums[m] >= target) r = m; // 中点值大于等于目标值，搜索左侧
            else l = m + 1; // 中点值小于目标值，搜索右侧
        }
        
        return nums[r]==target;
    }
}
```

- 时间：O($$logn$$)
- 空间：O(1)

```
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        // 去除数组末尾与开头相同的元素，避免干扰旋转点的判断
        int r = nums.size() - 1;
        while (r >= 0 && nums[r] == nums[0]) r--;
        // 如果所有元素都相同，直接判断目标值是否等于第一个元素
        if (r < 0) return target == nums[0];

        // 第一次二分查找：找到旋转点（即数组中的最大值）
        int l = 0, R = r;
        while (l < r) {
            int m = (l + r + 1)/2; // 取中点，注意 +1 避免死循环
            if (nums[0] <= nums[m]) l = m; // 中点在前半部分，旋转点在右侧
            else r = m - 1; // 中点在后半部分，旋转点在左侧
        }

        // 根据目标值的位置，确定搜索范围
        if (nums[0] <= target) l = 0; // 目标值在前半部分
        else l = r + 1, r = R; // 目标值在后半部分

        // 第二次二分查找：在确定的范围内查找目标值
        while (l < r) {
            int m = (l + r)/2; // 取中点
            if (nums[m] >= target) r = m; // 中点值大于等于目标值，搜索左侧
            else l = m + 1; // 中点值小于目标值，搜索右侧
        }
        
        return nums[r]==target;
    }
};
```

