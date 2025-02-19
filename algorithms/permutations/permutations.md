[46. 全排列](https://leetcode.cn/problems/permutations/)

给定一个不含重复数字的数组 `nums` ，返回其 *所有可能的全排列* 。你可以 **按任意顺序** 返回答案。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```



### 法一：DFS

```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<bool> st;
    vector<int> path;
    vector<vector<int>> permute(vector<int>& nums) {
        int n=nums.size();
        st=vector<bool>(n);
        path=vector<int>(n);

        dfs(nums,0);
        return res;
    }
    void dfs(vector<int>& nums,int u){
        if(u==nums.size()){
            res.push_back(path);
            return;
        }
        for(int i=0;i<nums.size();i++){
            if(!st[i]){
                path[u]=nums[i];
                st[i]=true;
                dfs(nums,u+1);
                st[i]=false;
            }
        }
    }
};
```

- 时间：O($$n*n!$$)
  - 递归树节点数：全排列的数量为 n!，其中 n是数组长度。
  - 每个节点的操作：每次递归需要遍历数组，时间复杂度为 O(n)。
- 空间：O($$n*n!$$)
  - 递归栈深度：递归深度为 n，空间复杂度为 O(n)。
  - 存储结果：结果数量为 n!，每个排列长度为 n，空间复杂度为 O(n⋅n!)。
  - 标记数组 `st` 和当前排列 `path`：额外空间为 O(n)*O*(*n*)。