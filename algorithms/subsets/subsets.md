[78. 子集](https://leetcode.cn/problems/subsets/)：不重复，任意顺序返回

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```



### 1、位运算

```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        // 5  000 - 101
        int n=nums.size();
        vector<vector<int>> res;
        for(int i=0;i<1<<n;i++){
            vector<int> path;
            for(int j=0;j<n;j++){
                if(i>>j &1)path.push_back(nums[j]);
            }
            res.push_back(path);
        }
        return res;
    }
};
```

- 时间：O($$n*2^n$$)
- 空间：O($$n*2^n$$)，存储所有子集



### 2、DFS

```cpp
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;
    vector<vector<int>> subsets(vector<int>& nums) {
        dfs(nums,0);
        return ans;
    }
    void dfs(vector<int>& nums,int u){
        if(u==nums.size()){
            ans.push_back(path);
            return;
        }
        dfs(nums,u+1);
        path.push_back(nums[u]);
        dfs(nums,u+1);
        path.pop_back();
    }
};
```

- 时间：O($$n*2^n$$)
  - 每个子集需要 O(n)的时间生成（栈深度）
- 空间：O($$n*2^n$$)，存储所有子集