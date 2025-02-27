*完全平方数的最少数量* 。

 `f[j]` 表示将整数 `j` 表示为完全平方数的最小数量

```
class Solution {
public:
    int numSquares(int n) {
        vector<int> f(n+1,INT_MAX);
        f[0]=0;
        f[1]=1;
        for(int i=1;i*i<=n;i++){//遍历平方根
            for(int j=i*i;j<=n;j++)f[j]=min(f[j],f[j-i*i]+1);
        }
        return f[n];
    }
};
```

