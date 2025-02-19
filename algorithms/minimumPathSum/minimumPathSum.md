[64. 最小路径和](https://leetcode.cn/problems/minimum-path-sum/)

给定一个包含非负整数的 `*m* x *n*` 网格 `grid` ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。
```





### 1、DP

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n=grid.size(),m=grid[0].size();
        vector<vector<int>> f(n,vector<int>(m,INT_MAX));
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(!i && !j)f[i][j]=grid[i][j];
                else{
                    if(i)f[i][j]=min(f[i][j],f[i-1][j]+grid[i][j]);
                    if(j)f[i][j]=min(f[i][j],f[i][j-1]+grid[i][j]);
                }
            }
        }
        return f[n-1][m-1];
    }
};
```

- 时间：m*n
- 空间：m*n