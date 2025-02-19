37、解数独



**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/04/12/250px-sudoku-by-l2g-20050714svg.png)

```
输入：board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
输出：[["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
解释：输入的数独如上图所示，唯一有效的解决方案如下所示：
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/04/12/250px-sudoku-by-l2g-20050714_solutionsvg.png)





### 法一：DFS

暴搜每行、每列、每个3*3单元格

```cpp
class Solution {
public:
    bool row[9][9],col[9][9],cell[3][3][9];
    void solveSudoku(vector<vector<char>>& board) {
        memset(row,false,sizeof row);
        memset(col,false,sizeof col);
        memset(cell,false,sizeof cell);
        for(int i=0;i<9;i++){
            for(int j=0;j<9;j++){
                if(board[i][j]!='.'){
                    int t=board[i][j]-'1';
                    row[i][t] = col[j][t] = cell[i/3][j/3][t] = true;
                }
            }
        }
        dfs(board,0,0);
    }
    bool dfs(vector<vector<char>>& board,int x,int y){
        if(y==9)x++,y=0;
        if(x==9)return true;
        if(board[x][y]!='.')return dfs(board,x,y+1);
        for(int i=0;i<9;i++){
            if(!row[x][i] && !col[y][i] && !cell[x/3][y/3][i]){
                char t=i+'1';
                row[x][i]=col[y][i]=cell[x/3][y/3][i]=true;
                board[x][y]=t;
                if(dfs(board,x,y+1))return true;
                row[x][i]=col[y][i]=cell[x/3][y/3][i]=false;
                board[x][y]='.';
            }
        }
        return false;
    }
};
```

- 时间：O($$9^m$$)，其中 m是空格数。每个空格最多尝试 9 个数字，递归深度为m
- 空间：O($$1$$)，使用固定大小的数组 `row`、`col` 和 `cell`