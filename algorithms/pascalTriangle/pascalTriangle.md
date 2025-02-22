[118. 杨辉三角](https://leetcode.cn/problems/pascals-triangle/)

拉直看

```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> f;
        for(int i=0;i<numRows;i++){
            vector<int> level(i+1);
            level[0]=level[i]=1;
            for(int j=1;j<i;j++)level[j]=f[i-1][j-1]+f[i-1][j];
            f.push_back(level);
        }
        return f;
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n^2$$)