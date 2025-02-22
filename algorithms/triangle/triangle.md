[120. 三角形最小路径和](https://leetcode.cn/problems/triangle/)



### 1、DP

```cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& f) {
        for(int i=f.size()-2;i>=0;i--)//从倒数第二行向上枚举
            for(int j=0;j<=i;j++){//下+下右
                f[i][j]+=min(f[i+1][j],f[i+1][j+1]);
            }
        return f[0][0];
    }
};
```

- 时间：O($$n^2$$)
- 空间：1