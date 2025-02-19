34、在排序数组中查找元素的第一个和最后一个位置

**示例 1：**

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

**示例 2：**

```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```





### 法一：二分

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if(nums.empty())return {-1,-1};
        int l=0,r=nums.size()-1;
        int L;
        while(l<r){
            int m=l+r>>1;
            if(nums[m]>=target)r=m;
            else l=m+1;
        }
        if(nums[r]!=target)return {-1,-1};
        L=r;
        l=0,r=nums.size()-1;
        while(l<r){
            int m=l+r+1>>1;
            if(nums[m]<=target)l=m;
            else r=m-1;
        }
        return {L,r};
    }
};
```

- 时间：O($$logn$$)
- 空间：O($$1$$)