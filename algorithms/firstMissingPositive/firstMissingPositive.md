[41. 缺失的第一个正数](https://leetcode.cn/problems/first-missing-positive)

给你一个未排序的整数数组 `nums` ，请你找出其中没有出现的最小的正整数。

请你实现时间复杂度为 `O(n)` 并且只使用常数级别额外空间的解决方案。

 

**示例 1：**

```
输入：nums = [1,2,0]
输出：3
解释：范围 [1,2] 中的数字都在数组中。
```

**示例 2：**

```
输入：nums = [3,4,-1,1]
输出：2
解释：1 在数组中，但 2 没有。
```



### 法一：原地置换

脑筋急转弯

```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        // 1,2,3,4 5
        int n=nums.size();
        for(int i=0;i<n;i++){
            while(nums[i]>0 && nums[i]<=n && nums[i]!=nums[nums[i]-1])swap(nums[i],nums[nums[i]-1]);
        }
        for(int i=0;i<n;i++){
            if(i+1!=nums[i])return i+1;
        }
        return n+1;

    }
};
```

- 时间复杂度：*O*(*N*)，其中*N*是数组的长度。
- 空间复杂度：*O*(1)。