[39. 组合总和](https://leetcode.cn/problems/combination-sum/)

给你一个 **无重复元素** 的整数数组 `candidates` 和一个目标整数 `target` ，找出 `candidates` 中可以使数字和为目标数 `target` 的 所有 **不同组合** ，并以列表形式返回。你可以按 **任意顺序** 返回这些组合。

`candidates` 中的 **同一个** 数字可以 **无限制重复被选取** 。如果至少一个数字的被选数量不同，则两种组合是不同的。 

对于给定的输入，保证和为 `target` 的不同组合数少于 `150` 个。

 

**示例 1：**

```
输入：candidates = [2,3,6,7], target = 7
输出：[[2,2,3],[7]]
解释：
2 和 3 可以形成一组候选，2 + 2 + 3 = 7 。注意 2 可以使用多次。
7 也是一个候选， 7 = 7 。
仅有这两种组合。
```

**示例 2：**

```
输入: candidates = [2,3,5], target = 8
输出: [[2,2,2,2],[2,3,3],[3,5]]
```

**示例 3：**

```
输入: candidates = [2], target = 1
输出: []
```



### 法一：DFS

 ```cpp
 class Solution {
 public: 
     vector<vector<int>> res;
     vector<int> path;
     vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
         dfs(candidates,0,target);
         return res;
     }
     void dfs(vector<int>& candidates,int u,int target){
         if(target==0){
             res.push_back(path);
             return;
         }
         if(u==candidates.size())return;
         for(int i=0;i*candidates[u]<=target;i++){
             dfs(candidates,u+1,target-i*candidates[u]);
             path.push_back(candidates[u]);
         }
 
         for(int i=0;i*candidates[u]<=target;i++)path.pop_back();
     }
 };
 ```

- 时间复杂度：O($$k^n$$)
  - **递归深度**：最多为 ($$target/min(candidates)$$)。
  - **每个节点的分支**：取决于候选数的个数和重复使用次数。
  - **最坏情况**：候选数可以重复使用，复杂度为指数级别，约为 \(O(k^n)\)，其中 \(k\) 是候选数个数，\(n\) 是递归深度。

- 空间复杂度：\(O$$(k^n*m)$$)
  - **递归栈**：深度为 \(O(n)\)。
  - **存储结果**：结果数量可能为指数级别，空间复杂度为 \(O$$(k^n*m)$$)，其中 \(m\) 是组合的平均长度。

