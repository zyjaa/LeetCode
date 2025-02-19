[51. N 皇后](https://leetcode.cn/problems/n-queens/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/queens.jpg)

```
输入：n = 4
输出：[[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
解释：如上图所示，4 皇后问题存在两个不同的解法。
```





### 法一：DFS

```cpp
class Solution {
public:
    vector<vector<string>> res;
    vector<bool> row,col;
    vector<bool> dg,udg;
    int n;
    vector<string> path;
    vector<vector<string>> solveNQueens(int _n) {
        n=_n;
        row=col=vector<bool>(n);
        dg=udg=vector<bool>(2*n);
        path=vector<string>(n,string(n,'.'));
        dfs(0);
        return res;
    }
    void dfs(int u){
        if(u==n){
            res.push_back(path);
            return;
        }
        for(int i=0;i<n;i++){
            if(!row[u] && !col[i] && !dg[i-u+n] && !udg[i+u]){
                row[u]=col[i]=dg[i-u+n]=udg[i+u]=true;
                path[u][i]='Q';
                dfs(u+1);
                path[u][i]='.';
                row[u]=col[i]=dg[i-u+n]=udg[i+u]=false;
            }
        }
    }
};
```

- 时间：O($$n!$$)
- 空间：O($$n^2*n!$$)
  - 递归栈：n
  - 辅助数组：n
  - res存储所有解，每个解是n*n，n！个解



**位运算优化**

```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> res;
        vector<string> board(n, string(n, '.')); // 初始化棋盘
        dfs(res, board, 0, 0, 0, 0, n); // 从第0行开始搜索
        return res;
    }

    void dfs(vector<vector<string>>& res, vector<string>& board, int row, int col, int dg, int udg, int n) {
        if (row == n) { // 找到一个解
            res.push_back(board);
            return;
        }

        int availablePositions = ((1 << n) - 1) & ~(col | dg | udg); // 可用的位置
        while (availablePositions) {
            int pos = availablePositions & -availablePositions; // 取最低位的1
            availablePositions &= availablePositions - 1; // 移除最低位的1
            int colIndex = __builtin_ctz(pos); // 计算列索引

            board[row][colIndex] = 'Q'; // 放置皇后
            dfs(res, board, row + 1, col | pos, (dg | pos) << 1, (udg | pos) >> 1, n); // 递归下一行
            board[row][colIndex] = '.'; // 回溯
        }
    }
};
```

复杂度不变