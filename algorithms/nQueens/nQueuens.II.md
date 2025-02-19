[52. N 皇后 II](https://leetcode.cn/problems/n-queens-ii/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：2
解释：如上图所示，4 皇后问题存在两个不同的解法。
```

**示例 2：**

```
输入：n = 1
输出：1
```





### 1、DFS

```cpp
class Solution {
public:
    int n;
    vector<bool> dg,udg,col;
    int totalNQueens(int _n) {
        n=_n;
        dg=udg=vector<bool>(n*2);
        col=vector<bool>(n);
        return dfs(0);// 处理第0行
    }
    int dfs(int u){
        if(u==n)return 1;
        int res=0;
        for(int i=0;i<n;i++){// 枚举列
            if(!col[i] && !dg[i-u+n] && !udg[u+i]){
                // 1. 列未被占用（!col[i]）
            	// 2. 对角线未被占用（!dg[i - u + n]）
           		// 3. 反对角线未被占用（!udg[u + i]）
                col[i]=dg[i-u+n]=udg[u+i]=true;
                res+=dfs(u+1);
                col[i]=dg[i-u+n]=udg[u+i]=false;
            }
        }
        return res;
    }
};
```

- 时间：O($$n!$$)
- 空间：O($$n$$)