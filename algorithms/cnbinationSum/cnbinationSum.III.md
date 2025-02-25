```
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    vector<vector<int>> combinationSum3(int k, int n) {
        dfs(1,n,k);
        return res;
    }
    void dfs(int u,int n,int k){
        if(!n && !k){
            res.push_back(path);
            return;
        }
        for(int i=u;i<=9;i++){
            if(i<=n){
                path.push_back(i);
                dfs(i+1,n-i,k-1);
                path.pop_back();
            }
        }
    }
};  
```

 时间复杂度：

1. **组合数**：从 `1` 到 `9` 中选择 `k` 个数字的组合数是 `C(9, k)`。
2. **总时间复杂度**：O(C(9, k) × k)，其中 `C(9, k)` 是组合数，`k` 是每个组合的长度。
