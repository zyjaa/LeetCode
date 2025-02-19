[53. 最大子数组和](https://leetcode.cn/problems/maximum-subarray/)：具有最大和的连续子数组

**例 1：**

```
输入：nums = [-2,1,-3,4,-1,2,1,-5,4]
输出：6
解释：连续子数组 [4,-1,2,1] 的和最大，为 6 。
```

**示例 2：**

```
输入：nums = [1]
输出：1
```



### 1、模拟

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int res=INT_MIN;
        int last=0;
        for(auto x:nums){
            last=max(last,0)+x;
            res=max(res,last);
        }
        return res;
    }
};
```

- 时间：O(n)
- 空间：O(1)