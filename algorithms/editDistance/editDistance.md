[72. 编辑距离](https://leetcode.cn/problems/edit-distance)

给你两个单词 `word1` 和 `word2`， *请返回将 `word1` 转换成 `word2` 所使用的最少操作数* 。

你可以对一个单词进行如下三种操作：

- 插入一个字符
- 删除一个字符
- 替换一个字符

 

**示例 1：**

```
输入：word1 = "horse", word2 = "ros"
输出：3
解释：
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```



### 1、DP

- i、j不等，取min
- i、j等，取min

```cpp
class Solution {
public:
    int minDistance(string a, string b) {
        int n=a.size(),m=b.size();
        a=' '+a,b=' '+b;
        vector<vector<int>> f(n+1,vector<int>(m+1,INT_MAX));
        for(int i=0;i<=n;i++)f[i][0]=i;
        for(int i=0;i<=m;i++)f[0][i]=i;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                f[i][j]=min(f[i][j-1],f[i-1][j])+1;
                f[i][j]=min(f[i][j],f[i-1][j-1]+(a[i]!=b[j]));
            }
        }
        return f[n][m];
    }
};
```

- 时间：m*n
- 空间：m*n



**优化空间**为：O(min(m,n))

1. 使用两个一维数组 `prev` 和 `curr`，分别表示上一行和当前行的状态。
2. 在每次迭代中更新 `curr`，然后将 `curr` 赋值给 `prev`，继续下一行的计算。

```cpp
class Solution {
public:
    int minDistance(string a, string b) {
        int n = a.size(), m = b.size();
        a = ' ' + a, b = ' ' + b;
        vector<int> prev(m + 1, 0), curr(m + 1, 0);
        for (int j = 0; j <= m; j++) prev[j] = j;
        for (int i = 1; i <= n; i++) {
            curr = i;
            for (int j = 1; j <= m; j++) {
                curr[j] = min(curr[j - 1], prev[j]) + 1;
                curr[j] = min(curr[j], prev[j - 1] + (a[i] != b[j]));
            }
            prev = curr;
        }
        return prev[m];
    }
};
```

