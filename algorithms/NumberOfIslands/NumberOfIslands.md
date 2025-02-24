### 1、Floor  Fill（DFS）

```cpp
class Solution {
public:
    int n,m;
    int dx[4]={0,1,0,-1},dy[4]={1,0,-1,0};
    vector<vector<bool>> st;
    int numIslands(vector<vector<char>>& grid) {
        n=grid.size(),m=grid[0].size();
        st=vector<vector<bool>>(n,vector<bool>(m));
        int res=0;
        for(int i=0;i<n;i++)
            for(int j=0;j<m;j++){
                if(!st[i][j] && grid[i][j]=='1'){
                    dfs(grid,i,j);
                    res++;
                }
            }
        return res;
    }
    void dfs(vector<vector<char>>& grid,int x,int y){
        st[x][y]=true;
        for(int i=0;i<4;i++){
            int a=x+dx[i],b=y+dy[i];
            if(a>=0 && b>=0 && a<n && b<m && grid[a][b]=='1' && !st[a][b])dfs(grid,a,b);
        }
    }
};
```

- 时间：m*n
- 空间：m*n
