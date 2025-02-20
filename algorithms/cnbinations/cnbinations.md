[77. 组合](https://leetcode.cn/problems/combinations)

给定两个整数 `n` 和 `k`，返回范围 `[1, n]` 中所有可能的 `k` 个数的组合。

你可以按 **任何顺序** 返回答案。

 

**示例 1：**

```
输入：n = 4, k = 2
输出：
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```



### 1、DFS

```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    vector<vector<int>> combine(int n, int k) {
        dfs(n,k,1);
        return res;
    }
    void dfs(int n,int k,int u){
        if(!k){
            res.push_back(path);
            return;
        }
        for(int i=u;i<=n;i++){
            path.push_back(i);
            dfs(n,k-1,i+1);
            path.pop_back();
        }
    }
};
```







```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int> path;
        dfs(n, k, 1, path, res);
        return res;
    }

    void dfs(int n, int k, int u, vector<int>& path, vector<vector<int>>& res) {
        if (k == 0) {
            res.push_back(path);
            return;
        }
        for (int i = u; i <= n - k + 1; i++) { // 剪枝优化
            path.push_back(i);
            dfs(n, k - 1, i + 1, path, res);
            path.pop_back();
        }
    }
};
```

- 时间：O($$C_{n}^{k}*k$$)
  - 从 `n` 个数字中选择 `k` 个：$$C_{n}^{k}$$
  - 每次递归选择一个数字，递归深度为 `k`。
  - 组合问题：不考虑顺序，复杂度不包含 k!*k*!。
  - 排列问题：考虑顺序，复杂度包含 k!*k*!。
- 空间：O($$C_{n}^{k}*k$$)
  - 需要存储所有组合，$$C_{n}^{k}$$
  - 递归的最大深度为 `k`