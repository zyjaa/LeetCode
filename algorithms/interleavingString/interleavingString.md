[97. 交错字符串](https://leetcode.cn/problems/interleaving-string/)

给定三个字符串 `s1`、`s2`、`s3`，请你帮忙验证 `s3` 是否是由 `s1` 和 `s2` **交错** 组成的。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

```
输入：s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
输出：true
```



### 1、DP

- 对于每个位置，检查以下两种情况：
  1. 如果 `s1` 的第 `i` 个字符等于 `s3` 的第 `i+j` 个字符，则 `f[i][j]` 的值取决于 `f[i-1][j]`（即去掉 `s1` 的当前字符后是否能组成 `s3` 的前 `i+j-1` 个字符）。
  2. 如果 `s2` 的第 `j` 个字符等于 `s3` 的第 `i+j` 个字符，则 `f[i][j]` 的值取决于 `f[i][j-1]`（即去掉 `s2` 的当前字符后是否能组成 `s3` 的前 `i+j-1` 个字符）。
- 如果以上任意一种情况为 `true`，则 `f[i][j]` 为 `true`。

```cpp
class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        if(s1.size()+s2.size()!=s3.size())return false;
        int n=s1.size(),m=s2.size(),a=s3.size();
        s1=' '+s1,s2=' '+s2,s3=' '+s3;
        vector<vector<bool>> f(n+1,vector<bool>(m+1));
        for(int i=0;i<=n;i++){
            for(int j=0;j<=m;j++){
                if(!i && !j)f[i][j]=true;
                else{
                    if(i && s1[i]==s3[i+j])f[i][j]=f[i-1][j];
                    if(j && s2[j]==s3[i+j])f[i][j]=f[i][j] || f[i][j-1];
                }
            }
        }
        return f[n][m];
    }
};
```

- 时间：m*n
- 空间：m*n