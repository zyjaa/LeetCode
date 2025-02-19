33、搜索旋转排序数组

整数数组 `nums` 按升序排列，数组中的值 **互不相同** 。

你必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题。

 

**示例 1：**

```
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1
```

**示例 3：**

```
输入：nums = [1], target = 0
输出：-1
```



### 法一：二分

这题就是分2段，第1段所有数大于第2段，注意二分时候的边界

```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l=0,r=nums.size()-1;
        while(l<r){
            int m=l+r+1>>1;
            if(nums[m]>=nums[0])l=m;
            else r=m-1;
        }
        if(target>=nums[0])l=0;//说明答案在第1段
        else l=r+1,r=nums.size()-1;//答案在第2段
        while(l<r){
            int m=l+r>>1;
            if(nums[m]>=target)r=m;
            else l=m+1;
        }
        if(target==nums[r])return r;
        return -1;
    }
};
```

- 时间：O(n)
- 空间：O(1)