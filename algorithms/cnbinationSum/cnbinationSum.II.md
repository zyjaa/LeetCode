[40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)

给定一个候选人编号的集合 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用 **一次** 。

**注意：**解集不能包含重复的组合。 

 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
输出:
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
输出:
[
[1,2,2],
[5]
]
```



### 法一：DFS

```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        dfs(candidates,0,target);
        return res;
    }
    void dfs(vector<int>& candidates,int u,int target){
        if(!target){
            res.push_back(path);
            return;
        }
        if(u==candidates.size())return;
        int k=u;
        while(k<candidates.size() && candidates[u]==candidates[k])k++;
        int cnt=k-u;
        for(int i=0;i<=cnt && candidates[u]*i<=target;i++){
            dfs(candidates,u+cnt,target-candidates[u]*i);
            path.push_back(candidates[u]);
        }
        for(int i=0;i<=cnt && candidates[u]*i<=target;i++){
            path.pop_back();
        }
    }
};
```

- 时间：O($$2^n$$)
  - 每个元素有两种选择（使用或不使用），总共有$$2^n$$种组合。剪枝优化无法改变指数级复杂度，剪枝只能优化常数因子，无法将复杂度降低到多项式级别。
- 空间：O($$2^n*m$$)
  - 递归栈深度：$$2^n$$
  -  m是组合的平均长度