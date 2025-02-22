 [128. 最长连续序列](https://leetcode.cn/problems/longest-consecutive-sequence/)

请你设计并实现时间复杂度为 `O(n)` 的算法解决此问题。

**示例 1：**

```
输入：nums = [100,4,200,1,3,2]
输出：4
解释：最长数字连续序列是 [1, 2, 3, 4]。它的长度为 4。
```



### 1、模拟

```cpp
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int n=nums.size();
        unordered_set<int> S(nums.begin(),nums.end());
        int res=0;
        for(auto x:nums){
            if(!S.count(x-1)){
                int y=x;
                S.erase(x);
                while(S.count(y+1)){
                    y++;
                    S.erase(y);
                }
                res=max(res,y-x+1);
            }
        }
        return res;
    }
};
```

- 时间：n
- 空间：n
