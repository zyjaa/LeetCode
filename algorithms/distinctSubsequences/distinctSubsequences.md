[115. 不同的子序列](https://leetcode.cn/problems/distinct-subsequences/)



### 1、DP

`f[i][j]` 表示 `s` 的前 `i` 个字符中有多少个子序列等于 `t` 的前 `j` 个字符

```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        // f[i][j]  1-i,1-j
        // s[i] t[j]
        int n=s.size(),m=t.size();
        s=' '+s,t=' '+t;
        vector<vector<long long>> f(n+1,vector<long long>(m+1));
        for(int i=0;i<=n;i++)f[i][0]=1;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                f[i][j]=f[i-1][j];//字符不匹配，只能看s前i-1个字符的了
                if(s[i]==t[j])f[i][j]+=f[i-1][j-1];//匹配：当前这个字符和之前的配对，之前做过的那个hash[t]还记得吧，
                f[i][j]%=INT_MAX;
            }
        }
        return f[n][m];
    }
};
```

