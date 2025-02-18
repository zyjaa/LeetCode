**18、题意**

给你一个由 `n` 个整数组成的数组 `nums` ，和一个目标值 `target` 。请你找出并返回满足下述全部条件且**不重复**的四元组 `[nums[a], nums[b], nums[c], nums[d]]` （若两个四元组元素一一对应，则认为两个四元组重复）：

- `0 <= a, b, c, d < n`
- `a`、`b`、`c` 和 `d` **互不相同**
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

你可以按 **任意顺序** 返回答案 。

 

**示例 1：**

```
输入：nums = [1,0,-1,0,-2,2], target = 0
输出：[[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
```

**示例 2：**

```
输入：nums = [2,2,2,2,2], target = 8
输出：[[2,2,2,2]]
```





### 法一：排序+4指针

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        vector<vector<int>> res;
        for(int i=0;i<nums.size();i++){
            if(i && nums[i]==nums[i-1])continue;
            for(int j=i+1;j<nums.size();j++){
                if(j>i+1 && nums[j]==nums[j-1])continue;
                for(int k=j+1,u=nums.size()-1;k<u;k++){
                    if(k>j+1 && nums[k]==nums[k-1])continue;
                    while(k<u-1 && (long long)nums[i]+nums[j]+nums[k]+nums[u-1]>=target)u--;
                    if((long long)nums[i]+nums[j]+nums[k]+nums[u]==target)res.push_back({nums[i],nums[j],nums[k],nums[u]});
                }
            }
        }
        return res;
    }
};
```

- 时间复杂度：O($$N^3$$)
- 空间复杂的：O($$logN$$)