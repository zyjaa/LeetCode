 [130. 被围绕的区域](https://leetcode.cn/problems/surrounded-regions/)

### 1、DFS

反向思考：把从边边的O开始DFS，遍历到的所有点都标记为.，其他都是x

```cpp
class Solution {
public:
    int n,m;
    vector<vector<char>> _board;
    int dx[4]={1,0,-1,0},dy[4]={0,1,0,-1};
    void solve(vector<vector<char>>& board) {
        n=board.size(),m=board[0].size();
        _board=board;
        for(int i=0;i<n;i++){
            if(board[i][0]=='O')dfs(i,0);
            if(board[i][m-1]=='O')dfs(i,m-1);
        }
        for(int i=0;i<m;i++){
            if(board[0][i]=='O')dfs(0,i);
            if(board[n-1][i]=='O')dfs(n-1,i);
        }
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(_board[i][j]=='.')board[i][j]='O';
                else board[i][j]='X';
            }
        }

    }
    void dfs(int x,int y){
        _board[x][y]='.';
        for(int i=0;i<4;i++){
            int a=x+dx[i],b=y+dy[i];
            if(a>=0 && a<n && b<m && b>=0 && _board[a][b]=='O')dfs(a,b);
        }
    }
};
```

- 时间：m*n
- 空间：m*n
