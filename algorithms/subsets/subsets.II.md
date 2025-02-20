[90. 子集 II](https://leetcode.cn/problems/subsets-ii/)

给你一个整数数组 `nums` ，其中可能包含重复元素，请你返回该数组所有可能的 子集（幂集）。

解集 **不能** 包含重复的子集。返回的解集中，子集可以按 **任意顺序** 排列。

 

**示例 1：**

```
输入：nums = [1,2,2]
输出：[[],[1],[1,2],[1,2,2],[2],[2,2]]
```



### 1、DFS

```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        dfs(nums,0);
        return res;
    }
    void dfs(vector<int>& nums,int u){
        if(u==nums.size()){
            res.push_back(path);
            return;
        }
        // 统计当前元素 nums[u] 的重复次数
        int k=u+1;
        while(k<nums.size() && nums[k]==nums[u])k++;
        for(int i=0;i<=k-u;i++){
            //1 2 2 3
            dfs(nums,k);
            path.push_back(nums[u]);
        }
        for(int i=0;i<=k-u;i++){
            path.pop_back();
        }
    }
};
```

- 时间复杂度：O(n×2^n)，其中n是数组的长度。
  - 每个元素有选或不选两种选择，总共有 2^n 个子集。
  - 每个子集需要 O(n)的时间复制到结果集中。
- **空间复杂度**：O(n)，递归栈的深度为 n。