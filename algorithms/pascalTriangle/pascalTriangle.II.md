[119. 杨辉三角 II](https://leetcode.cn/problems/pascals-triangle-ii/)

### 1、模拟

```cpp
class Solution {
public:
    vector<int> getRow(int n) {
        vector<vector<int>> f(2,vector<int>(n+1));
        for(int i=0;i<=n;i++){
            f[i&1][0]=f[i&1][i]=1;//滚动数组
            for(int j=1;j<i;j++)f[i&1][j]=f[i-1&1][j]+f[i-1&1][j-1];
        }
        return f[n&1];
    }
};
```

- 时间：O($$n^2$$)
- 空间：n