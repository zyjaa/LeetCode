[62. 不同路径](https://leetcode.cn/problems/unique-paths/)

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

 

**示例 1：**

![img](https://pic.leetcode.cn/1697422740-adxmsI-image.png)

```
输入：m = 3, n = 7
输出：28
```





### 1、DP

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> f(n,1);
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                f[j]+=f[j-1];
            }
        }
        return f[n-1];
    }
};
```

- 时间：m*n
- 空间：n



### 2、组合数学

$$C_{m+n-2}^{m-1}$$

```cpp
class Solution {
    long long comb(int n, int k) {
        k = min(k, n - k);
        long long res = 1;
        for (int i = 1; i <= k; i++) {
            res = res * (n + 1 - i) / i;
        }
        return res;
    }

public:
    int uniquePaths(int m, int n) {
        return comb(m + n - 2, m - 1);
    }
};
```

- 时间复杂度：O(min(*m*,*n*))。
- 空间复杂度：O(1)。